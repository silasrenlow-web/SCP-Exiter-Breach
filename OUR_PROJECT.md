# Our SCP:CB Mod Project — Setup (prepared 2026-11-01)

## What "current" means (NOT 1.3.11)
- 1.3.11 (2018) was the last release by Regalis / Undertow Games.
- The game was revived by the **SCP-CB Community Preservation Project** (CPP).
- Steam release: **v1.3.12 on 20 Feb 2026** (Steam app 2178380, free), DirectX 9,
  Steam Workshop + built-in mod system, CBRE-EX room editor bundled.
- Latest Steam update: **v1.3.12.7 — Halloween Event 2026** (SCP-330 event).
- Source repo: https://github.com/SCP-CB-CPP/scpcb
  (org was renamed from SCP-CB-Community-Preservation-Project to SCP-CB-CPP;
  old links redirect)
- **Default branch: `dx9`** — this is the live development branch.
  Other branches: `scripting` (upcoming AngelScript update, not stable),
  `blitzpro`, `legacy-speedrunning`, `dx7-deprecated`.
- This local copy = `dx9` @ commit `5bf650edd2219be77a6b4fd636938c69ae088f05`
  (2026-10-26, "Merge branch 'main' into dx9") — ahead of the v1.3.12.6
  GitHub release tag, includes the fixes shipped in Steam's v1.3.12.7.
  GitHub has no v1.3.12.7 tag/release yet (checked 2026-11-01).
- License: CC BY-SA 3.0 (same as the original).

## GitHub status — OUR repo: SCP Exiter Breach
- **Our repo: https://github.com/silasrenlow-web/SCP-Exiter-Breach**
  ("SCP Exiter Breach", public, description "Fork of SCP:CB to add more
  stuff.") — created by Eric himself on 2026-11-01 because the stored PAT
  cannot create repos: creating one failed TWICE (2026-11-01) with
  `403 Resource not accessible by personal access token` on POST /forks
  AND on POST /user/repos — the same fine-grained-PAT limit family as
  PR creation / runner tokens.
- It is NOT a GitHub "fork" object (it's a fresh repo Eric made), so
  upstream syncs are done manually by Muse: branch `dx9` in our repo is
  a pristine import of upstream SCP-CB-CPP/scpcb `dx9`, branch `main` is
  the SCP Exiter Breach line (same start + our files/changes).
- The `Localization` submodule (~1.4 GB upstream repo) is NOT imported;
  English data in `Data/` is complete in-tree. Add it later only if we
  need other languages.
- Workflow agreed 2026-11-01: Muse makes all modifications and pushes
  `muse/*` branches to this repo; Eric pulls, compiles with BlitzPRO,
  playtests, and reports bugs/ideas back. See PLAYTEST.md.
- Engine secured 2026-11-01: BlitzPRO.Legacy.v2.100.zip (8.8 MB, official
  Euclid-Labs-Studio release, notes confirm it's the engine that compiles
  Steam v1.3.12) at ~/workspace/your_files/ + ~/workspace/scpcb-engine/.
  Its bundled userlibs/*.decls match the repo's in content (line endings
  only differ); still copy the repo's over per README.
- Remotes: `upstream` = SCP-CB-CPP/scpcb, `origin` = SCP-Exiter-Breach.

## Building on Windows (Eric's Cyborg) — IMPORTANT, docs conflict
- The in-repo `Instructions.txt` is OUTDATED: it says Blitz3D v1.108c +
  mavless_bin.zip (that was the 1.3.11 / Regalis setup).
- The current `README.md` is the authority for 1.3.12:
  - Compiler: **BlitzPRO Legacy v2.100**
    https://github.com/Euclid-Labs-Studio/BlitzPRO/releases/tag/legacy-v2.100
  - Before compiling: copy all `.decls` files from this repo's `Userlibs\`
    folder into the Blitz installation's `userlibs` folder.
  - Entry point: `Game.bb` (it just does `Include "Main.bb"`).
  - Compile `Game.bb`, output is `SCP - Containment Breach.exe`.
- `Localization` is a git submodule (empty in this zip snapshot; a real
  `git clone --recurse-submodules` fills it).

## Two ways to add our own stuff
### Route A — Mod folder (no recompile, try this first)
- `Mods/<ModName>/` with `info.ini` (see `Mods/ExampleMod/` and our
  blank `Mods/StarterMod/`), `icon.png`, and mirrored folders:
  `Data/`, `GFX/`, `SFX/`, `Maps/`, `Loadingscreens/`, `Localization/`.
- Files placed there override / extend the base game by load order
  (Mods menu in-game, enable/disable, Ctrl+move = front/back of list).
- Good for: textures, sounds, loading screens, items.ini entries,
  SCP-294 drinks, rooms.ini entries, custom maps (.cbmap2, made in CBRE-EX),
  strings/subtitles.
- Steam achievements are disabled on custom maps.

### Route B — Source edit (full power, needs BlitzPRO compile)
Key files:
- `Main.bb` (385 KB) — main loop, player, `InitEvents`
- `UpdateEvents.bb` (388 KB) — all room/SCP events (`UpdateEvents`)
- `NPCs.bb` (260 KB) — SCP / NPC behaviour
- `MapSystem.bb` (303 KB) — map generation, `CreateMap`, `FillRoom`
- `Menu.bb`, `Items.bb`, `Save.bb`, `Achievements.bb`, `ModManager.bb`
- `Data/*.ini` — items.ini, rooms.ini, events.ini, NPCs.ini,
  SCP-294.ini, strings.ini, subtitles.ini drive a lot without code.
- Adding a room (from Instructions.txt, still accurate for this part):
  entry in `Data/rooms.ini` + place via `CreateMap` / fill via `FillRoom`
  in `MapSystem.bb`; mesh made in CBRE-EX / 3DWS, formats .b3d / .rmesh.
- Adding an event: `CreateEvent` in `InitEvents` (Main.bb) + behaviour
  in `UpdateEvents` (UpdateEvents.bb).

## Local copy
- `~/workspace/scpcb-current/` — zip snapshot of `dx9` (338 MB unpacked),
  git-initialised on branch `dx9` with upstream/origin remotes set.
  It is a snapshot, not a full-history clone (full clone via the proxy
  was too slow / disconnected; codeload zip worked).
