# Template update: automatic publishing + plugin source

You are Claude Code working in `ClassVR-Prototypes/xr-prototype-template`.
Do all of this, commit in sensible steps, push, and report plainly.

## 1. Bring the kit submodule up to date

    git submodule update --init --remote --merge kit
    git add kit

Confirm `kit/plugins/classvr-prototyping-kit/.claude-plugin/plugin.json` says
version 0.17.0 or later. If it is older, the kit's latest commit has not been
pushed yet — stop and say so.

## 2. Add the auto-publish workflow from the kit

    cp kit/plugins/classvr-prototyping-kit/skills/share-xr-app/assets/pages/auto-publish.yml .github/workflows/auto-publish.yml
    cp kit/plugins/classvr-prototyping-kit/skills/share-xr-app/assets/pages/pages.yml         .github/workflows/pages.yml
    cp kit/plugins/classvr-prototyping-kit/skills/share-xr-app/assets/pages/build_pages.py    .github/scripts/build_pages.py

## 3. Point Claude Code at the kit's GitHub marketplace

Replace the whole of `.claude/settings.json` with:

    {
      "extraKnownMarketplaces": {
        "classvr-prototypes": {
          "source": { "source": "github", "repo": "ClassVR-Prototypes/classvr-prototyping-kit" }
        }
      },
      "enabledPlugins": {
        "classvr-prototyping-kit@classvr-prototypes": true
      }
    }

Reason: cloud sessions clone without submodules, so `./kit` is empty at the
moment plugins load. The GitHub source loads every time; `kit/` stays for
other AI tools and as the local copy.

## 4. Remove this folder, commit, push

    git rm -r _setup
    git add -A
    git commit -m "Publish finished work automatically; load the kit plugin from GitHub"
    git push

If you are on a `claude/…` branch, the auto-publish workflow does not exist on
main yet, so say so — the user merges this one PR by hand (the last time).

## 5. Tell the user

Say what changed, and remind them: repos made from this template *before*
today do not have `auto-publish.yml` — ask Claude in that repo to "add the
auto-publish workflow from the kit" if wanted.
