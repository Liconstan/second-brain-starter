---
name: my-writing-voice
description: "Use when drafting anything [YOUR_FIRST_NAME] sends under their own name (emails, Slack messages, DMs, applications, outreach) so it sounds like [YOUR_FIRST_NAME] and avoids AI-sounding patterns."
---

# The writing voice of [YOUR_FIRST_NAME]

Use this for any text [YOUR_FIRST_NAME] will send under their own name: emails, Slack posts and DMs, LinkedIn messages, grant or application answers, and outreach.

This is a hand-made skill: [YOUR_FIRST_NAME] owns every line, and an agent changes it only when asked. The method below works on day one. The parts that are personal (greeting, sign-off, filler words, reference emails) start with neutral defaults in "Settings" and in examples marked **Example, replace**. Replace them with real ones as the agents collect sent mail and chat messages in `writing/` and notes in `me/writing-voice.md`. The fastest way: send an agent this memo: "Read writing/ and me/writing-voice.md, and propose updates to my writing voice skill. Show me five real examples for each claim."

## Settings

Fill in later. Until a line is filled, use the default after it.

- Greeting in email: [EMAIL_GREETING]. Default: "Hi {Name}," and "Hey {Name}," for peers.
- Sign-off in email: [EMAIL_SIGNOFF]. Default: "Best," then the first name.
- Filler words, used lightly: [VOICE_FILLER_WORDS]. Default: "just", "Also,", "I think", "actually", "If you have time".
- Other habits and notes: [WRITING_STYLE_NOTES]. Default: none beyond this skill.
- AI-writing detector: [AI_DETECTOR_TOOL]. Default: Pangram. The score lessons below were learned with Pangram and hold for detectors of the same kind.
- Booking link for a real conversation: [BOOKING_LINK] (see "Calendar link").

## The goal

Write the shortest version that still says everything it needs to, in the voice of [YOUR_FIRST_NAME], with as low an AI-detector score as possible.

Three things count as "better," in this order:

1. **The content is right.** Every ask, date, link, and detail needed is there. Never cut substance to lower a score.
2. **It reads as human.** Lower "AI" and "AI-assisted" percentages are better.
3. **It's short.** Between two versions that say the same thing, the shorter one wins.

This guide should rest on real material: about 40 hand-typed sent emails, about 35 Slack messages, and detector reports on AI drafts. Until `writing/` holds that, the lessons below come from a long series of tests by the person who built this kit, and they carry over well.

## What makes a draft score 100% human

Several emails were rewritten until the detector scored them 100% human. Two lessons came out of it.

### First lesson: texture (an email went from 70% AI to 100% human)

The content barely changed. What changed:

1. **First person and active.** "I've been drafting" instead of "We're building." "Mostly I'd reach out" instead of "It would mostly mean."
2. **Filler words, used lightly** (see Settings).
3. **Plain nouns.** "a small pot of money" instead of "a regranting pool".
4. **Conversational asks.** "Would you mind...", "can you...", "whatever's easier", "Comments in the doc are easiest, but...".
5. **Exclamation marks** on the greeting or a warm line: one or two per email at most, and often none. Count them before you finish. In a blind test, the real messages used about half as many exclamation marks as the model drafts.

### Second lesson: reasons and specifics beat casual words (an email went from 100% AI to 100% human)

The first rewrite used all the texture tricks and still scored 100% AI. It failed because:

- **Short, identical sections.** Four sections, each two or three short sentences ending in a question.
- **Casual phrases stacked together.** "Robin just agreed to", "our research stuff", "put you on our website" packed into tiny sections reads as AI imitating casual.
- **Flattery and stock lines.** "You know this field better than anyone", "the kind of thing I'd love an advisor's eyes on", "And the conference too, if it fits."
- **No specifics.** No dates, no reasons, nothing that only fit this reader.

What fixed it:

- **Fewer, longer sections** (two instead of four), with some longer sentences that connect ideas the way a person talks.
- **Lead with the real reason.** "Our funder's main feedback on our grant was that we should be getting more input from people who know the field, especially on which projects we fund. So I'm asking a few people to be advisors..."
- **Concrete details:** "before we send it out in October", "Since it's meant to come after the intro course", "The spring conference too, if there's room."
- **A named first task:** "A concrete first ask: ..."
- **No flattery.**

Other emails that scored 100% human had the same strengths: named people, a parenthetical explaining the setup, and the writer's own reason for the ask ("the biggest bottleneck right now is mentors, since most of the senior people are already taking on a lot").

### Reference email (Example, replace with a real one from `writing/`)

> Hi Sam,
>
> Thanks for adding me to the research community Slack!
>
> **Advising and small grants.** Our funder's main feedback on our grant was that we should be getting more input from people who know the field, especially on which projects we fund. So I'm asking a few people to be advisors, and Robin just agreed to. Would you be open to it too? It'd mostly be me reaching out now and then, and we'd list you on our website.
>
> A concrete first ask: we're about to give out a small pot of grants to projects in our program (list of recipients here). If you have time before we send it out in October, can you skim it and let me know if anyone seems like a bad fit?
>
> **Course and newsletter.** Here's the draft of the course and the feedback form. Since it's meant to come after the intro course, I mostly want to know where it overlaps too much. Also, once the course opens, could we get it into your newsletter? The spring conference too, if there's room.
>
> Let me know if you have any questions!

Rule of thumb: **give the reason, name the specifics, ask plainly, in first person. Don't characterize, reassure, sell, or flatter.**

## What the detector punishes

**Scored as AI:**
- Abstract descriptions of a thing instead of facts about it: "It's research-track and project-based, aimed at people who've done an intro course and want to start doing research."
- Soft idioms: "with an eye to overlap", "round things out well", "I'd love an advisor's eyes on".
- Selling the ask: "It's a light commitment: ...", "Any reactions would help a lot."
- Reassurance chains and purpose tails: "so nothing is final yet, but I wanted you to see...", "so I can plan around it."
- Generic praise or flattery: "your view of the field would be a big help", "You know this better than anyone".
- Many short, same-shaped sections, even with casual wording.

**Scored as AI-assisted:**
- Clean, even, impersonal phrasing, even when factual: "It would mostly mean occasional input on our programs, and we'd list you on our website."

**Scored as human:**
- Concrete, checkable facts: "None of our upcoming programs are on your events page yet."
- Direct questions with specifics: "Could you add our conference (Boston, March 12-14)?"
- Plain next steps: "I'll send details on our course and spring program once applications open."
- The writer's own reasons and dictated wording, kept close to verbatim.

## The core of the voice

These are sensible defaults. Change any line that does not match [YOUR_FIRST_NAME].

1. **Short.** Most emails are 2 to 5 sentences. Most Slack messages are one or two lines. Short means few topics, not choppy sentences.
2. **Ask early.** One line of connection at most, then the ask within the first two sentences.
3. **Bold headers for multi-topic emails.** When an email covers two or more distinct topics, use a short bold label for each (for example **Conference.** or **Course feedback.**) followed by plain sentences. Merge related topics under one header rather than making many tiny sections. Skip headers in one-topic emails and in Slack.
4. **A short closing line.** End with one brief line like "Let me know if you have any questions!" or "Let me know what you think." Keep it to one sentence, then the sign-off.
5. **Light hedging, flat facts.** "I think" and "just" are frequent. Pushback is plain: "I still don't see the changes on there."

## Hyperlinks

Scan every draft for places a link helps the reader act, and add them. Link the words themselves, not a bare "here" where avoidable.

- Docs, forms, and drafts the reader is asked to look at (a course draft, a feedback form, an interest form, a brief).
- Events and programs of [YOUR_ORG] by name. Their links are in `me/key-links.md`.
- The recipient's own work when it is mentioned (a paper, talk, blog, website).
- Outside pages being discussed.

If a link is needed but unknown, leave a clear marker in curly brackets like {link to the content form} and say so in chat.

## Email

**Greetings.** See Settings. Bare "Hi," for groups. No greeting on quick replies and ops forwards. The first sentence can stay on the greeting line. Never "Dear".

**Sign-off.** See Settings. Quick replies often have no sign-off. Avoid stock sign-offs such as "Warm regards", "Kind regards", "Warmly" unless Settings says otherwise.

**Openers.** "It was great [seeing / catching up with / finally meeting] you at {event}!" "Hope you're doing well!" Or straight in: "Hi, Alex kindly agreed to give feedback on the paper draft."

**How to ask.** A question or plain imperative, lightly softened:
- "Do you mind rebooking for another time?"
- "Would you mind taking a look for overlap?"
- "Is it possible to just move my payment back into the grant pool?"
- "Do you have any folks in your network that you think would be a good fit?"
- "If it gets off the ground, would you be interested in helping to run it? ... Just putting it out there as a consideration for now. :)"

**How to thank.** "Thanks so much", "Thanks again for...", "Thanks for {specific thing}", sometimes with the plain value: "It will save us a lot of time. :)"

**Lines to calibrate against (Example, replace with real lines from `writing/`):**
- "Hey Jordan, It was great finally meeting you at the workshop. We should keep the lines of communication open about hiring in this field."
- "I really appreciate the interview process. It is refreshing not to have another application to fill out. But just FYI, I don't think we have gone through any formal application process with you before."
- "Thanks for thinking about it, Alex! No worries at all if nothing comes to mind, but I appreciate you keeping it on your radar."
- "Fantastic! Yes, please do fill out the form so we have you in the system. Looking forward to chatting on Friday."

**By audience.**
- Internal and ops: terse, imperative, often no greeting, lowercase start okay.
- Funders: short, warm, not flowery. Numbers stated bluntly. Corrections direct but kind ("just FYI...").
- Senior researchers and academics: same warmth plus one line of shared context and the real reason for the ask. Don't get stiffer, and don't flatter.
- Peers: "Hey", an exclamation mark, maybe ":)".

**People at the same organization.** When emailing two or more people at the same organization, mention the other outreach in one line: "Just so you know, I also emailed Sam about advising us and getting our programs into the newsletter." If the other person might be the better owner of an ask, say so and let them redirect: "If you'd rather be the one I talk to about that, just let me know!" Exception: don't name one person to another when they may be competing for the same thing (for example two candidates for one role). Flag that choice in chat instead.

**Calendar link.** The booking link is [BOOKING_LINK]. Offer it only when there's something worth a real conversation: a partnership or collaboration, a new advisory or leadership role, an open-ended decision, or several related asks that are easier to talk through. Don't add it to simple asks like filling out a form, skimming a doc, or updating a listing. Keep it to one line, linked on the word "calendar": "If it's easier to talk through any of this, you can grab time on my calendar."

## Slack

- One or two lines. Several short messages in a row rather than one long one.
- Starts: "hey", "Yeah", "yup", "Ok", "Ah", "Hmm..", "Btw,", "Thanks for...". Lowercase starts are normal.
- Asks: "when you have a chance", "was wondering if you could", "Is it possible to...? No worries if this is not possible", "Wdyt?". @-mention the person.
- Feedback: agree first, then hedge and give replacement wording with a short reason. "I would just avoid saying 'best in class'. Maybe just say more careful or more thorough."
- Vocabulary (defaults, replace with real ones): "sounds good", "I'm thinking...", "I would be ok if", "feel free to", "no worries", "a bit", "pretty", "promising", "FWIW", "Wdyt".
- Emoji: rare, one at the end at most.
- Structured community announcements follow the skill in `skills/slack-announcement/` instead.

### Slack posts to the team: channels and threads

The list above fits quick DMs. Posts to a team channel or thread read differently. In a blind test, real team posts beat every model, because the models chopped them into short lines with an exclamation mark and a "Wdyt?". Team posts:
- Narrate what happened in order, in full sentences: "Spoke recently to Jordan who generously offered... I told them that... and they agreed. I will put @Sam in the email chain to arrange for this."
- Run as one or two flowing paragraphs, not a stack of one-line messages. A sentence may end with no period.
- Open with the news or "Update:" or "Okay I've...", with no greeting and no sign-off.
- Hedge the writer's own view softly: "Preliminarily, I think...", "We should probably also...", "this seems to be a good forcing function".
- Put the @-mention at the start of the ask, as a full question: "@Robin What do you think about sending it out to all our newsletter subscribers..."
- Close the floor openly: "Let me know if others have different thoughts."
- Use no exclamation marks, and keep "Wdyt" for DMs.
- A new thread in any channel opens with an emoji and a bold subject line, then the content in the thread. The exact two-part format is in the `slack-message-drafts` skill.

### How to run work in team messages

Defaults that make team messages move work forward. Drop any that [YOUR_FIRST_NAME] does not want.
- **Propose, set a deadline, go.** For a decision that is easy to undo, say what will happen and when, and that it goes ahead unless someone objects: "I'm going to move the weekly meeting to Tuesdays from next week unless anyone objects." Ask first only for one-way doors: money, anything public, and anything with a partner or a funder.
- **Named owners.** Every hand-off @-mentions the people it is for, one or several, and says what each one should do, with enough context to decide. When several share a task, say who leads. Never an unnamed ask to a whole channel.
- **Say how sure you are**, when it helps others weigh in: "I'm about 60% we keep the same venue."
- **Project talk goes in the project channel**, not in DMs, so others can see it and join in.
- **Invite pushback, with no penalty for being wrong:** "Let me know if others have different thoughts", or "I'm very open to updating on this."

## Hard rules

- Never use em dashes or en dashes. Use " - ", commas, periods, or parentheses. Write ranges as "12-14".
- Use straight apostrophes and quotes, not curly ones.
- No semicolons.
- No aphorisms or rhetorical asides.
- No flattery ("better than anyone", "so many", "exactly the kind of").
- Don't reuse the same sentence or paragraph across several recipients. Each message needs at least one detail that only fits that person.
- Keep the dictated wording of [YOUR_FIRST_NAME] close to verbatim. Detectors consistently score it as human.
- Don't add fake typos or invent details to sound specific. Only use facts that are true.

## Patterns to avoid

| Pattern | Flagged example | Write instead |
|---|---|---|
| Abstract description | "It's research-track and project-based, aimed at people who've done an intro course and want to start doing research." | "I've been drafting a course for people who've done an intro course." |
| Label, colon, tidy list | "It's a light commitment: occasional input on our programs and being listed on our website." | "It'd mostly be me reaching out now and then, and we'd list you on our website." |
| Impersonal "It would mean" | "It would mostly mean occasional input on our programs." | "Mostly I'd reach out occasionally for input." |
| Formal "We're building" | "We're building a Research Methods Course for..." | "I've been drafting a research methods course and want to make sure it doesn't just duplicate the intro one." |
| Ask without a reason | "Would you be open to advising us?" (alone) | Lead with why: "Our funder's main feedback was that we should get more input from people who know the field... So I'm asking a few people to be advisors." |
| Flattery | "You know this course better than anyone, so..." | "Since it's meant to come after the intro course, I mostly want to know where it overlaps too much." |
| Soft idiom | "with an eye to overlap" / "round things out well" / "I'd love an advisor's eyes on" | Say it plainly or cut it. |
| Generic praise | "Your view of the field would be a big help." | Name the reason or cut it. |
| Three items in a neat row | "a quick skim... to sense check them, and to flag any you'd disagree with" | "can you skim it and let me know if anyone seems like a bad fit?" |
| Reassurance chain | "It's still under consideration, so nothing is final yet, but I wanted you to see the proposed setup." | "It's still under consideration, but I wanted you to see it." |
| Vague value statement | "Any reactions to the draft would help a lot." | "Would love any comments." |
| Purpose tail | "...so I can plan around it." | "...and roughly when you could start." |
| Tidy tag line | "And the conference too, if it fits." | Give the specific: "The spring conference too, if there's room." |
| Filler offer | "Happy to set up a call if that's easier." | Use the calendar line only when a real conversation is warranted. Otherwise just the closing line. |
| Many tiny same-shaped sections | Four sections, each two short sentences plus a question | Merge into two sections with longer, connected sentences. |

Also never: "I hope this email finds you well", "I wanted to reach out", "Following up on my previous email", "delighted", "thrilled", "leverage", "synergy", "touch base", "at your earliest convenience", "Please don't hesitate to reach out", "delve", "robust", "seamless", "exciting opportunity", "I hope this gives a clearer sense of...", apologizing for length, or summarizing at the end.

## Process (iterative)

1. **Check the Gmail Drafts first** for an existing draft to the same person, and build on it instead of creating a duplicate.
2. **Read the reader's file** in `people/`: the section "How [YOUR_FIRST_NAME] writes to them" has the channel, the tone and the latest real message.
3. **Draft from the facts.** For each ask, write down the real reason and at least one specific (date, name, number, what the person said). Lead with the reason.
4. **Group topics.** Aim for two or three sections at most. Merge related asks.
5. **Add links** everywhere they help the reader act.
6. **Cut.** Remove any sentence that describes, reassures, sells, or flatters rather than informs or asks. If the email is over about 150 words, check whether every topic is needed.
7. **Add texture lightly.** First person, a few filler words, plain nouns. Don't pile casual phrases into short sections.
8. **Check the table and hard rules.** Rewrite any match.
9. **Score if possible.** If a detector result is available (pasted by [YOUR_FIRST_NAME], or from a connected detector), rewrite the windows marked AI first, then AI-assisted. Rescore.
10. **Stop when** the detector shows human written, or further changes would cost content or make the text odd. Pick the shorter version when scores tie.
11. **Vary across recipients.** When drafting several similar emails, change structure and wording for each. If two recipients share an organization, mention the other outreach (see "People at the same organization").
12. **Flag assumptions and missing facts in chat,** not in the draft.

## Learning loop

When [YOUR_FIRST_NAME] pastes detector results or edits one of your drafts:

1. Compare the flagged or edited text with what replaced it, and note which parts scored human.
2. Name the pattern in one line.
3. Fix the current draft.
4. Save the version that was sent, word for word, in `writing/` and in the reader's file in `people/`.
5. Offer to add the pattern to the tables above, with the example and a better version, and to swap an **Example, replace** item for the real one. Propose the full updated skill for [YOUR_FIRST_NAME] to save; don't edit it silently.
