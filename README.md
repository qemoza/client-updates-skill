# Client Updates Skill

A skill for Claude Code that writes the first draft of your client updates. You read it, you change it, you send it.

This is the skill we use for our own client updates. We took our clients and our tools out, so it works for any agency.

From the video [Clients Going Quiet? Send This Update](https://youtu.be/7sXI4dK1pug).

## What it does

You type `/update` and a client's name. Claude looks at the record of your work. Then it writes a short update the client can read on a phone.

The update has this shape:

1. A one line opener.
2. What got finished.
3. What is moving now.
4. The one thing you need from them.

That is three or four short paragraphs. There are no bullet points. If you need nothing from the client, the last part is left out.

It only writes a draft. It does not send anything.

It answers the three things a client wants to know:

- Is my thing moving?
- Is anything waiting on me?
- Is anything wrong?

## Who it is for

Anyone who does work for clients and has to tell them how it is going. Agency owners, freelancers, account managers.

You do not need to be an engineer. If you can type a message, you can use it.

## What you need

- **Claude Code.** Get it at [claude.com/claude-code](https://claude.com/claude-code). Claude Code is paid. A paid Claude plan covers it.
- **Somewhere your work leaves a trace.** A task board, your code, a Slack channel, an email thread, call notes, or a note you write at the end of the day. One is enough to start.
- **A few minutes to read each draft.** Claude writes the first draft. You are still the one who sends it.

You do not need to connect anything on day one. If Claude cannot read a source, it asks you to paste it.

## Set it up

1. Install Claude Code. Follow the steps on the page linked above, then sign in.
2. Pick the folder on your computer where you keep your client work. If you have none, make a new empty folder and call it `clients`.
3. Open Claude Code in that folder.
4. Copy the text in the box below. Paste it into Claude Code, where you type your messages, and press enter.

```
Set up the client update skill for me.

1. Get this repo: https://github.com/qemoza/client-updates-skill
2. Copy its .claude/skills/update folder into .claude/skills/update in this folder.
3. Do not change any other file of mine.
4. Tell me when it is ready and how to run it.
```

5. Claude may ask if it is allowed to download and copy the files. Say yes.
6. Close Claude Code and open it again in the same folder.
7. Type `/update` where you type your messages and press enter.

The first time, Claude asks you some questions. Who are your clients? Where is your task board? Where do you talk to each client? You can answer any of them with: I do not have that. Claude saves your answers in that folder, so it only asks once there.

### If you downloaded the ZIP

1. On the repo page, press the green **Code** button, then **Download ZIP**.
2. Unzip it. You get a folder named `client-updates-skill-main`.
3. Open Claude Code in the folder where you keep your client work.
4. Paste this into Claude Code:

```
The client update skill is in my Downloads folder, in client-updates-skill-main.
Copy its .claude/skills/update folder into .claude/skills/update in this folder.
Do not change any other file of mine.
```

Let Claude copy the files for you. The skill sits in a folder named `.claude`, and that folder is hidden. To see hidden folders on a Mac, press Command, Shift and the period key in Finder. On Windows, open the View menu in File Explorer and turn on hidden items.

### Where the skill goes

| You want it in | Put the `update` folder here |
|---|---|
| One project | `.claude/skills/update` inside that project |
| Every project on your computer | `.claude/skills/update` inside your home folder |

## Run it

| You type | You get |
|---|---|
| `/update Nora` | One update for Nora |
| `/update Nora weekly` | The same update, plus two or three numbers |
| `/update` | Claude asks which client |

Claude shows you the draft on screen. It also saves it in a folder named `client-updates/drafts`, inside the folder you opened.

Next to each draft it saves a facts sheet. The facts sheet lists every fact and where it came from. Use it to check the draft.

## Where the facts come from

Claude writes from the record. It does not write from memory. It can read up to six places:

- **The board.** Your task or project tool. What got finished and what is in progress.
- **The code.** What shipped.
- **The channel.** Slack or email with the client. What they already know and what they asked.
- **The calls.** Your call notes. What was promised.
- **Their accounts.** Ads or analytics. The numbers.
- **The end of day log.** What you wrote down that the tools do not show.

Every one is optional. Start with what you have. Add more later.

## Read every update before you send it

This part matters most.

Claude writes the first draft. A person reads it and sends it. The skill tells Claude to never send anything.

Claude can still get things wrong. It can add a small promise nobody made. It can get a name or a number wrong. So read every draft, and check these:

- Cut what the client already knows.
- Cut how it works under the hood.
- Cut a scary number they cannot act on.
- If something is still being tested, make sure the update says so.
- Check every name, number and date.
- Check the ask. Do you really need it?

Then put it in your own words and send it yourself.

## Keep the folder private

The `client-updates` folder holds your clients' names and what you did for them. Keep it somewhere private. Do not put it in a public place.

## More than one person on a client

If a teammate already has a draft for that client that day, the skill adds to it. The client gets one update. They do not get one from each person.

For this to work, your team has to share the `client-updates` folder. A shared drive works. So does a private repo.

## The weekly report

The weekly report is the same message with two or three numbers added. The numbers get one short paragraph near the top. Run `/update Nora weekly`.

The numbers come from the client's account, from a file you export, or from what you paste. The skill tells Claude to never make a number up. Check them anyway.

## What is in this repo

```
.claude/skills/update/SKILL.md      the skill Claude reads
templates/update-shape.md           the shape, and what to cut
templates/facts-sheet.md            the facts sheet, blank
templates/example-updates.md        two made up updates
templates/weekly-report-example.md  one made up weekly report
LICENSE                             MIT
```

The templates are for you to read. The skill works without them.

The examples are made up. The clients, the work and the numbers in them are invented.

## Make it yours

The skill is one text file. Open `SKILL.md` and change it, or ask Claude to change it for you. Change the opener. Change the paragraphs. Add a rule for a client who likes it shorter.

Keep one rule: a person reads every update before it goes out.

## License

MIT. Use it, change it, share it.
