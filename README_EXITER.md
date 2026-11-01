# SCP Exiter Breach

Our modified version of **SCP - Containment Breach** — based on the
**current** game, not the old 1.3.11:

- Base: SCP-CB Community Preservation Project's **v1.3.12** (Steam, 2026),
  source https://github.com/SCP-CB-CPP/scpcb, branch `dx9`
  @ `5bf650edd2219be77a6b4fd636938c69ae088f05` (2026-10-26).
- Branch `dx9` in this repo = that pristine upstream snapshot.
- Branch `main` = SCP Exiter Breach. All our additions live here
  (and on `muse/*` feature branches until Eric merges them).
- The original game and source are licensed CC BY-SA 3.0 — see `README.md`
  and `Credits.txt`. This is a fan modification, not affiliated with
  Undertow Games or the CPP team.

Working on it:
- Engine/compiler: **BlitzPRO Legacy v2.100** — see `PLAYTEST.md` for the
  full setup (install engine, copy `Userlibs/*.decls`, open `Game.bb`).
- Project notes, file map, and the two ways to add stuff (mod folder vs
  source edit): see `OUR_PROJECT.md`.
- Workflow: Muse makes the modifications, Eric playtests them.
