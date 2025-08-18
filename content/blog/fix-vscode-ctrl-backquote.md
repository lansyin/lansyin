+++
title = "Fixing Ctrl+Backtick in VSCode"
date = 2023-06-25
updated = 2024-05-01
taxonomies.tags = ["utilities"]
+++

Yesterday, I encountered this [issue][issu] while coding with Visual Studio Code. The default terminal shortcut `` Ctrl+` `` didn't work on my new laptop. After some research, I learned that some CJK keyboards/IMEs may reserve it for internal use, and the reserved key can still be used globally. So I tried to write a [fixer][proj] to register it as a global hotkey and forward its keypress messages. Fortunately, it worked.

<!-- more -->

{{ update(date="2024-03-29") }}

While it would be ideal to implement the fixer as a VSCode extension, I'm not familiar with front-end development. Currently, the fixer runs continuously in the background whenever the system is running, leading to some unnecessary troubles:

- The message forwarding is achieved by a simple mimicking. Sometimes it causes unexpected behavior in other programs.
- Users may play games, and it would be disastrous if the fixer were identified as a cheat program.

To tackle these troubles, the fixer implements a naive detection. It operates only if the title of the active window ends with ` - Visual Studio Code` or ` - VSCode`.

{{ update(date="2024-04-29") }}

Recently, I struggled to learn about the basics of VSCode extension development and finally wrapped the fixer into an [extension][ext]. It works well and also avoids the negative effects caused by the non-extension one.

{{ update(date="2024-05-01") }}

Today, I discovered that the root cause lies in the "Switch to this IME" option in the IME settings, which occupies `` Ctrl+` `` by default. And disabling it just solved the issue. So, all my previous work has been pointless all along. What a dramatic turn of events...

[issu]: https://github.com/Microsoft/vscode/issues/63659
[proj]: https://github.com/lansyin/vscode-cjk-toggle-terminal-fixer
[ext]: https://github.com/lansyin/ctrl-oem3
