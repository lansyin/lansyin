+++
title = "Fixing Ctrl+Backtick in VSCode"
date = 2023-06-25
updated = 2024-05-01
taxonomies.tags = ["utilities"]
+++

The other day, I ran into a problem while coding in VS Code — the default terminal shortcut `` Ctrl+` `` just wouldn't work on my new laptop. After digging around, I found out that some CJK IMEs hook this shortcut for their own use. The good news is that the key combination can still be captured by a global hotkey, so I put together a [small tool][proj] that registers it and forwards the keypress to VS Code. And it actually worked — lucky me!

<!-- more -->

{{ update(date="2024-03-29") }}

Ideally, I would've built this as a VS Code extension, but I don't know much about front-end development. So instead, the tool runs in the background full-time, which comes with a couple of downsides:

- The key forwarding is done through a crude simulation, which can occasionally mess with other programs.
- If you're running a game, the tool could be flagged as a cheat by anti-cheat software — not great.

To minimize these issues, I added a simple window detection: the tool only kicks in when the active window's title ends with ` - Visual Studio Code` or ` - VSCode`.

{{ update(date="2024-04-29") }}

Eventually, I decided to learn the ropes of VS Code extension development, and I managed to turn the tool into a proper [extension][ext]. It works smoothly and avoids all the side effects that came with the standalone version.

{{ update(date="2024-05-01") }}

Turns out, the real culprit was a setting called "Switch to this IME" in the IME configuration, which grabs `` Ctrl+` `` by default. Disabling it fixed everything — making all my previous efforts completely unnecessary. What a plot twist...

[issu]: https://github.com/Microsoft/vscode/issues/63659
[proj]: https://github.com/lansyin/vscode-cjk-toggle-terminal-fixer
[ext]: https://github.com/lansyin/ctrl-oem3
