# BACKLOT — Game Design Document

**Designed by REED**
**Status: Complete GDD v1.0**

---

## 1. Player Fantasy Statement

> "I am the person who decides which films get made. I discover raw scripts, wrangle brilliant and volatile artists, survive chaotic shoots, and present my work to the world — always balancing the film I believe in against the money I need to survive. Every movie I greenlight is a bet on what matters."

That is the fantasy. Not "I make movies." Not "I run a business." The fantasy is the tension between those two things, held in the player's hands every single second. The player wants to feel like an indie film producer in the mid-2000s: scrappy, passionate, perpetually broke, surrounded by talented people who might be geniuses or might be disasters, and one Sundance premiere away from either vindication or ruin.

What is the core emotion? **Agonizing conviction.** The feeling of looking at a script about a deaf saxophonist in Reno and thinking, "This is either the best thing I've ever read or the most self-indulgent garbage on my desk — and I'm going to bet $400,000 to find out." That is the moment. That is the hook. If the player does not feel that pull in the first ten minutes, we have failed.

---

## 2. Core Loop

### 2.1 The 30-Second Loop: Decide

The atomic unit of gameplay is a decision. Every 30 seconds, the player is reading a piece of incoming material — a script coverage report, a casting headshot with attached demands, a budget line item, a crisis event on set, a festival invitation — and making a binary or ternary choice. Approve or reject. Actor A or Actor B. Spend more or cut the scene. Submit to Sundance or hold for Cannes.

Each decision modifies at least two of the game's six core resource axes:

| Resource Axis | Range | What It Represents |
|---|---|---|
| **Budget** | $0 — Studio Max | Cash on hand for current production |
| **Film Quality** | 0 — 100 | Composite score of the current film |
| **Morale** | 0 — 100 | Average crew/cast willingness to push |
| **Reputation** | 0 — 100 | Industry perception of the studio |
| **Talent Loyalty** | -50 to +50 per person | Individual relationship score with each talent |
| **Artistic Identity** | Spectrum: Commercial <-> Auteur | Where the studio sits on the art-commerce axis |

The 30-second loop is: **Receive information. Evaluate tradeoffs. Commit.** The player should never be idle. If they are, the pacing is broken.

### 2.2 The 5-Minute Loop: Produce

Every 5 minutes, the player moves through one major phase of a production. There are five phases per film:

1. **Development** (~5 min): Select a script, commission rewrites, shape the material
2. **Pre-Production** (~5 min): Cast talent, hire crew, lock locations, set budget
3. **Production** (~8 min): Manage the shoot day-by-day, handle crises, make creative calls
4. **Post-Production** (~5 min): Edit the cut, choose score and grade, finalize the film
5. **Release** (~4 min): Choose festival strategy, negotiate distribution, collect results

Total production cycle: approximately 25-30 minutes. This means the player completes roughly 2 films per hour of play. Each phase has its own rhythm, its own decision density, and its own failure modes. Development is contemplative. Pre-Production is strategic. Production is reactive and high-pressure. Post-Production is surgical. Release is the exhale — the moment where the player watches the consequences land.

### 2.3 The Meta Loop: Build the Studio

Across sessions (60-90 minutes each), the player is building a studio identity film by film. Each completed production permanently modifies the studio's:

- **Financial position** (profit or loss flows into the next project)
- **Reputation score** (critical and commercial reception shifts how the industry sees you)
- **Talent relationships** (who will work with you again, who will not)
- **Artistic Identity axis** (your slate defines your brand)
- **Available opportunities** (better scripts, bigger talent, more festivals open up as reputation grows)

The meta question shifts over time:
- **Films 1-3**: "Can I survive?" (financial pressure dominates)
- **Films 4-8**: "Can I thrive?" (creative ambition vs. commercial safety)
- **Films 9+**: "What have I built?" (legacy, identity, creative ecosystem)

### 2.4 Core Loop Diagram

```
                        ┌─────────────────────────────────────────────┐
                        │            THE META LOOP (Session)          │
                        │  Studio Identity evolves film by film       │
                        │  Reputation + Finances + Talent Pool grow   │
                        │                                             │
                        │   ┌─────────────────────────────────────┐   │
                        │   │      THE 5-MINUTE LOOP (Phase)      │   │
                        │   │                                     │   │
                        │   │  DEVELOPMENT ──► PRE-PRODUCTION     │   │
                        │   │       │               │             │   │
                        │   │       ▼               ▼             │   │
                        │   │   [Script]       [Cast + Crew]      │   │
                        │   │       │               │             │   │
                        │   │       └───────┬───────┘             │   │
                        │   │               ▼                     │   │
                        │   │         PRODUCTION                  │   │
                        │   │         (The Pressure Cooker)       │   │
                        │   │               │                     │   │
                        │   │               ▼                     │   │
                        │   │       POST-PRODUCTION               │   │
                        │   │         (The Avid Bay)              │   │
                        │   │               │                     │   │
                        │   │               ▼                     │   │
                        │   │           RELEASE                   │   │
                        │   │      (Festival + Distribution)      │   │
                        │   │               │                     │   │
                        │   └───────────────│─────────────────────┘   │
                        │                   ▼                         │
                        │          ┌─────────────────┐                │
                        │          │    OUTCOMES      │                │
                        │          │  Revenue         │                │
                        │          │  Awards          │                │
                        │          │  Reputation ±    │                │
                        │          │  Talent shifts   │                │
                        │          └────────┬────────┘                │
                        │                   │                         │
                        │                   ▼                         │
                        │          GREENLIGHT NEXT FILM               │
                        │          (Back to Development)              │
                        └─────────────────────────────────────────────┘

  ┌──────────────────────────────────────────────────────────────────┐
  │              THE 30-SECOND LOOP (Decision)                       │
  │                                                                  │
  │   INFORMATION ──► EVALUATE TRADEOFFS ──► COMMIT ──► FEEDBACK    │
  │   (script, crisis,    (2+ resource        (choice     (numbers   │
  │    headshot, offer)    axes at stake)      is final)   shift,    │
  │                                                       talent     │
  │                                                       reacts)    │
  └──────────────────────────────────────────────────────────────────┘
```

---

## 3. Core Mechanics

### 3.1 The Greenlight Table

**Player verb**: READ, EVALUATE, GREENLIGHT

**System description**: The Greenlight Table is the player's primary decision space and the entry point for every production. Scripts arrive through four channels:

| Source | Frequency | Quality Range | Cost |
|---|---|---|---|
| **Writer Pool** (internal writers) | 1-2 per season | Medium-High | Writer salary (already paid) |
| **Cold Submissions** | 3-5 per season | Low-High (high variance) | Option fee: $2K-$10K |
| **Agent Pitches** | 1-2 per season | Medium-High | Option fee: $10K-$50K + attached talent demands |
| **Development Slate** (player commissions) | Player-initiated | Variable (depends on writer + brief) | Writer fee: $15K-$80K |

Each script is procedurally generated with the following attributes (all on 1-100 scales unless noted):

| Attribute | What It Measures | Visible to Player? |
|---|---|---|
| **Genre** | Category (drama, comedy, thriller, horror, doc-hybrid, experimental) | Yes |
| **Tone** | Spectrum from light to heavy (1-100) | Yes (via coverage report language) |
| **Structural Ambition** | How unconventional the narrative structure is (1-100) | Yes |
| **Thematic Depth** | How substantive the themes are (1-100) | Partially (coverage hints at it) |
| **Commercial Viability** | How marketable the concept is (1-100) | Yes |
| **Pretension Index** | Gap between what the script thinks it is and what it is. Formula: `abs(Self_Assessment - Actual_Quality)` | Hidden (player must learn to read it) |
| **Base Quality** | Raw screenplay quality before production modifiers (1-100) | Hidden (estimated via coverage) |
| **Budget Demand** | How much the script needs to be produced well. (Categorical: Micro $50K-$150K / Low $150K-$500K / Mid $500K-$1.5M / High $1.5M-$3M) | Yes |

Coverage reports are procedurally authored text blocks that communicate these attributes through voice, not numbers. A script with Structural Ambition 85 and Commercial Viability 30 might read: "A three-timeline structure built around a woman dismantling her marriage in reverse chronological order. Challenging. Requires a director who trusts the audience. This does not have a wide theatrical play but could be a festival cornerstone if executed precisely."

The Greenlight decision is irreversible per season. The player can develop up to 3 scripts per in-game year but can only greenlight 3 into full production (one per four-month production window). Greenlighting a script commits the studio's resources and locks in downstream consequences.

**Feedback**: When a script is greenlit, the cork board updates — the script moves from the "INCOMING" pile to the "IN DEVELOPMENT" board. The writer reacts (grateful, nervous, demanding). Budget projections appear. The studio's upcoming slate shifts visually. The player feels the weight of commitment.

**Depth**: Mastery of the Greenlight Table means learning to read the Pretension Index without seeing it. A beginner greenlights the script that sounds coolest. An expert knows that a script with Structural Ambition 90 and Base Quality 45 is a trap — it is a writer who wants to be Charlie Kaufman but lacks the skill. The expert also knows that a genre script with Commercial Viability 75 and Thematic Depth 60 is the ideal "fund the slate" project. At hour 50, the player is reading coverage reports the way a real producer does — between the lines.

### 3.2 The Talent Web

**Player verb**: SCOUT, NEGOTIATE, MANAGE

**System description**: The Talent Web is a persistent, living network of 80-120 simulated creative professionals (the sweet spot from design question testing; see Section 6). Each talent is defined by:

**Core stats (1-100 scale)**:

| Stat | Applies To | What It Means |
|---|---|---|
| **Skill** | All | Raw ability in their craft |
| **Range** | Actors, Directors | Versatility across genres/tones |
| **Vision** | Directors, Writers | Strength of personal creative voice |
| **Reliability** | All | Likelihood of showing up, staying sober, meeting deadlines |
| **Ego** | All | Self-regard. High ego demands more: higher salary, more creative control, better billing |
| **Ambition** | All | Drive to advance career. High ambition means they leave for bigger studios faster |
| **Chemistry Modifier** | Actors | Per-pair compatibility score with other actors. Range: -30 to +30. Stacks with skill for performance quality |

**Personality traits** (each talent has 2-3 from a pool of 20):
Examples: Method Actor, People Pleaser, Control Freak, Night Owl, Perfectionist, Hard Drinker, Mentor, Diva, Workhorse, Recluse, Scene Stealer, Loyal, Mercenary, Temperamental, Visionary, By-the-Book, Improviser, Political, Confrontational, Quiet Professional.

Traits generate events during Production and modify interactions:
- A **Method Actor** with Ego > 70 will refuse direction changes mid-shoot (crisis event probability: 40% per production)
- A **Perfectionist** DP paired with a **Night Owl** Director increases overtime costs by 15% but boosts Cinematography quality by +8
- A **Loyal** actor who has worked with you twice before takes a 20% salary cut on the third project

**Relationship system**: Every talent has a relationship score with the studio (-50 to +50) and with every other talent they have worked with (-50 to +50). Relationship scores shift based on:

| Event | Studio Relationship Change | Inter-Talent Relationship Change |
|---|---|---|
| Successful collaboration | +5 to +15 | +3 to +10 |
| Failed/troubled production | -5 to -20 | -5 to -15 |
| Oscar/Palme d'Or nomination | +10 to studio | +5 between collaborators |
| Fired from production | -30 to studio | N/A |
| Contract honored cleanly | +3 | N/A |
| Contract disputes | -10 to -25 | N/A |
| Talent poached by rival | -15 to studio | N/A |

**Negotiation system**: Casting an actor requires negotiation with their agent. The agent's ask is based on:

```
Base Ask = (Skill * 500) + (Ego * 200) + (Recent_Success_Modifier)
Negotiation Range = Base Ask * 0.7 to Base Ask * 1.3
Studio Relationship Discount = Relationship_Score * 0.5% (so +50 relationship = 25% discount)
```

Example: An actor with Skill 72, Ego 55, no recent success modifier, and +20 studio relationship:
- Base Ask: (72 * 500) + (55 * 200) = $36,000 + $11,000 = $47,000
- Range: $32,900 to $61,100
- Relationship discount: 20 * 0.5% = 10%
- Likely deal: ~$42,300

The player does not see these formulas. They see the agent say "Mara's asking sixty but she likes what you did with the Delaney script, so there's some flexibility." The system is under the hood. The player learns the patterns.

**Feedback**: The Talent Web is visualized as a literal web — a network graph on a cork board with headshots as nodes and colored strings as connections. Red strings mean conflict. Green strings mean strong collaboration. Gold strings mean "will work together again for less money." When the player hovers over a talent, their stats bloom outward and their connection strings illuminate. When casting is finalized, the web reorganizes to show the production's team clustered together, and any tensions flash red briefly.

**Depth**: At hour 20, the player is casting for skill. At hour 50, they are casting for chemistry, reliability, and relationship leverage. At hour 100, they are thinking three films ahead: "If I cast Mara now and she has a good experience, she'll do the Alejandro script next year for scale, and that's the one that could win Cannes." The Talent Web rewards long-term social thinking. It turns casting from an optimization problem into a strategic relationship game.

### 3.3 The Production Clock

**Player verb**: MANAGE, RESPOND, SACRIFICE

**System description**: Once cameras roll, the game enters its most reactive phase. A production runs for 15-40 shoot days depending on budget tier:

| Budget Tier | Shoot Days | Crisis Events per Day | Decisions per Day |
|---|---|---|---|
| Micro ($50K-$150K) | 15-18 | 0.8 | 1-2 |
| Low ($150K-$500K) | 20-25 | 1.0 | 2-3 |
| Mid ($500K-$1.5M) | 25-32 | 1.2 | 2-4 |
| High ($1.5M-$3M) | 32-40 | 1.5 | 3-5 |

Each day, the player sees a brief dailies report (how footage quality is trending) and faces 1-3 decision events drawn from a weighted crisis deck. The deck is seeded at the start of production based on cast traits, crew traits, script complexity, location quality, and budget adequacy.

**Crisis event categories and weights**:

| Category | Base Weight | Modified By |
|---|---|---|
| **Talent conflict** | 15% | +2% per point of Ego above 60 for any cast member |
| **Technical failure** | 10% | +3% if budget adequacy < 70% |
| **Weather/location** | 10% | +5% for exterior-heavy scripts |
| **Creative disagreement** | 20% | +3% per point of Director Vision above 70 |
| **Budget overrun** | 15% | +2% per day over schedule |
| **Personal crisis** | 10% | +4% if any talent Reliability < 40 |
| **Opportunity** (positive event) | 15% | +3% if Morale > 70 |
| **Breakthrough** (great take, magic moment) | 5% | +2% if actor Chemistry Modifier > 15 |

Each crisis presents 2-3 response options that trade resources against each other:

**Example crisis**: "Day 12. Your lead actor and director are not speaking after yesterday's take dispute. The actor wants to improvise the confession scene. The director insists on the scripted version."

| Option | Cost | Benefit |
|---|---|---|
| Side with the actor | Director Morale -15, Director Loyalty -10 | Performance Quality +5 (if actor Skill > 65) or -5 (if < 65) |
| Side with the director | Actor Morale -15, Actor Loyalty -10 | Coherence +5 (script is maintained) |
| Call a meeting, split the difference | Half day lost ($Budget * 0.03), both Morale -5 | Relationship preserved, shoot two versions (+2 coverage options in Avid Bay) |

The Production Clock also tracks a hidden **Momentum** value (0-100) that represents how the shoot feels as a whole. Momentum starts at 50 and shifts based on daily outcomes:

```
Momentum += (positive_events * 3) - (negative_events * 4) + (morale_average * 0.1) - 1
```

The `-1` represents natural entropy: shoots lose momentum if nothing actively sustains them. High Momentum (>70) grants +5% chance of Breakthrough events. Low Momentum (<30) grants +10% chance of cascading crises.

**Feedback**: The production office transforms during this phase. The whiteboard shooting schedule updates in real time — crossed-out days, moved scenes, emergency additions. Dailies play as brief montages (scene cards with quality ratings appearing). The player hears crew chatter shifting in tone. When Momentum drops below 30, the office lights feel dimmer. When it rises above 70, there is an audible energy — laughter in the background, the rattle of a productive set.

**Depth**: A beginner survives production by reacting to each crisis independently. An expert front-loads difficult scenes (exteriors, emotional peaks, scenes with temperamental actors) into the first week when Morale is high and Momentum is neutral. They keep a contingency budget of 15-20% for overruns. They know that siding with the director early builds trust that pays off when they need to override the director later. They use the third option ("shoot two versions") strategically — not to avoid conflict, but to give themselves editorial options in the Avid Bay.

### 3.4 The Avid Bay (Post-Production)

**Player verb**: SHAPE, CUT, REFINE

**System description**: Production generates a pool of scene cards. Each card has quality ratings across five axes:

| Axis | What It Measures | Generated From |
|---|---|---|
| **Performance** | Acting quality | Actor Skill + Chemistry + Director guidance |
| **Cinematography** | Visual quality | DP Skill + Budget adequacy + Location quality |
| **Pacing** | Scene rhythm and momentum | Script Structure + Director Vision + Number of takes |
| **Emotional Impact** | How the scene hits | Performance + Script Thematic Depth + Music (added in post) |
| **Coherence** | How well the scene fits the whole | Script Structure + Editorial approach + Whether production deviated from the script |

The player has 8-15 scene cards per film depending on script complexity. The editor (a Talent Web character with their own Skill stat) assembles them into a cut. The player chooses an **Editorial Approach**:

| Approach | Performance Mult. | Cinematography Mult. | Pacing Mult. | Emotional Impact Mult. | Coherence Mult. |
|---|---|---|---|---|---|
| **Tight & Propulsive** | 0.9x | 0.9x | 1.3x | 0.9x | 1.1x |
| **Slow & Meditative** | 1.1x | 1.2x | 0.7x | 1.2x | 1.0x |
| **Nonlinear** | 1.0x | 1.0x | 0.8x | 1.1x | 0.7x (+0.3x if editor Skill > 75) |
| **Montage-Heavy** | 0.8x | 1.3x | 1.1x | 1.0x | 0.8x |
| **Naturalistic** | 1.3x | 0.9x | 1.0x | 1.1x | 1.0x |
| **Editor's Choice** (delegate) | Uses editor's Vision stat to auto-select best approach | | | | |

After the editorial approach, two additional layers are applied:

**Score** (from a Composer talent):
```
Score_Modifier = Composer_Skill * 0.15
Applied to: Emotional Impact (+Score_Modifier), Pacing (+Score_Modifier * 0.5)
```

**Color Grade** (from the DP or a separate Colorist):
```
Grade_Modifier = Colorist_Skill * 0.10
Applied to: Cinematography (+Grade_Modifier), Emotional Impact (+Grade_Modifier * 0.3)
```

**Final Film Quality** is calculated as:

```
Film_Quality = (Performance_Avg * 0.30) + (Cinematography_Avg * 0.15) +
               (Pacing_Avg * 0.20) + (Emotional_Impact_Avg * 0.20) +
               (Coherence_Avg * 0.15)
```

This weighted formula means performance and pacing are king — which reflects reality. A beautifully shot film with wooden acting and bad rhythm is a screensaver, not a movie.

**Feedback**: The Avid Bay is visualized as a timeline with scene cards arranged sequentially. Quality axes are shown as colored bars on each card. When the player selects an editorial approach, the cards visually rearrange, and quality bars animate to show the multiplier effects. The player can see exactly what is being gained and lost. When the final film score crystallizes, the screen shows a "rough cut screening" — the score appears as an audience reaction (walkouts, polite applause, standing ovation), not as a raw number.

**Depth**: A beginner picks the editorial approach that sounds coolest. An expert matches the approach to the footage's strengths. If the shoot produced standout performances but mediocre cinematography, they choose Naturalistic (1.3x Performance). If the structure fell apart during production, they avoid Nonlinear (0.7x Coherence) unless their editor is exceptional. The expert also knows that the "Editor's Choice" option — delegating to a high-Skill editor — is often the best play when the footage is messy, because the editor's Vision stat acts as a safety net. Post-production is where expert players rescue troubled productions and where careless players destroy good ones.

### 3.5 The Festival Circuit

**Player verb**: STRATEGIZE, SUBMIT, REACT

**System description**: Completed films enter the release pipeline. The player chooses from five major festival tracks and a non-festival release path:

| Festival | Prestige Value | Distribution Deal Density | Jury Taste Profile | Submission Cost |
|---|---|---|---|---|
| **Sundance** | 80 | High (American buyers) | Favors: Emotional Impact, Performance. Disfavors: Low Pacing. | $3,000 |
| **Cannes** | 100 | Medium (international buyers) | Favors: Cinematography, Structural Ambition. Disfavors: High Commercial Viability. | $5,000 |
| **Toronto (TIFF)** | 70 | Very High (broadest buyer pool) | Balanced. Slight favor: Commercial Viability + Quality combo. | $2,500 |
| **Venice** | 85 | Low (prestige only) | Favors: Thematic Depth, Cinematography. Disfavors: Genre films. | $4,000 |
| **Berlin** | 75 | Medium | Favors: Political themes, Structural Ambition. Disfavors: Conventional structure. | $3,500 |
| **Skip Festivals** | 0 | Self-directed | N/A | $0 |

Each festival has a simulated jury panel with taste weights that shift by 10-20% each in-game year (representing changing cultural winds). The jury evaluates the film against its taste profile:

```
Festival_Score = (Film_Quality * 0.6) + (Taste_Alignment * 0.3) + (Buzz_Modifier * 0.1)
```

Where `Buzz_Modifier` is generated by:
- Star power of cast (high-Reputation actors generate buzz)
- Studio reputation (studios with past wins get a +5 to +15 buzz bump)
- Marketing spend (player allocates $0-$20K on festival marketing: posters, parties, screener copies)

**Festival outcomes** (based on Festival_Score vs. competition):

| Percentile | Outcome | Effect |
|---|---|---|
| Top 5% | **Grand Prize** (Palme d'Or, Golden Bear, etc.) | Reputation +25, Distribution offers x3, Talent Loyalty +15 to all cast/crew |
| Top 15% | **Jury Prize / Nominee** | Reputation +15, Distribution offers x2, Talent Loyalty +8 |
| Top 40% | **Positive Reception** | Reputation +5, Distribution offers x1.5 |
| 40-70% | **Mixed Reception** | Reputation +0, Standard distribution offers |
| Bottom 30% | **Cold Reception** | Reputation -5, Reduced distribution interest |
| Bottom 5% | **Walkout / Pan** | Reputation -15, Talent Loyalty -10, Press haunts you for 2 projects |

**Feedback**: The festival sequence is the most dramatic moment in the loop. The player sees a darkened theater. The film's title card appears. An audience meter fills in real time (based on the score calculation happening behind the curtain). Press quotes generate procedurally. The awards ceremony plays out with the player in the audience — names read, reactions animated. A Grand Prize win triggers the single biggest emotional payoff in the game. A walkout is the single lowest point.

**Depth**: Expert players learn to read jury trends. If Cannes spent two years rewarding slow meditative films, it is likely to swing toward something energetic next cycle. Experts also game the competition — they track what rival studios are submitting (if the Rival Studio stretch feature is active) and avoid submitting their intimate drama in a year when three other studios have bigger dramas with bigger casts. The festival circuit rewards both quality filmmaking and strategic timing.

### 3.6 The Ledger (Financial System)

**Player verb**: BUDGET, INVEST, SURVIVE

**System description**: The Ledger tracks all financial flows. Starting conditions:

| Item | Amount |
|---|---|
| **Seed Funding** | $500,000 |
| **Credit Line** | $250,000 (12% annual interest) |
| **Operating Costs** | $8,000/month (rent, utilities, base staff) |
| **Year 1 Runway (no revenue)** | ~14 months before bankruptcy |

Revenue sources and their characteristics:

| Source | Timing | Amount Range | Depends On |
|---|---|---|---|
| **Theatrical Distribution** | 3-6 months post-festival | $5K-$500K | Film Quality, Distribution deal, Genre appeal |
| **VOD / Cable Sales** | 6-12 months post-completion | $10K-$200K | Film Quality, Star power, Genre |
| **DVD / Physical Media** | 4-8 months post-theatrical | $5K-$150K | Film notoriety, Genre (horror/cult films outperform) |
| **International Sales** | Variable | $10K-$300K | Festival prestige, Genre universality |
| **Festival Prize Money** | Immediate | $5K-$50K | Winning a prize |
| **Investor Injection** | Negotiated | $100K-$1M | Studio Reputation, Commercial track record |
| **Grant Funding** | Seasonal application | $20K-$100K | Artistic Identity (must be >60 on Auteur scale), Project merit |

Distribution deal structure: After a festival screening, distributors offer deals. The player chooses:

```
Advance vs. Revenue Split:
- High Advance ($50K-$200K upfront) / Low Split (15-25% of gross to studio)
- Low Advance ($10K-$50K upfront) / High Split (35-50% of gross to studio)
- No Advance / Full Revenue (studio self-distributes, keeps 70-85%, but pays marketing costs)
```

The studio must maintain positive cash flow. If cash hits $0 and the credit line is maxed, the player enters a **Crisis State**: they have 3 months to close a deal, sell a script, or find an investor, or the studio closes. Bankruptcy is the hard fail state. But there is a softer failure state — **Creative Irrelevance** — triggered when Reputation drops below 15 for 12 consecutive months. At that point, no quality talent will work with the studio, no good scripts arrive at the Greenlight Table, and the player is effectively stuck making bad films with bad people. This is worse than bankruptcy because the game does not end — it just stops being fun. The player can recover from irrelevance, but it takes 2-3 films of rebuilding, which is a significant time investment.

**Feedback**: The Ledger is displayed as a CRT monitor running a period-appropriate spreadsheet application. Numbers are color-coded: green for positive cash flow, red for negative, yellow for "you have 3 months." A burn-rate bar shows how long the studio can survive at current spending. When the player greenlights a new project, the budget projection drops visibly, and the runway bar shortens. When revenue arrives, the bar extends with a satisfying green animation.

**Depth**: The financial game is about slate management. A beginner makes one film at a time. An expert overlaps production windows — one film in post while another is in development — to keep revenue flowing. They use commercial genre films (horror is cheap to make and has reliable returns) to fund ambitious dramas. They learn that grant funding requires maintaining artistic credibility, so they cannot pivot entirely to commercial work without losing that revenue stream. The Ledger punishes feast-or-famine strategies and rewards consistent, sustainable production.

---

## 4. Systems Interactions

Where's the depth? It is in the intersections. Every system in Backlot touches every other system, and the interesting decisions live in those connections.

### 4.1 Positive Feedback Loops (Snowball Effects)

**The Prestige Spiral**: A festival win increases Reputation, which attracts better Talent, which produces better Films, which wins more festivals. This is the virtuous cycle the player is always trying to trigger.

```
Festival Win → Reputation +15-25 → Better scripts arrive → Better talent accepts lower rates
→ Higher Film Quality → Better festival outcomes → repeat
```

**Risk**: This spiral can make the game too easy once triggered. It is capped by three forces:
1. Better talent has higher Ego, creating more Production crises
2. Reputation creates expectations — a studio with Reputation 80 that releases a Film Quality 55 loses more Reputation (-10) than a Reputation 30 studio releasing the same film (-3)
3. Success attracts investor pressure toward commercial projects, pulling against the Artistic Identity that won festivals

**The Loyalty Dividend**: Working well with talent builds Loyalty, which reduces costs on future projects, which improves budget adequacy, which improves Production outcomes, which further builds Loyalty.

```
Good Collaboration → Talent Loyalty +5-15 → Salary discount next time → More budget for production quality → Better film → Better collaboration experience → repeat
```

### 4.2 Negative Feedback Loops (Rubber Banding / Balance)

**The Ego Tax**: The best talent in the game has the highest Ego scores. As the player builds a reputation and attracts top-tier talent, they also attract top-tier ego demands — final cut approval, casting approval, billing disputes, salary escalation. This means the player's "best" productions are also the most volatile.

```
Attract Star Talent → High Ego demands → More crises during production → Budget overruns
→ Reduced financial runway → Harder to attract star talent next time
```

**The Ambition Trap**: High-Structural-Ambition scripts have higher ceilings but much lower floors. A Structural Ambition 90 script can produce a Film Quality 95 masterpiece or a Film Quality 25 incoherent mess, depending on execution. Commercial scripts (Ambition 30-50) cluster in the 40-65 quality range — safe, predictable, survivable. The game's most ambitious path is also its riskiest.

**The Industry Treadmill**: Operating costs increase by 5% per in-game year (inflation, rising rents, staff salary expectations). Revenue from physical media decreases by 8% per year starting in Year 3 (the DVD collapse). This creates a slow squeeze that forces the player to either grow or die — they cannot simply maintain the status quo.

### 4.3 Emergent Possibilities

These are interactions the player discovers through play, not through tutorials:

**The Muse Dynamic**: If the same actor and director work together on 3+ films with positive outcomes, they develop a "Muse" bond. The Muse bond grants: Chemistry Modifier +20 (stacks), Salary discount 30%, and a unique event chain where the director writes a script specifically for that actor. The Muse script has guaranteed high Thematic Depth and Performance ceiling but is unmarketable to anyone else — if the actor leaves, the script is dead. This creates a deep attachment between the player and specific talent pairings.

**The Comeback Arc**: A talent who has a catastrophic failure (film walks out, personal crisis, fired from a production) develops a "Comeback" flag. If the player casts a Comeback-flagged talent in a project that succeeds, the talent gains +20 Loyalty to the studio and generates a press event: "Remarkable return to form." The audience and critics love a redemption story. This means that hiring damaged talent is a high-risk, high-reward strategy.

**The Slate Identity Effect**: If the player's last 3 films share a genre or thematic focus, the studio develops a "Specialization" bonus: +10 to Film Quality for that genre/theme (the studio has developed institutional knowledge). But it also triggers a "-5 to industry interest in scripts outside the specialization" penalty — the player gets pigeonholed. Breaking out of a specialization requires deliberately making a film in a different genre and accepting the penalty hit.

**The Festival Shelf Life**: A film that premieres at a major festival but does not win any prizes has a "shelf life" of 12 in-game months for distribution deals. After that, distributors lose interest and the film's revenue potential drops by 50%. But if the player holds the film and enters it in a second festival within that window, it gets a Buzz penalty of -20 (festivals do not like second-run films). The player must decide: take the best deal available now, or gamble on a second festival.

---

## 5. Progression Design

### 5.1 Player Growth Vectors

The player grows along three simultaneous axes, each with its own progression curve:

**Skill Growth (Player Knowledge)**: The player gets better at reading the systems. This is not stat-based — it is genuine player skill accumulation.

| Hours Played | Skill Level | What the Player Understands |
|---|---|---|
| 0-2 | Novice | Basic production pipeline, budget management, casting by stats |
| 2-8 | Apprentice | Talent personalities matter, crisis event seeding, editorial approach matching |
| 8-20 | Journeyman | Talent Web manipulation, slate management, festival timing, financial planning across 2-3 films |
| 20-50 | Expert | Muse dynamics, Comeback casting, specialization management, multi-year strategic planning |
| 50+ | Master | Reading Pretension Index from coverage alone, engineering specific festival jury matchups, building self-sustaining talent ecosystems |

**Studio Growth (Systemic Progression)**: The studio itself levels up based on Reputation thresholds.

| Reputation Tier | Threshold | Unlocks |
|---|---|---|
| **Unknown** | 0-19 | Base game. 2 script sources. Micro/Low budget only. No major festival access. |
| **Emerging** | 20-39 | Agent Pitches unlock. Low/Mid budget available. Sundance and TIFF accessible. 1 additional writer slot. |
| **Established** | 40-59 | All script sources active. All budget tiers available. All festivals accessible. Office upgrade (visual). Investor interest begins. |
| **Respected** | 60-79 | Top-tier talent becomes available. Grant funding increases. Festival Buzz bonus +10. Rival studios acknowledge you (if feature active). |
| **Prestige** | 80-100 | Talent seeks you out proactively. Distribution deals improve by 30%. Legacy events trigger. The industry profiles your studio. |

**Content Unlock Pacing**: New mechanics and options are introduced at a controlled rate to avoid overwhelming the player.

| Film # | New Element Introduced | Design Rationale |
|---|---|---|
| 1 | Simplified production (fewer crises, single editorial approach choice) | Let the player learn the pipeline without being punished |
| 2 | Full crisis deck activates, all editorial approaches unlock | Player now understands the pipeline; add decision depth |
| 3 | Talent Web relationship system becomes visible | Player now has repeat collaborators; show the web |
| 4 | Festival strategy becomes meaningful (multiple festivals available) | Player has enough reputation for choices to matter |
| 5 | Investor system activates | Player needs more money; introduce the art-vs-commerce tension mechanically |
| 6 | Talent Ego events escalate | Player has attracted good talent; now deal with the cost |
| 8 | Muse dynamic can trigger | Player has long-term relationships; reward them |
| 10 | Legacy events begin | Player has a body of work; reflect it back |

### 5.2 Difficulty Curve

The difficulty curve is **stepped with escalating pressure**, not linear. Each "step" corresponds to a shift in the game's dominant challenge:

```
Difficulty
    │
    │                                          ┌────── Legacy
    │                                     ┌────┘       Pressure
    │                                ┌────┘             (Films 10+)
    │                           ┌────┘
    │                      ┌────┘   Ambition vs.
    │                 ┌────┘        Survival
    │            ┌────┘             (Films 4-8)
    │       ┌────┘
    │  ┌────┘   Learning the
    │──┘        Pipeline
    │           (Films 1-3)
    │
    └───────────────────────────────────────────────► Films Completed
        1    2    3    4    5    6    7    8    9   10+
```

**Films 1-3 (Learning)**: The difficulty is figuring out the production pipeline. The game is somewhat forgiving — the first film's budget is subsidized, crises are less frequent, and there is always at least one viable festival option. The player should complete Film 1 successfully (even if the film is mediocre) and start to struggle on Film 2-3 as training wheels come off.

**Films 4-8 (Ambition vs. Survival)**: The difficulty shifts to resource management. The DVD revenue decline begins. Talent costs escalate. Better scripts demand bigger budgets. The player must learn slate management — balancing commercial and artistic projects, overlapping production windows, managing cash flow across multiple films. This is where most players will hit their first crisis moment: "I can't afford the film I want to make."

**Films 9+ (Legacy Pressure)**: The difficulty becomes reputational. The studio has an identity, and every film either reinforces or challenges it. Former collaborators return with demands. The press scrutinizes the slate. A bad film at Reputation 75 is more damaging than a bad film at Reputation 30. The player must manage expectations while continuing to take creative risks. The game never becomes easy — the nature of the challenge simply evolves.

### 5.3 Pacing Structure

Each in-game year follows a seasonal structure that creates natural rhythmic variation:

| Season | Duration (real time) | Primary Activity | Pacing Feel |
|---|---|---|---|
| **Winter** (Jan-Mar) | ~15 min | Sundance/Berlin results land. Greenlight decisions for Spring film. Grant applications. | Reflective, strategic |
| **Spring** (Apr-Jun) | ~20 min | Production 1. Cannes submissions. Talent scouting for summer. | Active, high-pressure |
| **Summer** (Jul-Sep) | ~15 min | Post-production on Spring film. Venice/TIFF results. Development on Fall project. | Surgical, contemplative |
| **Fall** (Oct-Dec) | ~20 min | Production 2 (or 3 if the player is ambitious). Award season rumblings. Year-end financials. | Active, culminating |

The year ends with a **Studio Review** screen: a one-page summary of the year's films, financials, and key events. This provides a natural breathing point — a moment for the player to assess, plan, and feel the weight of their decisions before the next year begins.

---

## 6. Risk Assessment

Here is where I get honest about what could kill this game. Good design is not just knowing what to build — it is knowing what might break.

### 6.1 What Could Be Unfun

**Risk 1: Decision Fatigue in Production**
The Production Clock generates 1-5 decisions per shoot day across 15-40 days. That is potentially 200 decisions per production, many of which involve similar tradeoff structures (budget vs. quality vs. morale). If decisions start feeling samey by day 15, the player checks out.

*Mitigation*: Crisis events are categorized and no single category can fire more than twice in a row. Every 5th day is a "quiet day" with zero or one decisions. Breakthrough events (positive surprises) are front-loaded slightly into the second half of production to reward survival. If testing reveals fatigue, the Production Clock compresses to weekly decisions (7-10 decision points per production instead of 15-40).

**Risk 2: Talent Web Overwhelming the Player**
80-120 active talents is rich but potentially paralyzing. If the player feels they need to track every relationship to make good decisions, the cognitive load becomes unmanageable.

*Mitigation*: The Talent Web visualizes only first- and second-degree connections to the player's current project. An "Agent Recommendation" system surfaces 3-5 talent suggestions for each role based on fit (the system does the first-pass filtering). Deep Web manipulation is expert-level play, not required for competent play. If testing reveals overwhelm, the active talent count drops to 60-80.

**Risk 3: Financial Death Spiral**
If the player's first 2 films both lose money, they may enter an unrecoverable financial state — not enough money to make a good film, which means bad films, which means less money. This is not fun. It is not even educational. It is just punishing.

*Mitigation*: Three safety valves:
1. **Emergency Grant**: If cash drops below $50K and Reputation is above 10, a one-time "indie emergency fund" grant of $75K is available. This is a one-per-playthrough lifeline.
2. **Scale-Down Option**: The player can always make a Micro-budget film ($50K-$150K). Even in financial crisis, a micro-budget project is producible.
3. **Mentorship Event**: On the player's first financial crisis, a veteran producer NPC offers advice and a $30K bridge loan. This is narrative and financial support combined.

**Risk 4: Procedural Scripts Feeling Hollow**
If coverage reports read like Mad Libs — "A [adjective] [genre] about a [character] in [location]" — the Greenlight Table collapses. The player needs to feel like they are reading real script coverage, not generated text.

*Mitigation*: Scripts are generated from authored template pools, not pure procedural generation. Each genre has 30-50 authored logline templates with variable slots for character, setting, and thematic specifics. Coverage reports are assembled from 200+ authored phrase fragments that are combined based on script attributes. The voice must feel human. This is the single highest priority content creation task.

**Risk 5: Art-vs-Commerce Binary Feels Reductive**
If "artistic" and "commercial" become two buttons the player toggles between, the theme collapses into a false dichotomy. Real filmmaking is messier than that.

*Mitigation*: The Artistic Identity axis is a spectrum, not a binary. Commercial films can have artistic merit (high Commercial Viability + high Thematic Depth). Arthouse films can have commercial breakouts (low Commercial Viability but high Film Quality creates a "sleeper hit" event). The game rewards mixing the slate, not committing to one extreme. The most successful strategies involve deliberate balance: commercial projects fund artistic risks, and artistic successes attract commercial opportunities.

**Risk 6: Late-Game Repetition**
After Film 10, is the player just doing the same thing with bigger numbers? If the Production Clock feels identical on Film 12 as it did on Film 4, the game has a content ceiling problem.

*Mitigation*: Three late-game systems inject fresh dynamics:
1. **Industry Shift Events** (Year 5+): Major industry changes that alter the meta — digital cameras replace film (production costs drop, DP arguments change), streaming platforms emerge (new distribution channel, different economics), a major studio collapses (talent flood the indie market)
2. **Legacy Events** (Film 10+): Personalized events based on the player's history — a retrospective article, a former collaborator's memoir that mentions you, a film school teaching your early work
3. **The Second Studio Problem** (Reputation 80+): The player is offered the chance to expand — open a second office, produce more films per year, hire a development executive. Expansion changes the game from "hands-on producer" to "studio head," introducing delegation and oversight mechanics. This is the transition from Football Manager to Football Chairman.

### 6.2 Playtest Priorities

Testing is ordered by what validates core assumptions fastest. If any of these fail, major design revisions are needed.

| Priority | Playtest Focus | Key Question | Success Metric | When |
|---|---|---|---|---|
| **P0** | Greenlight Table + Coverage Reports | Do coverage reports feel like real scripts? Does the greenlight decision feel meaningful? | 8/10 testers can articulate why they chose one script over another based on the coverage | Week 1-2 of prototype |
| **P0** | Production Clock Decision Pacing | Does the shoot feel tense without becoming tedious? | Tester engagement does not drop below baseline during the second half of a 25-day production | Week 2-3 of prototype |
| **P1** | Talent Web Readability | Can players identify good casting choices from the Talent Web without being overwhelmed? | 7/10 testers use relationship data (not just skill stats) in casting decisions by Film 3 | Week 3-4 of prototype |
| **P1** | Financial Viability of Both Paths | Can a pure-art player and a pure-commerce player both survive 5 films? | Both strategies reach Film 5 with positive cash flow in at least 60% of playthroughs | Week 4-6 of prototype |
| **P2** | Festival Strategy Depth | Do players feel agency in festival submission, or does it feel random? | 7/10 testers can explain their festival strategy and how it differs from a default choice | Week 6-8 of prototype |
| **P2** | Avid Bay Satisfaction | Does post-production feel like a meaningful creative space, or like a math problem? | Testers spend >2 minutes considering editorial approach (not just picking the first option) | Week 6-8 of prototype |
| **P3** | 5-Film Arc Emotional Curve | Does the player's emotional journey match the designed arc (naive excitement to competence to legacy)? | Post-session interviews confirm at least 3 of 5 emotional beats | Week 8-12 of prototype |
| **P3** | Talent Web Emergent Stories | Do players form memorable relationships with specific talents? | 8/10 testers can name a specific talent and tell a story about them after a 2-hour session | Week 8-12 of prototype |

---

## 7. Economy Balance Framework

### 7.1 Revenue vs. Cost Targets by Studio Tier

The economy must support both artistic and commercial strategies while maintaining pressure. Here are the target financial ranges per film at each studio tier:

| Tier | Avg Production Cost | Avg Revenue (Commercial Path) | Avg Revenue (Art Path) | Target Margin |
|---|---|---|---|---|
| Unknown | $80K-$150K | $50K-$200K | $20K-$120K | Break-even to slight loss (learning phase) |
| Emerging | $150K-$400K | $120K-$500K | $80K-$350K | 10-30% margin (survival phase) |
| Established | $300K-$1M | $250K-$1.2M | $150K-$800K + grants | 15-35% margin (growth phase) |
| Respected | $500K-$2M | $400K-$2.5M | $300K-$1.5M + grants + prizes | 20-40% margin (stability) |
| Prestige | $800K-$3M | $600K-$4M | $500K-$3M + prizes + legacy revenue | 25-50% margin (legacy) |

The art path generates less raw revenue but unlocks grant funding ($20K-$100K/year) and festival prizes ($5K-$50K per win) that partially close the gap. The commercial path generates more revenue but does not access grants and has lower festival placement (reducing Reputation growth). Neither path should be more than 30% more profitable than the other at any tier — if it is, the economy is broken.

### 7.2 Currency Flow Diagram

```
                    INCOMING                           OUTGOING
                    ────────                           ────────
           ┌─────────────────────┐            ┌─────────────────────┐
           │ Theatrical Revenue  │            │ Production Budgets  │
           │ VOD / Cable Sales   │            │ Talent Salaries     │
           │ DVD Sales           │──────┐     │ Operating Costs     │
           │ International Sales │      │     │ Festival Fees       │
           │ Festival Prizes     │      ▼     │ Marketing           │
           │ Investor Funding    │   [STUDIO  │ Credit Interest     │
           │ Grant Funding       │    CASH]   │ Option Fees         │
           │ Distribution Adv.   │      │     │ Writer Fees         │
           └─────────────────────┘      │     └─────────────────────┘
                                        │
                                        ▼
                                  ┌───────────┐
                                  │  RUNWAY   │
                                  │  (months  │
                                  │  until    │
                                  │  crisis)  │
                                  └───────────┘
```

### 7.3 Key Economic Ratios

These ratios must be maintained for the economy to feel healthy:

| Ratio | Target | If Too High | If Too Low |
|---|---|---|---|
| Production Cost / Studio Cash | 40-70% | Player can't afford a bad film | No financial tension |
| Annual Operating Cost / Annual Revenue | 15-30% | Overhead feels punishing | Money is too easy |
| Best Talent Salary / Micro Budget | 30-60% | Star casting is prohibitive | Star casting is trivial |
| Festival Prize / Production Cost | 5-20% | Prizes feel meaningless | Prizes replace distribution |
| Grant Funding / Artistic Film Cost | 15-35% | Grants don't matter | Grants eliminate financial risk for art films |

---

## 8. Open Questions for Playtesting

These are the questions I cannot answer from a design document. They require players. They require observation. They require the humility to admit that the spreadsheet is not the game.

1. **Production Clock granularity**: Day-by-day or week-by-week? The design spec calls for day-by-day, but if testing reveals decision fatigue by day 15, the week-by-week fallback must be tested. The question is not "which is more realistic?" but "which is more fun at the third production?"

2. **Talent Web sweet spot**: 80-120 active talents is the current target. At what number does the web shift from "rich ecosystem" to "overwhelming spreadsheet"? My instinct says 80 is the floor, 100 is the sweet spot, and 120 requires better filtering UI than I have currently designed.

3. **Coverage report voice**: How authored is "authored enough"? If 30 logline templates per genre feels hollow after 10 films, we need 50. If 50 still feels hollow, we may need a more sophisticated generation system or a smaller but more deeply written script pool. This is a content quality problem, not a systems design problem. It needs writers, not designers.

4. **First-film scaffolding**: How much should the first film be on rails? The current design gives a simplified Production Clock and subsidized budget. Is that enough? Should Film 1 be a curated experience with a pre-selected script and pre-selected cast, letting the player focus purely on production decisions? Or does that rob the player of the greenlight moment that defines the game?

5. **Soft failure (Creative Irrelevance)**: Is Reputation dropping below 15 the right threshold? Too low and the player never experiences it. Too high and it triggers prematurely. The threshold should be calibrated so that approximately 20% of players experience creative irrelevance at least once in a full playthrough, and 80% of those players can recover from it.

6. **Comeback casting payoff**: Is +20 Loyalty and a press event enough to incentivize the risk of casting damaged talent? Or does it need a Film Quality bonus (audience loves a redemption story) to make the math work?

7. **Industry Shift Events timing**: Year 5 for the first major shift — does that give the player enough time to establish comfortable patterns before disrupting them? The events should feel like seismic shifts, not annoyances. If they land too early, the player has not built enough to care. If they land too late, the player has mastered the systems and the shifts are trivial.

8. **Session length target**: The design targets 60-90 minutes per session (roughly 2 films). Is that right for the audience? Management sim players tend toward longer sessions (2-3 hours). Film enthusiasts tend toward shorter ones (30-60 minutes). Where does the Backlot audience actually land? The seasonal structure allows natural save points at every quarter, so sessions can flex from 15 minutes (one season) to 3 hours (a full in-game year), but the pacing must feel intentional at the 60-90 minute mark.

9. **The Avid Bay as skill check**: Does post-production feel like a meaningful creative decision or a math optimization? If testers immediately identify the "correct" editorial approach based on footage stats, the system lacks ambiguity. The multiplier tables may need hidden variance (plus or minus 10-15%) to prevent deterministic optimization and reward intuition over calculation.

10. **Art-vs-commerce spectrum balance**: Over 100 playthroughs, do art-focused and commerce-focused studios both reach Film 10 at roughly equal rates? If one strategy dominates, the theme collapses. The economy must support both, and neither should feel like the "correct" way to play.

---

*This document is a starting point, not a finished blueprint. Every number in these tables is a hypothesis. Every mechanic description is a theory about what will be fun. The only way to know if any of this works is to build the Greenlight Table, put scripts in front of a player, and watch their face when they read the coverage report for a film about a deaf saxophonist in Reno.*

*If they lean forward, we have a game.*

*If they do not, we go back to the loop.*

*-- REED*
