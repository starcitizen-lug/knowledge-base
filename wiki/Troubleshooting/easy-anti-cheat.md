---
title: "🤡 Easy Anti-Cheat"
description: "Known Easy Anti-Cheat compatibility issues and helpful troubleshooting steps to resolve them"
parent: "Troubleshooting"
nav_order: 5
md_message: "You are viewing raw source files... Go to https://wiki.starcitizen-lug.org/ to use the wiki!"
---

# 🤡 Easy Anti-Cheat


{: .important-title }
>
> Check the [latest news](/#news) for any changes


## Error after pressing Launch Game
- Possible error codes `210` and `#1`
- Vanilla Wine versions >10.1 made changes that break Easy Anti-Cheat
- Use the [LUG Helper](/Tips-and-Tricks#how-to-add-a-wine-runner) to switch to a [recommended](/Tips-and-Tricks#recommended-runners) wine runner
- Ensure you have **not** changed the default install location in the RSI Launcher `C:\Program Files\Roberts Space Industries`


## Failed to load the embedded resources
- Possible game error code `60099`
- This can occur of your system is set to certain languages'
- To fix, use the LUG-Helper to [edit your launch script](/Tips-and-Tricks#how-to-edit-the-launch-script) and add the following environment variable:
    - `export LC_ALL=en_US.utf8`
