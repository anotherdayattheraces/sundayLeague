# PROJECT_CONTEXT.md

This is the source of truth for the project. Read it at the start of every session and update it whenever something significant changes.

_Last updated: 2026-11-23_

---

## 1. Vision

A standalone football game built in **Unreal Engine 5.8**. It aims to be a serious alternative to FIFA/EA Sports FC, and its gameplay, responsiveness and footballing feel are inspired by **PES 2021**. PES 2021 is a reference for how the game should feel. It is not something to copy: all systems and assets are original.

- **Short term:** a high-quality, playable football experience with satisfying controls, realistic ball physics, intelligent player behaviour and meaningful tactics.
- **Long term:** a commercial Steam release, then possibly consoles and cross-platform multiplayer.
- **Approach:** a small number of excellent, reliable systems is better than a large game full of unfinished features.

### Core gameplay priorities
- Responsive, fluid movement with convincing acceleration, deceleration and turning
- Natural ball control and dribbling
- Realistic passing, shooting and crossing
- Physical challenges, tackles, interceptions and shielding
- Contextual animations
- Believable ball physics: spin, bounce, deflections
- Intelligent teammates and opposition
- Goalkeepers with convincing positioning and reactions
- Formations, player roles and team instructions
- A strong sense of weight, momentum and physicality

---

## 2. Current phase

**Phase 1: Foundations.** Not started in this repo.

| | Status |
|---|---|
| Clean UE 5.8 project (`.uproject`, `Config/`) | ❌ Not yet created in `A_1st_Punt` |
| Folder and naming structure | ❌ Proposed below, not yet applied |
| Pitch, markings, goals, environment | ❌ |
| Project documentation | ✅ This file and `CLAUDE.md` |
| Version control | ⚠️ Git repo exists (`main`), but Git LFS for binary assets isn't set up |

### Earlier prototype work (needs locating)
Earlier sessions built prototype Blueprints for Phase 2/3: `BP_Football` (physics ball), `BP_FootballPlayer` (momentum movement), `BPC_BallControl` (dribbling and first touch), `BPC_Kicking` (pass, through ball, long ball, shot), Enhanced Input actions and several test rigs, all under `/Game/Football/`.

**As of 2026-11-23 these assets weren't found on disk.** The sibling projects `../Sundayv01` (only pitch materials in `Content/Football/`) and `../MCP_Setup` don't contain them. Before rebuilding anything, find out where that project is (another drive, an unsynced OneDrive folder, or never saved). If it turns up, decide whether to migrate it into this repo.

---

## 3. Roadmap

Don't move on to a phase until the current one is stable.

1. **Foundations:** clean project, folder and naming structure, pitch/markings/goals/environment, docs, version control.
2. **Player and ball:** ball actor and physics, player character and movement (acceleration, turning, stopping), possession, dribbling, close control, player-ball interactions.
3. **Football mechanics:** passing, through balls, shooting, crossing; tackling, interceptions, shielding, first touches; animations and blending; goal detection; basic goalkeeper.
4. **Match gameplay:** multiple players and teams, player switching, positioning, formations, basic tactics, teammate and opposition AI, a full match loop.
5. **Advanced systems:** better AI and tactical awareness, advanced goalkeeping, player attributes, traits and styles, contextual animations, atmosphere and presentation.
6. **Multiplayer:** server-authoritative architecture, replication, matchmaking, lobbies, team selection, online 11v11; cross-platform later.
7. **Full game:** menus, settings, profiles, clubs, squads, customisation, progression and career, online and competitive modes, Steam release prep.

### First milestone: a playable prototype
- [ ] Properly scaled pitch
- [ ] One controllable outfield player
- [ ] Physically simulated football
- [ ] Player movement and ball control
- [ ] Dribbling
- [ ] Basic passing and shooting
- [ ] Goal that detects a scored goal

After that: a second player, then small-sided matches, then 11v11.

---

## 4. Folder structure

**Current (repo root):**
```
A_1st_Punt/
├── CLAUDE.md, PROJECT_CONTEXT.md
├── .gitignore, .gitattributes
└── Content/            (only empty Collections/ and Developers/)
```

**Proposed `Content/` layout (to apply in Phase 1):**
```
Content/Football/
├── Core/        GameMode, GameState, PlayerController
├── Ball/        BP_Football, physical materials
├── Player/      BP_FootballPlayer, components (BPC_*), animation
├── Input/       Input actions (IA_*) and mapping contexts (IMC_*)
├── Pitch/       Pitch, goals, markings, materials
├── Maps/        Levels (L_*)
└── Dev/         Test rigs and debug actors: prototypes, never shipped
```
Naming: `BP_` Blueprint, `BPC_` Blueprint component, `ABP_` anim Blueprint, `BS_` blend space, `M_`/`MI_` material/instance, `L_` level, `IA_`/`IMC_` input.

---

## 5. Systems

None in this repo yet. List each system here once it exists: what it does, where it lives, what it talks to.

---

## 6. Technical decisions

| Date | Decision | Why |
|---|---|---|
| 2026-11-23 | Build gameplay as Blueprints through the unreal-mcp editor connection | The user isn't a programmer; Blueprints can be inspected in the editor. Move hot paths to C++ later if performance needs it. |
| 2026-11-23 | Keep gameplay logic in reusable components (`BPC_*`) on the player, not one big character Blueprint | Lets AI players and future networked players reuse the same logic |
| 2026-11-23 | Design for server authority without building multiplayer yet | Avoids a rewrite in Phase 6 (philosophy point 9) |

---

## 7. Known bugs and limitations

- The earlier prototype assets are missing (see §2).
- Git LFS isn't configured, so committing `.uasset`/`.umap` files will bloat the repo.

---

## 8. Completed milestones

- 2026-11-23: Project documentation created (`CLAUDE.md`, `PROJECT_CONTEXT.md`).

---

## 9. Next tasks

1. Find the earlier prototype project and decide: migrate it or start fresh.
2. Create the UE 5.8 project in `A_1st_Punt` (`.uproject`, `Config/`).
3. Set up Git LFS for `*.uasset` / `*.umap` in `.gitattributes`.
4. Create the `Content/Football/` folder structure.
5. Build a properly scaled pitch (about 105 × 68 m) with markings and goals.
