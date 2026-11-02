<p align="center">
  <img src="logos/shipify-icon.svg" alt="Shipify package delivery icon" width="180">
</p>

# Shipify

Shipify guides repository releases: synchronize version files, commit, tag, push, publish GitHub Release assets for CLI and app builds on supported macOS, Linux, and Windows targets, then update `luban-homebrew` (macOS), `cangjie-nix` (Linux), and `shennong-bucket` (Windows) through pull requests.

## Latest release

Shipify 0.1.4 enforces releases from a clean `main` synchronized with `origin/main`. On `main`, it commits and pushes release-related changes after checking that no unrelated work is present. It also requires a README update for every release, asks the target repository's agent to verify or add a safe pnpm `clean` script, and opens `luban-homebrew` feature branches against `main`. Use the separate `post-ship` skill to return the originating checkout to an up-to-date local `main`.

Shipify reads channel checkout paths from `~/.shipify/setting.json`. Relative paths resolve from the repository being released. The file uses this shape:

```json
{
  "channels": {
    "macos": { "path": "/Volumes/ORICO/ws/prj/systembug/luban-homebrew" },
    "linux": { "path": "/Volumes/ORICO/ws/prj/systembug/cangjie-nix" },
    "windows": { "path": "/Volumes/ORICO/ws/prj/systembug/shennong-bucket" }
  }
}
```

## Install

```bash
npx skills add borg0ai/as-shipify --skill shipify --agent '*' --global --yes
npx skills add borg0ai/as-shipify --skill post-ship --agent '*' --global --yes
```

## Validate and discover

Run from this repository root:

```bash
node ../skillify/skillify/scripts/validate-skill.mjs skills/shipify
node ../skillify/skillify/scripts/validate-skill.mjs skills/post-ship
npx skills add . --list
```

## Layout

```text
skills/
  shipify/
    SKILL.md
    skill-release.json
    LICENSE
    references/channels.md
  post-ship/
    SKILL.md
    skill-release.json
    LICENSE
logos/shipify-icon.svg
logos/shipify-avatar-512.png
README.md
LICENSE
```
