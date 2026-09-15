# One-time setup for this template repository

You are Claude Code working in `ClassVR-Prototypes/xr-prototype-template`.
Do all of the following, then commit and push. Report in plain words what
you did and anything that failed.

## 1. Add the kit as a submodule at `kit/` (it is declared but not added)

`.gitmodules` already declares a submodule named `kit`, but no gitlink was
ever committed. Fix it:

    git rm --cached kit 2>/dev/null || true
    rm -rf kit prototyping-kit
    git submodule add --force -b main https://github.com/ClassVR-Prototypes/classvr-prototyping-kit kit

Confirm `git ls-files -s kit` shows a `160000` entry and `kit/plugins/classvr-prototyping-kit/.claude-plugin/plugin.json` exists.

## 2. Move the config files into place

    mkdir -p .claude .github/workflows .github/scripts
    git mv _setup/claude-settings.json .claude/settings.json
    git mv _setup/pages.yml            .github/workflows/pages.yml
    git mv _setup/update-kit.yml       .github/workflows/update-kit.yml
    git mv _setup/build_pages.py       .github/scripts/build_pages.py
    git rm -r _setup

(If `_setup` files are not yet tracked, plain `mv`/`rm` and `git add` are fine.)

## 3. Commit and push

    git add -A
    git commit -m "Template setup: kit submodule, Claude settings, Pages and update workflows"
    git push

If you are on a `claude/…` branch rather than `main`, say so — the user will
merge the PR. Do not change anything under `kit/`.

## 4. Tell the user

Say: what was added, whether the submodule is populated, and remind them of
the two GitHub settings they must tick by hand: **Settings → General →
Template repository**, and (for repos made from this template, not this one)
**Settings → Pages → Source: GitHub Actions**.
