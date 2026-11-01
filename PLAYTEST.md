# Playtest Setup — Eric's Cyborg (Windows)
Prepared 2026-11-01. Game: SCP - Containment Breach v1.3.12 (current CPP version, NOT 1.3.11).

## The workflow we agreed
- Muse makes all the modifications (code, mods, fixes) and pushes them to
  Eric's GitHub repo on `muse/*` branches.
- Eric pulls, compiles/runs, and **playtests**. Bugs / ideas go back to Muse,
  Muse fixes, repeat. Merges into `dx9` are Eric's, same as DCB.

## Step 0 — DONE (2026-11-01)
Eric created our repo himself (the stored GitHub token cannot create
repos — verified twice: fork POST and repo-create POST both 403):
**https://github.com/silasrenlow-web/SCP-Exiter-Breach** — "SCP Exiter Breach".
Muse imported the upstream source into it:
- branch `dx9` = pristine upstream v1.3.12 snapshot (for clean diffs)
- branch `main` = SCP Exiter Breach line (start here)
Note: the huge `Localization` submodule is not in our repo; English is
fully in-tree under `Data/`. So for OUR repo, clone WITHOUT
`--recurse-submodules` (Step 2 below is already written that way).

## Step 1 — Play the untouched current game right now (optional, 2 min)
Install the free Steam version (v1.3.12.7, newest):
Steam app 2178380, "SCP – Containment Breach". No compiling needed.
This is the clean reference for "what does stock 1.3.12 feel like".

## Step 2 — Get our source on the Cyborg
```
git clone https://github.com/silasrenlow-web/SCP-Exiter-Breach.git
cd SCP-Exiter-Breach
```
You land on branch `main` — that's our SCP Exiter Breach line.
(Upstream's `Localization` submodule is deliberately not in our repo.)

## Step 3 — Install the engine (BlitzPRO Legacy)
- File: `BlitzPRO.Legacy.v2.100.zip` (8.8 MB) — Muse downloaded and
  verified the official GitHub release. Its release notes literally say:
  "This version of the engine is used to compile SCP - Containment Breach
  v1.3.12 on Steam."
  Source: https://github.com/Euclid-Labs-Studio/BlitzPRO/releases/tag/legacy-v2.100
- Unzip it anywhere (e.g. `C:\BlitzPRO Legacy\`). It contains
  `BlitzPRO Legacy.exe` (IDE) and `bin\blitzcc.exe` (compiler).
- **Then copy the repo's `Userlibs\*.decls` (3 files) into the engine's
  `userlibs\` folder, overwriting.** (Checked 2026-11-01: the engine's
  bundled copies have identical content, only line endings differ —
  copying the repo ones anyway is the README's instruction and is safe.)

## Step 4 — Run / compile OUR version
1. Open `BlitzPRO Legacy.exe`.
2. Open `Game.bb` from your clone folder (it just includes `Main.bb`).
3. Run it from the IDE (Run Program button) to playtest from source, OR
   use Create Executable and save it as `SCP - Containment Breach.exe`
   **in the clone folder** (the game loads Data/GFX/SFX relative to the exe).
4. Playtest. Report back to Muse: what broke, what felt wrong, exact
   room/SCP/item if you can — screenshots/video help a lot.

## EXPECTED: Windows "Malicious file" popup (SmartScreen)
BlitzPRO Legacy.exe (and later, our compiled game exe) triggers a big red
Windows SmartScreen "Malicious file" popup. This is a **reputation**
warning, not a virus detection: the exe is unsigned and rarely
downloaded, so Windows has no trust history for it.
Verified 2026-11-01: our `BlitzPRO.Legacy.v2.100.zip` SHA-256
`a509b2380cfed97ba5d194c00816ccdb3b7026552db04614d8581c6992b27738`
matches GitHub's official published digest for the Euclid-Labs-Studio
release asset byte-for-byte. The launcher `BlitzPRO Legacy.exe` inside
is 110,080 bytes, SHA-256
`a546b94646c97f979d7e5b4aa49b6d3b0ec358a8d2debbf0393546495639bc2e`.
To run: on the popup click **More info** -> **Run anyway**.
Expect the same popup the first time you run our compiled game exe too.

## Notes
- Do NOT use the old Blitz3D 1.108 + mavless_bin instructions in
  `Instructions.txt` — that's the dead 1.3.11 setup.
- Mod-folder-only changes (`Mods\...`) do NOT need a recompile: they also
  work dropped into the Steam install's `Mods` folder.
- Save files / options: `options.ini` lives next to the exe.
