@AGENTS.md

The ClassVR Prototyping Kit is registered as a plugin by
`.claude/settings.json`, loaded straight from its GitHub repository
(`ClassVR-Prototypes/classvr-prototyping-kit`) so it is there even in a cloud
session, where `kit/` is not checked out. Use its skills directly:
`/new-xr-app`, `/share-xr-app`, `/preview-xr-app`, `/publish-xr-app`,
`/check-headset`, and `xr-app-rules` on every edit. If the skills are missing,
read the `SKILL.md` files from `kit/` instead — run
`git submodule update --init --recursive` first if that folder is empty.
