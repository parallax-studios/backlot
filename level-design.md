# BACKLOT — Level Design Document

**Designed by GRID, Level Designer**
**Status: Complete Level Design v1.0**

---

## INTRODUCTION: WHAT IS A LEVEL IN BACKLOT?

Where does the player LOOK in this game? Not at hallways or rooms — at decisions. At a stack of scripts on a desk. At a whiteboard shoot schedule. At a dark theater filling with silhouettes. Backlot is not a spatial game, but it is absolutely a level design game, because every production is a level.

**A level is a complete film production cycle. That is the unit.**

Each production takes the player through five distinct spaces (phases), each with its own pacing, decision density, sightlines, and flow. The player enters Development naive about what this film will become. They exit Release with a finished work and a pile of consequences. That journey — greenlight to premiere — is a 25-30 minute experience that must teach, test, escalate, and resolve.

My job is to make each production feel like moving through a shaped space. Where is the tutorial? Where is the tension spike? Where is the exhale? Where does the player get lost, and how do I breadcrumb them back? These are level design questions. The fact that the level is made of time and choices instead of geometry and collision does not change the discipline.

Let me show you the architecture.

---

## 1. LEVEL STRUCTURE: THE FIVE PHASES

Every production is structured as five sequential rooms. Each room has a purpose, a pacing target, and a designed flow.

### 1.1 PHASE ONE: DEVELOPMENT (The Contemplation Room)

**Level Purpose:** Teach the player what this film could be. Establish stakes. Let the player commit.

**Emotional Beat:** Possibility. The script is raw potential. Every choice feels reversible. Nothing has gone wrong yet.

**Duration:** 3-5 minutes real-time

**Decision Density:** Low (3-5 major decisions)

**Flow:**
```
ENTER: The Greenlight Table
    │
    ├─ Read coverage report ────► Evaluate attributes (tone, ambition, viability)
    │                               │
    │                               ▼
    ├─ Option the script ──────► Budget projection appears
    │                               │
    │                               ▼
    ├─ Commission rewrites? ───► Writer reacts (loyalty shift)
    │                               │
    │                               ▼
    └─ Lock script ─────────────► Script attributes finalized
                                    │
                                    ▼
EXIT: Script locked. Budget set. Pre-production unlocked.
```

**Breadcrumbing Strategy:**
- The coverage report is the breadcrumb. It is written to guide attention: genre and tone establish vibe, Budget Demand creates immediate constraint awareness, Pretension Index (hidden) is the skill-check.
- Visual breadcrumb: The script's physical appearance on the cork board shifts from "INCOMING" pile to "IN DEVELOPMENT" slot. The player sees the commitment happen spatially.
- Audio breadcrumb: The writer reacts to being optioned. If the writer is excited, the player feels validation. If the writer is nervous, tension enters early.

**Pacing Curve:**
```
Tension
   │                              ┌──── (Decision: Commission rewrite or proceed?)
   │                         ┌────┘
   │                    ┌────┘
   │               ┌────┘ (Coverage report read — player evaluates)
   │          ┌────┘
   │     ┌────┘ (Player chooses this script from the pile)
   └─────┘
      Time →
```

Development is the quietest phase. The curve is a gentle climb. No crises, no chaos — just the player and the material. This is intentional. The calm here makes the Production chaos hit harder.

**What This Phase Teaches:**
- How to read coverage reports (literacy in the game's primary information type)
- Budget constraint awareness (if they option a High-budget script with a Micro bank account, they learn immediately)
- Writer personalities matter (rewrite demands reveal character)

**Difficulty Considerations:**
- **Film 1:** The first coverage report is simplified. Only 2-3 scripts available. Budget is subsidized. This is tutorial space — let the player learn the verbs.
- **Film 4+:** The Greenlight Table has 5-8 scripts available. Coverage reports are dense. Pretension Index traps are common. Expert players are reading between the lines.
- **Film 10+:** Scripts arrive with attached talent demands ("I'll option this if you cast my client"). Development becomes negotiation, not just evaluation.

**Playtesting Metrics:**
- Time spent reading coverage reports (target: 45-90 seconds per script)
- Rewrite commission rate (target: 30-50% of players commission at least one rewrite by Film 3)
- Player's stated reason for greenlighting (qualitative — do they articulate a creative vision or just say "it sounded cool"?)

---

### 1.2 PHASE TWO: PRE-PRODUCTION (The Chessboard)

**Level Purpose:** Test strategic thinking. Force the player to build a team within constraints. Show them the Talent Web.

**Emotional Beat:** Anticipation and doubt. The player is assembling the pieces. Every hire is a bet. The shoot feels close but not real yet.

**Duration:** 4-6 minutes real-time

**Decision Density:** Medium-High (8-12 decisions)

**Flow:**
```
ENTER: Casting and crew hiring begins
    │
    ├─ Scout talent ────────► View Talent Web (skills, ego, relationships)
    │                           │
    │                           ▼
    ├─ Negotiate salaries ──► Budget adjusts in real-time
    │                           │
    │                           ▼
    ├─ Lock cast ───────────► Chemistry warnings appear (if any)
    │                           │
    │                           ▼
    ├─ Hire crew (DP, editor, composer) ──► Team assembled
    │                           │
    │                           ▼
    ├─ Lock locations ──────► Location quality set (affects crisis deck)
    │                           │
    │                           ▼
    └─ Set final budget ─────► Budget adequacy calculated
                                │
                                ▼
EXIT: Production begins. The clock starts ticking.
```

**Breadcrumbing Strategy:**
- **Visual breadcrumb:** The Talent Web is a literal web. When the player hovers over a talent, their connections illuminate. Green strings mean "worked together successfully." Red strings mean conflict. The player's eye is drawn to patterns.
- **Numerical breadcrumb:** Agent asks are color-coded. Green = affordable, Yellow = tight but doable, Red = you cannot afford this without cuts elsewhere. The player does not need to do math — the color tells the story.
- **Character breadcrumb:** Ray (the agent) surfaces 3-5 casting suggestions per role. This is a soft guide — the player can ignore it, but it reduces paralysis for new players.

**Pacing Curve:**
```
Tension
   │                                        ┌─── (Final budget set — point of no return)
   │                                   ┌────┘
   │                              ┌────┘ (Location quality locked)
   │                         ┌────┘
   │                    ┌────┘ (Cast assembled — chemistry issues surface)
   │               ┌────┘
   │          ┌────┘ (Salary negotiation — budget pressure felt)
   │     ┌────┘
   └─────┘ (Enter Pre-Production)
      Time →
```

Pre-Production tension escalates steadily. Each decision narrows future options. By the time the player locks the budget, they should feel the weight of commitment — and a flutter of "Did I build this right?"

**What This Phase Teaches:**
- Talent Web navigation (relationships are resources)
- Budget tradeoffs (you cannot afford everyone you want)
- Chemistry dynamics (casting Actor A changes what happens if you cast Actor B)
- Crew importance (the DP affects Production crisis deck, the editor affects Post-Production outcomes)

**Difficulty Considerations:**
- **Film 1:** Pre-built crew suggestions. Only 10-15 talents in the available pool. Chemistry system simplified (no negative modifiers, only positive bonuses).
- **Film 4+:** Full Talent Web active (80-120 talents). Complex chemistry dynamics. Agents play hardball. Rival studios may poach talent mid-negotiation (if Rival Studio feature active).
- **Film 10+:** Legacy hires. Former collaborators have expectations. "You cast me in your first three films and then ghosted me for two years — I'm taking the other offer unless you explain why I should stay."

**Encounter Breakdown:**

| Decision Point | What's At Stake | Player Verb |
|---|---|---|
| **Casting Lead Role** | Performance quality ceiling, salary cost, chemistry with ensemble, ego-driven crisis probability | Evaluate, Negotiate, Commit |
| **Hiring DP** | Cinematography quality floor, production cost, creative friction with director, crisis event type weighting | Evaluate, Hire |
| **Locking Locations** | Visual quality, exterior-driven crisis probability, budget burn | Approve, Reject |
| **Setting Final Budget** | How much cushion exists for overruns, morale baseline (underfunded = low morale start) | Allocate, Finalize |

**Playtesting Metrics:**
- Time spent in Talent Web (target: 2-4 minutes — long enough to explore, short enough not to paralyze)
- Chemistry warnings triggered (target: 20-40% of productions should have at least one chemistry tension)
- Budget adequacy at wrap (target: 60-90% — too low and the player feels punished, too high and there is no tension)
- Use of Agent Recommendation feature (if >70% of players ignore it, the feature is noise; if >90% rely on it entirely, it is doing too much work)

---

### 1.3 PHASE THREE: PRODUCTION (The Pressure Cooker)

**Level Purpose:** Escalate tension. Test reactive decision-making. Force compromise. Break the player's plan.

**Emotional Beat:** Controlled chaos spiraling toward uncontrolled chaos, then (if the player navigates well) a fragile stabilization. This is the boss fight.

**Duration:** 6-10 minutes real-time

**Decision Density:** High (15-40 decisions depending on shoot length)

**Flow:**
```
ENTER: Day 1 of shoot. Momentum = 50. Morale = baseline.
    │
    ├─ Shoot Day 1-5 ──────► Crisis events fire. Player responds.
    │                           │
    │                           ▼
    ├─ Dailies review ─────► Quality trends visible (performance, cinematography)
    │                           │
    │                           ▼
    ├─ Shoot Day 6-15 ─────► Escalation. Momentum drops or climbs based on responses.
    │                           │
    │                           ▼
    ├─ Midpoint crisis ────► Major decision (fire someone? Reshoot? Cut a scene?)
    │                           │
    │                           ▼
    ├─ Shoot Day 16-End ───► Final push. Momentum modifiers amplify.
    │                           │
    │                           ▼
    └─ Wrap ────────────────► Footage pool generated. Morale final state recorded.
                                │
                                ▼
EXIT: Production complete. Exhausted but done. Post-Production unlocked.
```

**Breadcrumbing Strategy:**

This is where breadcrumbing becomes life-or-death. The player is drowning in decisions. Where do they LOOK?

- **Visual breadcrumb:** The whiteboard shooting schedule is the map. Crossed-out days, moved scenes, red-flagged problem sequences. The player's eye should scan it like a general scans a battlefield map.
- **Audio breadcrumb:** Crew chatter shifts in tone. Early days: energetic murmur. Mid-shoot (low Momentum): tense silence, muttered frustration. Late shoot (high Momentum): laughter, the rattle of a productive set. The audio IS the emotional state.
- **Momentum meter:** A visual representation of Momentum (0-100). When it drops below 30, the meter pulses red. When it climbs above 70, it glows gold. This is the player's primary "am I winning or losing?" feedback signal.
- **Crisis event framing:** Every crisis is presented with a clear tradeoff structure. Option A costs X, gains Y. Option B costs Z, gains W. The player should never ask "What does this button do?" — the costs and benefits must be transparent.

**Pacing Curve:**
```
Tension
   │
   │                                  ┌────┐ ┌─ (Breakthrough events possible)
   │                             ┌────┘    └─┘
   │                        ┌────┘ (Midpoint crisis — tension spike)
   │                   ┌────┘
   │              ┌────┘  (Momentum drops — cascading crises begin)
   │         ┌────┘
   │    ┌────┘ (First crisis — player adjusts to reactive pacing)
   └────┘
      Day 1    Day 5    Day 10    Day 15    Day 20    Wrap
```

Production is a sawtooth curve. Crisis, response, brief calm, crisis. The rhythm is designed to create breathing space between decisions while maintaining pressure. Every 5th day is a "quiet day" (zero or one decision) to prevent decision fatigue.

**What This Phase Teaches:**
- Crisis triage (not every crisis needs the expensive solution)
- Momentum management (early decisions compound)
- Talent personality patterns (Method Actors fire specific crisis types; Perfectionists create different problems)
- When to let go (sometimes the director's bad idea is faster than fighting them)

**Difficulty Considerations:**
- **Film 1:** 15-18 shoot days. Crisis frequency: 0.8 per day. No cascading crisis chains. Breakthrough events weighted higher. The player should complete Film 1 Production feeling stressed but successful.
- **Film 4+:** 20-32 shoot days. Crisis frequency: 1.0-1.2 per day. Cascading crises enabled (one unresolved crisis seeds the next). Momentum decay enabled (natural entropy -1 per day). This is the standard Production experience.
- **Film 10+:** 25-40 shoot days. Crisis frequency: 1.2-1.5 per day. Legacy events fire (former collaborators reference past productions, creating callbacks). Weather/location crises are more punishing. The player must be expert-level to navigate cleanly.

**Encounter Breakdown:**

Production encounters are procedurally generated from crisis decks, but they follow design templates:

| Crisis Type | Player Verb | Resource Tradeoff | Narrative Purpose |
|---|---|---|---|
| **Talent Conflict** (Actor vs. Director) | Mediate, Side With Actor, Side With Director | Morale vs. Creative Control | Force the player to choose a relationship to damage |
| **Technical Failure** (Camera breaks, location falls through) | Spend Money, Lose Time, Improvise | Budget vs. Schedule | Test resource management under pressure |
| **Creative Disagreement** (Director wants to reshoot, DP disagrees on coverage) | Allow Reshoot, Deny Reshoot, Compromise | Budget/Time vs. Quality | Reveal what the player values (quality or efficiency?) |
| **Personal Crisis** (Actor's agent calls mid-shoot with competing offer) | Match Offer, Let Them Walk, Negotiate | Budget vs. Loyalty vs. Production Continuity | Test relationship investment |
| **Opportunity** (Great take, magic moment, unexpected chemistry) | Lean Into It (spend time), Capture and Move On | Schedule vs. Quality Ceiling | Reward the player for good casting, create positive spikes |
| **Breakthrough** (Performance transcendence) | None (auto-success) | None | Pure positive feedback. The player FEELS success. |

**Playtesting Metrics:**
- Momentum at wrap (target distribution: 10% <30, 30% 30-50, 40% 50-70, 20% >70)
- Decision time per crisis (target: 15-30 seconds average — fast enough to feel reactive, slow enough to consider)
- Crisis resolution distribution (are players using all three response types, or gravitating to one?)
- Player-reported stress level (qualitative — Production should feel intense but not miserable)
- Quiet day pacing (do players notice and appreciate the breathing room, or does it feel like dead air?)

---

### 1.4 PHASE FOUR: POST-PRODUCTION (The Surgical Suite)

**Level Purpose:** Give the player a moment of creative control after the chaos. Let them shape the raw material. Teach them that editing is storytelling.

**Emotional Beat:** Contemplation with edges of dread. The footage is what it is. The question is: what can we make from it?

**Duration:** 4-6 minutes real-time

**Decision Density:** Low-Medium (4-6 major decisions)

**Flow:**
```
ENTER: Footage review. Scene cards displayed with quality ratings.
    │
    ├─ Review scene cards ──────► Player sees what Production delivered
    │                               │
    │                               ▼
    ├─ Choose editorial approach ──► Performance/Cinematography/Pacing/Emotion/Coherence multipliers apply
    │                               │
    │                               ▼
    ├─ Hire/assign composer ────► Score modifiers calculated
    │                               │
    │                               ▼
    ├─ Color grade ─────────────► Cinematography boost applied
    │                               │
    │                               ▼
    ├─ Rough cut screening ─────► Internal audience reaction (soft preview of festival performance)
    │                               │
    │                               ▼
    └─ Lock final cut ──────────► Film Quality score crystallizes
                                    │
                                    ▼
EXIT: Film complete. Release phase unlocked.
```

**Breadcrumbing Strategy:**
- **Visual breadcrumb:** The Avid Bay timeline. Scene cards arranged sequentially, color-coded by quality axis. Strong performance scenes glow green on the Performance bar. Weak cinematography scenes show red on the Cinematography bar. The player's eye scans for patterns: "I have great performances but weak pacing — I need an editorial approach that boosts pacing."
- **Editorial approach tooltips:** Each approach shows EXACTLY what it does. "Tight & Propulsive: +30% Pacing, -10% Performance, +10% Coherence." Transparency is the breadcrumb. The player should never guess.
- **Editor Voice:** If the player hired a high-Skill editor, the editor offers a suggestion. "This footage wants to breathe. I'd go Slow & Meditative." This is a soft guide, not a mandate. Expert players may override it.
- **Rough cut screening:** Before locking the final cut, the player watches a simulated rough cut screening. The audience reaction (restless, engaged, moved) previews the film's likely performance. If the reaction is weak, the player can revisit the editorial approach. This is a checkpoint before the point of no return.

**Pacing Curve:**
```
Tension
   │
   │                                              ┌─── (Lock final cut — commitment)
   │                                         ┌────┘
   │                                    ┌────┘ (Rough cut screening — preview results)
   │                               ┌────┘
   │                          ┌────┘ (Score and grade applied)
   │                     ┌────┘
   │                ┌────┘ (Editorial approach chosen)
   │           ┌────┘
   └───────────┘ (Footage review — assessment)
      Time →
```

Post-Production starts flat (assessment is low-tension) and builds to a single decision spike: locking the cut. This is the opposite of Production's sawtooth rhythm. It is deliberate — after the chaos, the player needs surgical focus.

**What This Phase Teaches:**
- Editorial approach matching (read the footage strengths, choose the approach that amplifies them)
- Crew skill impact (a great editor can save a troubled production; a weak editor can ruin a smooth shoot)
- The gap between plan and reality (the film you shot is not always the film you imagined)
- Iteration value (the rough cut screening is a chance to adjust before committing)

**Difficulty Considerations:**
- **Film 1:** Only 3 editorial approaches available (Tight & Propulsive, Naturalistic, Editor's Choice). Multiplier effects are simplified. The rough cut screening is always positive or neutral (no harsh feedback yet).
- **Film 4+:** All 6 editorial approaches available. Full multiplier complexity. Rough cut screening can be brutal if the footage is weak. High-Skill editors unlock hidden bonuses (e.g., Nonlinear approach gets +0.3x Coherence if editor Skill > 75).
- **Film 10+:** Editor personality traits emerge. A Perfectionist editor takes longer but adds +5 to final quality. A Fast-and-Loose editor works in half the time but caps quality ceiling. The player must choose crew not just for skill but for workflow fit.

**Encounter Breakdown:**

| Decision Point | What's At Stake | Player Verb |
|---|---|---|
| **Editorial Approach** | Which quality axes are amplified, which are diminished | Evaluate Footage, Choose Approach |
| **Composer Hire** | Emotional Impact and Pacing boost magnitude | Hire, Assign |
| **Color Grade** | Cinematography polish, final visual coherence | Approve, Iterate |
| **Rough Cut Response** | Opportunity to adjust editorial approach or proceed | Assess, Adjust or Lock |

**Playtesting Metrics:**
- Editorial approach diversity (are players using all approaches, or defaulting to one?)
- Rough cut iteration rate (target: 20-40% of players adjust after rough cut screening)
- Editor's Choice usage (if >60% of players delegate to Editor's Choice, the system is too complex; if <10%, the option is not trusted)
- Post-Production satisfaction (qualitative — does this phase feel creative or like a math problem?)

---

### 1.5 PHASE FIVE: RELEASE (The Judgment Hall)

**Level Purpose:** Resolve the production arc. Deliver consequences. Create the emotional payoff (triumph or devastation). Set up the next cycle.

**Emotional Beat:** Anticipation, then catharsis (positive or negative), then reflection. This is the exhale.

**Duration:** 3-5 minutes real-time

**Decision Density:** Low (2-4 major decisions)

**Flow:**
```
ENTER: Film locked. Festival strategy begins.
    │
    ├─ Choose festival ─────────► Sundance, Cannes, TIFF, Venice, Berlin, or Skip
    │                               │
    │                               ▼
    ├─ Set marketing budget ────► $0-$20K allocation (affects Buzz)
    │                               │
    │                               ▼
    ├─ Submit film ─────────────► Jury evaluation (behind curtain)
    │                               │
    │                               ▼
    ├─ PREMIERE SEQUENCE ───────► Darkened theater. Audience meter fills. Press quotes generate.
    │                               │
    │                               ▼
    ├─ Festival outcome ────────► Grand Prize / Jury Prize / Positive / Mixed / Cold / Walkout
    │                               │
    │                               ▼
    ├─ Distribution deals ──────► Offers appear. Player chooses advance vs. split vs. self-distribute.
    │                               │
    │                               ▼
    └─ Revenue & Reputation ────► Ledger updates. Talent loyalty shifts. Studio identity adjusts.
                                    │
                                    ▼
EXIT: Film complete. Return to Studio Overview. Greenlight next project or assess financial health.
```

**Breadcrumbing Strategy:**

Release is about clarity and spectacle. The breadcrumbs are emotional, not informational.

- **Visual breadcrumb:** The festival choice screen shows each festival's Prestige, Distribution Deal Density, and Taste Profile as icons, not text. Sundance = American flag + handshake (prestige + deals). Cannes = Palme d'Or icon + art palette (ultimate prestige + artistic taste). The player reads these at a glance.
- **The Premiere Sequence:** This is the centerpiece. The player sits in a dark theater. The film's title card appears. The audience meter begins to fill — slowly at first, then faster or slower based on the Festival_Score calculation happening behind the curtain. Press quotes scroll: "A remarkable debut." "Overstuffed and undercooked." "The lead performance is a revelation." The player WATCHES their work being judged. This is not a spreadsheet. This is theater.
- **Awards ceremony:** If the film places in the top percentiles, the ceremony plays out. Names are read. The player's film is called (or not). This is the single biggest emotional spike in the entire game. A Grand Prize win should feel like winning an actual award.

**Pacing Curve:**
```
Tension
   │
   │                        ┌──────┐ (AWARDS CEREMONY — peak or valley)
   │                   ┌────┘      └──┐
   │              ┌────┘                └───┐
   │         ┌────┘ (Premiere — audience meter fills)
   │    ┌────┘
   └────┘ (Festival choice — quiet strategic decision)
      Time →
```

The premiere is the spike. Everything before it is setup. Everything after it is denouement. The curve is shaped like a single mountain peak.

**What This Phase Teaches:**
- Festival strategy (matching film attributes to jury taste)
- Marketing spend ROI (is $20K buzz worth it for a borderline film?)
- Distribution deal structures (advance vs. split vs. self-distribution tradeoffs)
- Reputation mechanics (a great film at a mismatched festival underperforms; a good film at the right festival overperforms)

**Difficulty Considerations:**
- **Film 1:** Only Sundance and TIFF accessible. Jury taste profiles simplified. Festival outcome is forgiving (bottom 5% walkout chance is disabled — the player will not experience catastrophic failure on Film 1).
- **Film 4+:** All five festivals accessible. Full jury simulation active. Competition from rival studios (if feature active) affects percentile placement. Walkout risk enabled.
- **Film 10+:** Jury taste trends become readable. The player has 10 films of festival data — they can see patterns. "Cannes has favored slow, meditative films for three years; they are due for a swing." Expert play involves meta-reading the festival circuit.

**Encounter Breakdown:**

| Decision Point | What's At Stake | Player Verb |
|---|---|---|
| **Festival Choice** | Prestige potential, distribution deal likelihood, jury taste fit | Strategize, Choose |
| **Marketing Spend** | Buzz modifier (affects Festival_Score), budget burn | Allocate |
| **Distribution Deal** | Immediate cash vs. long-term revenue, risk vs. safety | Evaluate Offers, Negotiate, Accept |
| **Next Steps** | Greenlight next film or address financial crisis | Assess Studio Health, Decide |

**Playtesting Metrics:**
- Festival diversity (are players using all five festivals, or gravitating to one?)
- Marketing spend distribution (is the $0-$20K range meaningful, or do players always spend max or zero?)
- Distribution deal choice distribution (Advance vs. Split vs. Self should all be viable strategies)
- Premiere sequence emotional impact (qualitative — does the player lean forward during the premiere?)
- Time spent in Studio Review post-release (if players immediately skip to next film, the reflection moment is failing)

---

## 2. META-LEVEL FLOW: THE STUDIO ARC

A single production is a level. But the studio's evolution across 10+ productions is a campaign. Where does the player LOOK across multiple films? What is the pacing curve of a 5-hour session?

### 2.1 The First Five Films (Tutorial Campaign)

The first five productions are not just gameplay — they are an authored learning arc. Each film teaches a new layer.

**Film 1: THE LEARN**
- Purpose: Introduce the pipeline. Let the player complete one full production cycle without catastrophic failure.
- Scaffolding: Simplified Greenlight (2-3 scripts), curated Talent Web (10-15 options), reduced Production crisis frequency, forgiving festival outcome.
- Emotional beat: "I made a film."

**Film 2: THE STRUGGLE**
- Purpose: Remove scaffolding. Let the player fail.
- New elements: Full crisis deck activates. All editorial approaches unlock. Financial pressure begins (Film 1 revenue may not cover Film 2 costs).
- Emotional beat: "This is harder than I thought."

**Film 3: THE WEB**
- Purpose: Reveal the Talent Web's depth. Show the player that relationships are resources.
- New elements: Returning collaborators offer loyalty discounts. A high-Ego talent creates a major Production crisis. Chemistry dynamics become explicit.
- Emotional beat: "People remember how I treated them."

**Film 4: THE SPLIT**
- Purpose: Force the art-vs-commerce decision explicitly.
- New elements: An investor offers funding contingent on making a commercial project. A grant becomes available if the player maintains high Artistic Identity. The player cannot do both.
- Emotional beat: "What kind of studio am I building?"

**Film 5: THE STAKES**
- Purpose: Show the player their legacy. Make them care.
- New elements: A retrospective article generates, summarizing the player's first five films. Former collaborators react to the player's trajectory. A major talent offers to work with the player again — or refuses, citing past treatment.
- Emotional beat: "I am not just making films. I am building something."

### 2.2 Pacing Across a Session (60-90 Minutes)

A session typically contains 2-3 productions. The pacing must account for fatigue and variety.

**Recommended session structure:**

```
FILM A (Full production cycle) ──► 25-30 minutes ──► High intensity (Production phase)
    │
    ▼
STUDIO REVIEW ──► 2-3 minutes ──► Low intensity (assessment, breathing room)
    │
    ▼
FILM B (Full production cycle) ──► 25-30 minutes ──► High intensity
    │
    ▼
STUDIO REVIEW ──► 2-3 minutes ──► Low intensity
    │
    ▼
(Optional) FILM C (Development only) ──► 5 minutes ──► Low intensity (setup for next session)
    │
    ▼
SAVE POINT
```

The Studio Review is the critical decompression space. If the player goes Film A → Film B → Film C without reflection, fatigue sets in. The review is not just information — it is pacing.

### 2.3 Difficulty Curve Across 10+ Films

The game's difficulty is not linear. It is stepped, with escalating pressure.

```
Difficulty
    │
    │                                          ┌────── (Legacy Pressure)
    │                                     ┌────┘       Films 10+
    │                                ┌────┘
    │                           ┌────┘   (Ambition vs. Survival)
    │                      ┌────┘        Films 4-8
    │                 ┌────┘
    │            ┌────┘   (Learning Curve)
    │       ┌────┘        Films 1-3
    │  ┌────┘
    └──┘
      1    2    3    4    5    6    7    8    9   10+
```

**Films 1-3:** Learning the systems. Difficulty is mechanical literacy.

**Films 4-8:** Mastering the systems. Difficulty is resource scarcity and strategic planning.

**Films 9+:** Living with consequences. Difficulty is reputational — every choice is weighted by history.

---

## 3. SPATIAL DESIGN: THE OFFICE AS LEVEL

The office is not a playable space in the traditional sense — the player does not walk through it. But it is the persistent hub, and its visual design is level design.

### 3.1 The Office as Emotional Mirror

The office evolves based on the player's success and choices. This is environmental storytelling that doubles as progression feedback.

**Early-Game Office (Films 1-3):**
- Converted loft. Exposed brick. Mismatched furniture.
- Cork board: INCOMING pile (thick), IN DEVELOPMENT (one script), COMPLETED (empty or one film).
- Whiteboard: Current shoot schedule.
- Poster: A Jarmusch or early Soderbergh film (aspirational reference).
- Desk: Cold coffee, stacks of headshots, a ringing landline.
- **What the player FEELS:** Scrappy possibility. "We are building something."

**Mid-Game Office (Films 4-8, Reputation 40-59):**
- Same space, professionalized. Better furniture. A real conference table.
- Cork board: INCOMING pile (thicker — more submissions), IN DEVELOPMENT (2-3 scripts overlapping), COMPLETED (3-5 framed one-sheets).
- Desk: Laptop replaces some paper. Coffee machine instead of single mug.
- Awards shelf: Festival laurels (if any).
- **What the player FEELS:** "We have become a business. Is that good?"

**Late-Game Office (Films 9+, Reputation 60+):**
- Expanded space or renovated loft. The office looks like a place where successful work happens.
- Cork board: INCOMING pile (huge — the industry knows your name), COMPLETED wall (gallery of one-sheets).
- Framed press: Retrospective articles, profiles.
- Talent Web: Expanded, with gold strings (Muse bonds) visible.
- **What the player FEELS:** "This is my legacy. But who am I now?"

**Critical Design Rule:** The office should NEVER feel corporate. Even at maximum success, it should feel like a place where people who care too much about work are doing that work. The moment it feels like a generic office, the game's soul is lost.

### 3.2 The Backlot as Visual Heartbeat

Visible through the office window. The backlot shows production activity.

**During Production Phase:** Bustle. Camera on dolly. Crew in motion. Lights being rigged. The player's eye is drawn to the window — visual confirmation that the shoot is happening.

**Between Productions:** Empty. A half-struck set. Quiet. The absence should feel like potential (if the player is financially healthy) or like failure (if the player is in crisis).

**After a Major Success:** The backlot upgrades. Better equipment. More crew. A sense of permanence. The player SEES their success reflected spatially.

---

## 4. BREADCRUMBING PHILOSOPHY

In a decision-heavy game, breadcrumbing is not about showing the player where to go. It is about showing the player where to LOOK.

### 4.1 Visual Breadcrumbs

**Color-coding:**
- Green = safe, affordable, positive
- Yellow = caution, tight, neutral
- Red = danger, unaffordable, negative
- Gold = opportunity, reward, breakthrough

Example: In Pre-Production, salary asks are color-coded. The player's eye scans for green (affordable) and avoids red (unaffordable). They do not need to read every number — the color is the breadcrumb.

**Spatial hierarchy:**
- Important information is larger, centered, or elevated.
- Secondary information is smaller, peripheral.
- The player's eye should land on the most important decision point first.

Example: In the Greenlight Table, the script title and genre are large. Budget Demand is color-coded and prominent. The full coverage report is collapsible — the player can dig deeper if they want, but the top-level info guides the first pass.

**Animation as emphasis:**
- When a stat changes, it animates briefly. A salary negotiation drops the budget number, and the number flashes yellow. The player's eye is drawn to the consequence.

### 4.2 Audio Breadcrumbs

**Diegetic soundscape:**
- The office hum: phones ringing, keyboard clatter, muffled conversation in the next room.
- During Production: the soundscape shifts. On-set chatter. The clack of a clapperboard. When Momentum is high, laughter. When Momentum is low, tense silence.
- During Release: the theater ambience. The murmur of a crowd before a premiere. The shift to silence as the film starts.

**Audio cues for state changes:**
- Budget drops below $50K: a subtle tension drone begins.
- Momentum drops below 30: the office soundscape mutes slightly, becomes more oppressive.
- A festival win: a swell of applause (diegetic — from the awards ceremony).

Audio tells the player how to FEEL, which guides where to focus attention.

### 4.3 Character Voice as Breadcrumb

Characters offer guidance, but never mandatory direction.

**Ray (Agent):** "My client loves the script. Here's the ask: $45K. But there's flexibility if you've worked together before."
- The breadcrumb: Relationship history affects cost. The player is nudged to check Talent Web loyalty scores.

**June (Producer):** "Your director wants to shoot on 16mm. That's a 20% budget bump. You have $180K total. I love texture. I also love making payroll."
- The breadcrumb: Budget math embedded in character voice. The player does not need a calculator — June did the math for them.

**Elena (Director, during Production crisis):** "I need twenty more minutes on this set. The wide shot has a compositional problem."
- The breadcrumb: This is a time-vs-quality tradeoff. The player understands the stakes from Elena's framing.

Character voice should never TELL the player what to do. It should FRAME the decision so the player can see the tradeoffs clearly.

---

## 5. DIFFICULTY TUNING

Difficulty in Backlot is not about making the game harder. It is about calibrating challenge to player skill growth.

### 5.1 Difficulty Knobs

The game has several systemic difficulty levers that adjust dynamically or per-film:

| Lever | Low Difficulty (Film 1) | Standard Difficulty (Film 4+) | High Difficulty (Film 10+) |
|---|---|---|---|
| **Crisis Frequency** | 0.8 per shoot day | 1.0-1.2 per shoot day | 1.2-1.5 per shoot day |
| **Talent Web Size** | 10-15 available | 60-100 available | 80-120 available, with poaching |
| **Budget Cushion** | +30% seed funding | Standard seed funding | No subsidy, rising costs |
| **Festival Forgiveness** | Walkout disabled | Full outcomes enabled | Jury trends, rival competition |
| **Talent Ego Impact** | Low ego crises rare | Standard ego mechanics | High ego + legacy expectations |

### 5.2 Adaptive Difficulty (Optional Design)

If playtesting reveals that fixed difficulty is too punishing or too easy:

**Soft Rubber-Banding:**
- If the player fails two consecutive films (negative revenue both times), the next script pool includes one "safe bet" script (high Commercial Viability, medium-high Base Quality, low risk).
- If the player succeeds on three consecutive films with Reputation gains, the next Talent Web includes one high-Ego, high-Skill talent who demands creative control (a designed challenge).

**Mentorship Events (First Crisis Only):**
- On the player's first financial crisis, June offers a bridge loan and advice. This is a one-time safety net.
- On the player's first festival walkout, Tomasz (festival programmer) sends a private note: "This happens. The question is what you make next." This is emotional support, not mechanical, but it prevents demoralization.

---

## 6. PLAYTESTING PRIORITIES

Level design is theory until it meets players. Here is what I need to know.

### 6.1 Phase-Level Metrics

| Phase | Key Question | Success Metric |
|---|---|---|
| **Development** | Do coverage reports engage? | 8/10 players spend >30 sec reading each report |
| **Pre-Production** | Is Talent Web navigable? | 7/10 players use relationship data by Film 3 |
| **Production** | Is crisis pacing sustainable? | Player engagement does not drop below baseline after Day 15 |
| **Post-Production** | Does editorial choice feel creative? | Players spend >90 sec considering approach (not defaulting) |
| **Release** | Does the premiere deliver catharsis? | Qualitative: players react visibly (lean forward, audible response) |

### 6.2 Meta-Level Metrics

| Scope | Key Question | Success Metric |
|---|---|---|
| **Single Production** | Does the 25-30 min arc feel complete? | 8/10 players reach Release without fatigue complaints |
| **Session (2-3 Films)** | Is the 60-90 min pacing sustainable? | Players report wanting to continue after session end |
| **Campaign (10 Films)** | Does difficulty scale meaningfully? | Film 10 feels harder than Film 5, but not unfairly |

### 6.3 Qualitative Observation Points

**Watch for:**
- **Where do players get stuck?** If >50% of players stall in Pre-Production, the Talent Web is too dense. If they stall in Post-Production, editorial approach clarity is failing.
- **Where do players look?** Eye-tracking or screen recording reveals whether visual breadcrumbs are working. If the player's gaze wanders during a crisis event, the framing is unclear.
- **Where do players feel?** The premiere sequence, the first festival win, the first walkout — these should produce visible emotional reactions. If they do not, the level design has failed to create stakes.

---

## 7. OPEN QUESTIONS FOR PLAYTESTING

I cannot answer these from the design doc. I need players.

**Production Clock Granularity:**
- Day-by-day creates 15-40 decisions per production. Does this feel tense or tedious by Day 20? If tedious, compress to week-by-week (5-8 decision points per production). Test both.

**Talent Web Density:**
- At what size does the Web shift from "rich ecosystem" to "paralysis spreadsheet"? My instinct: 80 is the floor, 100 is the sweet spot, 120 requires better UI filtering. Test at 60, 80, 100, 120.

**Studio Review Pacing:**
- Is 2-3 minutes enough breathing room between productions? Or does it feel like a speed bump? Test with and without forced review screens.

**Office Evolution Visibility:**
- Do players NOTICE the office changes? Or is the hub background noise? If >50% of players do not comment on office upgrades, the environmental storytelling is invisible.

**Premiere Sequence Impact:**
- Does the premiere deliver the emotional spike the game is built around? Film the playtest. Watch the player's face during the premiere. If they are checking their phone, the sequence is broken.

**Late-Game Repetition:**
- Does Film 12 feel meaningfully different from Film 6? Or is it just bigger numbers? Test legacy events, industry shifts, and Muse dynamics. If none of these inject freshness, the game has a content ceiling.

**Art vs. Commerce Balance:**
- Over 50 playthroughs, do art-path and commerce-path studios survive to Film 10 at equal rates? If one path dominates by >20%, the economy is unbalanced.

---

## 8. LEVEL DESIGN PRINCIPLES FOR BACKLOT

These are the rules I follow when tuning any phase, encounter, or decision.

**PRINCIPLE 1: Every room has a purpose.**
Development teaches. Pre-Production tests strategy. Production tests reaction. Post-Production tests creativity. Release delivers consequences. No phase exists just to exist.

**PRINCIPLE 2: Pacing is king.**
Tension, release, tension, release. Never flat. Never all peaks. Production is sawtooth. Post-Production is a slow climb. Release is a single mountain. The rhythm must vary.

**PRINCIPLE 3: Breadcrumbs, not rails.**
The player should always know where to LOOK, but never be told where to GO. Show the tradeoff clearly, then step back.

**PRINCIPLE 4: Feedback is immediate and visible.**
When the player makes a decision, something changes on screen within 2 seconds. A number shifts. A character reacts. The whiteboard updates. Invisible consequences are not consequences.

**PRINCIPLE 5: The space tells the story.**
The office is the player's studio. The backlot is their production. The theater is their judgment. Every space has emotional meaning. None are generic.

**PRINCIPLE 6: Respect the player's time.**
If a decision can be automated without loss of meaning, automate it. The player should only make decisions that MATTER. Everything else is noise.

**PRINCIPLE 7: Failure is a teacher, not a punishment.**
A walkout at Sundance is not a game over. It is a story beat. The player should feel the sting, learn from it, and be given the tools to recover. Punitive failure is lazy design.

**PRINCIPLE 8: Late-game depth comes from memory.**
By Film 10, the player has a history. Characters remember. The Talent Web remembers. The player's choices echo. The depth is not in new mechanics — it is in the weight of accumulated decisions.

---

## CONCLUSION: THE LEVEL IS THE FILM

Where does the player LOOK in Backlot? At a desk covered in scripts. At a Talent Web connecting people who hate each other. At a whiteboard schedule falling apart in real time. At a dark theater filling with strangers. At a one-sheet on the wall that represents 30 minutes of their life and a piece of their studio's soul.

Every production is a level. Every level is a story. And the campaign — the studio's rise, plateau, or collapse across 10+ films — is the player's masterpiece.

The space is not geometry. It is time, decisions, relationships, and consequences. But the design principles are the same. Pacing. Flow. Breadcrumbing. Difficulty curves. Encounter design. Emotional beats.

I see the world in sightlines, chokepoints, and flow paths. In Backlot, the sightline is a coverage report. The chokepoint is a Production crisis. The flow path is Development → Pre-Production → Production → Post-Production → Release. And the player's eyes, attention, and heart follow that path because I built it to guide them.

If they lean forward during the premiere, we have a level.

If they do not, we go back to the whiteboard.

**-- GRID**
