---
name: build-tutorial
description: Turns something you built with AI (a code repo, or a run of AI chats) into a tutorial record of what you tried, what broke and what you decided, then writes it up as a workshop, a blog or newsletter post, or a README section.
---

# build-tutorial

One tutorial record per build, written up as many times as you need. A case study trims the mess to sell the result. A tutorial keeps it, because the mess is what people learn from: what you tried, what broke, what you decided, and how someone else could make their own version.

The steps below are the usual path, not a fixed script. If a build calls for a different order or an extra section, suggest it.

Most runs will be on things built before anyone was taking notes. Expect thin commit messages ("updates", "fix") and fill the gaps from session transcripts, chats and the builder's own memory.

## Before the first run

Ask the builder three things once, and remember the answers for later runs if you can:

1. **Where records should be saved.** Default: a `tutorials/` folder next to the repo (not inside it, so nothing gets committed by accident). A notes app, Google Drive or Notion are fine if they're connected.
2. **What can't be made public.** Client names, employer work, anything under NDA. These never appear in a record meant for sharing.
3. **How they write.** A writing-style or voice skill if they have one, or two or three things they've written that sound like them.

## Step 1. Set up

Settle five things, asking only what you can't work out yourself:

1. Which build, and where it lives (a repo, or the chats and folders for a chat-based build).
2. Which mode. **Repo mode** is for code builds and works best in Claude Code on the computer where the build happened, since that's where the session transcripts are. **Chat mode** is for work done in claude.ai conversations, like social graphics or a deck.
3. Who it's for: a workshop or training, a post, or both. The record is the same; the write-ups differ.
4. Whether it can be public. Work done for a client or an employer usually can't.
5. Questions it answers. Ask whether the builder keeps any record of what people have asked them: workshop Q&A, comments, replies, DMs, a notes page. If they do, find the questions this build answers. Real questions are the best guide to what a tutorial should cover, and a post that opens on one lands faster than one that opens on the build. If there's no such list, skip this.

If a record for this build already exists, read its sources and changelog and sweep only what's new.

## Step 2. Sweep (repo mode)

1. **Get full history.** Work in the local copy, pulled up to date (`git pull`). If cloning, don't use `--depth`, or the history is gone. If the build was restarted in a fresh repo at some point, ask for the old one and sweep both.
2. **Map the timeline.** `git log --reverse --stat --format='%h %ad %an %s%n%b' --date=short` gives the order of events with authors and commit trailers. Note the stack from package.json (or the equivalent) and the README.
3. **Work out which tool did what.** People often switch between AI coding tools mid-build. Clues: commit trailers (Claude Code adds a Co-Authored-By line naming Claude by default), author names, branch names, and instruction files like CLAUDE.md or AGENTS.md and when they appeared. Lay the timeline out in stretches by tool. Why they switched is part of the story.
4. **Find the turning points.** Look for commits with large deletions, reverts, renamed or removed files, dependencies added then dropped, messages with fix, try, revert, again or wip, and clusters of commits on one file in one day. Those are usually the "tried something, it didn't work" moments. Pull the diffs with `git show` and keep the before and after of the files that matter.
5. **Read the session transcripts.** Claude Code saves sessions as JSONL under `~/.claude/projects/`, in folders named after the path the repo was in. Codex CLI saves sessions under `~/.codex/sessions/`, in dated folders. Match sessions to the build by repo name and dates, not just the current path, since folders get moved. These hold the builder's prompts, what the tool tried, the errors and the fixes, which is where most of the story is when commits are sparse. Search for errors, corrections ("no", "instead", "that's not it", "try") and pasted screenshots. If some work ran in a cloud or desktop app and left nothing on disk, say so and ask the builder to export or screenshot it.
6. **Find old visuals.** Hosts like Vercel and Netlify keep a deployment per push, so earlier versions may still be live at preview URLs. For small static projects, reconstruct an old state yourself: check out the commit into a throwaway `git worktree`, serve the built folder, and screenshot it. For mobile shots, drive a headless browser that does real device emulation — Puppeteer or Playwright, or the DevTools protocol; plain `chrome --headless --window-size=375,812` renders the desktop layout cropped to the width, so the responsive breakpoints never fire. Save the images as files (doc connectors often can't take image uploads). For anything needing a database, a CMS or secret keys, don't burn time on it; ask what the builder saved.
7. **Scrub as you go.** Transcripts and old commits can hold API keys, tokens, passwords, client names and personal data. None of it goes into the record, a screenshot or a code image.

## Step 2. Sweep (chat mode)

1. Search past chats for the project's distinctive words and open the right ones. In claude.ai, chats inside a Project and chats outside one are searched separately, so say so if the build likely sits on the other side.
2. Read any artifacts from the build; earlier versions may be there.
3. Generated images usually don't come back from chat history. Ask where the rounds were saved and work from those.
4. Track what the builder asked for, what they pushed back on, and what changed between rounds. Their feedback is the lesson in a chat-based tutorial.

## Step 3. Build the iteration log, then ask the builder

Before writing anything long, lay out the turning points as a short log. For each one: date, tool, what happened, the evidence (commit, transcript, chat), before and after, and the lesson in one sentence. Show it and ask what only they know: why they cut something, why they switched tools, what they were going for, what they'd do differently, which moment they'd want on screen. Mark their answers as theirs.

## Step 4. Write the record

1. **Header.** Project, dates, links (live site, repo, license), audience, public or private, and the audience questions it answers, if any.
2. **The problem.** What they wanted and why it mattered, in plain terms.
3. **Tools and starting point.** The stack, which AI tools built which parts, and an honest note on where it started, crediting any tutorial, template or open-source asset it built on, with its license.
4. **What they tried.** The iteration log in order, with before-and-after pairs. Include what got thrown away.
5. **Snags.** Specific things that broke or took many tries, and how they got past them. At least one per tutorial; it's what audiences remember.
6. **Decisions only they could make.** Taste calls, cuts, what felt right.
7. **Recreate it.** A start-small version someone can do in an afternoon, the full build as a step overview, and the prompts they'd paste into an AI tool to get going.
8. **Assets.** Code images, screenshots, preview links, each with its source.
9. **Gaps.** What couldn't be found, and who could fill it.
10. **Sources swept** and a **changelog.**

Write in the builder's voice, using their writing-style skill or samples if they gave them. Plain words, specific details, no hype. Don't make the build sound easier or smoother than the evidence shows. Every claim traces to a source or to the builder.

If you're filing the record into a doc tool that can only create, not edit in place (some connectors work this way), settle the text first — the voice pass included — and create the doc once. Keep the Markdown working copy as the living draft rather than re-making the doc on every change.

## Step 5. Write it up on request

Confirm the format and where it's going each time.

- **Workshop or training.** The story in a few slides, one live demo moment, an exercise (usually the start-small version), and a link people can fork. A talk track in full sentences. Use the record's audience questions for the Q&A.
- **Blog or newsletter post.** Story first, two or three images that carry the before and after, and a start-small box near the end. If the record lists audience questions, the post can open on one.
- **README section.** A "Make it yours" section for a public repo, with a prompt people can paste.
- **Code images.** Before-and-after snippets as clean images (an HTML page screenshotted headlessly works), trimmed to the lines that changed, in the builder's brand colors and type if they have them.

Save each write-up next to the record and add a changelog line.

## Step 6. Close out

Tell the builder in two or three lines what the tutorial covers, what's missing, and where it's saved.

## For future builds: capture as you go

When the builder starts something new, offer a light habit so the next tutorial writes itself: commit at each real milestone with one sentence on what changed and why, keep a short `build-log.md` for tries that didn't make it into a commit, and save a screenshot when something visual lands. When people ask about the build, write their questions down too; those become the tutorial's opening. Suggest it once per build.

## Rules

- One record per build; merge on repeat runs.
- Nothing private goes into a public write-up: client or employer work, secrets, personal data.
- Credit the tutorials, templates and assets a build started from, with licenses.
- No claim in a write-up that isn't in the record.
