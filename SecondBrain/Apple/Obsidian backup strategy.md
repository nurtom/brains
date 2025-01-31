---
mode: private
---

- Setup a vault in iCloud
	- should sync automatically between macOS and iOS and ipadOS (including the .git subfolder)
- Initialize the vault as a git repository
- When adding notes on mac
	- for syncing to windows git push is necessary
	- for syncing to iOS iCloud should take care automatically
- When adding a note on windows
	- for sync to Mac a git push from windows is needed
	- for sync to iOS a git pull on on mac is needed after the push
- When adding notes on mobile
	- push from macOS (syncs automatically via git) and then pull on windows is necessary
- Checkout Obsidian community plugin for git: https://apps.apple.com/de/app/moom-classic/id419330170?mt=12 to maybe automate pull/push

> [!warning]
> start with a clean repo using this ```.gitignore``` to ignore the Obsidian workspace folder
>```bash
>SecondBrain/.obsidian
>SecondBrain/.trash
>SecondBrain/DS_Store
>.obsidian
>.trash
>DS_Store
>```






