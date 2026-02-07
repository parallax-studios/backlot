# BACKLOT — QA Plan

**CRASH, QA Lead**
**Status: Test Strategy v1.0**
**Target Platform: PC (Steam Primary), Switch Secondary**

---

## 1. What We're Testing (And What Could Go Wrong)

BACKLOT is a management sim where your resources have opinions. That is the hook, and that is the first place it can break. If the simulation collapses under edge cases, if the economy death-spirals, if save files corrupt after Film 12, if procedural scripts all sound the same by hour three — the game is dead.

This is not a renderer. This is not a physics sandbox. This is a data-driven, event-heavy, state-machine-orchestrated simulation with 80-120 persistent agents and procedural content generation. The failure modes are not crashes. The failure modes are:
- **Unfun loops** (decision fatigue, repetition, predictability)
- **Broken economy** (unrecoverable bankruptcy, runaway success)
- **Hollow content** (procedural text that feels algorithmic)
- **Invisible bugs** (relationship graph corruption, event deck reseeding incorrectly)
- **Save file death** (corruption, bloat, version incompatibility)

Define "works." Works means: the player completes 10 films without hitting a blocking bug, without feeling decision fatigue, and with a studio that tells a story they can articulate. If they cannot say "I am the studio that makes X," the emergent narrative has failed, and that is a bug.

---

## 2. Quality Gates (What Must Pass Before Shipping)

### Gate 1: Vertical Slice (Week 8)
**Must Pass:**
- One complete production cycle playable end-to-end (Greenlight → Release)
- Coverage reports read like authored text, not Mad Libs
- Player can articulate why they greenlit one script over another
- Production Clock does not feel tedious by day 10 of a 15-day shoot
- Festival outcome feels consequential (reputation shift is visible, distribution offers make sense)
- Save/load works without data loss

**Blocker Criteria:**
- Coverage reports fail the "read aloud" test (if it sounds generic when read aloud, it is generic)
- Player disengages during Production Clock phase
- Save file loads incorrectly or corrupts

**Test Lead Responsibility:** CRASH personally playtests vertical slice. If coverage reports do not pass the read-aloud test, NOVA and the content team are blocked until fixed.

---

### Gate 2: Core Loop Complete (Week 16)
**Must Pass:**
- 5-film playthrough without blocking bugs
- Talent Web is readable (player uses relationship data, not just skill stats, in casting decisions)
- Financial viability of both art and commerce paths confirmed (playthroughs reach Film 5 with positive cash flow)
- Event deck does not repeat the same crisis 3+ times in a single production
- Studio progression is visible (reputation unlocks new opportunities, office evolves, talent pool expands)
- Save files with 5+ completed films load in <2 seconds

**Blocker Criteria:**
- Either art or commerce strategy fails to survive 5 films (economy imbalance)
- Talent Web UI is incomprehensible (playtesters cannot explain casting choices)
- Repeated event fatigue (same crisis text 3+ times in one shoot)
- Performance drops below 60 FPS on min spec hardware

**Test Lead Responsibility:** Full regression suite runs. Economy balance spreadsheet is locked. Event deck weights are verified against design spec.

---

### Gate 3: Content Complete (Week 24)
**Must Pass:**
- 10-film playthrough without content repetition
- Procedural scripts feel diverse (no "I have seen this logline before" across 30+ scripts)
- Press quotes align with film quality and festival outcome (scathing quotes for walkouts, ecstatic for wins)
- Talent personalities are distinct (playtesters can describe 3+ talents by name after a 2-hour session)
- UI polish complete (animations, transitions, feedback loops, diegetic elements functional)
- Audio integration complete (ambient office sounds, diegetic music, festival theater atmosphere)

**Blocker Criteria:**
- Content repetition detected (identical loglines, identical crisis events within 3 films)
- Press quotes misaligned with outcomes (positive quotes for a walkout)
- Performance regression (FPS drop, load time increase)
- Audio bugs (missing sounds, incorrect triggers)

**Test Lead Responsibility:** Content audit. Manual sweep of all procedural pools for duplicates, near-duplicates, and tonal inconsistencies.

---

### Gate 4: Beta Release Candidate (Week 36)
**Must Pass:**
- 20-film regression playthrough (full studio lifecycle)
- All critical and high-severity bugs closed
- Steam integration functional (cloud saves, achievements)
- Switch port (if shipping) functional and stable
- No crash-to-desktop in 10-hour stress test
- Save file compatibility verified across versions
- Localization readiness (all UI text externalized, no hardcoded strings)

**Blocker Criteria:**
- Any crash-to-desktop
- Save file corruption or incompatibility
- Steam features broken (cloud saves do not sync, achievements do not unlock)
- Performance regression on target hardware

**Test Lead Responsibility:** Final certification. CRASH signs off. If this gate does not pass, we do not ship.

---

## 3. Test Plan by System

### 3.1 The Greenlight Table (Script Generation & Selection)

**What We're Testing:**
- Script generation produces diverse, readable coverage reports
- Script attributes align with coverage text (a script described as "ambitious" has high Structural Ambition stat)
- Player can greenlight scripts and option costs are deducted correctly
- Writer relationships update when scripts are selected or rejected

**Happy Path:**
1. Player enters Greenlight phase
2. 3-5 scripts are available
3. Player reads coverage reports
4. Player greenlights one script
5. Budget is reduced by option cost
6. Script moves to "In Development" board
7. Writer relationship updates

**Sad Path:**
- Player has insufficient budget to option any script → Verify error messaging, verify fallback (free scripts still available)
- Player greenlights script, then immediately saves/loads → Verify script state persists
- Player greenlights script with pretension_index > 70 (high ambition, low quality) → Verify downstream production struggles

**Evil Path (Exploits & Edge Cases):**
- Rapidly click greenlight button multiple times → Should not greenlight the same script twice or deduct budget twice
- Save/load loop to reroll script pool → Is this intended behavior or should script pool be fixed per season?
- Greenlight 3 scripts in one season when only 3 production windows exist → Verify UI blocks greenlighting beyond capacity

**Test Data:**
- Generate 100 scripts, manually review coverage reports for repetition and quality
- Verify attribute → coverage text alignment (spot-check 20 scripts: does "heavy" tone correlate with tone stat > 70?)
- Edge values: pretension_index at 0, 50, 100 — does coverage reflect?

**Automated Tests:**
- Generate 1000 scripts, verify no duplicate loglines
- Verify all coverage reports are >50 characters (detect empty/broken generation)
- Verify script budgets align with budget_tier enum

**Risk Assessment:**
- **HIGH RISK:** Coverage reports feel generic. This kills the entire mechanic. Requires content review, not just functional testing.
- **MEDIUM RISK:** Pretension Index is invisible to player but critical to outcomes. Hard to validate without deep playtesting.

**Regression Checklist (Post-Fix Verification):**
- [ ] Script generation produces diverse loglines across 50+ scripts
- [ ] Coverage text accurately reflects script attributes
- [ ] Greenlight action is idempotent (cannot double-greenlight)
- [ ] Option costs deduct correctly
- [ ] Writer relationships update on greenlight/reject
- [ ] Script state persists across save/load

---

### 3.2 The Talent Web (Relationship System)

**What We're Testing:**
- 80-120 talents exist with distinct stats and personalities
- Relationship graph tracks studio and inter-talent relationships correctly
- Casting negotiation respects relationship discounts and trait modifiers
- Talent Web visualization displays connections without UI explosion

**Happy Path:**
1. Player enters casting phase
2. Player views Talent Web, sees available actors
3. Player selects actor, agent presents ask
4. Player negotiates, actor accepts
5. Relationship score updates (+2 for successful negotiation)
6. Actor is marked unavailable for duration of production

**Sad Path:**
- Player offers 50% of actor's ask → Actor rejects, relationship decreases (-1)
- Player casts two actors with negative relationship (-30) → Production generates conflict events
- Actor has Loyal trait and studio_relationship > 30 → Accepts lower offer (verify discount applies)

**Evil Path:**
- Cast the same actor in overlapping productions → Should be blocked (availability check)
- Rapidly hire/fire actor to manipulate relationship score → Verify relationship penalties apply
- Save/load during negotiation → Verify offer state persists
- Corrupt relationship graph by setting studio_relationship to 10000 → Clamp validation

**Relationship Decay Testing:**
- Do not cast actor for 6+ in-game months → Verify relationship decays by 1 point
- Cast actor every film → Verify loyalty bonus builds (+5-15 per collaboration)

**Chemistry System Testing:**
- Cast two actors with chemistry_modifier +20 → Verify scene quality Performance bonus applies
- Cast two actors with chemistry_modifier -20 → Verify conflict event probability increases

**Talent Web Visualization:**
- Load 120 talents with 50% relationship density → Verify UI does not freeze
- Hover over talent node → Verify connection strings highlight correctly
- Filter by role (Actors only) → Verify visualization updates

**Automated Tests:**
- Generate 120 talents, verify all have valid stats (0-100 range)
- Verify relationship graph is symmetric (if A→B = 20, then B→A = 20)
- Verify chemistry map contains only valid talent IDs

**Risk Assessment:**
- **HIGH RISK:** Talent Web overwhelms player. If UI is unreadable or agent count feels like spreadsheet management, players disengage.
- **MEDIUM RISK:** Relationship corruption (graph desync, invalid IDs). Hard to detect without deep save/load stress testing.
- **LOW RISK:** Negotiation math error. Easy to verify with unit tests.

**Regression Checklist:**
- [ ] All 120 talents load without errors
- [ ] Relationship graph is symmetric and clamped (-50 to +50)
- [ ] Negotiation respects relationship discounts
- [ ] Chemistry modifiers apply to scene quality
- [ ] Talent availability blocks double-casting
- [ ] Relationship decay applies after 6 months of no contact
- [ ] Talent Web visualizes without performance degradation

---

### 3.3 The Production Clock (Crisis Event System)

**What We're Testing:**
- Event deck seeds correctly based on cast/crew traits and script attributes
- Crisis events present 2-3 meaningful choices
- Event resolution applies effects correctly (morale, budget, scene quality, loyalty)
- Momentum system influences event probabilities dynamically
- Production does not feel repetitive or tedious across multiple shoots

**Happy Path:**
1. Production begins, event deck seeds
2. Day 1: Crisis event fires (e.g., "Talent Conflict")
3. Player selects option 2 ("Side with director")
4. Effects apply: actor_morale -15, actor_loyalty -10, scene_coherence +5
5. Momentum updates based on outcome
6. Day 2: Different event category fires
7. Production completes after 15-40 days

**Sad Path:**
- Budget overrun event fires when budget is already at 0% → Verify cannot go negative, verify crisis state triggers
- Morale drops to 0 → Verify does not block production, verify Momentum plummets
- Same event category fires 3 times in a row → Should be blocked by design (max 2 consecutive repeats)

**Evil Path:**
- Save/load mid-production → Verify event deck state persists, verify no event re-fires
- Save scum: load before crisis event, try different option → Is this intended? (Likely yes, but verify no state corruption)
- Trigger every crisis event in one production by manipulating seed weights → Verify event deck does not run out of events

**Decision Fatigue Testing:**
- **Critical Playtest Metric:** Complete a 30-day production. Does engagement drop after day 15?
- Verify "quiet day" mechanic (every 5th day has 0-1 decisions)
- Verify Breakthrough events increase in second half of production (reward for surviving)

**Momentum System Testing:**
- Start production with morale 50, momentum 50
- Trigger 3 negative events in a row → Momentum should drop below 30
- Verify at Momentum < 30, Talent Conflict and Budget Overrun events increase (+5% weight)
- Trigger 3 positive events in a row → Momentum should rise above 70
- Verify at Momentum > 70, Breakthrough events increase (+5% weight)

**Event JSON Validation:**
- Load all event JSON files, verify schema compliance
- Verify all event options have valid effect keys
- Verify conditional effects (e.g., "+5 if actor.skill > 65 else -5") parse correctly

**Automated Tests:**
- Simulate 100 productions, verify event distribution matches design weights (±10%)
- Verify no event category repeats more than 2 consecutive times
- Verify all event effects apply correctly (morale/budget/quality updates)

**Risk Assessment:**
- **HIGH RISK:** Decision fatigue. If Production Clock feels like a slog, players abandon sessions mid-film.
- **MEDIUM RISK:** Event repetition. If the same event text appears 3+ times in one production, immersion breaks.
- **LOW RISK:** Event deck seeding math error. Easy to validate with simulation.

**Regression Checklist:**
- [ ] Event deck seeds correctly based on cast/crew/script
- [ ] Event categories do not repeat more than 2 consecutive times
- [ ] Quiet days occur every 5 days
- [ ] Momentum system modifies event weights correctly
- [ ] All event effects apply correctly
- [ ] Production completes without blocking bugs
- [ ] Save/load mid-production preserves event state

---

### 3.4 The Avid Bay (Post-Production Quality Calculation)

**What We're Testing:**
- Scene cards generate with quality axes correctly calculated from production
- Editorial approach multipliers apply correctly
- Score and color grade modifiers stack correctly
- Final Film Quality calculation matches design formula
- Player can see what shifts when they select editorial approach

**Happy Path:**
1. Production completes, 8-15 scene cards generated
2. Player views scene cards in Avid Bay timeline
3. Player selects "Naturalistic" editorial approach
4. Scene card Performance values multiply by 1.3x (verify UI animates)
5. Player adds score (composer skill 75 → +11.25 to Emotional Impact)
6. Player adds color grade (colorist skill 80 → +8 to Cinematography)
7. Final Film Quality calculated and displayed

**Sad Path:**
- Production was troubled (low morale, budget overruns) → Scene card quality should be low (20-40 range)
- Player selects Nonlinear approach with editor skill 60 (< 75 threshold) → Coherence penalty applies (0.7x, no bonus)
- Player delegates to editor (Editor's Choice) with editor skill 90 → Verify editor auto-selects best approach

**Evil Path:**
- Select editorial approach, save, load, change approach → Verify scene cards recalculate correctly
- Set all scene card values to 100, apply Tight & Propulsive (performance 0.9x) → Verify clamping applies (stays at 100, not 90)
- Apply score with composer skill 0 → Verify no crash, modifier is 0

**Editorial Approach Validation:**
- For each approach, verify multipliers match design spec table (Section 4.4 of tech doc)
- Tight & Propulsive: performance 0.9x, cinematography 0.9x, pacing 1.3x, emotional_impact 0.9x, coherence 1.1x
- Slow & Meditative: performance 1.1x, cinematography 1.2x, pacing 0.7x, emotional_impact 1.2x, coherence 1.0x
- Nonlinear: coherence 0.7x (or 1.0x if editor.skill > 75)

**Final Film Quality Formula Validation:**
```
Film_Quality = (Performance_Avg * 0.30) + (Cinematography_Avg * 0.15) +
               (Pacing_Avg * 0.20) + (Emotional_Impact_Avg * 0.20) +
               (Coherence_Avg * 0.15)
```
- Manually calculate expected Film Quality for 5 test films, verify calculated value matches ±2 points

**Automated Tests:**
- Generate 100 scene card pools, apply all editorial approaches, verify multipliers apply correctly
- Verify clamping (all scene card values stay 0-100 after modifiers)
- Verify Final Film Quality is always 0-100

**Risk Assessment:**
- **MEDIUM RISK:** Editorial approach selection feels like math optimization, not creative choice. Requires playtesting to validate "feel."
- **LOW RISK:** Calculation errors. Easy to validate with unit tests.

**Regression Checklist:**
- [ ] Scene cards generate with correct quality axes
- [ ] Editorial approach multipliers apply correctly
- [ ] Score and color grade modifiers stack correctly
- [ ] Final Film Quality calculation matches design formula
- [ ] UI animates scene card quality shifts when approach is selected
- [ ] Clamping prevents values >100 or <0
- [ ] Editor's Choice auto-selects best approach based on footage

---

### 3.5 The Festival Circuit (Jury Scoring & Outcomes)

**What We're Testing:**
- Festival jury taste profiles are distinct
- Jury scoring formula calculates correctly
- Competition simulation generates realistic percentile outcomes
- Festival outcome effects apply correctly (reputation, distribution multiplier, talent loyalty)
- Press quotes align with outcome tone

**Happy Path:**
1. Player submits film to Sundance
2. Jury scores film based on taste profile (emotional_impact 30%, performance 25%, pacing 20%)
3. Film competes against 30-50 simulated rival films
4. Film ranks in top 15% → Jury Prize outcome
5. Reputation +15, distribution_multiplier 2.0x, talent loyalty +8
6. Press quotes generate: "positive" tone

**Sad Path:**
- Player submits high-commercial-viability film to Cannes → Verify commercial_viability_penalty applies (-0.5 modifier)
- Player submits low-quality film (quality 30) to any festival → Bottom 5% outcome (Walkout)
- Walkout outcome applies: reputation -15, talent loyalty -10, walkout_stigma flag set

**Evil Path:**
- Submit same film to multiple festivals in sequence → Verify Buzz penalty applies after first festival (-20 buzz)
- Submit film with marketing_spend = $0 → Verify buzz = 0, outcome is purely quality-based
- Submit film with quality 100 to a festival with misaligned taste (e.g., slow meditative film to action-focused jury) → Should still rank high but not guaranteed Grand Prize

**Jury Taste Shift Testing:**
- Advance 5 in-game years → Verify jury taste profiles shift 10-20% per year
- Track Sundance emotional_impact weight across 5 years → Should vary within 0.20-0.40 range
- Verify taste shifts are logged (for player pattern recognition)

**Festival Outcome Distribution Testing:**
- Simulate 100 films with quality 70, submit to Sundance → Outcome distribution should cluster around Positive Reception (top 40%)
- Simulate 100 films with quality 90, submit to Cannes → Outcome distribution should include Grand Prizes (top 5%)
- Verify no outcome is impossible (even a quality 30 film can theoretically avoid Walkout if competition is weak)

**Press Quote Validation:**
- Walkout outcome → Verify press quotes are "scathing" tone
- Grand Prize outcome → Verify press quotes are "ecstatic" tone
- Mixed Reception outcome → Verify press quotes are "mixed" tone
- Spot-check 20 press quotes: do they read as authored, not algorithmic?

**Automated Tests:**
- Verify jury scoring formula: `(film_quality * 0.6) + (taste_alignment * 0.3) + (buzz * 0.1)`
- Verify percentile mapping matches design spec (top 5% = Grand Prize, etc.)
- Verify outcome effects apply correctly (reputation, distribution_multiplier, loyalty)

**Risk Assessment:**
- **MEDIUM RISK:** Festival outcomes feel random. If player cannot discern pattern, they disengage from strategic submission.
- **MEDIUM RISK:** Press quotes feel generic. Same risk as coverage reports.
- **LOW RISK:** Jury scoring math error. Straightforward to validate.

**Regression Checklist:**
- [ ] Jury taste profiles are distinct per festival
- [ ] Jury scoring formula calculates correctly
- [ ] Competition percentile determines outcome correctly
- [ ] Outcome effects apply (reputation, distribution, loyalty)
- [ ] Press quotes align with outcome tone
- [ ] Buzz penalty applies to second festival submission
- [ ] Jury tastes shift 10-20% per year

---

### 3.6 The Ledger (Financial System)

**What We're Testing:**
- Cash flow tracks correctly (revenue in, expenses out)
- Operating costs increase 5% per year
- Credit line draws correctly when cash is negative
- Bankruptcy triggers when cash + credit exhausted
- Revenue streams pay out over time correctly
- Distribution deal generation matches festival outcome
- Runway calculation is accurate

**Happy Path:**
1. Studio starts with $500K cash, $250K credit line
2. Player greenlights $200K film
3. Operating costs deduct $8K/month for 4 months (pre-production + production)
4. Film completes, premieres at Sundance (Positive Reception)
5. Distribution deal offers: High advance ($80K) / Low split (20%), or Low advance ($30K) / High split (40%)
6. Player selects High advance
7. Revenue streams generate: Theatrical ($150K over 6 months), VOD ($50K over 12 months), DVD ($30K over 8 months)
8. Monthly revenue ticks deposit cash
9. Runway extends as revenue arrives

**Sad Path:**
- Studio cash drops to $0 with credit line available → Credit draws automatically
- Studio cash + credit both at $0 → Bankruptcy triggers, game over
- Player makes 3 films in rapid succession with no revenue → Cash hemorrhage, runway drops to 0

**Evil Path:**
- Take on massive debt (credit line maxed), then receive large revenue influx → Verify debt interest accrues monthly
- Self-distribute film (option C: no advance, 75% split, pay marketing costs) → Verify marketing cost deducts upfront
- Advance year 10 times rapidly → Verify operating costs increase 5% per year compounded
- DVD revenue in Year 1 vs Year 5 → Verify 8% annual decline after Year 3

**Economic Balance Testing (Critical):**
- **Art Path Playthrough:** Make 5 films with low commercial_viability (< 40), high thematic_depth (> 70)
  - Expected outcome: Festival success, grant funding unlocks, revenue lower but stable
  - Must survive to Film 5 with positive cash flow
- **Commerce Path Playthrough:** Make 5 films with high commercial_viability (> 60), genre = Horror/Thriller
  - Expected outcome: Reliable distribution deals, higher revenue, less festival prestige
  - Must survive to Film 5 with positive cash flow
- **Mixed Path Playthrough:** Alternate commercial and artistic projects
  - Expected outcome: Balanced revenue, moderate festival success
  - Must survive to Film 5 with positive cash flow

**Revenue Stream Testing:**
- Film completes, distribution deal signed (advance $50K, 6-month theatrical payout $100K)
- Verify advance pays immediately (cash += $50K)
- Verify theatrical revenue pays monthly ($16.6K/month for 6 months)
- Advance 6 months → Verify theatrical stream completes
- Verify VOD stream begins after theatrical completes

**Runway Calculation Validation:**
- Cash $200K, credit line unused $250K, operating cost $8K/month → Runway = 56.25 months
- Cash $50K, credit maxed $0, operating cost $10K/month → Runway = 5 months
- Verify UI displays runway accurately

**Automated Tests:**
- Simulate 100 months of operating costs, verify cash decreases correctly
- Simulate credit interest accrual, verify 12% annual rate applies monthly
- Simulate revenue streams, verify monthly payouts sum to total_amount

**Risk Assessment:**
- **HIGH RISK:** Economy imbalance. If art or commerce path is unviable, the game's core tension collapses.
- **MEDIUM RISK:** Financial death spiral. If player's first 2 films fail, unrecoverable state.
- **LOW RISK:** Calculation errors. Easy to validate with unit tests.

**Regression Checklist:**
- [ ] Cash flow tracks correctly (revenue and expenses)
- [ ] Operating costs increase 5% per year
- [ ] Credit line draws when cash is negative
- [ ] Bankruptcy triggers correctly
- [ ] Revenue streams pay out monthly
- [ ] Distribution deals generate correctly based on festival outcome
- [ ] Runway calculation is accurate
- [ ] Both art and commerce paths reach Film 5 with positive cash flow

---

### 3.7 Save/Load System

**What We're Testing:**
- Full simulation state saves to disk
- Save file loads without data loss or corruption
- Save file version migration works
- Save files are <500KB uncompressed
- Load time is <2 seconds
- Autosave triggers at phase transitions
- Manual save works at any time
- Save slots support 5 manual + 1 autosave

**Happy Path:**
1. Complete 3 films
2. Manually save to Slot 1
3. Continue playing, complete Film 4
4. Load Slot 1 save
5. Verify studio state matches Film 3 completion (3 films in archive, cash accurate, reputation matches)

**Sad Path:**
- Save mid-production (day 15 of 30) → Load → Verify production resumes correctly (event deck state persists, scene cards intact)
- Save with 20+ completed films → Verify save file size <500KB
- Save with corrupted data (set invalid talent ID) → Verify load fails gracefully with error message (no crash)

**Evil Path:**
- Save, edit JSON manually (change cash to $9999999), load → Verify validation detects corruption
- Save in v1.0, upgrade to v1.1, load → Verify migration applies (new fields added with defaults)
- Delete save file while game is running → Verify autosave creates new file, no crash
- Save while event is mid-resolution → Verify event state persists correctly

**Version Migration Testing:**
- Create save in v0.9 (hypothetical old version)
- Add new field to studio state in v1.0 ("artistic_identity")
- Load v0.9 save → Verify migration adds field with default value (50.0)
- Verify save version updates to "1.0" after migration

**Save File Size Stress Test:**
- Complete 20 films with max talent count (120), max relationship density
- Save file → Verify size <500KB uncompressed
- Compress save file → Verify size <150KB compressed
- Load file → Verify load time <2 seconds

**Autosave Validation:**
- Transition from Greenlight → Pre-Production → Verify autosave triggers
- Crash game during Production → Restart → Verify autosave restores to last phase transition
- Check autosave timestamp → Should update every phase transition

**Save Slot Metadata:**
- Save to Slot 1 → Verify UI displays: studio name, year, season, last film title, timestamp
- Save to Slot 2 → Verify Slot 1 is not overwritten
- Overwrite Slot 1 → Verify old save is replaced, metadata updates

**Automated Tests:**
- Save/load 100 times in sequence → Verify no data loss (hash studio state before/after)
- Simulate save corruption (delete random JSON keys) → Verify load fails gracefully

**Risk Assessment:**
- **HIGH RISK:** Save file corruption. If player loses 10 hours of progress, they abandon the game.
- **MEDIUM RISK:** Save file bloat. If saves exceed 1MB by Film 20, performance degrades.
- **LOW RISK:** Version migration. Well-understood problem with clear mitigation.

**Regression Checklist:**
- [ ] Full simulation state saves without data loss
- [ ] Save file loads correctly
- [ ] Save file size <500KB uncompressed
- [ ] Load time <2 seconds
- [ ] Autosave triggers at phase transitions
- [ ] Manual save works at any time
- [ ] Save slots support 5 manual + 1 autosave
- [ ] Version migration applies correctly
- [ ] Corrupted saves fail gracefully (no crash)

---

### 3.8 Performance & Stability

**What We're Testing:**
- Game runs at 60 FPS on min spec hardware (2019 mid-tier laptop, Intel i5, 8GB RAM, integrated graphics)
- Frame budget: logic 2ms, UI 4ms, total <16.67ms
- No memory leaks over 10-hour session
- No crash-to-desktop in stress test
- Load times (scene transitions, save/load) are acceptable

**Performance Targets:**
| Metric | Target | Test Method |
|---|---|---|
| Frame Rate | 60 FPS | Continuous 30-min session, monitor FPS counter |
| Logic Budget | <2ms per frame | Godot profiler, simulate full production cycle |
| UI Update | <4ms per frame | Profile Talent Web visualization with 120 agents |
| Scene Transition | <300ms | Measure phase transition time (Greenlight → Pre-Production) |
| Save Time | <1 second | Save with 20 completed films |
| Load Time | <2 seconds | Load with 20 completed films |
| Memory Usage | <1GB | Monitor over 10-hour session, check for leaks |

**Stress Testing:**
- **10-Hour Session:** Complete 10 films in one session, monitor FPS, memory, crashes
- **Talent Web Max Load:** 120 talents, 50% relationship density, force-directed graph rendering → Verify 60 FPS
- **Event Deck Spam:** Trigger 100 crisis events in rapid succession → Verify no frame drops
- **Save/Load Loop:** Save and load 50 times in sequence → Verify no memory leak, no performance degradation

**Min Spec Validation:**
- Test on 2019 laptop (Intel i5-8250U, 8GB RAM, Intel UHD 620 graphics, 1280x720)
- Run full production cycle → Verify 60 FPS sustained
- Load 120 talents in Talent Web → Verify UI responsive

**Memory Leak Detection:**
- Use Godot profiler to track memory allocations
- Play for 2 hours → Check memory usage
- Play for 5 hours → Check memory usage
- Play for 10 hours → Check memory usage
- Memory should plateau, not grow linearly (indicates leak)

**Automated Performance Tests:**
- Script 100-film simulation, run in fast-forward mode (skip UI animations)
- Monitor frame time, memory usage
- Verify no crash, no memory leak

**Risk Assessment:**
- **MEDIUM RISK:** Performance degradation after 5+ films (memory leak, save file bloat)
- **LOW RISK:** FPS drops. This is a 2D UI game, performance budget is generous.

**Regression Checklist:**
- [ ] 60 FPS sustained on min spec hardware
- [ ] Logic budget <2ms per frame
- [ ] UI update budget <4ms per frame
- [ ] Scene transitions <300ms
- [ ] Save time <1 second
- [ ] Load time <2 seconds
- [ ] No memory leak over 10-hour session
- [ ] No crash-to-desktop in stress test

---

## 4. Test Cases (Sample Critical Paths)

### TC-001: Complete One Film (Smoke Test)
**Priority:** P0 (Blocker)
**Preconditions:** New game, studio initialized
**Steps:**
1. Enter Greenlight phase, select script "The Apiarist"
2. Enter Pre-Production, cast actor "Mara Chen" (skill 72, ego 55)
3. Enter Production, complete 18-day shoot (accept all default choices)
4. Enter Post-Production, select "Naturalistic" editorial approach
5. Enter Festival, submit to Sundance
6. Receive outcome (verify outcome in top 40%)
7. Verify reputation increased, revenue streams generated

**Expected Result:** Film completes without errors, studio advances to Film 2

**Actual Result:** _[To be filled during test execution]_

**Pass/Fail:** _[To be filled during test execution]_

---

### TC-002: Art Path Viability (5-Film Economic Balance)
**Priority:** P0 (Blocker)
**Preconditions:** New game
**Steps:**
1. Greenlight 5 scripts with commercial_viability < 40, thematic_depth > 70
2. Cast low-cost talent (keep production budgets <$300K)
3. Submit all films to Cannes or Sundance (prestige festivals)
4. Verify festival success (at least 3 films in top 40%)
5. Apply for grant funding (unlock after Reputation 40)
6. Complete Film 5

**Expected Result:** Studio cash flow positive, runway >6 months

**Actual Result:** _[To be filled during test execution]_

**Pass/Fail:** _[To be filled during test execution]_

---

### TC-003: Commerce Path Viability (5-Film Economic Balance)
**Priority:** P0 (Blocker)
**Preconditions:** New game
**Steps:**
1. Greenlight 5 scripts with commercial_viability > 60, genre = Horror or Thriller
2. Keep production budgets low ($150K-$400K)
3. Submit films to Toronto (high distribution deal density)
4. Accept high-advance distribution deals (prioritize upfront cash)
5. Complete Film 5

**Expected Result:** Studio cash flow positive, runway >6 months

**Actual Result:** _[To be filled during test execution]_

**Pass/Fail:** _[To be filled during test execution]_

---

### TC-004: Save/Load Mid-Production
**Priority:** P1 (High)
**Preconditions:** Production in progress, day 15 of 30
**Steps:**
1. Pause mid-production, manually save to Slot 2
2. Continue production, complete Film
3. Load Slot 2 save
4. Verify production resumes at day 15
5. Verify event deck state persists (no duplicate events)
6. Complete production from day 15

**Expected Result:** Production resumes correctly, no data loss

**Actual Result:** _[To be filled during test execution]_

**Pass/Fail:** _[To be filled during test execution]_

---

### TC-005: Talent Poaching (Relationship Conflict)
**Priority:** P2 (Medium)
**Preconditions:** Actor "Dex Amari" has studio_relationship +30, recent success (Palme d'Or nomination)
**Steps:**
1. Advance 6 months (trigger poaching check)
2. Rival studio offers Dex $80K (30% premium over player's usual rate)
3. Verify Dex evaluates offer based on loyalty + ambition traits
4. If Dex accepts, verify availability = false, studio_relationship decreases by -15

**Expected Result:** Dex's decision respects relationship and traits

**Actual Result:** _[To be filled during test execution]_

**Pass/Fail:** _[To be filled during test execution]_

---

### TC-006: Decision Fatigue (Production Clock Engagement)
**Priority:** P0 (Blocker)
**Preconditions:** 30-day production (high-budget film)
**Steps:**
1. Enter Production with $1.5M budget, 30-day schedule
2. Track player engagement (subjective observation: are they still reading event text by day 20?)
3. Verify "quiet day" occurs every 5 days
4. Verify event categories do not repeat more than 2 consecutive times
5. Complete 30-day production

**Expected Result:** Player remains engaged through day 30, does not skip event text

**Actual Result:** _[To be filled during test execution]_

**Pass/Fail:** _[To be filled during test execution]_

---

### TC-007: Bankruptcy Recovery (Financial Death Spiral)
**Priority:** P1 (High)
**Preconditions:** Studio cash $30K, credit maxed, runway 3 months
**Steps:**
1. Complete one film with minimal budget ($50K micro-budget)
2. Submit to festival, receive Positive Reception
3. Distribution deal advance $40K, revenue stream $80K over 6 months
4. Verify cash flow stabilizes, runway extends

**Expected Result:** Player can recover from near-bankruptcy with micro-budget film

**Actual Result:** _[To be filled during test execution]_

**Pass/Fail:** _[To be filled during test execution]_

---

### TC-008: Coverage Report Quality (Read-Aloud Test)
**Priority:** P0 (Blocker)
**Preconditions:** 20 generated scripts
**Steps:**
1. Generate 20 scripts with diverse genres and attributes
2. Read coverage reports aloud
3. Evaluate: Do they sound authored or algorithmic?
4. Check for repetition (identical phrases, near-duplicate loglines)
5. Verify attribute alignment (script described as "heavy" has tone > 70)

**Expected Result:** 18/20 coverage reports pass read-aloud test (sound authored)

**Actual Result:** _[To be filled during test execution]_

**Pass/Fail:** _[To be filled during test execution]_

---

### TC-009: Festival Outcome Predictability (Strategy Validation)
**Priority:** P1 (High)
**Preconditions:** 5 films with varying quality (40, 60, 70, 85, 95)
**Steps:**
1. Submit quality-40 film to Sundance → Expect Cold Reception or Walkout (bottom 30%)
2. Submit quality-60 film to Toronto → Expect Mixed Reception (40-70%)
3. Submit quality-70 film to Sundance → Expect Positive Reception (top 40%)
4. Submit quality-85 film to Cannes (aligned taste: high cinematography) → Expect Jury Prize (top 15%)
5. Submit quality-95 film to Cannes → Expect Grand Prize (top 5%)

**Expected Result:** Outcomes align with quality and taste alignment

**Actual Result:** _[To be filled during test execution]_

**Pass/Fail:** _[To be filled during test execution]_

---

### TC-010: Talent Loyalty Arc (Muse Dynamic)
**Priority:** P2 (Medium)
**Preconditions:** Actor "Mara Chen" and Director "Elena Voss" have worked together on 2 films (both Positive Receptions)
**Steps:**
1. Cast Mara and Elena together on Film 3
2. Verify chemistry_modifier +20 applies (stacks)
3. Verify salary discount 30% applies to Mara
4. Complete Film 3 successfully
5. Verify "Muse" event triggers: Elena writes script specifically for Mara
6. Greenlight Muse script

**Expected Result:** Muse bond develops, unique event chain unlocks

**Actual Result:** _[To be filled during test execution]_

**Pass/Fail:** _[To be filled during test execution]_

---

## 5. Edge Case & Exploit Testing

**What breaks when the player does THIS?**

### Edge Case: Empty Talent Pool
- **Setup:** Fire or lose all actors through poaching
- **Test:** Attempt to cast a film → Verify error messaging, verify fallback (default actors always available)

### Edge Case: Zero Budget Greenlight
- **Setup:** Studio cash $5K, cheapest script option cost $10K
- **Test:** Attempt to greenlight → Verify blocked, verify UI shows insufficient funds

### Edge Case: Maximum Relationship (Clamp Validation)
- **Setup:** Manually set actor studio_relationship to +100 (exceeds max +50)
- **Test:** Load save → Verify relationship clamps to +50
- **Test:** Negotiate with actor → Verify discount does not exceed max

### Edge Case: Negative Scene Quality
- **Setup:** Production with terrible morale (0), low-skill talent, budget overruns
- **Test:** Scene cards generate → Verify quality values clamp to 0 (not negative)

### Edge Case: Festival Submission with No Budget for Fee
- **Setup:** Studio cash $1K, Cannes submission fee $5K
- **Test:** Attempt to submit → Verify blocked or credit draws (if available)

### Exploit: Save Scumming Script Pool
- **Setup:** Enter Greenlight phase, dislike available scripts
- **Test:** Save, quit, reload → Does script pool reroll or stay fixed?
- **Expected:** Script pool should be fixed per season (seeded deterministically)

### Exploit: Infinite Negotiation Loop
- **Setup:** Offer actor $1, actor rejects, relationship -1
- **Test:** Repeat 100 times → Verify relationship bottoms at -50, verify actor does not accept $1 offer

### Exploit: Double-Cast Actor via Rapid Clicks
- **Setup:** Actor available, two casting slots open
- **Test:** Rapidly click "Cast" on same actor for both slots
- **Expected:** Second click blocked, actor marked unavailable after first cast

### Exploit: Skip Production via Save/Load
- **Setup:** Production day 1 of 30
- **Test:** Save, quit, manually edit save JSON to set production day = 30
- **Expected:** Load fails gracefully (validation detects corruption) OR game allows but scene quality is 0 (no production occurred)

---

## 6. Platform-Specific Testing

### PC (Steam) — Primary Platform

**Steam Integration:**
- [ ] Cloud saves sync correctly (save on PC 1, load on PC 2)
- [ ] Achievements unlock correctly (first film, first festival win, 10 films, Palme d'Or)
- [ ] Steam overlay works (Shift+Tab)
- [ ] Controller support (optional but recommended for accessibility)

**Resolution Testing:**
- [ ] 1280x720 (min spec) → UI readable, text not truncated
- [ ] 1920x1080 (recommended) → UI scales correctly
- [ ] 2560x1440 → UI scales correctly
- [ ] 3840x2160 (4K) → UI scales correctly, performance stable

**Input Testing:**
- [ ] Mouse navigation works (click, hover, scroll)
- [ ] Keyboard shortcuts work (Tab, Enter, Esc)
- [ ] Gamepad navigation (if implemented)

---

### Switch — Secondary Platform

**Controller Navigation:**
- [ ] Left stick navigates UI panels
- [ ] Right stick scrolls content
- [ ] A button confirms
- [ ] B button cancels
- [ ] Shoulder buttons cycle tabs
- [ ] All interactive elements reachable via controller

**Resolution Testing:**
- [ ] 1280x720 handheld → UI readable on 6.2" screen, min font 16pt
- [ ] 1920x1080 docked → UI scales correctly

**Performance:**
- [ ] 60 FPS target (30 FPS acceptable fallback)
- [ ] No frame drops during Talent Web visualization
- [ ] Load times <3 seconds (Switch SSD is slower than PC)

**Suspend/Resume:**
- [ ] Suspend game mid-production → Resume → Verify state persists
- [ ] Suspend during save → Resume → Verify save completes or rolls back cleanly

---

## 7. Regression Testing (Post-Fix Verification)

After any bug fix, verify the following regression checklist:

### Full Production Cycle Regression
- [ ] Complete one film end-to-end (Greenlight → Release)
- [ ] Verify all phases transition correctly
- [ ] Verify no new bugs introduced

### Save/Load Regression
- [ ] Save at each phase (Greenlight, Pre-Prod, Production, Post, Festival)
- [ ] Load each save → Verify phase resumes correctly

### Economy Regression
- [ ] Run 5-film playthrough (art path)
- [ ] Run 5-film playthrough (commerce path)
- [ ] Verify both reach Film 5 with positive cash flow

### Talent Web Regression
- [ ] Cast 10 different actors across 3 films
- [ ] Verify relationships update correctly
- [ ] Verify chemistry modifiers apply
- [ ] Verify Talent Web visualizes without errors

### Event Deck Regression
- [ ] Complete 3 productions (different budget tiers)
- [ ] Verify event deck seeds correctly
- [ ] Verify no event category repeats 3+ times consecutively

---

## 8. Performance Benchmarks

**Test Environment:**
- **Min Spec:** Intel i5-8250U, 8GB RAM, Intel UHD 620, 1280x720, Windows 10
- **Recommended:** Intel i7-10700, 16GB RAM, GTX 1650, 1920x1080, Windows 11

**Benchmarks:**

| Test | Min Spec Target | Recommended Target | Actual (Min) | Actual (Rec) |
|---|---|---|---|---|
| Idle Menu | 60 FPS | 60 FPS | _[TBD]_ | _[TBD]_ |
| Greenlight UI | 60 FPS | 60 FPS | _[TBD]_ | _[TBD]_ |
| Talent Web (120 agents) | 60 FPS | 60 FPS | _[TBD]_ | _[TBD]_ |
| Production Clock | 60 FPS | 60 FPS | _[TBD]_ | _[TBD]_ |
| Avid Bay | 60 FPS | 60 FPS | _[TBD]_ | _[TBD]_ |
| Festival Sequence | 60 FPS | 60 FPS | _[TBD]_ | _[TBD]_ |
| Save Time (20 films) | <2 sec | <1 sec | _[TBD]_ | _[TBD]_ |
| Load Time (20 films) | <3 sec | <2 sec | _[TBD]_ | _[TBD]_ |
| Memory Usage (10hr) | <1GB | <1GB | _[TBD]_ | _[TBD]_ |

**If any benchmark fails:** Profile, optimize, retest. Do not ship below target.

---

## 9. Bug Severity Classification

**Severity Levels:**

| Severity | Definition | Example | Response Time |
|---|---|---|---|
| **S1: Blocker** | Game unplayable, data loss, crash-to-desktop | Save file corruption, startup crash | Fix immediately, block release |
| **S2: Critical** | Core feature broken, no workaround | Festival submission does nothing, Production Clock does not advance | Fix within 48 hours |
| **S3: High** | Feature broken but workaround exists | Talent Web visualization broken (can cast via list view) | Fix before release |
| **S4: Medium** | Feature works but behaves incorrectly | Event deck repeats 3 times (should be 2 max) | Fix before release if time allows |
| **S5: Low** | Cosmetic, minor annoyance | Typo in coverage report, UI element misaligned | Fix post-launch or defer |

**Blocker Criteria for Release:**
- Zero S1 bugs
- Zero S2 bugs
- <5 S3 bugs (and all have workarounds documented)

---

## 10. Test Automation Strategy

**What We Automate:**
- Unit tests for formulas (jury scoring, film quality calculation, negotiation math)
- Save/load integrity (hash comparison before/after)
- Procedural generation validation (no duplicate loglines in 1000 scripts)
- Event deck distribution (simulate 100 productions, verify weights ±10%)
- Performance smoke tests (load game, simulate one film, measure frame time)

**What We Do NOT Automate:**
- Content quality (coverage reports, press quotes) → Requires human judgment
- Decision fatigue → Requires human playtest observation
- "Feel" of systems (does casting feel strategic? does Production Clock feel tense?) → Playtesting

**Automation Tools:**
- GDScript test suite (Godot's built-in unit test framework)
- CI/CD pipeline (GitHub Actions) runs tests on every commit to `develop`
- Smoke test suite runs on every build

**Test Coverage Goal:** 70% of logic code covered by automated tests. 100% of critical formulas covered.

---

## 11. Open QA Questions (For Design/Dev Team)

These are questions I cannot answer from the design doc alone. They require designer input or prototyping.

1. **Script pool reroll:** If player dislikes Greenlight scripts, can they save/load to reroll? Or is script pool seeded deterministically per season? (Impact: save scumming exploit)

2. **Event deck exhaustion:** If a production runs 40 days with high crisis frequency, can the event deck run out of unique events? (Impact: repetition, immersion break)

3. **Talent relationship floor:** If player abuses actor (fires mid-production, lowballs repeatedly), can relationship drop below -50? Or is -50 hard floor? (Impact: clamp validation)

4. **Bankruptcy recovery:** If studio hits $0 cash + $0 credit, is game over immediate? Or is there a 3-month grace period for emergency grant? (Design doc mentions emergency grant — when does it trigger?)

5. **Festival buzz penalty:** If player submits same film to 2 festivals, design doc says -20 buzz penalty. Does this apply to Sundance → Cannes submission in same year? Or only if player resubmits to same festival? (Clarify scope)

6. **Talent poaching frequency:** Rival studios check for poaching every 6 months. If player has 10 high-reputation actors, do all 10 get poached simultaneously? Or is there a cap (e.g., max 2 talents poached per year)? (Impact: difficulty spike)

7. **DVD decline start year:** Design doc says DVD revenue declines 8%/year starting Year 3. Is this calendar Year 3 (2007 in-game) or after player completes Film 3? (Clarify trigger)

8. **Muse script marketability:** Muse script is "unmarketable to anyone else" — does this mean commercial_viability is locked at 0? Or just that the specific actor is required for production? (Impact: player strategy)

9. **Soft failure (Creative Irrelevance):** Reputation < 15 for 12 months = soft failure. Does the game explicitly tell the player they are in Creative Irrelevance state? Or is it invisible, and player discovers through gameplay consequences? (Impact: UI feedback)

10. **Quiet day frequency:** Every 5th day is a "quiet day" (0-1 decisions). Is this strictly every 5th day (5, 10, 15, 20, 25, 30)? Or is it weighted probability (20% chance per day after day 4)? (Impact: implementation)

---

## 12. Closeout

This is the plan. The tests are the contract. If it passes the gates, it ships. If it does not, we do not ship it and patch later. That is how save-corruption bugs make it to launch. That is how 1-star reviews flood in before the hotfix lands.

Testing starts Week 1. Vertical slice playtesting starts Week 2. If coverage reports do not pass the read-aloud test, we block until they do. If the Production Clock feels like a slog by day 15, we compress to weekly decisions. If the economy does not support both art and commerce paths, we do not ship until it does.

The player does not care about your clever event deck algorithm. They care about whether they feel like a producer making hard choices. If they do, we have a game. If they do not, we have a spreadsheet with a UI.

What happens if the player does THIS? That is the question. Every edge case. Every exploit. Every moment where the simulation could break. We find it before they do. Every single one.

Define "works."

**-- CRASH**
