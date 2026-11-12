---
name: ios-shortcut-install
description: Use when a tool of [YOUR_FIRST_NAME]'s must put an iOS Shortcut on an iPhone, for data only a Shortcut can read or send. Covers building the file, verifying keys on the Mac, signing, delivery, diagnostics and tap-by-tap steps.
purpose: A Shortcut that installs from one tap on the iPhone, runs on the latest iOS on the first try, and says on the phone and on the server what it did.
helper_model: fable medium
model_why: code against undocumented Apple formats, where a guessed key fails without an error
created_by: agent
created: [SYNC_START_DATE]
last_used: [SYNC_START_DATE]
source: the Memo starter kit
---

# Install an iOS Shortcut from code

## Goal

[YOUR_FIRST_NAME] should never build a Shortcut by hand or debug one on the phone. The agent writes the Shortcut file in code, signs it on the Mac, and [YOUR_FIRST_NAME] installs it with a few taps. Each run then shows what the server saved, or why it saved nothing. Action keys written from memory cost several rounds of reinstalls; verify them on the Mac instead, as below.

## When to use

- A new integration that must run on the iPhone because only a Shortcut can read the data, or must send it from the phone.
- A change to a Shortcut the agent built earlier.
- [YOUR_FIRST_NAME] reports that a Shortcut runs but the server gets nothing, or the answer on the phone says a value was left out.

## When not to use

- Data with a web API: the server pulls it itself.
- A Mac-only automation: run it on the Mac with launchd.
- Steps for [YOUR_FIRST_NAME] to build in the Shortcuts app: avoid this; the agent makes the file.

## Steps

### Part 1. Build the file

1. Write the Shortcut as an XML property list in code: `WFWorkflowActions`, each action with `WFWorkflowActionIdentifier` and `WFWorkflowActionParameters`, every action with its own `UUID`. Variables are `{ OutputName, OutputUUID, Type: 'ActionOutput' }`, inside a `WFTextTokenString` with the object character `￼` at `{0, 1}`, or a `WFTextTokenAttachment`.
2. Verify every action identifier and parameter key on the Mac, never from memory:
   - Parameter keys: the English string tables. `plutil -convert json -o - /System/Library/PrivateFrameworks/WorkflowKit.framework/Versions/A/Resources/Localizable.loctable` and `.../ActionKit.framework/Versions/A/Resources/Localizable.loctable`, then search the `en` table for the summary line, for example "Calculate the ${WFStatisticsOperation} of ${Input}". The names inside `${...}` are the keys.
   - Real examples by Apple: the gallery files in `/System/Library/PrivateFrameworks/WorkflowKit.framework/Versions/A/Resources/Gallery.bundle/Contents/Resources/*.wflow` (read with `plutil -convert json -o - <file>`). `MorningReport.wflow` has a working date filter, `ActionItems.wflow` a text filter, and several show `getvalueforkey` and `showresult`.
   - Strings not in a table (type names, filter keys): `strings -a` over the shared cache in `/System/Volumes/Preboot/Cryptexes/OS/System/Library/dyld/dyld_shared_cache_arm64e.*`, written to a file in the scratchpad, then grep. ActionKit and WorkflowKit are in a few of the parts; search for `is.workflow.actions.<name>` to find them.
   - Name the source of each key in a code comment.
3. Send the values with Get Contents of URL (`downloadurl`): POST, `WFHTTPBodyType: JSON`, `WFJSONValues` as a `WFDictionaryFieldValue`, the token in an `Authorization: Bearer` header. Send each value as text (`WFItemType: 0`). An empty text means "no data", never zero.
4. End the Shortcut with Get Dictionary Value (`message`) of the server's answer, then Show Result. Every run then shows the server's one-line answer on the phone. Put names of fields in that answer, never private values.
5. Send a diagnostic with each value: a Count (Items) of what the lookup returned, under `<field>_count`. Then an empty value says which step gave nothing. The server keeps only what the count means, in words.
6. When one value can come from more than one encoding or filter, send each way as its own field (`<field>`, `<field>_alt`) and let the server take the first one with a number, with a note when it was not the first. One empty field must never lose the others.

### Part 2. Sign and deliver

7. Sign on the Mac: `shortcuts sign --mode anyone --input <in> --output <out>`. It needs the signed-in user session, the network and iCloud. The unsigned file holds the token, so write it only to a new mode-700 temporary folder and remove that folder in code when the command ends (for example Node `rmSync`; never a shell `rm -r`).
8. Deliver through Safari on the iPhone: a button on a page of the server asks for a short-lived address (a few minutes, behind the same login or private network as the server, for example Tailscale), and Safari downloads `<Name>.shortcut` with its name. No `shortcuts://` link, and no file in Files with a lost name: a name that does not end in `.shortcut` is a plain file to iOS.
9. Token rotation: each install makes a new token and the server keeps only its SHA-256. Keep the newest token and the two before it valid, so one press too many on the install button does not break the Shortcut that is already on the phone.

### Part 3. Diagnose

10. Keep a "last try" row on the server for each run: time, status, names of the fields that arrived, what was saved, what was left out and why, and notes. Names and reasons only, never a value. Show it on a status page as "Last try: ...".
11. To read it, select only those columns, read only. Never select from a table that holds the values.
12. Read the reasons in this order. 401: an old Shortcut with a retired token (reinstall). Empty with no count: a Shortcut from before the counts (reinstall). Count 0: the source gave nothing (permission, no data yet, or a filter that matches nothing). Count above 0 but no value: a broken action after the lookup (check its parameter keys). A "phone was locked" hint is one reason of several; never give it as the only one.

### Part 4. Steps on the iPhone, for [YOUR_FIRST_NAME]

13. Write every step tap by tap: device, app, screen, button, in the words on the screen. Name what to read at the end and what each answer means.
14. A change to the Shortcut file always needs a reinstall. Say plainly to delete the old Shortcut first, so there are not two with the same name. Shortest steps: in the Shortcuts app, touch and hold the Shortcut, then Delete. In Safari, open the install page, tap the install button, then Download. Tap the download arrow, then the file, then Add Shortcut. Tap the tile once, answer Always Allow, and read the result box. Last, check the schedule line on the card.
15. Schedule. The newer Shortcuts app has no Automation tab: the schedule is a line on the Shortcut card, such as "At 8:00 AM and 9:00 PM:", above its steps, with a "Describe a change" box below. Shortcut files have a trigger key (`WFWorkflowTriggers`), but its encoding is not verified, so do not write it; the file holds no schedule. After a reinstall, ask [YOUR_FIRST_NAME] to check that the line is there. On an older iOS: Automation tab, +, Time of Day, Run Immediately, pick the Shortcut.
16. Before the first run: the private network on (if the server uses one), the permission the Shortcut needs turned on in Settings, and Always Allow for each question on the first run.
17. A view of the data for [YOUR_FIRST_NAME] shows each day as a chart, not a table: bars for totals, dots for rates, gaps for missing days, and the value on tap. Keep a table behind "Show numbers".

## Keys and encodings checked on a Mac

These were verified against the string tables and Apple's gallery files. Check them again on a new macOS.

- **Calculate Statistics** (`is.workflow.actions.statistics`): the input key is `Input`, not `WFInput` ("Calculate the ${WFStatisticsOperation} of ${Input}"). **Count** (`is.workflow.actions.count`) is the same: `Input`, with `WFCountType: 'Items'`. **Get Dictionary Value** does use `WFInput`. Check each action separately.
- **A date filter row, "Start Date is today"**: write it exactly as Apple's `MorningReport.wflow` does, `{ Operator: 1002, Property: 'Start Date', Values: { Number: '7', Unit: 16 } }`. Unit 16 is the day, and the Number is the text "7". The look-alike `{ Number: 1, Unit: 16 }` matches nothing, without an error.
- **"is in the last 7 days"**: Operator 1001, `{ Number: 7, Unit: 16 }`.
- **An enumeration row** (a type or kind to match): `{ Operator: 4, Property: '<name>', Values: { Enumeration: { Value: <value>, WFSerializationType: 'WFStringSubstitutableState' } } }`, with the value spelled as Shortcuts names it, found in the shared cache.
- **A list in a text field** becomes one line per item, so two lists made from the same variable (for example dates with Date Format `Custom` `yyyy-MM-dd`, and values) pair up line by line. The server keeps each valid line and never lets an empty line wipe a stored day.
- **Past days**: when the source has history, send it in the same run (a filter over the last 31 days) instead of waiting for daily runs. Each run resends the whole window, so gaps fill themselves.

## Done when

- The plist passes `plutil -lint`, and every action identifier and parameter key was checked against the Mac's string tables or an Apple `.wflow`, with the source named in a code comment.
- The project's tests pass, including a test that pins each parameter key.
- A run on the phone shows the server's answer for every field that has data, and the server's last try matches it.
- The steps for [YOUR_FIRST_NAME] name the reinstall, whether to delete the old Shortcut, the permissions and the schedule check, tap by tap, with anything unverified marked as such.

## Pitfalls

- A wrong parameter key raises no error: the action silently gets no input, and the value arrives empty (`WFInput` for Calculate Statistics).
- A filter row written from memory can match nothing without any error. Copy Apple's own encoding.
- An empty text is not zero: the server must keep no row for it.
- A server that has only what the phone sent since install shows empty history. Send the history in the same run when the source has it.
- One empty field must not lose the others.
- A new token on every install breaks the Shortcut already on the phone, unless the last three stay valid.
- The "unlock the iPhone" hint misleads when the real cause is the Shortcut itself.
- The newer Shortcuts app has no Automation tab. Do not send steps for a tab that is not there.
- Never print values, tokens or secrets. The Shortcut file holds the token, so it never goes into a log, a memo or the repository.
