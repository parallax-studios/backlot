# BACKLOT — Technical Architecture Document

**BYTE, Lead Programmer**
**Status: Production-Ready Architecture v1.0**
**Target Platform: PC (Steam Primary), Switch Secondary**
**Estimated Core Loop Complete: 6-8 months, 2 programmers + 1 tech artist**

---

## 1. Executive Summary

BACKLOT is a management sim where your resources have opinions. The technical challenge is not rendering complexity or physics — it is simulation density. We need 80-120 persistent agents with relationship graphs, procedural event decks seeded by dozens of variables, a financial model that runs multi-year projections, and all of it has to respond to player decisions in under 200ms. This is a data-driven game. The engine is a state machine orchestrator wrapped around a relational database. The UI is the game. The art is the interface.

**Core Technical Pillars**:
1. Agent simulation with personality-driven behavior
2. Procedural content generation with authored voice (scripts, events, press quotes)
3. Event-driven production pipeline with crisis deck system
4. Multi-axis scoring and weighted outcome calculation
5. Save/load supporting full simulation state serialization
6. Modular data architecture for balance iteration

**Performance Budget**: 60fps UI on a 2019 mid-tier laptop. No real-time rendering complexity. The bottleneck is logic, not graphics. Target: 2ms per frame for simulation step, 4ms for UI updates, 10ms budget for procedural text generation.

**Risk Areas**: Procedural script generation quality, relationship graph pathfinding at scale, save file bloat past Film 20, decision fatigue in Production Clock.

Ship it simple. Ship it data-driven. Profile before you optimize.

---

## 2. Engine and Framework Recommendation

### 2.1 Engine Choice: **Godot 4.x**

**Rationale**:

This game is 95% UI, data systems, and logic. It does not need advanced 3D rendering, physics, or AAA-scale asset pipelines. What it needs:
- Robust UI toolkit with rich layout controls
- Fast iteration on interface design
- Clean separation of logic and presentation
- Good serialization support for save systems
- Lightweight builds (target <500MB install size)
- Multi-platform export without pain

Godot 4.x hits every requirement. The Control node system is perfect for building the diegetic office UI. The signal system maps cleanly to event-driven architecture. GDScript iteration speed is critical for a design that will shift during prototyping. The scene instancing model works well for modular UI panels (Greenlight Table, Talent Web, Avid Bay are all separate scenes composed at runtime).

**Alternatives Considered**:

| Engine | Pros | Cons | Verdict |
|---|---|---|---|
| **Unity** | Mature tooling, asset store, team familiarity | Heavier runtime, UI Toolkit still maturing, licensing concerns post-2023 | Overkill for a 2D UI-driven sim |
| **Unreal** | Blueprint rapid prototyping, excellent UI widgets | 2GB+ install size, long compile times, total overkill for scope | No |
| **Custom (Raylib/SDL)** | Full control, minimal dependencies | Reinventing UI framework, save system, serialization — 6 months burned before gameplay | Hubris. We ship games, not engines. |
| **Godot 4.x** | UI-first design, fast iteration, clean data handling, multi-platform, open source | Smaller community than Unity, fewer third-party assets | **CHOSEN** |

### 2.2 Language: **GDScript (Primary), C# (Hot Paths)**

GDScript for all gameplay logic, UI controllers, and event systems. Fast to write, fast to iterate, integrated debugger works well.

C# for computationally expensive systems if profiling reveals bottlenecks:
- Relationship graph pathfinding (if we implement multi-degree connection searches)
- Festival jury scoring across 50+ competing films
- Procedural text generation with complex grammar trees (if we go that route)

Start everything in GDScript. Move to C# only when the profiler proves it is necessary. Premature optimization is how projects die.

### 2.3 Version Control and Collaboration

**Git + GitHub/GitLab**. Text-based scene files in Godot 4.x merge cleanly. No special LFS needed for this project — assets are minimal.

**Branching Strategy**:
- `main`: Always stable, always builds
- `develop`: Integration branch for features
- `feature/*`: Individual systems (e.g., `feature/talent-web`, `feature/production-clock`)

**Build Pipeline**:
- GitHub Actions for automated builds on commit to `develop`
- Automated exports for Windows, Linux, macOS (Godot makes this trivial)
- Smoke test suite runs on every build: load game, simulate one production, verify save/load

---

## 3. Core Systems Architecture

### 3.1 High-Level Component Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                        GAME CONTROLLER                          │
│  (Orchestrates state machine, manages phase transitions)        │
└────────────┬────────────────────────────────────────────────────┘
             │
             ├──► [SIMULATION LAYER]
             │      │
             │      ├──► Studio State (finances, reputation, slate)
             │      ├──► Talent Pool Manager (all agents, relationships)
             │      ├──► Production Manager (current film state)
             │      ├──► Festival Simulator (jury scoring, outcomes)
             │      └──► Economy Manager (revenue flows, projections)
             │
             ├──► [EVENT SYSTEM]
             │      │
             │      ├──► Event Deck (crisis generation, weighted draws)
             │      ├──► Narrative Event Pool (authored events)
             │      └──► Trigger System (condition evaluation)
             │
             ├──► [PROCEDURAL GENERATION]
             │      │
             │      ├──► Script Generator (template + attribute system)
             │      ├──► Coverage Writer (coverage report text assembly)
             │      ├──► Press Quote Generator
             │      └──► Talent Name Generator
             │
             ├──► [SCORING & OUTCOME ENGINE]
             │      │
             │      ├──► Film Quality Calculator (weighted multi-axis)
             │      ├──► Festival Jury Evaluator
             │      ├──► Distribution Deal Generator
             │      └──► Reputation Impact Calculator
             │
             └──► [UI LAYER]
                    │
                    ├──► Greenlight Table UI
                    ├──► Talent Web Visualizer
                    ├──► Production Clock UI
                    ├──► Avid Bay UI
                    ├──► Festival Results UI
                    └──► Ledger UI
```

### 3.2 Data Flow: One Production Cycle

```
1. GREENLIGHT TABLE
   Player selects script
        ↓
   Script data → Studio State
   Budget allocated, writers assigned
        ↓

2. PRE-PRODUCTION
   Player casts talent
        ↓
   Talent agents negotiate → Talent Pool Manager updates relationships
   Budget finalized → Economy Manager updates projections
   Event Deck seeded with weights based on cast/crew traits
        ↓

3. PRODUCTION (15-40 days)
   Each day:
        Event System → Draw from crisis deck → Present decision to player
        Player choice → Update morale/budget/loyalty → Feedback to UI
        Footage quality calculated per scene → Stored in Production Manager
        ↓
   Production complete → Scene card pool generated
        ↓

4. POST-PRODUCTION
   Player selects editorial approach
        ↓
   Avid Bay applies multipliers to scene cards
   Score/color grade applied
        ↓
   Final Film Quality calculated → Stored in Studio State
        ↓

5. FESTIVAL RELEASE
   Player selects festival
        ↓
   Festival Simulator scores film against jury taste + competition
        ↓
   Outcome generated (prize, reception, distribution offers)
        ↓
   Studio State updated: reputation, finances, talent loyalty shifts
        ↓

6. LOOP BACK TO GREENLIGHT TABLE
   New scripts generated based on updated reputation
   Talent pool updated with availability changes
```

### 3.3 State Machine Architecture

The game is a phase-driven state machine. Each phase has entry conditions, a set of valid actions, and exit conditions.

```gdscript
# Core state enum
enum GamePhase {
    STUDIO_SETUP,          # One-time: name studio, set identity
    GREENLIGHT,            # Select and develop scripts
    PRE_PRODUCTION,        # Casting, crew, budget lock
    PRODUCTION,            # Day-by-day shoot simulation
    POST_PRODUCTION,       # Editing, score, grade
    FESTIVAL_RELEASE,      # Submit, jury simulation, outcomes
    SEASON_TRANSITION,     # Financial review, time advances
    GAME_OVER              # Bankruptcy or player quit
}

# State manager (singleton)
class_name GameStateManager extends Node

var current_phase: GamePhase = GamePhase.STUDIO_SETUP
var studio: Studio              # Studio persistent data
var current_film: Film          # Active production data
var talent_pool: TalentPool     # All agents and relationships
var event_system: EventSystem   # Crisis deck and triggers

func transition_to(new_phase: GamePhase) -> void:
    # Validate transition legality
    if not is_valid_transition(current_phase, new_phase):
        push_error("Invalid state transition: %s -> %s" % [current_phase, new_phase])
        return

    # Exit current phase (cleanup, save intermediate state)
    _exit_phase(current_phase)

    # Enter new phase (initialize UI, seed data)
    current_phase = new_phase
    _enter_phase(new_phase)

    # Emit signal for UI updates
    emit_signal("phase_changed", new_phase)

func _enter_phase(phase: GamePhase) -> void:
    match phase:
        GamePhase.GREENLIGHT:
            # Generate new scripts based on reputation
            var script_pool = ScriptGenerator.generate_scripts(studio.reputation)
            emit_signal("scripts_available", script_pool)

        GamePhase.PRODUCTION:
            # Seed event deck based on current film's cast/crew
            event_system.seed_deck(current_film)
            production_day = 1

        GamePhase.FESTIVAL_RELEASE:
            # Generate available festivals based on reputation
            var festivals = FestivalSystem.get_available_festivals(studio.reputation)
            emit_signal("festivals_available", festivals)

        # ... handle other phases
```

**Design note**: The state machine is explicit and centralized. No implicit phase transitions. Every transition is logged (for debugging) and validated. If a bug causes an invalid state, the game logs it and refuses the transition rather than corrupting save data. Fail loudly in development, fail safely in production.

---

## 4. Key Gameplay Systems Technical Design

### 4.1 The Greenlight Table (Script Generation & Selection)

**System Responsibilities**:
- Generate 3-5 procedural scripts per season based on studio reputation
- Assemble coverage reports that communicate script attributes through natural language
- Handle script selection and option fees
- Trigger writer relationship updates

**Data Structure**:

```gdscript
class_name Script extends Resource

# Core attributes (1-100 scales)
var genre: String                    # Drama, Comedy, Thriller, etc.
var tone: float                      # 1=lighthearted, 100=heavy
var structural_ambition: float       # How unconventional the narrative is
var thematic_depth: float            # Substance of themes
var commercial_viability: float      # Marketability
var base_quality: float              # Raw screenplay quality
var pretension_index: float          # abs(self_assessment - base_quality)
var budget_demand: BudgetTier        # MICRO, LOW, MID, HIGH

# Metadata
var title: String
var writer_id: int                   # Reference to Talent
var logline: String                  # Procedurally generated
var coverage_text: String            # Assembled from templates
var option_cost: int                 # Purchase price
var source: ScriptSource             # WRITER_POOL, COLD_SUB, AGENT, etc.

enum BudgetTier { MICRO, LOW, MID, HIGH }
enum ScriptSource { WRITER_POOL, COLD_SUBMISSION, AGENT_PITCH, COMMISSIONED }
```

**Procedural Generation Strategy**:

Do NOT use pure algorithmic generation (Markov chains, GPT-style models). It produces generic slop. Instead: **Template-Based Assembly with Authored Components**.

**Script Generation Pipeline**:

1. **Determine Genre and Tone** (weighted by studio reputation and artistic identity)
2. **Roll Attributes** (base_quality, commercial_viability, etc. — Gaussian distributions with clamps)
3. **Select Logline Template** from authored pool (30-50 per genre)
4. **Populate Template Variables** (character type, setting, conflict)
5. **Assemble Coverage Report** from phrase library (200+ fragments)
6. **Calculate Option Cost** based on source and writer reputation

**Example Logline Template (Drama)**:

```
Template: "A {adjective} {character_type} in {location} must {conflict_verb} {conflict_object} before {deadline_phrase}."

Variables Pool:
- adjective: ["grieving", "ambitious", "reclusive", "disgraced", "idealistic"]
- character_type: ["architect", "cellist", "ex-cop", "veterinarian", "translator"]
- location: ["Minneapolis", "a dying steel town", "coastal Maine", "suburban Atlanta"]
- conflict_verb: ["confront", "unravel", "rebuild", "reconcile with"]
- conflict_object: ["his estranged daughter", "the night his brother died", "the marriage he destroyed"]
- deadline_phrase: ["his daughter's wedding", "the foreclosure", "winter arrives"]

Generated Logline: "A grieving cellist in coastal Maine must reconcile with his estranged daughter before winter arrives."
```

Each template has attribute hints (this template suggests tone: 65-85, thematic_depth: 60-90). The generator uses these to constrain attribute rolls.

**Coverage Report Assembly**:

Coverage consists of 3-4 sentence fragments pulled from a categorized phrase library:

```gdscript
# Coverage phrase library structure
var coverage_library = {
    "tone_light": [
        "Breezy and charming.",
        "The script has a lightness that could play well with festival crowds.",
        "Witty without being precious."
    ],
    "tone_heavy": [
        "Emotionally demanding material.",
        "This is a heavy lift for audiences — rewarding, but not an easy sit.",
        "The tone is uncompromising. It asks a lot."
    ],
    "ambition_high_quality_low": [
        "Ambitious structure, but the execution is shaky.",
        "The writer is swinging for the fences — and missing.",
        "Big ideas, underdeveloped craft."
    ],
    "commercial_low_quality_high": [
        "This is not a commercial play, but there's real substance here.",
        "A festival cornerstone if executed precisely.",
        "Marketability is a question mark, but the material is strong."
    ],
    # ... 50+ categories
}

func generate_coverage(script: Script) -> String:
    var fragments = []

    # Opening (logline)
    fragments.append(script.logline)

    # Tone assessment
    if script.tone < 40:
        fragments.append(coverage_library.tone_light.pick_random())
    elif script.tone > 70:
        fragments.append(coverage_library.tone_heavy.pick_random())

    # Quality vs. ambition
    if script.structural_ambition > 75 and script.base_quality < 60:
        fragments.append(coverage_library.ambition_high_quality_low.pick_random())

    # Commercial viability
    if script.commercial_viability < 40 and script.base_quality > 70:
        fragments.append(coverage_library.commercial_low_quality_high.pick_random())

    # Budget note
    fragments.append("Budget demand: %s." % BudgetTier.keys()[script.budget_demand])

    return " ".join(fragments)
```

**Performance Target**: Generate 5 scripts with full coverage in <100ms. This runs once per season, so performance is not critical, but it should be instant on player perception.

**Playtest Metric**: If players cannot articulate why they chose one script over another after reading coverage, the text generation has failed. This is a content quality problem, not a code problem. Budget 40-60 hours of writer time on phrase library.

---

### 4.2 The Talent Web (Agent Simulation & Relationship System)

**System Responsibilities**:
- Simulate 80-120 persistent creative agents (actors, directors, writers, crew)
- Track pairwise relationships between agents and between agents and studio
- Calculate negotiation outcomes based on relationship and market factors
- Trigger talent-driven events (loyalty, poaching, ego demands)

**Data Structure**:

```gdscript
class_name Talent extends Resource

# Identity
var id: int
var name: String
var role: TalentRole          # ACTOR, DIRECTOR, WRITER, DP, EDITOR, COMPOSER
var headshot_texture: Texture # Visual representation

# Core stats (1-100)
var skill: float
var range: float              # Actors/Directors only
var vision: float             # Directors/Writers only
var reliability: float
var ego: float
var ambition: float

# Actor-specific
var chemistry_map: Dictionary # {other_actor_id: chemistry_modifier (-30 to +30)}

# Career state
var reputation: float         # 0-100, separate from skill
var recent_success_modifier: float  # -20 to +20, decays over time
var availability: bool
var current_project_id: int   # -1 if available

# Personality (2-3 traits from pool of 20)
var traits: Array             # [Trait.METHOD_ACTOR, Trait.PERFECTIONIST]

# Relationships
var studio_relationship: float      # -50 to +50
var talent_relationships: Dictionary # {talent_id: relationship_score (-50 to +50)}

enum TalentRole { ACTOR, DIRECTOR, WRITER, DP, EDITOR, COMPOSER, PRODUCER }
enum Trait {
    METHOD_ACTOR, PEOPLE_PLEASER, CONTROL_FREAK, NIGHT_OWL, PERFECTIONIST,
    HARD_DRINKER, MENTOR, DIVA, WORKHORSE, RECLUSE, SCENE_STEALER,
    LOYAL, MERCENARY, TEMPERAMENTAL, VISIONARY, BY_THE_BOOK,
    IMPROVISER, POLITICAL, CONFRONTATIONAL, QUIET_PROFESSIONAL
}
```

**Relationship System Implementation**:

Relationships are stored in a sparse adjacency matrix. Most talents have never worked together, so storing every pairwise relationship is wasteful.

```gdscript
class_name TalentPool extends Node

var talents: Array[Talent] = []
var relationship_graph: Dictionary = {}  # {talent_id_A: {talent_id_B: score}}

func get_relationship(talent_a_id: int, talent_b_id: int) -> float:
    if talent_a_id in relationship_graph:
        if talent_b_id in relationship_graph[talent_a_id]:
            return relationship_graph[talent_a_id][talent_b_id]
    return 0.0  # Default: no relationship

func modify_relationship(talent_a_id: int, talent_b_id: int, delta: float) -> void:
    # Initialize nested dict if needed
    if not talent_a_id in relationship_graph:
        relationship_graph[talent_a_id] = {}
    if not talent_b_id in relationship_graph:
        relationship_graph[talent_b_id] = {}

    # Update bidirectional (relationships are symmetric)
    var current_ab = get_relationship(talent_a_id, talent_b_id)
    relationship_graph[talent_a_id][talent_b_id] = clamp(current_ab + delta, -50, 50)
    relationship_graph[talent_b_id][talent_a_id] = relationship_graph[talent_a_id][talent_b_id]

    emit_signal("relationship_changed", talent_a_id, talent_b_id, relationship_graph[talent_a_id][talent_b_id])
```

**Negotiation System**:

```gdscript
func calculate_actor_ask(actor: Talent, studio: Studio) -> int:
    var base_ask = (actor.skill * 500) + (actor.ego * 200) + (actor.recent_success_modifier * 1000)

    # Relationship discount
    var relationship_discount = actor.studio_relationship * 0.005  # 0.5% per point

    # Ambition penalty (ambitious actors want more)
    if actor.ambition > 70:
        base_ask *= 1.15

    # Apply discount
    var final_ask = base_ask * (1.0 - relationship_discount)

    return int(final_ask)

func negotiate(actor: Talent, offer: int, studio: Studio) -> bool:
    var ask = calculate_actor_ask(actor, studio)
    var acceptance_threshold = ask * 0.75  # Will accept offers at 75% of ask or higher

    # Trait modifiers
    if Trait.MERCENARY in actor.traits:
        acceptance_threshold = ask * 0.90  # Harder negotiation
    if Trait.LOYAL in actor.traits and actor.studio_relationship > 20:
        acceptance_threshold = ask * 0.65  # Easier for loyal talent

    if offer >= acceptance_threshold:
        # Accept and update relationship
        actor.studio_relationship += 2  # Successful negotiation builds trust
        return true
    else:
        # Reject and slight relationship hit
        actor.studio_relationship -= 1
        return false
```

**Visualization**:

The Talent Web is a force-directed graph rendered using Godot's `draw_*` functions in a custom Control node. Nodes are headshots. Edges are colored strings (red = conflict, green = positive, gold = muse bond).

```gdscript
func _draw():
    # Draw edges first (so nodes render on top)
    for talent_a_id in relationship_graph:
        for talent_b_id in relationship_graph[talent_a_id]:
            var score = relationship_graph[talent_a_id][talent_b_id]
            if abs(score) > 15:  # Only draw significant relationships
                var color = get_relationship_color(score)
                var pos_a = node_positions[talent_a_id]
                var pos_b = node_positions[talent_b_id]
                draw_line(pos_a, pos_b, color, 2.0)

    # Draw talent nodes (headshots)
    for talent in visible_talents:
        var pos = node_positions[talent.id]
        draw_texture_rect(talent.headshot_texture, Rect2(pos - Vector2(32, 32), Vector2(64, 64)))

func get_relationship_color(score: float) -> Color:
    if score < -15:
        return Color.RED
    elif score > 30:
        return Color.GOLD
    elif score > 15:
        return Color.GREEN
    else:
        return Color.GRAY
```

**Performance Considerations**:

80-120 talents with sparse relationships is manageable. Worst case (everyone has worked with everyone): 120 * 119 / 2 = 7,140 relationship pairs. At 8 bytes per float, that is ~57KB. Not a problem.

Chemistry calculations (actor pairs) are only evaluated during casting (20-30 times per production). Not a hot path.

Force-directed graph layout runs at 10fps in a background thread, not per-frame. The UI updates when node positions stabilize.

---

### 4.3 The Production Clock (Crisis Event System)

**System Responsibilities**:
- Simulate 15-40 shoot days per production
- Generate 1-5 crisis/opportunity events per day from a weighted deck
- Present decision points to player
- Update film state (morale, budget, scene quality, momentum)

**Event Deck Architecture**:

The event deck is seeded at the start of production based on cast/crew traits, script attributes, budget adequacy, and location quality. Events are NOT purely random — they are weighted draws from categorized pools.

```gdscript
class_name EventDeck extends Node

var crisis_pools: Dictionary = {
    EventCategory.TALENT_CONFLICT: [],
    EventCategory.TECHNICAL_FAILURE: [],
    EventCategory.WEATHER_LOCATION: [],
    EventCategory.CREATIVE_DISAGREEMENT: [],
    EventCategory.BUDGET_OVERRUN: [],
    EventCategory.PERSONAL_CRISIS: [],
    EventCategory.OPPORTUNITY: [],
    EventCategory.BREAKTHROUGH: []
}

var category_weights: Dictionary = {}  # {EventCategory: float weight}

enum EventCategory {
    TALENT_CONFLICT,
    TECHNICAL_FAILURE,
    WEATHER_LOCATION,
    CREATIVE_DISAGREEMENT,
    BUDGET_OVERRUN,
    PERSONAL_CRISIS,
    OPPORTUNITY,
    BREAKTHROUGH
}

func seed_deck(film: Film) -> void:
    # Base weights from design doc
    category_weights[EventCategory.TALENT_CONFLICT] = 0.15
    category_weights[EventCategory.TECHNICAL_FAILURE] = 0.10
    category_weights[EventCategory.WEATHER_LOCATION] = 0.10
    category_weights[EventCategory.CREATIVE_DISAGREEMENT] = 0.20
    category_weights[EventCategory.BUDGET_OVERRUN] = 0.15
    category_weights[EventCategory.PERSONAL_CRISIS] = 0.10
    category_weights[EventCategory.OPPORTUNITY] = 0.15
    category_weights[EventCategory.BREAKTHROUGH] = 0.05

    # Modify weights based on film's cast/crew/script
    for actor in film.cast:
        if actor.ego > 60:
            category_weights[EventCategory.TALENT_CONFLICT] += 0.02
        if actor.reliability < 40:
            category_weights[EventCategory.PERSONAL_CRISIS] += 0.04

    if film.director.vision > 70:
        category_weights[EventCategory.CREATIVE_DISAGREEMENT] += 0.03

    if film.budget_adequacy < 0.70:  # Budget is less than 70% of ideal
        category_weights[EventCategory.TECHNICAL_FAILURE] += 0.03
        category_weights[EventCategory.BUDGET_OVERRUN] += 0.02

    if film.script.is_exterior_heavy:
        category_weights[EventCategory.WEATHER_LOCATION] += 0.05

    if film.morale > 70:
        category_weights[EventCategory.OPPORTUNITY] += 0.03

    # Check for chemistry bonuses (breakthrough potential)
    for i in range(film.cast.size()):
        for j in range(i + 1, film.cast.size()):
            var chemistry = film.cast[i].chemistry_map.get(film.cast[j].id, 0)
            if chemistry > 15:
                category_weights[EventCategory.BREAKTHROUGH] += 0.02

    # Normalize weights to sum to 1.0
    var total = 0.0
    for weight in category_weights.values():
        total += weight
    for category in category_weights:
        category_weights[category] /= total

    # Load event pools from data (JSON files with authored events)
    _load_event_pools()

func draw_event() -> Event:
    # Weighted random selection
    var roll = randf()
    var cumulative = 0.0
    for category in category_weights:
        cumulative += category_weights[category]
        if roll <= cumulative:
            return _draw_from_pool(category)

    # Fallback (should never hit)
    return _draw_from_pool(EventCategory.OPPORTUNITY)

func _draw_from_pool(category: EventCategory) -> Event:
    var pool = crisis_pools[category]
    if pool.is_empty():
        push_warning("Event pool empty for category: %s" % category)
        return null
    return pool.pick_random()
```

**Event Data Structure**:

Events are authored in JSON and loaded at runtime. This allows designers to add/edit events without touching code.

```json
// events/production/talent_conflict_01.json
{
    "id": "talent_conflict_improvisation",
    "category": "TALENT_CONFLICT",
    "title": "Improvisation Dispute",
    "description": "Day {day}. Your lead actor and director are not speaking after yesterday's take dispute. The actor wants to improvise the confession scene. The director insists on the scripted version.",
    "conditions": {
        "actor_has_trait": "METHOD_ACTOR",
        "director_vision": ">65"
    },
    "options": [
        {
            "text": "Side with the actor",
            "effects": {
                "director_morale": -15,
                "director_loyalty": -10,
                "scene_quality_performance": "+5 if actor.skill > 65 else -5"
            }
        },
        {
            "text": "Side with the director",
            "effects": {
                "actor_morale": -15,
                "actor_loyalty": -10,
                "scene_quality_coherence": 5
            }
        },
        {
            "text": "Call a meeting, shoot both versions",
            "effects": {
                "budget": "-3%",
                "director_morale": -5,
                "actor_morale": -5,
                "additional_coverage_options": 2
            }
        }
    ]
}
```

**Event Resolution**:

```gdscript
func resolve_event(event: Event, option_index: int, film: Film) -> void:
    var option = event.options[option_index]

    # Apply effects from JSON
    for effect_key in option.effects:
        match effect_key:
            "actor_morale":
                film.morale += option.effects[effect_key]
            "budget":
                var pct = option.effects[effect_key]
                film.budget_remaining += film.budget_remaining * (float(pct.trim_suffix("%")) / 100.0)
            "scene_quality_performance":
                # Handle conditional effects (e.g., "+5 if actor.skill > 65 else -5")
                var effect_value = _evaluate_conditional_effect(option.effects[effect_key], film)
                film.current_scene.performance_quality += effect_value
            # ... handle all effect types

    # Update momentum
    _update_momentum(film, option)

    # Log for player feedback
    emit_signal("event_resolved", event, option)
```

**Momentum System**:

Momentum is a hidden secondary stat that influences event weights dynamically during production.

```gdscript
func update_momentum(film: Film, event_outcome: String) -> void:
    var delta = 0.0

    match event_outcome:
        "positive":
            delta = 3.0
        "negative":
            delta = -4.0
        "neutral":
            delta = 0.0

    # Morale bonus
    delta += film.morale * 0.1

    # Natural entropy
    delta -= 1.0

    film.momentum = clamp(film.momentum + delta, 0, 100)

    # Adjust event deck weights based on momentum
    if film.momentum > 70:
        event_deck.category_weights[EventCategory.BREAKTHROUGH] += 0.05
    elif film.momentum < 30:
        event_deck.category_weights[EventCategory.TALENT_CONFLICT] += 0.05
        event_deck.category_weights[EventCategory.BUDGET_OVERRUN] += 0.05

    event_deck.normalize_weights()
```

**Performance Target**: Event draw and resolution should complete in <5ms. Event pools are preloaded, not loaded on-demand.

**Decision Fatigue Mitigation**: Every 5th shoot day is a "quiet day" with zero or one decision. Breakthrough events are weighted higher in the second half of production.

---

### 4.4 The Avid Bay (Post-Production Quality Calculation)

**System Responsibilities**:
- Calculate scene card quality from production outcomes
- Apply editorial approach multipliers
- Layer score and color grade modifiers
- Calculate final Film Quality composite score

**Scene Card Data**:

```gdscript
class_name SceneCard extends Resource

var scene_id: int
var scene_name: String

# Quality axes (0-100)
var performance: float
var cinematography: float
var pacing: float
var emotional_impact: float
var coherence: float

# Calculated during production
func calculate_from_shoot(film: Film, scene_index: int) -> void:
    var actor = film.cast[scene_index % film.cast.size()]  # Simplified
    var director = film.director
    var dp = film.dp

    # Performance = Actor Skill + Chemistry + Director guidance
    performance = actor.skill
    if scene_index < film.cast.size() - 1:
        var chemistry = actor.chemistry_map.get(film.cast[scene_index + 1].id, 0)
        performance += chemistry * 0.5
    performance += director.vision * 0.2
    performance = clamp(performance, 0, 100)

    # Cinematography = DP Skill + Budget adequacy + Location
    cinematography = dp.skill
    cinematography += film.budget_adequacy * 20  # Budget impacts visuals heavily
    cinematography += film.location_quality * 0.3
    cinematography = clamp(cinematography, 0, 100)

    # Pacing = Script Structure + Director + Takes
    pacing = film.script.structural_ambition * 0.4
    pacing += director.vision * 0.3
    pacing += (100 - film.average_takes_per_scene) * 0.3  # Fewer takes = tighter pacing
    pacing = clamp(pacing, 0, 100)

    # Emotional Impact = Performance + Thematic Depth
    emotional_impact = performance * 0.6
    emotional_impact += film.script.thematic_depth * 0.4
    emotional_impact = clamp(emotional_impact, 0, 100)

    # Coherence = Script Structure + Editorial execution (applied later)
    coherence = film.script.structural_ambition * 0.5
    coherence += (100 - film.production_deviation) * 0.5  # Less deviation = more coherent
    coherence = clamp(coherence, 0, 100)
```

**Editorial Approach System**:

```gdscript
enum EditorialApproach {
    TIGHT_PROPULSIVE,
    SLOW_MEDITATIVE,
    NONLINEAR,
    MONTAGE_HEAVY,
    NATURALISTIC,
    EDITOR_CHOICE
}

var approach_multipliers = {
    EditorialApproach.TIGHT_PROPULSIVE: {
        "performance": 0.9,
        "cinematography": 0.9,
        "pacing": 1.3,
        "emotional_impact": 0.9,
        "coherence": 1.1
    },
    EditorialApproach.SLOW_MEDITATIVE: {
        "performance": 1.1,
        "cinematography": 1.2,
        "pacing": 0.7,
        "emotional_impact": 1.2,
        "coherence": 1.0
    },
    EditorialApproach.NONLINEAR: {
        "performance": 1.0,
        "cinematography": 1.0,
        "pacing": 0.8,
        "emotional_impact": 1.1,
        "coherence": 0.7  # Risk: +0.3 if editor.skill > 75
    },
    EditorialApproach.MONTAGE_HEAVY: {
        "performance": 0.8,
        "cinematography": 1.3,
        "pacing": 1.1,
        "emotional_impact": 1.0,
        "coherence": 0.8
    },
    EditorialApproach.NATURALISTIC: {
        "performance": 1.3,
        "cinematography": 0.9,
        "pacing": 1.0,
        "emotional_impact": 1.1,
        "coherence": 1.0
    }
}

func apply_editorial_approach(scene_cards: Array[SceneCard], approach: EditorialApproach, editor: Talent) -> void:
    var mults = approach_multipliers[approach]

    # Handle editor skill bonus for NONLINEAR
    if approach == EditorialApproach.NONLINEAR and editor.skill > 75:
        mults["coherence"] += 0.3

    # Apply multipliers to all scene cards
    for card in scene_cards:
        card.performance *= mults["performance"]
        card.cinematography *= mults["cinematography"]
        card.pacing *= mults["pacing"]
        card.emotional_impact *= mults["emotional_impact"]
        card.coherence *= mults["coherence"]

        # Clamp after multiplication
        card.performance = clamp(card.performance, 0, 100)
        card.cinematography = clamp(card.cinematography, 0, 100)
        card.pacing = clamp(card.pacing, 0, 100)
        card.emotional_impact = clamp(card.emotional_impact, 0, 100)
        card.coherence = clamp(card.coherence, 0, 100)

func apply_score(scene_cards: Array[SceneCard], composer: Talent) -> void:
    var score_modifier = composer.skill * 0.15
    for card in scene_cards:
        card.emotional_impact += score_modifier
        card.pacing += score_modifier * 0.5
        card.emotional_impact = clamp(card.emotional_impact, 0, 100)
        card.pacing = clamp(card.pacing, 0, 100)

func apply_color_grade(scene_cards: Array[SceneCard], colorist: Talent) -> void:
    var grade_modifier = colorist.skill * 0.10
    for card in scene_cards:
        card.cinematography += grade_modifier
        card.emotional_impact += grade_modifier * 0.3
        card.cinematography = clamp(card.cinematography, 0, 100)
        card.emotional_impact = clamp(card.emotional_impact, 0, 100)
```

**Final Film Quality Calculation**:

```gdscript
func calculate_film_quality(scene_cards: Array[SceneCard]) -> float:
    var avg_performance = 0.0
    var avg_cinematography = 0.0
    var avg_pacing = 0.0
    var avg_emotional_impact = 0.0
    var avg_coherence = 0.0

    for card in scene_cards:
        avg_performance += card.performance
        avg_cinematography += card.cinematography
        avg_pacing += card.pacing
        avg_emotional_impact += card.emotional_impact
        avg_coherence += card.coherence

    var count = float(scene_cards.size())
    avg_performance /= count
    avg_cinematography /= count
    avg_pacing /= count
    avg_emotional_impact /= count
    avg_coherence /= count

    # Weighted composite (matches design doc)
    var film_quality = (avg_performance * 0.30) + \
                       (avg_cinematography * 0.15) + \
                       (avg_pacing * 0.20) + \
                       (avg_emotional_impact * 0.20) + \
                       (avg_coherence * 0.15)

    return clamp(film_quality, 0, 100)
```

**UI Feedback**: Scene cards are displayed as timeline elements with colored quality bars. When an editorial approach is selected, the bars animate to show multiplier effects. The player sees exactly what shifts.

---

### 4.5 The Festival Circuit (Jury Simulation & Outcome Generation)

**System Responsibilities**:
- Simulate 5 major festivals with distinct taste profiles
- Score films against jury preferences and competition
- Generate outcomes (prizes, reception, distribution offers)
- Calculate reputation and financial impacts

**Festival Data**:

```gdscript
class_name Festival extends Resource

var name: String
var prestige_value: int          # 70-100
var distribution_deal_density: float  # How many buyers attend
var submission_cost: int
var jury_taste_profile: Dictionary    # {attribute: weight}
var reputation_threshold: int    # Min reputation to access

# Example: Sundance
static func create_sundance() -> Festival:
    var f = Festival.new()
    f.name = "Sundance"
    f.prestige_value = 80
    f.distribution_deal_density = 0.85  # High
    f.submission_cost = 3000
    f.reputation_threshold = 0
    f.jury_taste_profile = {
        "emotional_impact": 0.30,
        "performance": 0.25,
        "pacing": 0.20,
        "cinematography": 0.10,
        "thematic_depth": 0.15
    }
    return f

# Example: Cannes
static func create_cannes() -> Festival:
    var f = Festival.new()
    f.name = "Cannes"
    f.prestige_value = 100
    f.distribution_deal_density = 0.60
    f.submission_cost = 5000
    f.reputation_threshold = 20
    f.jury_taste_profile = {
        "cinematography": 0.35,
        "thematic_depth": 0.25,
        "structural_ambition": 0.20,  # From script
        "emotional_impact": 0.10,
        "performance": 0.10
    }
    # Anti-commercial bias
    f.commercial_viability_penalty = -0.5  # Deduct points for high commercial viability
    return f
```

**Jury Scoring System**:

```gdscript
func calculate_festival_score(film: Film, festival: Festival, studio: Studio) -> float:
    var film_attributes = {
        "performance": film.avg_performance,
        "cinematography": film.avg_cinematography,
        "pacing": film.avg_pacing,
        "emotional_impact": film.avg_emotional_impact,
        "coherence": film.avg_coherence,
        "thematic_depth": film.script.thematic_depth,
        "structural_ambition": film.script.structural_ambition
    }

    # Taste alignment score
    var taste_alignment = 0.0
    for attribute in festival.jury_taste_profile:
        var film_value = film_attributes.get(attribute, 50.0)  # Default 50 if missing
        var weight = festival.jury_taste_profile[attribute]
        taste_alignment += film_value * weight

    # Cannes anti-commercial penalty
    if festival.name == "Cannes" and film.script.commercial_viability > 60:
        taste_alignment += film.script.commercial_viability * festival.commercial_viability_penalty

    # Buzz modifier
    var buzz = 0.0
    for actor in film.cast:
        buzz += actor.reputation * 0.1
    buzz += studio.reputation * 0.5
    buzz += film.marketing_spend * 0.002  # $1K marketing = +2 buzz
    buzz = clamp(buzz, 0, 30)

    # Final score: 60% quality, 30% taste alignment, 10% buzz
    var final_score = (film.quality * 0.6) + (taste_alignment * 0.3) + (buzz * 0.1)

    return clamp(final_score, 0, 100)
```

**Competition Simulation**:

The player's film competes against 30-50 simulated competitor films. Competitor films are lightweight — just a quality score and a genre.

```gdscript
func generate_competition(festival: Festival, year: int) -> Array:
    var competitors = []
    var count = randi_range(30, 50)

    for i in range(count):
        var comp_film = {
            "title": "Competitor Film %d" % i,
            "quality": randf_range(40, 90),  # Gaussian around 65 would be better
            "genre": ["Drama", "Comedy", "Thriller", "Documentary"].pick_random()
        }
        competitors.append(comp_film)

    return competitors

func determine_outcome(film_score: float, competition: Array) -> FestivalOutcome:
    # Sort competition by score
    competition.sort_custom(func(a, b): return a.quality > b.quality)

    # Add player's film to the list
    var all_films = competition.duplicate()
    all_films.append({"quality": film_score})
    all_films.sort_custom(func(a, b): return a.quality > b.quality)

    # Find player's percentile
    var player_rank = 0
    for i in range(all_films.size()):
        if all_films[i].get("quality") == film_score:
            player_rank = i
            break

    var percentile = float(player_rank) / float(all_films.size())

    # Map percentile to outcome (from design doc)
    if percentile <= 0.05:
        return FestivalOutcome.GRAND_PRIZE
    elif percentile <= 0.15:
        return FestivalOutcome.JURY_PRIZE
    elif percentile <= 0.40:
        return FestivalOutcome.POSITIVE_RECEPTION
    elif percentile <= 0.70:
        return FestivalOutcome.MIXED_RECEPTION
    elif percentile <= 0.95:
        return FestivalOutcome.COLD_RECEPTION
    else:
        return FestivalOutcome.WALKOUT

enum FestivalOutcome {
    GRAND_PRIZE,      # Top 5%
    JURY_PRIZE,       # Top 15%
    POSITIVE_RECEPTION, # Top 40%
    MIXED_RECEPTION,  # 40-70%
    COLD_RECEPTION,   # 70-95%
    WALKOUT           # Bottom 5%
}
```

**Outcome Application**:

```gdscript
func apply_festival_outcome(outcome: FestivalOutcome, film: Film, studio: Studio) -> void:
    match outcome:
        FestivalOutcome.GRAND_PRIZE:
            studio.reputation += 25
            film.distribution_multiplier = 3.0
            for talent in film.cast + [film.director]:
                talent.studio_relationship += 15
            _generate_press_quotes(film, "ecstatic")

        FestivalOutcome.JURY_PRIZE:
            studio.reputation += 15
            film.distribution_multiplier = 2.0
            for talent in film.cast + [film.director]:
                talent.studio_relationship += 8
            _generate_press_quotes(film, "positive")

        FestivalOutcome.POSITIVE_RECEPTION:
            studio.reputation += 5
            film.distribution_multiplier = 1.5
            _generate_press_quotes(film, "warm")

        FestivalOutcome.MIXED_RECEPTION:
            # No change
            _generate_press_quotes(film, "mixed")

        FestivalOutcome.COLD_RECEPTION:
            studio.reputation -= 5
            film.distribution_multiplier = 0.7
            _generate_press_quotes(film, "cold")

        FestivalOutcome.WALKOUT:
            studio.reputation -= 15
            film.distribution_multiplier = 0.3
            for talent in film.cast + [film.director]:
                talent.studio_relationship -= 10
            film.walkout_stigma = true  # Haunts you for 2 projects
            _generate_press_quotes(film, "scathing")

    emit_signal("festival_outcome_applied", film, outcome)
```

**Press Quote Generation**:

Similar to coverage reports, press quotes are assembled from phrase libraries based on film attributes and outcome.

```gdscript
var press_phrases = {
    "ecstatic": [
        "A stunning achievement.",
        "The film of the festival.",
        "Visionary and unforgettable.",
        "This is what cinema can be."
    ],
    "positive": [
        "A strong, assured work.",
        "Impressive craft and genuine heart.",
        "Well worth your time."
    ],
    "mixed": [
        "Ambitious but uneven.",
        "Moments of brilliance amid stretches of tedium.",
        "Your mileage may vary."
    ],
    "scathing": [
        "A baffling misfire.",
        "What were they thinking?",
        "An endurance test for all the wrong reasons."
    ]
}

func _generate_press_quotes(film: Film, tone: String) -> void:
    var quotes = []
    for i in range(3):
        quotes.append(press_phrases[tone].pick_random())
    film.press_quotes = quotes
```

---

### 4.6 The Ledger (Financial Simulation)

**System Responsibilities**:
- Track all cash flows (revenue, expenses, investments)
- Calculate runway (months until bankruptcy)
- Generate distribution deal offers based on festival outcomes
- Simulate multi-year financial projections

**Studio Financial State**:

```gdscript
class_name Studio extends Resource

# Current state
var cash: int = 500_000          # Starting seed funding
var credit_line_max: int = 250_000
var credit_line_used: int = 0
var credit_interest_rate: float = 0.12  # Annual

# Ongoing costs
var monthly_operating_cost: int = 8_000
var operating_cost_inflation: float = 0.05  # Per year

# Income tracking
var total_revenue_lifetime: int = 0
var total_expenses_lifetime: int = 0

# Year tracking
var current_year: int = 1

func calculate_runway() -> float:
    var available_funds = cash + (credit_line_max - credit_line_used)
    var months = float(available_funds) / float(monthly_operating_cost)
    return months

func advance_month() -> void:
    # Deduct operating costs
    cash -= monthly_operating_cost
    total_expenses_lifetime += monthly_operating_cost

    # Accrue credit interest (monthly)
    if credit_line_used > 0:
        var monthly_interest = credit_line_used * (credit_interest_rate / 12.0)
        credit_line_used += int(monthly_interest)
        credit_line_used = mini(credit_line_used, credit_line_max)

    # Check for bankruptcy
    if cash < 0:
        if credit_line_used < credit_line_max:
            # Draw from credit line
            var needed = abs(cash)
            var available = credit_line_max - credit_line_used
            var draw = mini(needed, available)
            credit_line_used += draw
            cash += draw
        else:
            # Bankruptcy
            emit_signal("bankruptcy")

func advance_year() -> void:
    current_year += 1
    # Operating cost inflation
    monthly_operating_cost = int(monthly_operating_cost * (1.0 + operating_cost_inflation))
```

**Distribution Deal Generation**:

```gdscript
func generate_distribution_deal(film: Film, festival_outcome: FestivalOutcome) -> DistributionDeal:
    var base_advance = film.quality * 1000  # $1K per quality point
    base_advance *= film.distribution_multiplier  # Festival outcome modifier

    # Genre modifiers
    if film.script.genre == "Horror":
        base_advance *= 1.2  # Horror is easier to sell
    if film.script.commercial_viability < 30:
        base_advance *= 0.7  # Arthouse is harder

    var deal = DistributionDeal.new()

    # High advance / low split option
    deal.option_a_advance = int(base_advance * 1.5)
    deal.option_a_split = 0.20  # Studio gets 20% of gross

    # Low advance / high split option
    deal.option_b_advance = int(base_advance * 0.5)
    deal.option_b_split = 0.40  # Studio gets 40% of gross

    # Self-distribution (no advance, high split, but marketing costs)
    deal.option_c_advance = 0
    deal.option_c_split = 0.75  # Studio keeps 75%, but pays marketing
    deal.option_c_marketing_cost = int(base_advance * 0.3)

    return deal

class_name DistributionDeal extends Resource
var option_a_advance: int
var option_a_split: float
var option_b_advance: int
var option_b_split: float
var option_c_advance: int
var option_c_split: float
var option_c_marketing_cost: int
```

**Revenue Simulation**:

Distribution revenue arrives over 6-18 months post-release. We simulate this with a delayed revenue system.

```gdscript
class_name RevenueStream extends Resource
var film_id: int
var source: RevenueSource
var total_amount: int
var months_to_pay: int
var paid_so_far: int = 0

enum RevenueSource { THEATRICAL, VOD, DVD, INTERNATIONAL, FESTIVAL_PRIZE }

func tick_month(studio: Studio) -> void:
    if paid_so_far < total_amount:
        var monthly_payment = total_amount / months_to_pay
        studio.cash += monthly_payment
        studio.total_revenue_lifetime += monthly_payment
        paid_so_far += monthly_payment
        emit_signal("revenue_received", source, monthly_payment)
```

Each film generates multiple revenue streams:

```gdscript
func generate_revenue_streams(film: Film, deal: DistributionDeal, option_chosen: int) -> Array[RevenueStream]:
    var streams = []

    # Advance payment (immediate)
    var advance_stream = RevenueStream.new()
    advance_stream.film_id = film.id
    advance_stream.source = RevenueStream.RevenueSource.THEATRICAL
    advance_stream.total_amount = deal.get_advance(option_chosen)
    advance_stream.months_to_pay = 1  # Immediate
    streams.append(advance_stream)

    # Theatrical revenue (3-6 months)
    var theatrical_gross = estimate_theatrical_gross(film)
    var theatrical_stream = RevenueStream.new()
    theatrical_stream.film_id = film.id
    theatrical_stream.source = RevenueStream.RevenueSource.THEATRICAL
    theatrical_stream.total_amount = int(theatrical_gross * deal.get_split(option_chosen))
    theatrical_stream.months_to_pay = randi_range(3, 6)
    streams.append(theatrical_stream)

    # VOD/Cable (6-12 months)
    var vod_gross = estimate_vod_gross(film)
    var vod_stream = RevenueStream.new()
    vod_stream.film_id = film.id
    vod_stream.source = RevenueStream.RevenueSource.VOD
    vod_stream.total_amount = int(vod_gross * deal.get_split(option_chosen))
    vod_stream.months_to_pay = randi_range(6, 12)
    streams.append(vod_stream)

    # DVD (4-8 months, declining over time due to DVD collapse)
    var dvd_gross = estimate_dvd_gross(film, studio.current_year)
    var dvd_stream = RevenueStream.new()
    dvd_stream.film_id = film.id
    dvd_stream.source = RevenueStream.RevenueSource.DVD
    dvd_stream.total_amount = int(dvd_gross * deal.get_split(option_chosen))
    dvd_stream.months_to_pay = randi_range(4, 8)
    streams.append(dvd_stream)

    return streams

func estimate_theatrical_gross(film: Film) -> int:
    var base = film.quality * 2000  # $2K per quality point
    base *= film.distribution_multiplier
    # Star power
    for actor in film.cast:
        base += actor.reputation * 100
    return int(base * randf_range(0.7, 1.3))  # Variance

func estimate_dvd_gross(film: Film, year: int) -> int:
    var base = film.quality * 800
    # DVD decline after year 3
    if year >= 3:
        var decline_factor = pow(0.92, year - 2)  # 8% decline per year
        base *= decline_factor
    # Horror/cult bonus
    if film.script.genre in ["Horror", "Thriller"]:
        base *= 1.4
    return int(base * randf_range(0.6, 1.4))
```

**Financial Projections UI**:

The Ledger displays a runway bar and a 12-month rolling cash flow projection.

```gdscript
func calculate_cash_flow_projection(studio: Studio, months: int) -> Array:
    var projection = []
    var projected_cash = studio.cash

    for month in range(months):
        # Deduct operating costs
        projected_cash -= studio.monthly_operating_cost

        # Add expected revenue from active streams
        for stream in studio.active_revenue_streams:
            if stream.months_to_pay > 0:
                projected_cash += stream.total_amount / stream.months_to_pay

        projection.append(projected_cash)

    return projection
```

---

## 5. AI and Simulation Systems

### 5.1 Talent Agent AI (Career Decision Making)

Talents are agents that make autonomous decisions when not directly managed by the player. Key decisions:
- Accept or reject casting offers from rival studios
- Leave for Hollywood if reputation grows too high
- Demand salary increases after success
- Pitch passion projects to the player

**Agent Decision Logic**:

```gdscript
func talent_evaluate_external_offer(talent: Talent, offer: CastingOffer) -> bool:
    # Factors: salary, project prestige, relationship with offering studio, ambition
    var acceptance_score = 0.0

    # Salary weight
    var salary_ratio = float(offer.salary) / float(talent.calculate_fair_ask())
    acceptance_score += salary_ratio * 30.0

    # Prestige weight
    if offer.project_quality > 70:
        acceptance_score += 20.0

    # Ambition drives leaving
    if talent.ambition > 70:
        acceptance_score += 10.0

    # Loyalty reduces leaving
    if talent.studio_relationship > 30:
        acceptance_score -= talent.studio_relationship * 0.5

    # Trait modifiers
    if Trait.LOYAL in talent.traits:
        acceptance_score -= 20.0
    if Trait.MERCENARY in talent.traits:
        acceptance_score += 15.0

    # Decision threshold
    return acceptance_score > 50.0
```

**Rival Studio Offers**:

If the "Rival Studio" stretch feature is active, AI studios generate competing offers for top talent.

```gdscript
func rival_studio_poach_attempt(talent: Talent, player_studio: Studio) -> void:
    # Only target talent with high skill and recent success
    if talent.skill < 65 or talent.recent_success_modifier < 10:
        return

    # Generate competitive offer
    var rival_offer = CastingOffer.new()
    rival_offer.salary = talent.calculate_fair_ask() * 1.3  # 30% premium
    rival_offer.project_quality = randf_range(60, 85)

    # Does talent leave?
    if talent_evaluate_external_offer(talent, rival_offer):
        talent.availability = false
        talent.studio_relationship -= 15  # Sting of betrayal
        emit_signal("talent_poached", talent)
```

### 5.2 Festival Jury Simulation

Jury taste shifts 10-20% per year to simulate changing cultural winds. This prevents the player from optimizing a single formula.

```gdscript
func shift_jury_tastes(festival: Festival, year: int) -> void:
    # Randomly select 1-2 attributes to shift
    var attributes_to_shift = festival.jury_taste_profile.keys()
    attributes_to_shift.shuffle()

    for i in range(randi_range(1, 2)):
        var attribute = attributes_to_shift[i]
        var shift = randf_range(-0.15, 0.15)
        festival.jury_taste_profile[attribute] += shift
        festival.jury_taste_profile[attribute] = clamp(festival.jury_taste_profile[attribute], 0.05, 0.50)

    # Renormalize weights
    var total = 0.0
    for weight in festival.jury_taste_profile.values():
        total += weight
    for attribute in festival.jury_taste_profile:
        festival.jury_taste_profile[attribute] /= total
```

### 5.3 Relationship Decay and Maintenance

Relationships decay over time if not maintained (reflecting real-world networking).

```gdscript
func decay_relationships(talent_pool: TalentPool, months_passed: int) -> void:
    for talent in talent_pool.talents:
        # Studio relationship decays 1 point per 6 months of no contact
        if talent.months_since_last_project > 6:
            talent.studio_relationship -= 1
            talent.studio_relationship = max(talent.studio_relationship, -50)

        talent.months_since_last_project += months_passed
```

**Maintenance Events**:

Player can invest in relationship maintenance (parties, lunches, check-ins). These are triggered events, not direct actions.

---

## 6. Save System Design

### 6.1 Save Data Structure

The save file must capture full simulation state. This is a data-heavy game — everything matters.

**Save File Contents**:
- Studio state (finances, reputation, slate, year, season)
- All 80-120 talents (full stats, relationships, availability, career state)
- All completed films (archive with outcomes, reviews, revenue)
- Current film in-progress (phase, decisions made, scene cards, event history)
- Active revenue streams (pending payments)
- Festival jury taste profiles (historical tracking for strategy)
- Event deck state (which events have already fired)
- Player decisions log (for analytics and emergent narrative)

**Serialization Strategy**:

Godot's native `Resource` system supports serialization. All game state objects extend `Resource`.

```gdscript
func save_game(save_path: String) -> void:
    var save_data = {
        "version": "1.0",
        "studio": studio.to_dict(),
        "talent_pool": talent_pool.to_dict(),
        "completed_films": [],
        "current_film": current_film.to_dict() if current_film else null,
        "revenue_streams": [],
        "festivals": {},
        "event_deck_state": event_system.to_dict(),
        "decision_log": decision_log
    }

    # Serialize completed films
    for film in completed_films:
        save_data.completed_films.append(film.to_dict())

    # Serialize revenue streams
    for stream in active_revenue_streams:
        save_data.revenue_streams.append(stream.to_dict())

    # Serialize festival states
    for festival_name in festivals:
        save_data.festivals[festival_name] = festivals[festival_name].to_dict()

    # Write to disk
    var file = FileAccess.open(save_path, FileAccess.WRITE)
    if file:
        file.store_string(JSON.stringify(save_data, "\t"))
        file.close()
    else:
        push_error("Failed to write save file: %s" % save_path)

func load_game(save_path: String) -> bool:
    var file = FileAccess.open(save_path, FileAccess.READ)
    if not file:
        push_error("Failed to open save file: %s" % save_path)
        return false

    var json_text = file.get_as_text()
    file.close()

    var json = JSON.new()
    var parse_result = json.parse(json_text)
    if parse_result != OK:
        push_error("Failed to parse save file JSON")
        return false

    var save_data = json.data

    # Deserialize studio
    studio = Studio.from_dict(save_data.studio)

    # Deserialize talent pool
    talent_pool = TalentPool.from_dict(save_data.talent_pool)

    # Deserialize films
    completed_films.clear()
    for film_dict in save_data.completed_films:
        completed_films.append(Film.from_dict(film_dict))

    # Deserialize current film
    if save_data.current_film:
        current_film = Film.from_dict(save_data.current_film)

    # ... deserialize remaining state

    return true
```

**Save File Size Estimation**:

- Studio state: ~2KB
- 120 talents with relationships: ~200KB (worst case with full relationship graph)
- 20 completed films: ~100KB
- Current film state: ~10KB
- Revenue streams: ~5KB
- Misc: ~10KB

**Total per save: ~330KB**. Manageable. Compressed, this would be <100KB.

### 6.2 Autosave Strategy

Autosave at phase transitions (entering Greenlight, entering Production, etc.). The player can manually save at any time.

```gdscript
func _on_phase_changed(new_phase: GamePhase) -> void:
    # Autosave on every phase transition
    var autosave_path = "user://autosave.sav"
    save_game(autosave_path)
```

**Save Slot System**: 5 manual save slots + 1 autosave slot. The UI shows save metadata (studio name, year, season, last film title, timestamp).

### 6.3 Save Compatibility and Versioning

Save files include a version number. When loading, check version and migrate if needed.

```gdscript
func load_game_with_migration(save_path: String) -> bool:
    var save_data = _load_json(save_path)
    if not save_data:
        return false

    var version = save_data.get("version", "0.0")

    # Version migration
    if version == "0.9":
        # Migrate 0.9 -> 1.0 (example: add new studio field)
        save_data.studio["artistic_identity"] = 50.0
        save_data.version = "1.0"

    # Deserialize
    return _deserialize(save_data)
```

**Design principle**: Never break saves. Always migrate forward. Saves are player investment.

---

## 7. Performance Budget and Optimization Strategy

### 7.1 Performance Targets

| Metric | Target | Rationale |
|---|---|---|
| **Frame Rate** | 60 FPS | UI-driven game; no excuse for frame drops |
| **Frame Budget** | 16.67ms | 60 FPS = 16.67ms per frame |
| **Logic Budget** | 2ms | Simulation step (per frame) |
| **UI Update Budget** | 4ms | Rendering UI elements and text |
| **Input Response** | <100ms | Player clicks -> visible feedback |
| **Scene Transition** | <300ms | Phase transition should feel instant |
| **Save/Load Time** | <2 seconds | Acceptable wait for file I/O |

### 7.2 Known Bottlenecks and Mitigation

**Bottleneck 1: Relationship Graph Lookups**

With 120 talents, worst-case relationship queries could be O(n^2) if naive.

**Mitigation**: Sparse adjacency dictionary (only store non-zero relationships). Lookups are O(1) hash table access. Most talents have <10 relationships.

**Bottleneck 2: Procedural Text Generation**

Assembling coverage reports and press quotes involves string concatenation and random selection from large phrase pools.

**Mitigation**: Precompute all phrase lists at startup. Use string builder patterns (Godot's `String` concatenation is optimized, but still worth profiling). If coverage generation takes >50ms, cache generated scripts between sessions.

**Bottleneck 3: Event Deck Reweighting**

Adjusting event weights and renormalizing every production day could add up.

**Mitigation**: Only reweight when Momentum crosses thresholds (30, 70). Otherwise, use cached weights.

**Bottleneck 4: Festival Competition Simulation**

Sorting 50 films and calculating percentile per festival submission.

**Mitigation**: 50 elements is trivial. Even bubble sort would be <1ms. Use built-in sort. Not a concern.

**Bottleneck 5: UI Redraw (Talent Web Visualization)**

Force-directed graph layout can be expensive if recalculated every frame.

**Mitigation**: Run layout algorithm in a background thread at 10fps. The UI interpolates node positions smoothly. The player does not notice the lower update rate because the graph "settles" over time naturally.

### 7.3 Profiling Strategy

Do NOT optimize before profiling. Build the systems. Ship the prototype. Then profile.

**Profiling Tools**:
- Godot's built-in profiler (CPU, frame time, memory)
- Custom instrumentation for hot paths (manual timing with `Time.get_ticks_usec()`)

**Profiling Priorities**:
1. Full production cycle (Greenlight -> Release) under profiler
2. Talent Web with 120 agents at max relationship density
3. Save/load with 20+ completed films
4. Festival competition with 50 rival films

If any of these exceed budget, optimize. Otherwise, ship it.

---

## 8. Platform Considerations

### 8.1 PC (Steam) — Primary Platform

**Target Specs**:
- **Minimum**: Intel i5 (2019), 8GB RAM, integrated graphics, 1280x720
- **Recommended**: Intel i7 or equivalent, 16GB RAM, any GPU, 1920x1080

**Input**: Mouse and keyboard. This is a mouse-driven UI game. Keyboard shortcuts for power users (Tab to cycle UI panels, Enter to confirm, Esc to back out).

**Resolution**: Support 1280x720 up to 3840x2160 (4K). UI scales with DPI. Text rendering is vector-based (Godot's default font rendering is good enough).

**Steam Features**:
- **Cloud Saves**: Sync save files via Steam Cloud
- **Achievements**: Track milestones (first festival win, first bankruptcy recovery, 10 films completed, Palme d'Or win, etc.)
- **Trading Cards** (maybe): Low priority, but could be fun for a film-themed game

**Build Size**: Target <500MB. Godot exports are lean. Assets are minimal (2D UI textures, fonts, no 3D models).

### 8.2 Nintendo Switch — Secondary Platform

**Viability**: Management sims perform well on Switch (Game Dev Tycoon, Two Point Hospital both sold well). The session length (60-90 min) fits portable play.

**Input**: Controller support required. UI must adapt.
- Left stick: Navigate UI panels
- Right stick: Scroll content
- A button: Confirm
- B button: Cancel
- Shoulder buttons: Cycle tabs

**Resolution**: 1280x720 handheld, 1920x1080 docked. UI must be readable at 720p on a 6.2" screen. Minimum font size: 16pt.

**Performance**: Switch CPU is weaker than 2019 laptops. Target 30 FPS as acceptable fallback if 60 FPS proves difficult. The game is not twitch-based, so 30 FPS is fine.

**Porting Effort**: Godot exports to Switch via official SDK (requires Nintendo developer status). Estimate 2-4 weeks for controller UI adaptation and performance tuning.

### 8.3 Mobile (iPad) — Stretch Target

**Not Recommended for v1.0**. The UI density is high — lots of text, small interactive elements, multi-panel layouts. Adapting this to touch without rebuilding the UI from scratch is risky.

**If pursued**: Target iPad only (iPhone screen is too small). Rethink the UI as a touch-first interface (larger buttons, swipe gestures, simplified Talent Web).

---

## 9. Build Pipeline and Tools

### 9.1 Build Automation

**GitHub Actions Workflow**:

```yaml
# .github/workflows/build.yml
name: Build BACKLOT

on:
  push:
    branches: [develop, main]
  pull_request:
    branches: [develop]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Setup Godot
        uses: chickensoft-games/setup-godot@v1
        with:
          version: 4.2.0

      - name: Export Windows
        run: godot --headless --export "Windows Desktop" builds/backlot_win.exe

      - name: Export Linux
        run: godot --headless --export "Linux/X11" builds/backlot_linux.x86_64

      - name: Export macOS
        run: godot --headless --export "macOS" builds/backlot_mac.zip

      - name: Run Smoke Tests
        run: godot --headless --script tests/smoke_test.gd

      - name: Upload Artifacts
        uses: actions/upload-artifact@v3
        with:
          name: builds
          path: builds/*
```

**Smoke Test Suite**:

Basic validation that the game boots and core systems function.

```gdscript
# tests/smoke_test.gd
extends SceneTree

func _init():
    print("Running smoke tests...")

    # Test 1: Load game scene
    var main_scene = load("res://scenes/main.tscn").instantiate()
    assert(main_scene != null, "Main scene failed to load")

    # Test 2: Initialize studio
    var game_state = GameStateManager.new()
    game_state.initialize_new_game("Test Studio")
    assert(game_state.studio.cash == 500_000, "Studio initialization failed")

    # Test 3: Generate scripts
    var scripts = ScriptGenerator.generate_scripts(20)
    assert(scripts.size() >= 3, "Script generation failed")
    assert(scripts[0].coverage_text.length() > 50, "Coverage text is empty")

    # Test 4: Save and load
    game_state.save_game("user://smoke_test.sav")
    var loaded = game_state.load_game("user://smoke_test.sav")
    assert(loaded, "Save/load failed")

    print("All smoke tests passed!")
    quit()
```

### 9.2 Data Authoring Tools

**Script Template Editor**:

A simple in-engine tool for designers to write and test script generation templates without touching code.

```gdscript
# tools/script_template_editor.gd
extends Control

@onready var template_input = $TemplateInput
@onready var preview_output = $PreviewOutput

func _on_generate_preview_pressed():
    var template = template_input.text
    var generated_logline = ScriptGenerator.apply_template(template)
    preview_output.text = generated_logline
```

**Event Deck Editor**:

Edit event JSON files in-engine with validation.

```gdscript
# tools/event_editor.gd
extends Control

func _on_load_event_pressed():
    var file_path = event_file_dialog.current_path
    var event = load_event_json(file_path)
    populate_editor(event)

func _on_save_event_pressed():
    var event = extract_event_from_editor()
    save_event_json(event, current_file_path)
```

**Balance Spreadsheet Importer**:

Designers work in Google Sheets for balance (talent stats, financial targets, etc.). Export as CSV, import into the game.

```gdscript
func import_talent_csv(csv_path: String) -> void:
    var file = FileAccess.open(csv_path, FileAccess.READ)
    var line_num = 0
    while not file.eof_reached():
        var line = file.get_csv_line()
        if line_num == 0:
            line_num += 1
            continue  # Skip header

        var talent = Talent.new()
        talent.name = line[0]
        talent.role = Talent.TalentRole[line[1]]
        talent.skill = float(line[2])
        talent.ego = float(line[3])
        # ... parse remaining columns

        talent_pool.add_talent(talent)
        line_num += 1
    file.close()
```

### 9.3 Localization

**Not in v1.0**. English only for initial release.

**If pursued post-launch**: Godot's built-in localization system is solid. All UI text is already externalized (stored in JSON/CSV for procedural generation). Translation is straightforward.

**Challenge**: Procedural text generation (coverage reports, press quotes) is English-specific. Grammatical templates do not translate cleanly. Either:
1. Author separate phrase libraries per language (expensive)
2. Use simpler, less nuanced text generation for non-English (acceptable compromise)

---

## 10. Technical Risk Assessment

### 10.1 High-Risk Areas

**Risk: Procedural Script Quality (HIGH)**

**Impact**: If coverage reports feel generic or algorithmic, the Greenlight Table — the game's thesis mechanic — fails. Players do not engage. The game is dead.

**Mitigation**:
- Playtest P0: Coverage report quality must be validated in Week 1-2
- Budget 40-60 hours of writer time (not programmer time) on phrase library
- Have template-based assembly, NOT pure procedural generation
- If testing reveals hollowness, pivot to a smaller pool of fully authored scripts (100-150 pre-written scripts instead of infinite procedural)

**Likelihood**: Medium. This is a content quality problem, not a technical problem. Solvable with authorship.

**Risk: Decision Fatigue in Production Clock (MEDIUM)**

**Impact**: If players burn out by day 15 of a 30-day shoot, they disengage. Production becomes a slog. Session length collapses.

**Mitigation**:
- Playtest P0: Production pacing must be validated in Week 2-3
- "Quiet day" every 5 days (zero or one decision)
- Crisis event categories cannot repeat more than twice in a row
- If testing reveals fatigue, compress to week-by-week decisions (7-10 decision points per production instead of 30)

**Likelihood**: Medium. Solvable with pacing tuning. The fallback (weekly decisions) is well-understood.

**Risk: Talent Web Overwhelm (MEDIUM)**

**Impact**: If 120 talents feels like spreadsheet management instead of relationship building, players avoid the Talent Web entirely. Casting becomes stat optimization, not social strategy.

**Mitigation**:
- Playtest P1: Talent Web readability in Week 3-4
- Agent Recommendation system filters 120 talents down to 3-5 suggestions per role
- UI only shows first- and second-degree connections (not the full graph)
- If testing reveals overwhelm, reduce active talent count to 60-80

**Likelihood**: Low-Medium. The design includes filtering systems. Risk is UI clarity, not system design.

**Risk: Save File Bloat (LOW)**

**Impact**: After 20+ films, save files become multi-MB. Load times increase. Players complain.

**Mitigation**:
- Completed films archive metadata only (not full event history)
- Compress save files (Godot supports this natively)
- Max save size estimate: 500KB uncompressed, <150KB compressed

**Likelihood**: Low. The math shows this is not a concern unless the player completes 50+ films, which is unlikely in normal play.

**Risk: Festival Scoring Feels Random (MEDIUM)**

**Impact**: If players cannot understand why their film won or lost, they disengage from the festival system. Strategy collapses into hope.

**Mitigation**:
- Post-festival feedback shows score breakdown (taste alignment, quality, buzz)
- Coverage reports hint at festival fit ("This feels like a Cannes film")
- Jury taste profiles shift slowly (10-20% per year), not wildly

**Likelihood**: Low. The design includes feedback systems. Risk is UI communication.

### 10.2 Medium-Risk Areas

**Risk: Godot 4.x Stability**

**Impact**: Godot 4.x is relatively new (stable as of 4.2+, but younger than Unity/Unreal). Bugs in core systems (UI, serialization) could block development.

**Mitigation**:
- Use LTS release (4.2 or later)
- Avoid bleeding-edge features
- Prototype core systems (save/load, UI panels) in Week 1 to validate stability

**Likelihood**: Low. Godot 4.2+ is production-ready. Thousands of games ship on it.

**Risk: Controller UI Adaptation for Switch**

**Impact**: The UI is designed for mouse. Controller navigation could feel clunky. Porting effort balloons.

**Mitigation**:
- Design UI with controller in mind from the start (tab order, panel focus, button hints)
- Test with gamepad on PC early
- Budget 2-4 weeks for Switch port

**Likelihood**: Low-Medium. Manageable with early planning.

### 10.3 Low-Risk Areas

**Performance**: The game is logic-heavy but not computationally intensive. 60 FPS on a 2019 laptop is achievable.

**Scope Creep**: The feature pillars are locked. Stretch goals are clearly marked. The design is well-bounded.

**Team Size**: 2 programmers + 1 tech artist is sufficient for 6-8 months of core loop development. Not understaffed.

---

## 11. Development Milestones (Tech Perspective)

### 11.1 Milestone 1: Vertical Slice (Weeks 1-8)

**Goal**: One complete production cycle playable end-to-end. Greenlight -> Pre-Production -> Production -> Post -> Festival.

**Deliverables**:
- Game state machine (all phases functional)
- Greenlight Table with 20 procedural scripts (template-based)
- Casting system with 20 talents (simplified relationship graph)
- Production Clock with 10-day simplified shoot (5 crisis events)
- Avid Bay with editorial approach selection
- Festival submission with outcome generation (Sundance only)
- Save/load functional
- Basic UI (functional, not polished)

**Technical Focus**:
- Validate core architecture (state machine, event system, data flow)
- Prove procedural content generation works (scripts, events)
- Smoke test performance (should already hit 60 FPS at this stage)

**Playtest Goal**: Can a player complete one film and feel the decision tension?

### 11.2 Milestone 2: Core Loop Complete (Weeks 9-16)

**Goal**: Full production pipeline with all systems at feature parity with design doc.

**Deliverables**:
- 80 talents in Talent Pool (full relationship graph)
- All crisis event categories implemented (50+ events authored)
- All 5 festivals functional with distinct jury profiles
- Financial system with revenue streams and runway tracking
- Ledger UI with projections
- Talent Web visualization (force-directed graph)
- Studio progression (reputation tiers, unlocks)
- Seasonal structure (4 seasons per year, pacing)

**Technical Focus**:
- Performance tuning (hit 60 FPS with 80 talents and full relationship graph)
- Save file stability (test saves with 5+ completed films)
- Event deck balancing (playtest for decision fatigue)

**Playtest Goal**: Can a player complete 5 films and feel studio progression?

### 11.3 Milestone 3: Content and Polish (Weeks 17-24)

**Goal**: Expand content, polish UI, add juice and feedback.

**Deliverables**:
- 120 talents (final count)
- 150+ crisis events authored and tested
- 50 script logline templates per genre (300+ total)
- 200+ coverage phrase fragments
- Press quote generation (50+ phrases per tone)
- UI polish (animations, transitions, sound effects)
- Diegetic UI refinement (cork board, whiteboard, CRT monitor)
- Audio integration (ambient office sounds, diegetic music)

**Technical Focus**:
- Content pipeline tools (script editor, event editor)
- Balance tuning (financial targets, talent costs, festival scoring)
- Juice (UI animations, screen shake on bankruptcy, confetti on festival win)

**Playtest Goal**: Does the game feel alive? Does the office UI feel tactile and lived-in?

### 11.4 Milestone 4: Stretch Features (Weeks 25-32, Optional)

**Goal**: Add stretch features if time/budget allows.

**Candidates**:
- Rival Studio system (AI-controlled competing studios)
- Muse dynamic (actor/director bonds)
- Comeback casting arc
- Industry Shift Events (Year 5+)
- Awards Season track (Oscar campaign simulation)

**Technical Focus**:
- Rival AI logic (studio decision-making, talent poaching)
- Event chains (multi-stage narrative arcs)

**Decision Point**: Evaluate after Milestone 3. Ship without stretch features if core loop is solid.

### 11.5 Milestone 5: Beta and Launch Prep (Weeks 33-40)

**Goal**: Bug fixes, optimization, platform ports, Steam integration.

**Deliverables**:
- Steam integration (achievements, cloud saves)
- Switch port (if pursuing)
- Final performance pass (hit 60 FPS on min spec)
- Final balance pass (economy, festival scoring, talent costs)
- Launch trailer assets (capture footage)
- Store page materials (screenshots, key art, description)

**Technical Focus**:
- Bug triage and fixes
- Stability testing (long play sessions, edge cases)
- Platform-specific QA (Steam Deck, Switch if applicable)

**Playtest Goal**: Can a player complete 10+ films without hitting a blocking bug?

---

## 12. Closing Notes

This is not a rendering challenge. It is not a physics challenge. It is a systems design and simulation challenge. The hard part is making 80-120 agents feel like people, not stats. The hard part is making procedural text feel authored. The hard part is balancing a six-axis economy so that both art and commerce are viable strategies.

The technology is straightforward. Godot 4.x is a known quantity. The architecture is event-driven and data-driven — standard for management sims. The performance budget is generous for a 2D UI game.

The risk is in the content quality. If coverage reports feel generic, the game fails. If crisis events feel repetitive, the game fails. If the Talent Web feels like a spreadsheet, the game fails. These are not technical problems. They are authorship problems. Budget time for writing, not just coding.

Ship it simple. Ship it data-driven. Profile before you optimize. The player does not care about your clever pathfinding algorithm. They care about whether the script about a deaf saxophonist in Reno makes them lean forward and hit "Greenlight."

If they do, we have a game.

If they do not, we iterate.

---

**Document Complete. Ready for production planning.**

**BYTE out.**
