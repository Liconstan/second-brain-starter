---
name: signable-docs
description: Use when [YOUR_FIRST_NAME] wants a document that someone must sign or fill in (an agreement, a statement, an acknowledgement, a form). Covers the Google Doc draft, Google eSignature fields, signer order, and how to hand it over to send.
purpose: A Google Doc with an eSignature field for every blank, assigned to the right signer in the right order, that [YOUR_FIRST_NAME] sends after one read of the memo.
helper_model: fable medium
model_why: agreements, statements and policy forms are compliance work; the browser field placement alone could run on a cheaper tier
created_by: agent
created: [SYNC_START_DATE]
last_used: [SYNC_START_DATE]
source: the Memo starter kit
---

# Documents someone must sign or fill in

## Goal

A blank line in a Doc is not fillable. Google eSignature makes the Doc fillable by the right person, and [YOUR_FIRST_NAME] sends the request. Use the signature tool for names, dates, addresses, and anything where somebody must fill in a blank and sign it as the right person. Whoever represents [YOUR_ORG] or [YOUR_FIRST_NAME] is always the first signer.

The result is one Doc per signer, in the Drive folder where the signed copy will live, with every blank a field of the right type for the right signer, a screenshot that proves it, and a memo with the link and the one step left (Request eSignature).

## Settings

- Where the documents live: [SIGNED_DOCS_FOLDER]
- Who represents [YOUR_ORG] as Signer 1: [YOUR_NAME], [YOUR_ROLE]
- The signing tool: Google eSignature in Google Docs. It needs a Google Workspace plan that has it. With another tool, rewrite Part 2 for it and keep Parts 1 and 3.

## When to use

- [YOUR_FIRST_NAME] asks for something someone must sign, initial, date or fill in: an agreement, a conflict of interest statement, an acknowledgement, a form, or a template for one of these.
- A Doc exists and fields must be added, moved, reassigned or removed.

## When not to use

- A document nobody signs (a memo, a proposal, a policy text with no signature block): draft it as an ordinary Doc.
- A web form that someone else hosts: fill it in, never submit it.
- A PDF that must be signed as a PDF: eSignature works on Google Docs only. Convert it to a Doc first, or stop and say so.

## Steps

### Part 1. Draft the Doc

1. Draft a Google Doc in the folder where the signed copy will live (board and policy documents usually in a governance folder of [SIGNED_DOCS_FOLDER]). One Doc per signer when several people sign the same form, named "<Document> - <Person>". Keep a template Doc with no name.
2. No agent notes in the Doc: no "Draft by Claude" line, no drafting comments. Say that it is a draft in the memo instead.
3. Write every blank as a label at the end of its own short line with nothing after it: "Signature: ", "Printed name: ", "Date signed: ", "Address: ". The trailing space is optional: an HTML import strips it, and the field adds its own spacing. No underscores, no tick boxes, no stray spaces or tabs before the field. A signer can only fill fields; they cannot edit text, and eSignature has no checkbox. Each field is a fixed block about 129 pt wide, so a field at the end of a long line wraps and leaves an ugly gap; after a short line it sits cleanly beside the label.
4. Never one field per yes-or-no question: the blocks make awkward gaps and the form is slow to sign. Instead:
   - Write the questions as a plain list of things to consider, with no field on any item.
   - Then one affirmation line, "I have nothing to disclose under A to F.", followed by an Initials field.
   - Then "Or, I disclose the following:" followed by one Text field. The signer uses one of the two.
   - Six yes-or-no fields become two. The same pattern fits "tick all that apply": one Text field after the list.
   - Use real list formatting (createParagraphBullets with NUMBERED_UPPERALPHA_ALPHA_ROMAN), never typed "A." letters.
   - Conflict of interest statements, when the organization keeps a conflicts register: disclosures live in the register, not in the statement. Link the register as a plain hyperlink. No "I disclose the following" box and no "give the row numbers" wording. The signer initials one line confirming the register is complete and accurate for them.
5. Prefill every fact you know instead of leaving a field: the person's name, their role (from `people/_team.md` and the person's file in `people/`; officer titles only if the vault confirms they are current), the organization, the period. A role the signer types themselves can come out wrong. Only the template keeps a Text field for the role. Keep "Printed name" blank: the Name field fills it from the signer.
6. Never print signer numbers in the document: no "(Signer 1)" or "(Signer 2)" in the text. The order is set in the eSignature panel, not on the page. A label next to a signature block can make a reader think the wrong person signs where. Rules:
   - The signer's own block is three tidy lines under its own heading ("4. Signature"): "Signature: ", "Printed name: ", "Date signed: ".
   - The receiving or countersigning part gets its own numbered heading that names what it is, and one line naming the one person who signs it with their confirmed title, then its fields. Example with made-up names:
     "5. Received for [YOUR_ORG]" (heading)
     "Received by Robin Lee, Director:"
     "Signature: "
     "Date received: "
   - Never put a label that looks like a third signer ("For the Secretary:", "For the Board:") next to the signature blocks. If the board or an officer records something later, say so in one plain sentence at the very end ("The board records its review of this statement in the register and the minutes.") with no label and no field.
   - The intro line that says where to return the document names the same person as the receiving block ("Return the signed statement to Robin Lee, Director."). Check the two agree in every copy. Officer titles (Secretary, Treasurer) only if the vault confirms the election; otherwise "Director".
   - Statements the organization receives from its own people (conflict of interest statements, for example): the person who represents [YOUR_ORG] receives every statement except their own, and another director receives theirs. Every copy, the template included, has one signer slot and one receiver slot (Signature and Date received only, no Printed name line). The template's signer slot is "Covered Person".
7. Text edits go through the Google Docs tools (update_doc). Docs stores runs of spaces as non-breaking spaces, so a plain containsText with spaces often finds nothing: use searchByRegex with "." or ".+" in place of spaces. A "\n" in replaceText starts a new paragraph.
8. To remove a field that is already in the Doc, no browser is needed. read_doc shows each eSignature field as an inlineObjectElement with its own index. Each field is 1 index long, so deleteContentRange from its startIndex to startIndex+1 deletes it (or delete the whole line). The eSignature panel does not list fields, so check the removal with a screenshot or a second read_doc, not the panel. An open Doc in the browser shows the removal within a second or two. Only inserting needs the Docs page. If a click lands on the wrong line, undo with Cmd+Z (Ctrl+Z on Windows) in the Doc, or delete the stray field this way.

### Part 2. Put in the eSignature fields (browser, Docs page only)

The Docs and Drive APIs cannot insert eSignature fields. Only the Google Docs page in a browser can.

Never tell [YOUR_FIRST_NAME] that fields cannot be added because a connector cannot add them. They can be added through the Docs page as below. Insert them; do not report them as impossible. If your session has no browser tools, stop here and give [YOUR_FIRST_NAME] the steps of this part, spelled out click by click.

9. Use the browser tools of your session (Claude in Chrome), in the browser profile the agents use, on the computer where the agents run, never on a device [YOUR_FIRST_NAME] is working on. Load the claude-in-chrome tools in one ToolSearch call and use browser_batch for each run of clicks. Before starting, check the account avatar at the top right of the Doc: the Drive connector and the browser profile can be different Google accounts, and a profile's name is not its account. The Doc must open as its owner or an editor.
10. Open the Doc. Tools > eSignature opens a side panel with "Insert fields for" (a signer dropdown), fillable fields (Signature, Initials, Name, Text field) and an auto-filled field (Date signed).
11. Dropdown > Manage signers.
    - Rename Signer 1 to the person who represents [YOUR_ORG] or [YOUR_FIRST_NAME], for example "[YOUR_NAME], [YOUR_ORG]".
    - Click "Add another signer". The new row is empty ("Enter Signer 2 Label") and Save stays grey until you type a label, so name it after the other party, for example "Sam Rivera"; in a template, "Covered Person" or the role. Save.
    - After Save the dropdown lists signers by these labels and selects the first one. Switch signer with the dropdown before each group of inserts. The labels are for reference only; emails are entered when the request is sent. Up to 10 signers.
    - Three or more signers: click "Add another signer" once per extra signer, and type each label before adding the next, since the dialog shows "Every label must be non-empty" and greys Save while any row is blank. Each row gets its own colour dot: Signer 1 light blue, Signer 2 green, Signer 3 purple. Signer 1 has no delete icon; every later row has a trash icon on its right. The rows' top-to-bottom order is the signing order. There is no drag handle to reorder: to change the order, retype the labels in the rows you want.
12. Insert a field: pick the signer in the dropdown, click in the Doc at the far right of the label line (that puts the cursor at the end of the line), then click the field button in the panel. The field appears at the cursor as a block 129 pt wide and 31.5 pt high with 9 pt margins, so a line with a field is about twice as tall as a plain line, which is normal.
    - Signature for signatures, Initials for the "nothing to disclose" affirmation, Name for printed names, Date signed for every date (including "Date received"), Text field for everything else (the free-text disclosure, addresses, the role in a template).
    - Initials and Text field insert exactly like Signature: same click at the line end, same panel button, same width. The Initials block shows a small person-stamp icon; the Text field block shows a T-in-a-box icon and is slightly shorter (28.2 pt in read_doc against 31.5 pt for the others).
    - The panel's "Insert fields for" signer applies to every field you insert until you change it, so switch it before each signer's group and check the colour on the screenshot.
13. Insert from the bottom of the document upward. Each field pushes the text below it down, so working upward keeps the lines you still have to click where the last screenshot showed them. For three signers that means Signer 3's block first, then Signer 2's, then Signer 1's. Take a screenshot after each run of inserts and check that every field sits after its label and has the right signer colour.
14. To reassign or move a field that is already placed: click the field block in the Doc. It gets selection handles and an "Assigned to" popover with a signer dropdown (and Manage signers). Pick another signer and the block changes colour at once; no re-insert needed. The panel's "Insert fields for" dropdown does not follow this change. To move a field: click it, Cmd+X, click at the end of the new label line, Cmd+V. It keeps its type and signer. Do not depend on the popover's "Edit" link: it may do nothing visible.
15. Never click "Request eSignature". It turns blue as soon as the Doc has any signature field, even if some signers have none, so it is not a completeness check: check each signer's fields on the screenshot. [YOUR_FIRST_NAME] sends.
16. Save a screenshot of the finished signature section for the memo (the tool's save_to_disk puts it in a system temp folder; copy it to your scratchpad with a descriptive name), and close the tab.
17. Read the Doc back with read_doc and count the inlineObjectElements: one per field. read_doc shows no signer and no field type, so the count is the only API check; signer and type come from the screenshot.

### Part 3. Report to [YOUR_FIRST_NAME]

18. One memo per batch, with for each Doc: the link, the signer list (for example "Signer 1 [YOUR_NAME], [YOUR_ORG]: signature, date received. Signer 2 Sam Rivera: initials for nothing to disclose, one disclosure text field, signature, name, date signed"), the facts you prefilled and where they came from, and any text you changed to make it fillable.
19. The one step left, spelled out with the device, app, menu and button: "On your computer, in Chrome, open <link>. Click Tools, then eSignature. In the side panel, click the blue Request eSignature button at the bottom, type the signer emails (Signer 1 is you, Signer 2 is <name>), then click Request. Each signer gets an email; the signed PDF lands in Drive next to the Doc." Warn that the request locks the Doc text, so edits come first.
20. If something stopped you (eSignature missing from the Tools menu, a plan or shared-drive message, a field that would not insert), stop after the first Doc and quote exactly what the screen said. Do not try workarounds.

## Done when

- One Doc per signer in the right Drive folder, no agent notes, no signer numbers in the text, every known fact prefilled.
- Every blank is a field: right type, right signer, at the end of a short label line; the screenshot shows each signer's colour on each of their fields.
- Signer 1 is the person representing [YOUR_ORG] or [YOUR_FIRST_NAME]; the receiving block and the return line name the same person.
- read_doc counts as many inlineObjectElements as fields you placed.
- The tab is closed, the screenshot is in the scratchpad, and the memo has the link, the signer list, the prefilled facts and the Request eSignature step.
- Request eSignature was never clicked; nothing was sent.

## Pitfalls

- A field per yes-or-no question, or fields mid-line or after long lines (steps 3 and 4).
- "(Signer 1)" or a role label that reads as a third signer in the text (step 6).
- A helper reporting that fields cannot be added. They can, in the Docs page.
- Treating a blue Request eSignature button as "all signers have fields".
- Trusting the eSignature panel to list fields: it does not; use a screenshot or read_doc.
- Trusting read_doc for signer or type: it shows identical inline objects.
- Inserting top-down, so later clicks land on lines that moved. Bottom-up avoids misclicks.
- Forgetting to switch "Insert fields for" before the next signer's group: the field lands with the wrong colour. Fix it with the field's own "Assigned to" popover rather than deleting and re-inserting.
- Adding a second signer row before typing the first label: Save greys out with "Every label must be non-empty".
- Assuming the browser profile name is the Google account; check the avatar.
- Browser dialogs (alert or confirm) hang the extension. Trash a test Doc with the Drive tool, not the Docs page.
- Testing with real addresses or on the live document. Test on a copy, with signers "Test One" to "Test Three" at example.com, and never send the request.

## Known limits

- eSignature must be available on the Google Workspace plan; check the Tools menu once. It works on Docs inside a shared drive.
- Field types are Signature, Initials, Name, Text field and Date signed only. No checkbox, no radio, no dropdown, no address type: rewrite those blanks as Text fields.
- Fields have a fixed size (about 129 pt wide) and cannot sit inside a line of text without wrapping. Design around it: fields only at the end of short lines, and as few fields as the form allows (step 4).
- The Docs API can delete a field (it is an inline object) but not insert one, and cannot read a field's signer or type.
- Up to 10 signers. What the signer sees when filling a Text or Initials field is untested by this skill, since a test request is never sent.
- Drive upload through the browser extension, when the Drive API tool cannot take a large file: create a file input element with javascript_tool, load it with file_upload, then dispatch a drop event on the folder. The File object can be renamed in that step.
