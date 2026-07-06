# BLOCKLOOP // Blockheads Runner

Goal: continue building the Blockheads Runner game (index.html).

## Tasks

- [x] **BIP 110 boss: recolor to red/black + pixel "BIP 110" body text** — tier: MID — done-check: loading index.html#dev in a browser, triggering the LVL 9 debug button and letting the boss appear, shows a boss body that reads as black/dark with red highlights (not green) and legible, non-mirrored "BIP" / "110" pixel-style text on the torso. — **PASS**, verified with screenshots (roof:in/chargeH/fireH).

- [x] **Rooftop skyline: visible height variation (background art)** — tier: MID — done-check: screenshot of a "roof" zone level (e.g. level 7) shows a clearly jagged/uneven building skyline (varied heights, not a flat repeating silhouette), while ground collision/gameplay is unchanged (purely visual, no physics change). — **PASS**, verified with screenshots (roof vs street), no collision/physics touched. **Superseded by the task below** — user actually wants the running surface itself to change height, not just background buildings.
- [ ] **Rooftop hopping: the running surface itself changes height** — tier: HEAVY — done-check: in the roof zone, the player's actual path (not background art) visibly rises/falls between rooftop sections of different heights, traversed via jumps (reusing the `plats` standable-platform system), verified by demo-bot successfully crossing without unfair/impossible jumps, and without conflicting with the existing BIP 110 encounters or heart-platform spawns in the same zone.

- [x] **BIP 110 encounter #1 — ninja-star duel, gated by 5 collected stars** — tier: HEAVY — done-check: reaching the encounter's level without having thrown/collected 5 ninja stars in earlier levels shows the encounter does NOT trigger (or shows a locked/skip state); with >=5 stars collected, BIP 110 appears as a simpler early duel using the existing star-throw mechanic. No regression to the existing final BIP 110 (level 9) fight. — **PASS**: placed at level 7, gated on new `starsThrown>=5` counter, 1-cycle duel (vs 3 at level 9), verified gate-not-met/gate-met/level-9-regression all correct.

- [x] **BIP 110 encounter #2 — rope-ball duel (duck to dodge, throw back)** — tier: HEAVY — done-check: a new obstacle type ("rope-ball") that BIP 110 throws is added, player must duck under it or it's lethal like other obstacles; visually and behaviourally distinct from the existing rope/mtn/air obstacle types; appears in a mid-game encounter with BIP 110 as a second duel, gated on progress from encounter #1. — **PASS**: level 8, spiked ball-on-chain thrown at head height, duck to dodge, 2-cycle duel, verified hit->die and levels 7/9 regression-free.

- [x] **BIP 110 encounter #3 — laser finale, gated by collected hearts** — tier: MID — done-check: the existing level-9 laser boss fight only becomes reachable once the player has collected a set number of hearts (reusing `heartsGot`); below the threshold the encounter is skipped/deferred; at/above threshold it plays out as today's BIP 110 laser duel unchanged. — **PASS** (gated on heartsGot>=3, heartsGot now resets per run). Fixed a soft-lock the subagent's version left behind: level 9 previously had NO distance-based fallback (LVL_LEN[9]=999999, it only ever completed via bossDone), so when the gate isn't met the level would never end. Added a `heartsGot<3 && lvlDist>16000` fallback so an under-resourced run still progresses instead of stalling forever.

- [x] **Water crossing with floating/climbable blocks** — tier: HEAVY — done-check: a new section (targeted around level 6/10/11) requires jumping a gap wider than a normal jump, using intermediate floating blocks the player can stand on/climb across; verified by demo-bot or manual playtest successfully crossing without it reading as an unfair/impossible gap. — **PASS**: one-time set-piece at level 6, 380px water gap + stone stepping stone, reuses/fixes the existing plats collision system, distinct blue-water visual, bot crosses reliably (10/10), level 7/9 roof platforms unaffected.

## Log

<!-- escalations and hard stops get noted here by the loop -->
