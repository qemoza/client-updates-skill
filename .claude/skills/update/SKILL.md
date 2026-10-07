---
name: update
description: Draft a short client update from the record of the work. Reads whatever sources exist (task board, code, the client's Slack or email thread, call notes, ad or analytics numbers, the end of day log), writes three or four short paragraphs with no bullet points, merges into one update when a draft for that client already exists, saves it as a draft and never sends it. Use for "/update", "/update {client}", "/update {client} weekly", "write the client update", "draft today's update for {client}", "weekly report for {client}".
---

# /update: draft a client update from the record

You write the first draft of a client update. A person reads it, changes it and sends it.
You never send anything.

A client reading an update wants three answers, in one read on a phone:

1. Is my thing moving?
2. Is anything waiting on me?
3. Is anything wrong?

Every choice below serves those three questions.

## How it is run

| The person types | You do |
|---|---|
| `/update {client}` | One update for that client |
| `/update {client} weekly` | The same update, plus two or three numbers |
| `/update` | Ask which client. If the setup file lists clients, offer to draft all of them |

If you cannot tell which client it is for, ask one question: who is this update for?

## Hard rules

These hold in every step.

- **Draft only.** Never post, email, message or send the update anywhere. If the person asks you to send it, tell them to copy it and send it themselves.
- **Read only.** You may read the sources. Never change, close, move, post or edit anything inside them.
- **Facts come from the record.** A line goes in the update only if it is on the facts sheet. Your own memory of the conversation is not a source for what shipped.
- **Never invent** a number, a date, a promise, an answer or an ask.
- **Never sound more sure than the facts.** If something is still being tested, the update says so.
- **Keep it private.** The `client-updates` folder holds client names and client facts. Never put a password, an API key or a token in it.

## Step 0: Setup, the first time only

Look for `client-updates/setup.md` in the folder you are working in.

If it is there, read it and go to Step 1.

If it is missing, ask the person these questions in one message. Tell them every answer can be: I do not have that.

1. Which clients do you write updates for? For each one, the first name you greet and one line on what you do for them.
2. Do you say I or we to your clients?
3. Where is your task board? (the tool, and whether Claude is connected to it)
4. Where is the code or the work files? (folder paths, if any)
5. Where do you talk to each client? (a Slack channel, an email thread, something else)
6. Where do your call notes or transcripts go?
7. Do you report numbers to any client? From which account? (ads, analytics, a store, a CRM)
8. Do you keep an end of day log or a daily note? Where?

Write the answers to `client-updates/setup.md` in plain words. If a source needs a key, tell the person to put it in their own credentials store or a `.env` file that stays on their machine.

Tell the person once: the `client-updates` folder will hold client names and client facts, so keep it out of any public repo or public folder.

Setup must never block the first update. If the person wants to skip it, go on with what they give you and ask for the rest by paste.

## Step 1: Pick the day

- **Daily:** the update covers the most recent weekday before today, unless the person names another day.
- **Weekly:** the update covers the last full week, Monday to Sunday, or the seven days the person names.

Two names are used in every file path below. Write them the same way every time, or a teammate's draft will not be found.

- `{date}` is the day the work happened, written like `2026-03-09` (year, month, day). For a weekly report it is the last day of the week it covers. It is never the day the update is sent.
- `{client}` is the client's first name in lower case, like `nora`. If a folder for that client already exists under `client-updates/drafts`, use that folder as it is.

Say the day or the week in one line, then carry on. The person can correct it. Do not wait for a reply.

## Step 2: Look for a draft that already exists

Look for `client-updates/drafts/{client}/{date}.md`, or `{date}-weekly.md` for a weekly report. A teammate, or an earlier run, may have written one.

If none exists, go to Step 3.

If one exists, the client still gets **ONE** update. You will merge into it.

- Read it fully now.
- If its first line is `sent: yes`, it already went out. Leave that file alone. Tell the person, and ask whether they want a new update for the next day.
- Otherwise save a copy as `client-updates/drafts/{client}/{date}-before-merge.md`, so the first writer's words are never lost.
- Every fact in it goes onto the facts sheet in Step 4, tagged `[earlier draft]`.

## Step 3: Gather the facts

There are six places the facts come from. **Every one of them is optional.** Use the sources named in the setup file. For each one, try in this order:

1. A connected tool you can already read (a connector, an MCP server, a command line tool, a local folder).
2. A file or export the person points you to.
3. Ask the person to paste it.

Read what you can reach on your own first. Then ask for everything else **in one message**, never one question at a time. In that same message, ask two more things: do they have a call with this client today, and are they waiting on the client for anything. The person can answer any part with: nothing there.

What the person tells you counts as a source. Tag it `[person]` on the facts sheet and use their own words for how finished it is.

| Source | What you take from it |
|---|---|
| **The board** (task or project tool) | Tasks finished on that day. Tasks in progress. Tasks waiting on the client. |
| **The code** (or the work files) | What shipped on that day. In a git folder, read the log for that day. Work merged into the main branch counts as shipped. Work on an open branch is in progress. |
| **The channel** (Slack or email with the client) | What the client already knows. What they asked and did not get an answer to. Read the last few days. |
| **The calls** (notes or transcripts) | What was promised to the client, and what the client promised to send. Read the last two weeks, because an open promise still counts. |
| **Their accounts** (ads, analytics, store) | Numbers. Only for the weekly report, or when a number is the news. |
| **The end of day log** | What the person or their teammates wrote down that the tools do not show. |

If the person has no end of day log, offer this once, in the same message: tell me in a few lines what you did and I will save it to `client-updates/log/{client}/{date}.md`, so next time there is a record. If they already told you what they did, save that and do not ask again.

If every source is empty, nothing was pasted and there is no earlier draft, there is no update. Say: nothing to report for {client}. Never fill an update with guesses.

## Step 4: Write the facts sheet

Before you write a word of the update, write the facts sheet. Each line says where it came from.

```
Client: {first name}. Covers: {the day or the week}.
Call with them today: {yes, no or not known}

ALREADY SAID (they know this, leave it out)
- {thing} ({where and when it was said})

FACTS
- [board, finished] {what is now true}
- [code, shipped] {what is now true}
- [board, in progress] {what is moving} {the hedge, in the source's own words}
- [call, {day}] {what was promised, and by whom}
- [accounts, {period}] {number, copied exactly}
- [accounts, worked out] {a sum or a division, with the working}
- [log] {what was written down}
- [person] {what the person told you}
- [earlier draft] {a fact that only the earlier draft holds}

THEY ASKED (questions from the client with no answer yet)
- {the question} ({where and when}) {the answer, if a fact above holds it}

WAITING ON THEM
- {the exact thing, and what it blocks}

HELD BACK (real work the client does not need to read)
- {how it works under the hood}
- {tidying, refactors, internal fixes they never saw}
- {a scary number they cannot act on}
```

Rules for the sheet:

- One fact per line. Say what is now true for the client.
- Keep the hedge with the fact, in the words the source uses. Needs testing and still being tested are different things.
- Copy every number, name and date exactly as the source has it.
- A fact that is both finished and already said to the client goes under `ALREADY SAID`.
- `WAITING ON THEM` holds only things the record or the person shows you are blocked on. If there are none, the section is empty. If the record does not show whether the thing has arrived since, keep it and flag it in Step 7.
- One fact that shows up in two sources is still one line. Put both tags on it.
- An `[earlier draft]` fact is one you did not check yourself. Keep it, and say so in Step 7.
- You can see that code is merged. You often cannot see that it is live for the client. When you cannot, note it on the line and flag it in Step 7.
- When you are unsure whether the client already knows something, keep it in `FACTS` and flag it in Step 7.

Save the sheet to `client-updates/drafts/{client}/{date}-facts.md`, or `{date}-weekly-facts.md` for a weekly report.

## Step 5: Write the update

The shape:

```
Hey {first name}, quick one.

{What got finished. One sentence per thing. Say what is now true for them.}

{What is moving now. If it is still being tested, say so.}

{The one thing you need from them, in a sentence. If you need nothing, this paragraph is not there.}
```

Three or four short paragraphs, counting the opener. It should read like a person typing on a phone.

**The shape rules**

- No bullet points. No headers. No lists.
- Short sentences. Plain everyday words. A child could read it.
- First person. Use the I or we from the setup file.
- High level. One sentence per thing. Say the outcome and leave out how it was built.
- Write in the language the client writes in.
- No dashes used as punctuation. Use a period or a comma. A hyphen inside a word or a link is fine.
- No quotation marks. No emojis. No sign off and no name at the end.
- A link, if there is one, goes on its own line at the end.

**What to cut**

- Anything under `ALREADY SAID`. They know it.
- Everything under `HELD BACK`. How it works under the hood is yours to know.
- A scary number they cannot act on.

**What to keep, however short it gets**

- Bad news, and anything that changed.
- The hedge. Still testing it stays.
- A date or a number they have to act on. A number they decide on that went down is news. Say it plainly, and give a reason only if the record gives one.

**The ask**

- It is the last paragraph, in one or two sentences, and it says what it blocks.
- It comes only from `WAITING ON THEM`. If that section is empty, there is no ask. Never make one up so the update looks complete.

**A question the client asked**

- These sit under `THEY ASKED` on the facts sheet.
- If the facts hold the answer, the update answers it.
- If they do not, leave the question out of the draft and put it first in the Step 7 list. Only the person can answer it.

**Words that are earned**

- Say done, live or finished only when the facts sheet shows it shipped, or the person used that word themselves. Otherwise say worked on, got it working, or still testing.
- Never write a new date or a new promise. If a date was promised on a call, it is on the facts sheet and you may repeat it exactly.

**When you are merging into an earlier draft**

- Keep every distinct fact from both. When both say the same thing, it becomes one sentence.
- Keep the first writer's sentences where they already say it well.
- One opener. One voice. When more than one person did the work, change I to we.
- One ask at the end. If there are two real asks, keep the one that blocks the most work and show the other one to the person in Step 7. They decide.
- Still three or four short paragraphs. More facts means more sentences in a paragraph. It never means more paragraphs.
- Never drop a line from the earlier draft without saying which line and why in Step 7.

## Step 5b: The weekly report

The weekly report is the same message with two or three numbers added. The opener becomes: Hey {first name}, here is the week. Nothing else changes.

- The numbers get one short paragraph of their own, right after the opener. So a weekly report runs to five short paragraphs at most.
- Say which days the numbers cover.
- Pick the two or three numbers the client makes a decision on. Last week's figure next to one of them is fine. Every other number stays on their dashboard.
- Numbers come only from the account, an export or the person's paste. Copy them exactly. Never guess and never fill a gap.
- A simple sum or a division is fine. Round it to two decimal places. Show the working on the facts sheet so the person can check it.
- Compare to the week before only if you have last week's number from the same source.
- If the source gives no currency or unit for a number, write the number as it is and flag it in Step 7.
- If you cannot get the numbers, ask the person to paste them. If there are still none, write the update without them and say so in Step 7.

## Step 6: Check your own draft

Read the draft against the facts sheet, sentence by sentence.

- Does every sentence trace to a line under `FACTS`, `THEY ASKED` or `WAITING ON THEM`? Cut any that does not.
- Is every number, name and date the same as on the sheet? Check each one character by character.
- Did a hedge go missing? Put it back.
- Did you add a word that makes it stronger than the fact, or a promise, a reason or a next step that nobody wrote down? Cut it.
- Is anything from `ALREADY SAID` or `HELD BACK` in there? Cut it.
- Does it answer the three questions: is it moving, is anything waiting on me, is anything wrong?

## Step 7: Save the draft and hand it over

Save the update to `client-updates/drafts/{client}/{date}.md`, or `{date}-weekly.md` for a weekly report. The file holds the message and nothing else, so it can be copied as it is.

Then show the person, in this order:

1. The draft, in a code block.
2. **Check before you send.** A short list, most important first:
   - a question from the client that the facts could not answer
   - anything the client may already know
   - anything you could not confirm is live
   - an ask where the record does not show whether the thing has arrived
   - facts that came only from an earlier draft
   - what you changed or dropped in a merge, and a second ask you left out
   - a number with no currency or unit, and any number you worked out yourself
   - any source you could not read
   Leave out any item that has nothing in it.
3. What you held back and what you left out because the client already knows, in one line, so they can put something back if it is the news.
4. This line: Read it, change it into your own words, and send it yourself.

If the person has a call with that client today, say so. They may want to skip the written update and cover it on the call.

When the person later tells you an update was sent, add `sent: yes` as the first line of that draft file. Only do it on their word.

## What you never do

- Send, post or schedule the update.
- Mark a draft as sent on your own.
- Write over a draft that is marked as sent.
- Put a password, a key or a token into the `client-updates` folder.
- Change anything in the board, the code, the channel or the accounts while you gather facts.
