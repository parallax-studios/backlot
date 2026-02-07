# BACKLOT — Production Plan

**Producer: CLOCK**
**Status: Production-Ready v1.0**
**Target Delivery: 40 weeks from greenlight**
**Team: 2 programmers, 2 artists, 1 sound designer/composer, 1 writer, 1 producer (CLOCK)**

---

## 1. Project Overview

### 1.1 What We're Shipping

An indie film studio simulation management game where you greenlight scripts, wrangle talent, survive chaotic productions, and bet everything on festival premieres. PC primary (Steam), Switch secondary. 60fps, 2D UI-driven, systems-heavy.

**Not**: A 3D production sim. Not a narrative adventure. Not a film editing tool. This is a management game about people, relationships, and the gap between vision and budget.

### 1.2 Core Deliverable

One complete production cycle loop: Greenlight script → Cast talent → Shoot (15-40 days) → Edit → Submit to festival → See outcome → Repeat. That loop must be polished, balanced, and replayable. Everything else is detail.

### 1.3 Team Structure

| Role | Head Count | Responsibilities | Critical Path? |
|------|-----------|------------------|----------------|
| **Lead Programmer (BYTE)** | 1 | Core systems (state machine, simulation, save/load), data architecture | YES |
| **UI/Systems Programmer** | 1 | UI implementation (Godot Control nodes), event system, procedural generation | YES |
| **Art Director (PIXEL)** | 1 | Visual identity, UI mockups, asset pipeline, color/typography specs | YES (Weeks 1-12) |
| **UI Artist** | 1 | Asset production (2D textures, headshots, props, backgrounds) | YES (Weeks 13-24) |
| **Sound Designer/Composer (ECHO)** | 1 | SFX library, adaptive ambiance, music themes | YES (Weeks 17-32) |
| **Writer (Narrative Content)** | 1 | Script templates, coverage phrase library, event text, press quotes | YES (Weeks 9-20) |
| **Producer (CLOCK)** | 1 | Scope management, milestone tracking, dependency resolution, risk mitigation | YES (All weeks) |

**Total team: 7 people.** No outsourcing dependencies. No external blockers.

### 1.4 Budget Constraints

Assuming indie budget. Tight control on:
- Asset count (no bloat — quality over quantity)
- Headshot photography (hire local actors or use licensed stock, not custom shoot unless budget allows)
- Music composition (5 core themes + 40-60 temp tracks, not a full OST)
- Voice recording (unintelligible snippets, not full VO, 80 snippets max)

**What we CUT if time/budget tightens**: Rival Studio system, Awards Season track, Muse dynamics, office seasonal variations, procedural text complexity (fallback: smaller authored script pool).

### 1.5 Platform Targets

**Primary**: PC (Windows/Mac/Linux) via Steam. This is where management sims live.

**Secondary**: Nintendo Switch. Only pursue after PC version is stable and performing at 60fps. Budget 4 weeks for controller UI adaptation.

**Stretch (Do Not Plan For)**: iPad. Touch UI is a full redesign. Not v1.0.

---

## 2. Milestone Definitions

### MILESTONE 1: VERTICAL SLICE (Weeks 1-8)

**Entry Criteria**: Team assembled, design docs complete, Godot 4.x environment configured, version control live.

**Exit Criteria**: One complete film production cycle playable from greenlight to festival outcome. All core systems functional (not polished). Save/load works. No critical bugs. Playable by external tester without crashing.

**Deliverables**:
1. Game state machine operational (all 6 phases: Greenlight, Pre-Prod, Production, Post, Festival, Season Transition)
2. Greenlight Table UI with 20 procedural scripts (coverage reports must feel authored)
3. Talent Pool with 20 agents (simplified relationship graph, full stats)
4. Production Clock with 10-day simplified shoot (5 crisis events from authored pool)
5. Avid Bay with editorial approach selection and quality calculation
6. Festival system with 1 festival (Sundance), jury scoring, outcome generation
7. Financial Ledger with budget tracking and runway calculation
8. Save/load system functional (full state serialization)
9. Basic UI (cork board, whiteboard, CRT monitor aesthetic blocked in, not final art)
10. Placeholder audio (royalty-free ambiance, no custom SFX yet)

**Key Risks**:
- **Procedural script quality**: Coverage reports must not feel generic. If they do by Week 3, pivot to fully authored scripts (100 pre-written instead of infinite procedural).
- **Production Clock pacing**: If playtesters report fatigue by day 7, compress to weekly decisions immediately.
- **Save file corruption**: Test save/load after every system addition. Corrupted saves kill momentum.

**Acceptance Test**: External playtester completes one film cycle in 45-60 minutes without tutorial handholding and can articulate why they made key decisions.

---

### MILESTONE 2: CORE LOOP COMPLETE (Weeks 9-16)

**Entry Criteria**: Vertical Slice accepted, feedback integrated, team velocity measured (know our actual burn rate).

**Exit Criteria**: Full production pipeline with all systems at design doc parity. 80 talents, all 5 festivals, full financial model, relationship graph complete. Player can complete 5 films and feel progression.

**Deliverables**:
1. Talent Pool expanded to 80 agents with full relationship graph (pairwise relationships, chemistry, loyalty)
2. Crisis event deck complete (50+ authored events across all 8 categories)
3. All 5 festivals functional (Sundance, Cannes, Toronto, Venice, Berlin) with distinct jury profiles
4. Financial system with revenue streams (theatrical, VOD, DVD, international, prizes), investor system, grant funding
5. Ledger UI with 12-month cash flow projections and burn rate visualization
6. Talent Web visualization (force-directed graph on cork board, headshots as nodes, connection strings)
7. Studio progression system (reputation tiers, unlocks, artistic identity tracking)
8. Seasonal structure (4 seasons per year, time advances correctly, operating costs scale)
9. UI polish pass #1 (diegetic elements refined, animations for key interactions)
10. First audio pass (office ambiance bed, key SFX for player actions, placeholder temp music)

**Key Risks**:
- **Talent Web performance**: 80 agents with full relationship graph. Profile early. If frame rate drops below 60fps, reduce to 60 agents or optimize graph rendering (background thread).
- **Event fatigue**: 50 events is enough for 5 films. If repetition is noticeable, we need more. Budget writer time accordingly.
- **Festival scoring opacity**: Players must understand why they won or lost. If post-playtest feedback shows confusion, add score breakdown UI immediately.

**Acceptance Test**: Playtester completes 5 films across 2.5 in-game years without hitting blocking bugs. Financial death spiral is survivable with smart play. Talent relationships feel consequential.

---

### MILESTONE 3: CONTENT & POLISH (Weeks 17-24)

**Entry Criteria**: Core loop accepted, no critical bugs in backlog, performance stable at 60fps.

**Exit Criteria**: Content at scale. Procedural systems have depth. UI is polished and juicy. Audio is implemented and adaptive. Game feels alive.

**Deliverables**:
1. Talent Pool finalized at 120 agents (if performance allows; fallback: 80)
2. Crisis event library expanded to 150+ events (diversity to support 10+ film playthroughs)
3. Script generation library complete:
   - 50 logline templates per genre (300+ total across 6 genres)
   - 200+ coverage phrase fragments
   - Pretension Index fully tuned
4. Press quote generation library (50+ phrases per tone tier)
5. Headshot photography complete (80-120 unique headshots, processed to match color palette)
6. Prop and background asset production (scripts, envelopes, coffee cups, desk surfaces, cork boards, whiteboards, CRT monitors)
7. UI animation pass (camera pans, object drags, slate claps, page flips, all micro-interactions)
8. Audio SFX library complete (200+ SFX covering all game phases, see sound design doc Sections 3.1-3.6)
9. Music composition complete (5 core themes: Greenlight Table, The Take, Lights Go Down, Vindication, Lights Go Out)
10. Adaptive audio system implemented (ambiance beds respond to Morale/Momentum, dynamic mixing, diegetic temp music)

**Key Risks**:
- **Headshot sourcing**: If custom photo shoot is too expensive, pivot to licensed stock photography (Shutterstock/Adobe Stock). Ensure diversity and authenticity.
- **Audio asset count**: 200+ SFX is achievable but tight. Prioritize P0 sounds (player actions, critical alerts, ambiance beds). Cut P3 sounds (idle loops, rare Easter eggs) if time compresses.
- **Writer bandwidth**: Phrase library authorship is time-intensive. If writer is behind schedule by Week 18, freeze event authoring and focus on script/coverage quality.

**Acceptance Test**: Playtester completes 10 films. No repeated events within a single playthrough. Coverage reports feel distinct and authored. Festival premiere sequence has emotional weight. Audio communicates game state without looking at UI.

---

### MILESTONE 4: BETA & BALANCE (Weeks 25-32)

**Entry Criteria**: All content complete, no placeholder assets, game is feature-complete.

**Exit Criteria**: Game is shippable. Economy is balanced. Difficulty curve is tuned. All P0/P1 bugs fixed. Performance is stable on min spec hardware.

**Deliverables**:
1. Economy balance pass:
   - Both art-focused and commerce-focused strategies reach Film 10 in 60%+ of playthroughs
   - Revenue/cost ratios match design doc targets (see GDD Section 7.1)
   - Bankruptcy is rare but possible, creative irrelevance is a soft failure state
2. Festival jury tuning (taste profiles shift 10-20% per year, competition simulation balanced)
3. Talent cost/salary balance (no single talent breaks the economy, loyalty discounts are meaningful)
4. Production Clock pacing tuned (quiet days every 5 days, crisis fatigue eliminated)
5. Full QA pass:
   - 20-hour playthrough test (complete 12-15 films without crashes)
   - Save/load stress test (10 saves, load each, verify state integrity)
   - Edge case testing (bankruptcy recovery, talent poaching, festival walkouts)
6. Performance optimization pass:
   - 60fps on 2019 mid-tier laptop (Intel i5, 8GB RAM, integrated graphics)
   - Load times <2s for save files, <0.3s for phase transitions
   - Memory footprint <1GB
7. Accessibility features:
   - Colorblind modes (protanopia, deuteranopia, tritanopia)
   - Font scaling (100%, 125%, 150%)
   - High contrast mode
   - Audio accessibility (Dialogue Boost, Reduce Background, Mono Mix, Visual Alerts)
8. Tutorial/onboarding flow (first film is guided with mentor NPC hints, not intrusive)
9. Final UI polish (all animations smooth, no visual bugs, text is legible at 1080p)
10. Final audio mix (all 8 mix channels balanced, no clipping, LUFS targets met)

**Key Risks**:
- **Economy death spiral**: If art-path or commerce-path dominates, entire theme collapses. This is highest-priority balance work. If one strategy is 30%+ more profitable, redesign funding sources immediately.
- **Production fatigue**: If testers still report burnout during 30-day shoots, compress to week-by-week decisions. This is a core loop issue, not a balance issue.
- **Performance on min spec**: If 60fps is not achievable, reduce Talent Pool to 60, reduce headshot texture atlas size, simplify force-directed graph (static layout instead of real-time).

**Acceptance Test**: External beta playtesters (10 people, 2-3 hour sessions each) complete game without critical bugs. 80%+ report they would recommend the game. Metacritic/Steam review projection is "Positive" or better based on beta feedback.

---

### MILESTONE 5: LAUNCH PREP (Weeks 33-40)

**Entry Criteria**: Beta accepted, all critical/high-priority bugs fixed, game is content-complete and stable.

**Exit Criteria**: Game is on Steam, builds are exported for all platforms, store page is live, press has keys, launch trailer is ready.

**Deliverables**:
1. Steam integration:
   - Achievements (10-15 achievements: first film, first festival win, first bankruptcy, Palme d'Or, 10 films completed, etc.)
   - Cloud saves
   - Trading cards (optional, low priority)
   - Store page live (screenshots, trailer, description, tags)
2. Switch port (if pursuing):
   - Controller UI adaptation (d-pad navigation, button mappings, readable at 720p handheld)
   - Performance at 30fps minimum (60fps target)
   - Nintendo certification submission
3. Launch trailer:
   - 60-90 seconds
   - Hook: "What's the GIF?" moment (script greenlight → chaotic shoot → festival ovation)
   - Tone: Serious but not self-serious, conveys both systems depth and human drama
   - Capture footage from actual game (no bullshots)
4. Press kit:
   - 10-15 screenshots (1080p, showcasing each UI zone)
   - Key art (production office diorama shot)
   - Fact sheet (elevator pitch, features, release date, platforms, price)
   - Review keys distributed to press 2 weeks before launch
5. Final bug triage:
   - P0 bugs (crashes, save corruption, soft locks): ZERO
   - P1 bugs (major gameplay issues, balance exploits): <5
   - P2 bugs (minor UI glitches, typos, rare edge cases): <20
   - P3 bugs (polish issues, nice-to-haves): Logged for post-launch patch
6. Day-1 patch plan (if needed for last-minute critical fixes)
7. Community management prep:
   - Discord server or subreddit setup
   - FAQ document
   - Patch notes template
   - Bug reporting process

**Key Risks**:
- **Steam approval delay**: Submit build to Steam 2 weeks before target launch date. If rejected, we have time to fix and resubmit.
- **Switch certification delay**: Nintendo cert can take 4-6 weeks. If pursuing Switch, submit 6 weeks before target launch or plan Switch as post-launch (30-60 days after PC).
- **Press coverage gap**: If press doesn't pick up the game, launch sales suffer. Backup plan: strong community engagement on /r/tycoon, /r/BaseBuildingGames, Film Twitter.

**Acceptance Test**: Game launches on Steam without critical issues. Day-1 player experience is smooth (no widespread crashes, saves work, performance is acceptable). First week player retention is >40% (players who buy it play more than 2 hours).

---

## 3. Sprint Plan (40-Week Breakdown)

### Phase 1: Prototype & Vertical Slice (Weeks 1-8)

| Week | Focus | Lead | Deliverables | Dependencies |
|------|-------|------|--------------|--------------|
| **1** | Setup & Architecture | BYTE | Godot project configured, Git repo live, state machine skeleton, Studio/Film/Talent data structures defined | None |
| **1** | Concept Validation | PIXEL | Greenlight Table mockup (Figma), color palette test, typography specimens, silhouette test for key objects | None |
| **2** | Core Loop Prototype | BYTE | Greenlight phase functional (script generation, coverage display, greenlight decision), save/load skeleton | Week 1 |
| **2** | UI Foundation | UI Programmer | Godot UI scenes for Greenlight Table, basic cork board layout, script card drag-and-drop | Week 1 |
| **3** | Talent System | BYTE | TalentPool class, 20 agents created, relationship graph, negotiation logic | Week 2 |
| **3** | Procedural Scripts | Writer + UI Programmer | 20 script logline templates (5 per genre), coverage phrase library v1 (50 fragments), generation pipeline | Week 2 |
| **4** | Production Clock | UI Programmer | Production phase state machine, day-by-day loop, 5 crisis events authored, decision UI | Week 3 |
| **4** | Talent Web UI | PIXEL + UI Programmer | Cork board visualization mockup, headshot node layout, connection strings (static, not force-directed yet) | Week 3 |
| **5** | Post-Production | BYTE | Scene card generation from production, editorial approach system, quality calculation | Week 4 |
| **5** | Event System | UI Programmer | Event deck seeding, weighted draws, crisis event JSON parser | Week 4 |
| **6** | Festival System | BYTE | Sundance festival definition, jury scoring, competition simulation, outcome generation | Week 5 |
| **6** | Financial Ledger | UI Programmer | Studio cash tracking, budget allocation, revenue streams, bankruptcy check | Week 5 |
| **7** | Integration & Polish | All | Connect all phases into full loop, fix state transition bugs, save/load serialization complete | Weeks 1-6 |
| **7** | Placeholder Art | PIXEL | Basic UI sprites (scripts, headshots, props), office background, cork board, whiteboard textures | Weeks 1-6 |
| **8** | Vertical Slice Playtest | CLOCK + All | Internal playtest (2 team members), external playtest (1 target audience member), bug triage, feedback integration | Week 7 |

**Milestone 1 Gate**: If coverage reports feel generic or Production Clock is exhausting, STOP. Fix before proceeding.

---

### Phase 2: Core Loop Expansion (Weeks 9-16)

| Week | Focus | Lead | Deliverables | Dependencies |
|------|-------|------|--------------|--------------|
| **9** | Talent Pool Expansion | BYTE | 80 agents created, full relationship graph implemented, chemistry map for actors | M1 accepted |
| **9** | Event Authoring | Writer | 50 crisis events authored (across all 8 categories), JSON formatted, tested | M1 accepted |
| **10** | All Festivals | BYTE | Cannes, Toronto, Venice, Berlin implemented with distinct jury profiles, buzz calculation | Week 9 |
| **10** | Talent Web Graph | UI Programmer | Force-directed graph layout (background thread), connection string animation, headshot flip interaction | Week 9 |
| **11** | Revenue System | BYTE | Distribution deal generation, revenue stream ticking, investor system, grant funding | Week 10 |
| **11** | Studio Progression | UI Programmer | Reputation tiers, unlocks, artistic identity tracking, office upgrade visuals (basic) | Week 10 |
| **12** | Seasonal Structure | BYTE | 4 seasons per year, time advances, operating cost inflation, DVD revenue decline curve | Week 11 |
| **12** | Ledger UI | PIXEL + UI Programmer | CRT monitor asset, spreadsheet layout, cash flow projection graph, runway bar | Week 11 |
| **13** | UI Polish Pass 1 | PIXEL + UI Programmer | Camera pans between zones, script drag animations, headshot pin animation, slate clap transition | Weeks 9-12 |
| **13** | Audio Foundation | ECHO | Office ambiance bed, placeholder SFX for player actions (clicks, drags, stamps), menu music sketch | Weeks 9-12 |
| **14** | Balance Tuning 1 | BYTE + CLOCK | Financial targets tested (art vs commerce viability), talent salary curve, festival scoring weights | Week 13 |
| **14** | Content Expansion | Writer | Script templates expanded to 30 per genre (180 total), coverage library to 100 fragments | Week 13 |
| **15** | Integration Testing | All | 5-film playthrough test, save/load stress test, relationship graph pathfinding performance profiling | Week 14 |
| **16** | Milestone 2 Playtest | CLOCK + All | External playtest (3 people, 3-hour sessions), bug triage, feedback review | Week 15 |

**Milestone 2 Gate**: If 5-film playthrough reveals economy imbalance or decision fatigue, address before M3.

---

### Phase 3: Content Production & Polish (Weeks 17-24)

| Week | Focus | Lead | Deliverables | Dependencies |
|------|-------|------|--------------|--------------|
| **17** | Headshot Photography | PIXEL + UI Artist | 80-120 headshots sourced (stock or custom), processed to match palette, texture atlas built | M2 accepted |
| **17** | Audio SFX Production | ECHO | 100 SFX recorded/sourced (office sounds, paper, phone rings, equipment), categorized, labeled | M2 accepted |
| **18** | Script Library Finalization | Writer | 50 templates per genre (300 total), coverage library to 200 fragments, press quote library (50 phrases) | Week 17 |
| **18** | Prop Assets | UI Artist | Scripts, envelopes, coffee cups, pens, staplers, film canisters, all office props modeled/illustrated | Week 17 |
| **19** | Crisis Event Expansion | Writer | Event library to 150+ events, diversity ensured (no category feels repetitive within 10 films) | Week 18 |
| **19** | Background Assets | UI Artist | Desk surfaces (oak, walnut, metal), walls (drywall, brick), cork board, whiteboard, window views | Week 18 |
| **20** | Music Composition | ECHO | 5 core themes composed and recorded (Greenlight Table, The Take, Lights Go Down, Vindication, Lights Go Out) | Week 19 |
| **20** | UI Animation Pass | UI Programmer | All micro-interactions animated (hover states, drags, page flips, timeline scrubs, quality bars) | Week 19 |
| **21** | Adaptive Audio System | ECHO + UI Programmer | Ambiance beds respond to Morale/Momentum, dynamic mixing (8 channels), FMOD integration or Unity Audio | Week 20 |
| **21** | VFX & Animated Textures | UI Artist | Coffee stain spread, paper crumple, steam wisp, phone ring indicator, lighting effects | Week 20 |
| **22** | Diegetic Temp Music | ECHO | 40-60 temp music tracks sourced/composed, filtered for laptop speaker playback, genre-mapped | Week 21 |
| **22** | UI Component Library | PIXEL + UI Artist | All buttons, panels, borders, icons finalized, Figma component library, Unity prefabs | Week 21 |
| **23** | Audio SFX Finalization | ECHO | SFX library to 200+ sounds, all game phases covered, procedural audio systems (phone timing, crew chatter) | Week 22 |
| **23** | Content Integration | All | All assets imported to game, atlases built, performance tested, visual/audio bugs triaged | Week 22 |
| **24** | Milestone 3 Playtest | CLOCK + All | External playtest (5 people, 4-hour sessions targeting 10 films), content diversity validated | Week 23 |

**Milestone 3 Gate**: If content feels repetitive or audio doesn't communicate game state, extend this phase by 2 weeks.

---

### Phase 4: Beta & Balance (Weeks 25-32)

| Week | Focus | Lead | Deliverables | Dependencies |
|------|-------|------|--------------|--------------|
| **25** | Economy Balance | BYTE + CLOCK | Art vs commerce strategy parity tested, revenue/cost ratios tuned, bankruptcy/irrelevance thresholds validated | M3 accepted |
| **25** | Festival Tuning | BYTE | Jury taste profiles shift correctly, competition balanced, player agency in outcomes confirmed | M3 accepted |
| **26** | Talent Balance | BYTE | Salary curves, loyalty discounts meaningful, chemistry bonuses impactful, ego/ambition traits create tension | Week 25 |
| **26** | Production Pacing | BYTE + Writer | Quiet days every 5 days confirmed working, crisis fatigue eliminated, breakthrough events satisfying | Week 25 |
| **27** | QA Pass 1 | All | 20-hour playthrough (12-15 films), critical bugs logged, save/load stress tested, edge cases documented | Week 26 |
| **27** | Accessibility Features | UI Programmer | Colorblind modes implemented, font scaling (100/125/150%), high contrast mode, audio accessibility options | Week 26 |
| **28** | Performance Optimization | BYTE | Profile game, optimize hot paths (relationship graph, event deck, procedural generation), target 60fps on min spec | Week 27 |
| **28** | Tutorial/Onboarding | Writer + UI Programmer | Mentor NPC events authored, first-film guided experience, tutorial tooltips non-intrusive | Week 27 |
| **29** | Final UI Polish | PIXEL + UI Artist | All animations smooth, no visual bugs, text legible at 1080p, camera transitions seamless | Week 28 |
| **29** | Final Audio Mix | ECHO | 8 mix channels balanced, no clipping, LUFS targets met (-18 overall, see sound design doc Section 6.2) | Week 28 |
| **30** | QA Pass 2 | All | Bug triage (P0/P1 must be fixed), regression testing, performance validation | Week 29 |
| **31** | Beta Build | All | Beta build exported, distributed to 10 external testers, feedback collected | Week 30 |
| **32** | Beta Feedback Integration | All | Critical feedback addressed, final bugs fixed, balance tweaks based on beta data | Week 31 |

**Milestone 4 Gate**: If beta feedback reveals economy imbalance or core loop fatigue, extend by 2 weeks to fix.

---

### Phase 5: Launch Preparation (Weeks 33-40)

| Week | Focus | Lead | Deliverables | Dependencies |
|------|-------|------|--------------|--------------|
| **33** | Steam Integration | BYTE | Achievements implemented, cloud saves tested, store page configured | M4 accepted |
| **33** | Launch Trailer | PIXEL + CLOCK | Trailer scripted, footage captured, edited, music selected, 60-90s final cut | M4 accepted |
| **34** | Switch Port (if pursuing) | BYTE + UI Programmer | Controller UI adaptation, performance at 30fps minimum, Nintendo SDK integration | Week 33 |
| **34** | Press Kit | CLOCK + PIXEL | Screenshots captured, key art finalized, fact sheet written, review keys prepared | Week 33 |
| **35** | Final Bug Triage | All | P0 bugs = 0, P1 bugs <5, P2 bugs <20, P3 bugs logged for post-launch | Week 34 |
| **35** | Store Page Live | CLOCK | Steam store page published (2 weeks before launch), wishlists begin accumulating | Week 34 |
| **36** | Switch Certification (if pursuing) | BYTE | Nintendo cert submission (allow 4-6 weeks), feedback addressed | Week 35 |
| **36** | Community Setup | CLOCK | Discord or subreddit created, FAQ written, patch notes template ready | Week 35 |
| **37** | Press Outreach | CLOCK | Review keys distributed to press (2 weeks before launch), embargo date set | Week 36 |
| **37** | Day-1 Patch (if needed) | BYTE | Last-minute critical fixes packaged, tested, ready to deploy on launch day | Week 36 |
| **38** | Final QA Pass | All | Gold master candidate tested on all platforms, no blockers, Steam build submitted for approval | Week 37 |
| **39** | Launch Week Prep | All | Monitor Steam approval, prepare for launch day (server load if online features, community management) | Week 38 |
| **40** | LAUNCH | All | Game launches on Steam (and Switch if cert complete), community engagement, bug monitoring | Week 39 |

**Milestone 5 Complete**: Game is shipped. Post-launch patch plan active. Sales and review monitoring begins.

---

## 4. Risk Register

### 4.1 Critical Risks (Red)

| Risk ID | Risk Description | Likelihood | Impact | Mitigation | Contingency | Owner |
|---------|------------------|------------|--------|------------|-------------|-------|
| **R-001** | Procedural script coverage reports feel generic/algorithmic, destroying core mechanic | Medium | CRITICAL | Week 3: Playtest coverage quality. Budget 40-60 hours writer time on phrase library. Use template-based assembly, not pure procedural | If quality is insufficient: Pivot to 100-150 fully authored scripts instead of infinite procedural generation | Writer + CLOCK |
| **R-002** | Production Clock creates decision fatigue, players burn out before day 15 of 30-day shoot | Medium | HIGH | Week 4: Playtest production pacing. Implement "quiet day" every 5 days. Cap crisis events at 1-2 per day max. Monitor engagement | If fatigue persists: Compress to week-by-week decisions (7-10 decision points per production instead of 30) | BYTE + CLOCK |
| **R-003** | Economy death spiral: Art-path or commerce-path dominates, theme collapses | Medium | CRITICAL | Week 25: Dedicated balance pass. Test both strategies across 10 films. Revenue/cost ratios must support both within 30% variance | If imbalance detected: Redesign funding sources (adjust grant amounts, festival prize money, distribution splits) | BYTE + CLOCK |
| **R-004** | Save file corruption at scale (20+ films), players lose 10+ hours of progress | Low | CRITICAL | Weeks 7, 15, 30: Save/load stress testing. Version all save files. Implement auto-backup (last 3 saves) | If corruption occurs: Rollback to previous working build, fix serialization bug, notify players via patch | BYTE |
| **R-005** | Performance drops below 60fps with 120 talents and full relationship graph | Low-Medium | HIGH | Week 28: Profile on min spec hardware. Optimize relationship graph rendering (background thread, only show 1st/2nd degree connections) | If 60fps unachievable: Reduce Talent Pool to 60-80, reduce headshot atlas size, simplify graph layout to static | BYTE |

---

### 4.2 High Risks (Orange)

| Risk ID | Risk Description | Likelihood | Impact | Mitigation | Contingency | Owner |
|---------|------------------|------------|--------|------------|-------------|-------|
| **R-006** | Talent Web overwhelms players, feels like spreadsheet management not relationship building | Medium | MEDIUM | Week 11: Implement Agent Recommendation system (filters 120 talents to 3-5 suggestions per role). UI shows only active connections, not full graph | If overwhelm persists: Reduce active talent count to 60, improve filtering UI | UI Programmer + CLOCK |
| **R-007** | Festival scoring feels random, players can't understand why they won or lost | Medium | MEDIUM | Week 14: Post-festival feedback UI shows score breakdown (taste alignment %, quality %, buzz %). Coverage hints at festival fit ("Cannes film") | If opacity remains: Add more explicit jury taste descriptions, simplify scoring formula | BYTE |
| **R-008** | Headshot photography budget overrun or quality issues | Medium | MEDIUM | Week 17: Price compare stock photography vs. custom shoot. Ensure diversity and authenticity. Use Shutterstock/Adobe Stock if custom is >$2K | If quality is poor: Reshoot or source additional stock, delay M3 by 1 week | PIXEL + CLOCK |
| **R-009** | Audio asset production falls behind (200+ SFX is tight timeline) | Medium | MEDIUM | Week 17: Prioritize P0 sounds (player actions, critical alerts, ambiance beds). Cut P3 sounds (idle loops, Easter eggs) if needed | If behind schedule: Reduce SFX count to 150, source royalty-free library for low-priority sounds | ECHO + CLOCK |
| **R-010** | Writer bandwidth insufficient for phrase library + event authoring | Medium | MEDIUM | Week 18: Freeze event authoring at 100 events if writer is behind. Focus on script/coverage quality (higher priority) | If severely behind: Hire contract writer for event text only ($2K-$4K budget), writer focuses on procedural text | Writer + CLOCK |

---

### 4.3 Medium Risks (Yellow)

| Risk ID | Risk Description | Likelihood | Impact | Mitigation | Contingency | Owner |
|---------|------------------|------------|--------|------------|-------------|-------|
| **R-011** | Godot 4.x engine stability issues (new LTS version, potential bugs) | Low | MEDIUM | Use Godot 4.2+ LTS, avoid bleeding-edge features. Prototype core systems (save/load, UI panels) in Week 1 to validate stability | If critical engine bug: Report to Godot community, implement workaround, or downgrade to 4.1 if necessary | BYTE |
| **R-012** | Switch controller UI adaptation takes longer than budgeted 4 weeks | Medium | LOW | Week 34: Design UI with controller in mind from start (tab order, panel focus). Test with gamepad on PC early | If behind schedule: Delay Switch launch by 30-60 days post-PC, ship PC first | UI Programmer + CLOCK |
| **R-013** | Steam approval delay or rejection | Low | MEDIUM | Week 38: Submit to Steam 2 weeks before target launch. Ensure compliance with Steam guidelines (no offensive content, working DRM) | If rejected: Address feedback, resubmit within 3-5 days, delay launch by 1 week max | CLOCK |
| **R-014** | Press coverage gap, launch sales below projections | Medium | MEDIUM | Week 37: Distribute review keys 2 weeks before launch, target /r/tycoon, /r/BaseBuildingGames, Film Twitter, Letterboxd community | If press silent: Double-down on community engagement, run small influencer campaign ($500-$1K budget), extend launch discount window | CLOCK |
| **R-015** | Late-game content repetition (players notice repeated events/scripts after Film 12) | Low | LOW | Week 24: Playtest 10-film sequence, monitor for repetition. 150 events should support 12-15 films without obvious repeats | If repetition confirmed: Add 30-50 more events post-launch (first patch), communicate as "content expansion" | Writer + CLOCK |

---

## 5. Critical Path Analysis

### 5.1 What's on the Critical Path?

The critical path is the dependency chain that determines the shortest possible project duration. If ANY task on this path is delayed, the entire project is delayed.

**Critical Path (40 weeks)**:

```
Week 1: Project Setup →
Week 2-3: Core Loop Prototype (Greenlight + Talent System) →
Week 4-5: Production Clock + Festival System →
Week 6-7: Integration + Save/Load →
Week 8: M1 Playtest →
Week 9-10: Talent Pool Expansion + All Festivals →
Week 11-12: Revenue System + Studio Progression →
Week 13-14: UI Polish Pass 1 + Audio Foundation →
Week 15-16: M2 Playtest →
Week 17-18: Headshot Photography + Script Library Finalization →
Week 19-20: Crisis Event Expansion + Music Composition →
Week 21-22: Adaptive Audio System + Diegetic Temp Music →
Week 23-24: M3 Playtest →
Week 25-26: Economy Balance + Festival Tuning →
Week 27-28: QA Pass 1 + Performance Optimization →
Week 29-30: Final Polish (UI + Audio) →
Week 31-32: Beta Build + Feedback Integration →
Week 33-34: Steam Integration + Launch Trailer →
Week 35-36: Final Bug Triage + Store Page Live →
Week 37-38: Press Outreach + Final QA Pass →
Week 39-40: Launch Prep → LAUNCH
```

**Tasks NOT on critical path** (can be delayed without impacting launch):
- Switch port (can ship 30-60 days post-PC)
- Stretch features (Rival Studio, Awards Season, Muse dynamics)
- Office seasonal variations
- Secondary SFX (idle loops, Easter eggs)
- Localization (v1.0 is English-only)

---

### 5.2 Dependency Chains

**Chain 1: Procedural Systems** (high dependency)
- Script generation → Coverage phrase library → Greenlight Table UI → Player testing → Quality validation
- **Blocker**: If coverage quality fails in Week 3, this chain breaks. Pivot to authored scripts immediately.

**Chain 2: Talent System** (high dependency)
- Talent data structures → Relationship graph → Talent Web visualization → Negotiation system → Chemistry/Loyalty → Player testing
- **Blocker**: If relationship graph performance is poor (Week 11), reduce talent count or optimize before proceeding.

**Chain 3: Audio Pipeline** (medium dependency)
- SFX recording/sourcing → FMOD integration → Adaptive ambiance system → Audio mixing → Player testing
- **Parallel work**: Audio can proceed in parallel with art/code until Week 21 integration. Not on critical path until Week 29 (final mix).

**Chain 4: Art Assets** (medium dependency)
- Concept mockups → Asset production (headshots, props, backgrounds) → Texture atlases → Integration → Performance testing
- **Parallel work**: Art production (Weeks 17-23) happens in parallel with audio and systems work. Not on critical path until Week 23 (content integration).

---

### 5.3 What Can We Parallelize?

**Weeks 9-16** (M2 phase):
- BYTE: Talent Pool expansion, festivals, revenue system (critical path)
- UI Programmer: Talent Web graph, Ledger UI, seasonal structure (critical path)
- Writer: Event authoring, script templates (parallel, feeds into M3)
- PIXEL: Ledger UI mockups, office asset concepts (parallel, feeds into M3)
- ECHO: Office ambiance bed, placeholder SFX (parallel, feeds into M3)

**Weeks 17-24** (M3 phase):
- BYTE: Integration testing, balance tuning (critical path)
- UI Programmer: UI animation pass, adaptive audio integration (critical path)
- UI Artist: Headshot photography, prop assets, backgrounds (parallel)
- Writer: Script library expansion, crisis event authoring (parallel)
- ECHO: SFX production, music composition, temp music sourcing (parallel)

Maximum parallelization = 5 team members working independently. Risk: Integration bugs when parallel work merges. Mitigate with weekly integration builds and smoke tests.

---

## 6. Scope Management

### 6.1 The Iron Triangle

We have 40 weeks, 7 people, and a fixed core loop. These are LOCKED:

**TIME**: 40 weeks to launch. Not flexible (indie funding burns out, team morale decays beyond 40 weeks).

**TEAM**: 7 people. Not hiring more (budget constraint, onboarding overhead).

**SCOPE**: The only variable. If time or quality is threatened, we cut scope.

---

### 6.2 Feature Tiers

**TIER 1: NON-NEGOTIABLE (Core Loop)**
- Greenlight Table (script generation, coverage, greenlight decision)
- Talent Web (80+ agents, relationships, negotiation)
- Production Clock (15-40 day shoots, crisis events, morale/momentum)
- Avid Bay (editing, editorial approaches, quality calculation)
- Festival Circuit (5 festivals, jury scoring, outcomes)
- Financial Ledger (cash tracking, revenue streams, bankruptcy)
- Save/load system
- PC build (Windows/Mac/Linux)

**If any Tier 1 feature is at risk: STOP. Fix it. Everything else is secondary.**

---

**TIER 2: HIGHLY DESIRABLE (Depth & Polish)**
- 120 talents (fallback: 80)
- 150+ crisis events (fallback: 100)
- 300+ script templates (fallback: 180)
- Adaptive audio system (fallback: static ambiance beds)
- 5 music themes (fallback: 3 themes + royalty-free menu music)
- Accessibility features (colorblind modes, font scaling, audio options)
- Tutorial/onboarding flow
- Switch port

**If Tier 2 is at risk: Evaluate impact. Cut lowest-impact features first (music themes → Switch port → tutorial).**

---

**TIER 3: STRETCH GOALS (Nice-to-Have)**
- Rival Studio system
- Awards Season track
- Muse dynamic (actor/director bonds)
- Comeback casting arc
- Industry Shift Events (Year 5+)
- Office seasonal variations
- Criterion Shelf (trophy collection)
- Director's Chair Mode

**Tier 3 is NOT in the 40-week plan. Do not work on Tier 3 unless Tier 1 and Tier 2 are 100% complete.**

---

### 6.3 Cut List (NOT in v1.0)

These were in the design docs but are CUT from initial release:

1. **Multiplayer / competing studios at launch**: Too complex for v1.0. Single-player simulation must be airtight first.
2. **Real-time filmmaking gameplay** (player controls camera, blocks scenes): This is a producer sim, not a director sim. Scope explosion.
3. **Procedural dialogue trees with talent**: Talent interactions are event-driven with authored text, not open-ended conversation.
4. **Historical real-world actors or films**: All talent and films are fictional (licensing nightmare, creative freedom).
5. **Film-within-a-film playback**: Player never "watches" their films. Films exist as scores, reviews, and audience reactions.
6. **iPad/Mobile port**: Touch UI is a full redesign. Not v1.0.
7. **Localization**: English-only for initial release. Post-launch if successful.

---

### 6.4 Scope Triggers (When to Cut)

**Trigger 1: Milestone Playtest Failure**
- If M1 playtest (Week 8) reveals core loop is not fun, STOP. Do not proceed to M2. Fix core loop or redesign.
- If M2 playtest (Week 16) reveals economy is broken or content is repetitive, extend M2 by 2 weeks to fix. Cut Tier 2 features if needed.
- If M3 playtest (Week 24) reveals audio doesn't communicate game state or UI is confusing, extend M3 by 2 weeks. Cut Tier 3 features permanently.

**Trigger 2: Performance Failure**
- If Week 28 profiling reveals <60fps on min spec, cut in this order:
  1. Reduce Talent Pool from 120 to 80
  2. Reduce headshot texture atlas size (4096 → 2048)
  3. Simplify force-directed graph (static layout instead of real-time)
  4. Reduce crisis event count (150 → 100)

**Trigger 3: Team Velocity Below Target**
- If by Week 16, only 60% of M2 deliverables are complete, cut Tier 2 features:
  1. Reduce script templates (300 → 180)
  2. Reduce crisis events (150 → 100)
  3. Delay Switch port to post-launch
  4. Simplify adaptive audio (static beds instead of dynamic mixing)

**Trigger 4: Budget Overrun**
- If headshot photography costs >$3K, use stock photography exclusively
- If music composition costs >$5K, reduce from 5 themes to 3 + royalty-free menu music
- If voice recording costs >$2K, reduce voice snippet count from 80 to 50

---

## 7. Communication & Reporting

### 7.1 Team Rituals

**Daily Standups** (15 minutes, async via Slack/Discord):
- What did you complete yesterday?
- What are you working on today?
- Any blockers?

**Weekly Team Sync** (60 minutes, video call):
- Milestone progress review (are we on track?)
- Dependency check (is anyone blocked by someone else's work?)
- Risk review (any new risks? any risks escalating?)
- Demo recent work (show, don't tell)

**Bi-Weekly Playtests** (internal, 60-90 minutes):
- Rotate who plays (everyone on team plays the game every 2 weeks)
- Bug triage immediately after playtest
- Feedback logged, prioritized by CLOCK

**Milestone Reviews** (end of each milestone phase):
- Full team retrospective: What went well? What didn't? What do we change?
- External playtest feedback review
- Go/no-go decision for next milestone

---

### 7.2 Reporting Cadence

**To Team (Weekly)**:
- Milestone progress dashboard (% complete, on track / at risk / behind)
- Critical path status (green / yellow / red)
- Open bug count (P0 / P1 / P2 / P3)
- Risk register updates (any risks escalating?)

**To Stakeholders (Monthly, if applicable)**:
- Executive summary (1 page: progress, risks, budget status, next month plan)
- Playtest highlights (what's working, what's not)
- Adjusted launch date (if delays occur)

---

### 7.3 Decision-Making Authority

**CLOCK (Producer)** has final say on:
- Scope cuts (which features to drop)
- Timeline adjustments (delay milestones or cut content)
- Resource allocation (who works on what)
- Risk mitigation strategy

**BYTE (Lead Programmer)** has final say on:
- Technical architecture decisions
- Performance optimization strategy
- Platform feasibility (Switch port go/no-go)

**PIXEL (Art Director)** has final say on:
- Visual identity adherence (color palette, typography, style rules)
- Asset quality bar (what ships, what gets reworked)

**ECHO (Sound Designer)** has final say on:
- Audio mix priorities
- SFX quality bar

**Writer** has final say on:
- Procedural text quality (coverage reports, press quotes)
- Event narrative tone

**Conflicts escalate to CLOCK for final decision.**

---

## 8. Post-Launch Plan (Weeks 41-52)

### 8.1 First 30 Days Post-Launch

**Week 41-42: Launch Week**
- Monitor for critical bugs (crashes, save corruption, soft locks)
- Community management (Discord, subreddit, Steam forums)
- Hotfix patch if needed (P0 bugs only)
- Sales and review tracking

**Week 43-44: Patch 1.1**
- Address P1 bugs from launch week
- Balance tweaks based on player data (if art-path or commerce-path is dominating)
- QOL improvements (based on player feedback)

**Week 45-48: Content Patch 1.2 (Optional)**
- Add 30-50 new crisis events (address late-game repetition)
- Add 20-30 new script templates
- Implement 1-2 stretch features if time/budget allows (Muse dynamic, Comeback casting)

---

### 8.2 Switch Port (if not launched simultaneously)

**Weeks 41-44**: Controller UI adaptation, performance optimization
**Week 45**: Nintendo certification submission
**Week 49-52**: Switch launch (30-60 days post-PC)

---

### 8.3 Post-Launch Metrics to Track

**Sales**:
- Units sold (daily, weekly, monthly)
- Wishlist-to-purchase conversion rate (target: >30%)
- Regional breakdown (is EU or US stronger?)

**Engagement**:
- Average session length (target: 90+ minutes)
- Retention (% of players who play 2+ hours, target: >40%)
- Films completed per player (target: median 5-8 films)

**Reviews**:
- Steam reviews (target: "Very Positive" = 80%+ positive)
- Metacritic/OpenCritic scores (target: 75+)
- Refund rate (target: <10%)

**Community**:
- Discord/subreddit activity
- User-generated content (screenshots, studio stories)
- Bug reports (volume and severity trends)

---

## 9. Success Criteria

### 9.1 What Does Success Look Like?

**Minimum Viable Success (Break-Even)**:
- 5,000 units sold in first 3 months @ $20 = $100K gross revenue
- Steam reviews "Mostly Positive" or better (70%+ positive)
- Core loop is polished and bug-free
- Post-launch support is sustainable (1 patch per month for 3 months)

**Target Success (Profitable)**:
- 15,000 units sold in first 6 months = $300K gross revenue
- Steam reviews "Very Positive" (80%+ positive)
- Community engagement (active Discord, player-generated content)
- Post-launch content roadmap is funded (2-3 major patches over 6 months)

**Aspirational Success (Breakout)**:
- 50,000+ units sold in first year
- Metacritic 80+ (if enough critics review)
- Strong word-of-mouth (Reddit threads, YouTube playthroughs, Twitch streams)
- Sequel or DLC greenlit

---

### 9.2 What Does Failure Look Like?

**Critical Failure (Do Not Ship)**:
- Core loop is not fun after M2 playtest
- Procedural systems feel algorithmic/hollow
- Economy is broken (death spiral or no tension)
- Performance is <30fps on min spec

**If any of these occur, STOP. Redesign or cancel project.**

**Soft Failure (Ship but Underperforms)**:
- <3,000 units sold in first 3 months
- Steam reviews "Mixed" or worse (<60% positive)
- High refund rate (>15%)
- No community engagement (Discord is silent, no UGC)

**If soft failure occurs**: Minimize post-launch support, move team to next project, treat BACKLOT as learning experience.

---

## 10. Closing Notes from CLOCK

This is not a rendering challenge. This is not a physics challenge. This is a systems design and simulation challenge wrapped in a production management skin. The hard part is not making the game run at 60fps — Godot can do that in its sleep. The hard part is making 80-120 agents feel like people, making procedural text feel authored, and balancing a six-axis economy so that both art and commerce are viable strategies.

The technology is straightforward. The risk is in content quality. If coverage reports feel generic, the Greenlight Table fails. If crisis events feel repetitive, the Production Clock fails. If the Talent Web feels like a spreadsheet, the relationship system fails. These are authorship problems, not coding problems.

**What we know**:
- The design is solid. REED's core loop is tight. NOVA's character framework is rich. PIXEL's visual identity is clear. ECHO's audio strategy is emotionally precise. BYTE's technical architecture is pragmatic.
- The team is sized correctly. 7 people for 40 weeks is realistic for this scope.
- The platform is right. PC management sims have an audience. Steam is the distribution channel.

**What we control**:
- Scope. We cut features, not corners. Every cut is strategic, not desperate.
- Quality bar. We ship when it's ready, not when the calendar says so (within reason — 40 weeks is the ceiling).
- Communication. We surface risks early. We playtest often. We iterate based on data, not assumptions.

**What we don't control**:
- Market reception. We make the best game we can and trust the audience to find it.
- Press coverage. We pitch hard, but we can't force coverage.
- Timing. We can't control if a competitor ships a similar game 2 weeks before us.

**The plan is the plan until it isn't.** We will hit obstacles. We will discover bugs. We will get feedback that forces redesign. The milestone gates exist to catch these problems early, when they're fixable. If we hit a gate and the answer is "this isn't working," we stop, fix it, and adjust the plan.

**Scope is the lever.** Time and team are fixed. If we're behind schedule, we cut Tier 2 features. If we're still behind, we cut Tier 3 features. If we're still behind after that, we delay launch by 2-4 weeks maximum and cut nothing else.

**The core loop is sacred.** Greenlight → Cast → Shoot → Edit → Festival → Outcome. If that loop is not polished and compelling, nothing else matters. We can ship with 80 talents instead of 120. We can ship with 100 events instead of 150. We can ship without adaptive audio. But we cannot ship with a broken core loop.

Cut scope, not corners.

Ship something real.

What's the critical path?

---

**Production plan complete. Ready to greenlight.**

**— CLOCK**
