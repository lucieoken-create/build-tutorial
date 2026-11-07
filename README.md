# build-tutorial

A Claude skill that turns something you built with AI into a tutorial. It reads your repo's history and your Claude Code (and Codex) session logs, finds the moments where something broke or changed direction, asks you what only you know, and writes it all up as a record you can turn into a workshop, a post or a README.

I'm Lucie Oken. I run [hijinx](https://hijinx.studio), and I built this because I'd made things I wanted to teach from, and couldn't remember half of what I'd tried along the way. The session logs could.

## What you get

A tutorial record with the problem, the tools, what you tried (with before and after), the snags, the calls only you could make, and a "recreate it" section: a start-small version someone can do in an afternoon, a step overview of the full build, and prompts to paste. From the record it can write a workshop outline, a blog or newsletter post, or a "Make it yours" README section.

## Install in Claude Code

Start Claude Code in Terminal (`claude`), then run:

```
/plugin install build-tutorial --marketplace lucieoken-create/build-tutorial
```

## Install in claude.ai

Download this repo as a zip, unzip it, and zip just the `plugins/build-tutorial/skills/build-tutorial` folder. In claude.ai, go to Customize, then Skills, and upload that zip. The claude.ai copy is best for tutorials about work you did in chats; repo tutorials work best in Claude Code.

## Use it

Open Terminal in the folder of the project you want to write about, start `claude`, and say:

```
Use the build-tutorial skill on this repo.
```

It'll show you a short log of turning points before writing anything long, and ask you questions. Answer those well and the tutorial is good.

## Two warnings

Your session logs can contain API keys, client names and personal details. The skill is told to scrub them, but read everything before you publish.

It only finds what was saved. If you built in a cloud app that keeps no logs on your computer, it'll ask you for screenshots or exports.

## License

MIT. Use it, change it, share it.
