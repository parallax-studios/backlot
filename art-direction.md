# BACKLOT — Art Direction Document

**Art Direction by PIXEL**
**Status: Production-Ready Art Bible v1.0**
**Last Updated: 2026-02-07**

---

## 1. Visual Identity Statement

This is what BACKLOT looks like: a production office in a converted Soho loft, shot from above like a diorama. Cork boards bristling with headshots connected by red string. Whiteboard shooting schedules half-erased and rewritten in three different colors of dry-erase marker. Manila envelopes fat with scripts stacked on a desk next to cold coffee in a paper cup and a landline phone that never stops ringing. Festival laurels pinned to the wall with pushpins — some earned, some aspirational, all yellowing at the edges. Through the window, you can see a backlot: half-built sets, a camera on a dolly, crew members hauling C-stands in the late afternoon light.

The visual language is **diegetic tactility**. Everything in the interface exists in physical space. There are no floating menus. There are no abstract HUD elements. The UI is the office. When you read a script, you are looking at a physical script with dog-eared pages and margin notes in blue pen. When you cast an actor, you are pinning their headshot to a cork board. When you check the budget, you are looking at a CRT monitor running Excel 2003. The shooting schedule is a whiteboard with magnetic date strips. Festival programs are printed booklets with coffee rings on the covers.

This is not skeuomorphism for its own sake. This is **environmental storytelling through interface design**. The visual style communicates the materiality of indie filmmaking in the mid-2000s — a world caught between analog and digital, between Miramax's corpse and A24's birth. The player should feel like they are sitting at this desk, in this office, making these decisions. The screen is not a window into a game. The screen is the desk.

The color palette is warm, intimate, and saturated with intention. Every color earns its place:

- **Dark espresso** for the desk surfaces and shadows — this is the color of late nights
- **Manila cream** for scripts and envelopes — this is the color of incoming possibility
- **Sundance red** for urgency, passion, deadlines that haunt you
- **Cannes midnight blue** for prestige, ambition, the films you make to prove something
- **Money green** for the Ledger, for cash flow, for survival
- **Film canister silver** for industry infrastructure — the machinery that surrounds creation
- **Award gold** for validation, for the Palme d'Or dream, used sparingly because hope is a rare resource

The composition principle is **organized chaos**. The office is cluttered but legible. Every surface has papers on it, but you can always find what you need. This is not minimalist Scandinavian UI design. This is New York indie film producer chic — functional maximalism. The negative space is never empty. It is full of texture, full of evidence of work.

The lighting is **warm incandescent with long shadows**. Late afternoon sun through dirty windows. Desk lamps with brass fixtures. The glow of a CRT monitor in a dim room. This is not fluorescent office lighting. This is the lighting of a workspace where people care too much about what they are making. The shadows are as important as the light — they create depth, they hide details until you lean in, they make the space feel inhabited.

**The player should glance at a single screenshot and immediately understand**: this is a game about making independent films in the mid-2000s, this is serious but not self-serious, this office has a personality, and I want to sit at that desk.

If the visual identity does not communicate all of that in five seconds, we have failed.

---

## 2. Color Palette Specification

### 2.1 Primary Palette

These six colors form the foundation. Every screen uses all six. They are the studio's visual DNA.

| Color Name | Hex Code | RGB Values | Usage Rule | Forbidden Usage |
|---|---|---|---|---|
| **Espresso** | `#2C1810` | (44, 24, 16) | Desk surfaces, shadows, deep backgrounds, text on light surfaces | Never use for text smaller than 14pt on anything except cream/white backgrounds |
| **Manila** | `#D4A574` | (212, 165, 116) | Scripts, envelopes, cork boards, paper textures, neutral UI elements | Never use for primary text (insufficient contrast with cream backgrounds) |
| **Sundance Red** | `#8B2500` | (139, 37, 0) | Urgent UI elements, deadlines, negative financial indicators, connection strings showing conflict, festival branding (Sundance/Berlin specific) | Never use more than 15% of screen real estate — red is punctuation, not foundation |
| **Cannes Blue** | `#1A3A5C` | (26, 58, 92) | Prestige indicators, high-reputation UI elements, festival branding (Cannes/Venice specific), water-cooler conversations, awards | Never use for warning states or negative feedback |
| **Money Green** | `#4A7C59` | (74, 124, 89) | Positive financial indicators, cash flow bars, revenue notifications, "greenlight" buttons, grant funding | Never use for non-financial elements (green = money, period) |
| **Cream** | `#F5E6C8` | (245, 230, 200) | Paper stock, light backgrounds, script pages, primary text background, office walls in bright lighting | Never use pure white (`#FFFFFF`) — cream is warmer and period-appropriate |

### 2.2 Secondary Palette

These colors support the primary six. They appear in specific contexts and never dominate.

| Color Name | Hex Code | RGB Values | Usage Rule |
|---|---|---|---|
| **Film Silver** | `#C0C0C0` | (192, 192, 192) | Film canisters, equipment, CRT monitor bezels, metal fixtures, industry infrastructure |
| **Award Gold** | `#FFD700` | (255, 215, 0) | Festival laurels, award notifications, Palme d'Or/Golden Bear/Oscar indicators, rare prestige moments |
| **Dry-Erase Blue** | `#4A90E2` | (74, 144, 226) | Whiteboard schedule current-day markers, production phase indicators (pre-production) |
| **Dry-Erase Green** | `#7ED321` | (126, 211, 33) | Whiteboard schedule completed days, production phase indicators (wrap) |
| **Dry-Erase Red** | `#D0021B` | (208, 2, 27) | Whiteboard schedule crisis days, overruns, delays |
| **Legal Pad Yellow** | `#FFF59D` | (255, 245, 157) | Handwritten notes, post-it annotations, urgent reminders |
| **Blue Pen Ink** | `#1E3A8A` | (30, 58, 138) | Handwritten annotations on scripts, margin notes, signatures |
| **Coffee Stain** | `#6B4423` | (107, 68, 35) | Coffee ring textures on paper, stain overlays, aging effects |

### 2.3 UI State Colors

Consistent color coding for interactive states across all UI elements.

| State | Color | Opacity/Treatment | Usage |
|---|---|---|---|
| **Default** | Context-dependent (Manila for neutral, Cannes Blue for prestige, etc.) | 100% | Resting state of all interactive elements |
| **Hover** | Same as default | Subtle glow (8px blur, 40% opacity white) + 5% brightness increase | Applied to all hoverable elements |
| **Active/Pressed** | Same as default | -10% brightness, no glow | Click/tap feedback |
| **Disabled** | Grayscale conversion of default color | 40% opacity | Elements not currently available |
| **Selected** | Same as default | 2px solid border in Sundance Red, +10% saturation | Currently selected item in lists/menus |
| **Positive Feedback** | Money Green | Subtle pulse animation (scale 1.0 to 1.05 over 0.4s) | Revenue notifications, successful outcomes |
| **Negative Feedback** | Sundance Red | Shake animation (3px horizontal over 0.2s) | Budget warnings, relationship drops |
| **New/Unread** | Award Gold | Small pulsing dot in corner | New scripts, unread messages, pending decisions |

### 2.4 Accessibility Considerations

The palette must pass WCAG AA standards for contrast and must be colorblind-safe.

**Contrast Ratios** (tested against Cream background):
- Espresso on Cream: 8.2:1 (AAA pass for all text sizes)
- Cannes Blue on Cream: 7.1:1 (AAA pass)
- Sundance Red on Cream: 5.8:1 (AA pass for large text only)
- Money Green on Cream: 4.6:1 (AA pass for large text, use with caution on body text)

**Colorblind Modes** (implemented as palette swaps):

| Standard Color | Protanopia (no red) | Deuteranopia (no green) | Tritanopia (no blue) |
|---|---|---|---|
| Sundance Red | Dark Orange `#CC5500` | Dark Brown `#8B6914` | Magenta `#B8336A` |
| Money Green | Blue-Green `#2E8B8B` | Blue `#4169E1` | Teal `#20B2AA` |
| Cannes Blue | Dark Purple `#4B0082` | Dark Cyan `#008B8B` | Orange-Red `#DC143C` |

All colorblind modes are toggled via Settings. Default mode is standard palette.

**Text Readability Rules**:
- Minimum body text size: 12pt
- Minimum UI label text size: 10pt
- All body text is Espresso on Cream or Cream on Espresso
- All UI labels use high-contrast pairings only (Espresso/Cream, Cannes Blue/Cream)
- Colored text (red/green/blue) is always paired with an icon or pattern for redundancy

### 2.5 Color Usage by Screen Zone

The office is divided into functional zones. Each zone has a dominant color that creates spatial memory.

| Zone | Location | Dominant Color | Secondary Color | What Happens Here |
|---|---|---|---|---|
| **Greenlight Table** | Center-left desk area | Manila (scripts) | Espresso (desk) | Script reading, greenlight decisions |
| **Talent Web Board** | Right wall, cork board | Cream (photos) | Sundance Red (conflict strings) | Casting, relationship management |
| **Production Clock** | Center desk, whiteboard | Dry-Erase Blue/Green/Red | Espresso (frame) | Day-by-day shoot tracking |
| **Avid Bay** | Left desk, monitor space | Cannes Blue (UI chrome) | Film Silver (monitor bezel) | Editing, post-production |
| **Ledger** | Bottom-right desk corner, CRT monitor | Money Green (positive) / Sundance Red (negative) | Film Silver (monitor) | Financial tracking, budget management |
| **Festival Wall** | Top-right wall | Award Gold (laurels) | Cannes Blue (programs) | Festival results, distribution deals |

When the player is in a specific workflow (e.g., casting), that zone's camera angle is prioritized and its colors dominate the screen. The zones never overlap visually — each workflow has spatial and chromatic clarity.

---

## 3. Shape Language Guide

Shape language is the grammar of visual communication. Every object in BACKLOT speaks in one of three shape families. These families create visual hierarchy and communicate object personality at a glance.

### 3.1 The Three Shape Families

**Family 1: The Documents** (Rectangles with soft corners)
- **Primitive**: Rectangle, 2-4px corner radius
- **Personality**: Reliable, official, structured
- **Examples**: Scripts, envelopes, paper sheets, budget spreadsheets, festival programs
- **Proportions**: Never perfectly square. Aspect ratios range from 1:1.3 (letter size) to 1:1.5 (screenplay format)
- **Edge Treatment**: Slight paper texture, visible page edges when stacked
- **Shadow**: Soft drop shadow (4px offset, 12px blur, 20% opacity Espresso)

**Family 2: The Interface Elements** (Sharp rectangles and functional shapes)
- **Primitive**: Rectangle, 0-1px corner radius; circles only for buttons
- **Personality**: Utilitarian, mid-2000s software aesthetic, functional
- **Examples**: CRT monitors, whiteboard frames, desk drawer faces, power buttons, window frames
- **Proportions**: 4:3 for monitors (period-accurate), 16:9 forbidden (not yet dominant), golden ratio for window/frame proportions
- **Edge Treatment**: Hard edges, visible bezels, slight reflective sheen on screens
- **Shadow**: Ambient occlusion only (no drop shadows — these are physical objects)

**Family 3: The People** (Organic shapes, rounded)
- **Primitive**: Rounded rectangles (8-12px corner radius) for photos; irregular organic shapes for annotations
- **Personality**: Human, warm, imperfect
- **Examples**: Headshots, polaroids, handwritten notes, post-it notes, coffee stains
- **Proportions**: Headshots are 1:1.2 (portrait orientation), polaroids are 1:1 square with white borders
- **Edge Treatment**: Hand-cut feel for photos (subtle irregularity), wrinkled paper texture for notes
- **Shadow**: Strong directional shadow (suggests pinning depth: 2px offset, 8px blur, 40% opacity Espresso)

### 3.2 Shape Hierarchy Rules

The player's eye must be guided through visual weight, not through animation or blinking elements.

**Z-Index Layering** (from back to front):
1. **Background Layer** (the desk/wall surface): Flat, textured, no shadows
2. **Static Elements Layer** (cork boards, whiteboards, monitor housings): Subtle depth (ambient occlusion)
3. **Document Layer** (scripts, papers, spreadsheets): Soft drop shadows (4-8px blur)
4. **Interactive Layer** (photos being dragged, notes being written): Strong shadows (10-16px blur)
5. **Notification Layer** (pop-up events, alerts): Strongest shadows + slight scale increase (1.03x)

**Size Hierarchy**:
- **Primary action targets** (scripts on Greenlight Table): Minimum 180x240px (readable at 1080p)
- **Secondary information** (budget line items, talent stats): Minimum 120x40px
- **Tertiary details** (timestamps, footnotes): Minimum 80x20px

No interactive element smaller than 44x44px (iOS minimum touch target). Mouse targets can be smaller but never below 32x32px.

**Shape as Affordance**:
- **Rectangular with soft corners** = draggable document
- **Circular** = button (press to activate)
- **Rectangular with hard corners + bezel** = screen/monitor (informational, not interactive)
- **Polaroid/photo with rounded corners** = talent (click to see details)
- **Irregular organic shape** = annotation/note (flavor text, not interactive)

If an object's affordance is unclear from shape alone, the design has failed. The player should never click on a static element thinking it is interactive.

### 3.3 Silhouette Test Standards

Every major UI element must pass the silhouette test: if reduced to a solid black shape on white background, it must be instantly identifiable.

**Tested Elements and Required Recognition Rate**:
- Script (rectangular with corner bend): 90%+ recognition
- Headshot (square with white border): 85%+ recognition
- Monitor/screen (rectangle with thick bezel): 80%+ recognition
- Coffee cup (circle with handle): 75%+ recognition
- Telephone (rectangle with circular dial or numeric keypad): 70%+ recognition

If any element falls below threshold, it needs clearer shape differentiation. This test is performed with blind testers (shown silhouettes, asked "what is this?").

### 3.4 Negative Space Discipline

Organized chaos requires discipline. The office is cluttered but never cramped.

**Spacing Rules**:
- Minimum 24px clearance between interactive elements (prevents mis-clicks)
- Minimum 16px margin from screen edge to nearest content
- Minimum 12px padding inside any bordered container (buttons, panels, script pages)
- Maximum 60% screen density — at least 40% of screen is negative space (desk/wall surface)

**Breathing Room Zones**:
- Top 10% of screen: Reserved for date/time/season header — always clean
- Bottom 10% of screen: Reserved for primary action button/status bar — always clear
- Center 30% of screen: Highest content density zone — this is where decisions happen
- Edges: Lower density — this is where context lives (cork boards, filing cabinets, windows)

**Focal Point Hierarchy**:
At any moment, there is one primary focal point (the decision the player must make). This focal point is reinforced by:
1. Largest element on screen (1.5-2x the size of secondary elements)
2. Highest contrast against background
3. Positioned in center-third of screen (optimal eye position)
4. Surrounded by the most negative space

When focus shifts (e.g., from script reading to casting), the focal point animates smoothly to the new location (camera pan + subtle zoom, 0.6-0.8 seconds, ease-in-out curve).

---

## 4. Style Rules

These are the do's and don'ts that keep the visual identity consistent across every screen, every asset, every animation. This section is the art direction police manual.

### 4.1 DO's

**DO use textures on every surface.**
The world is material. The desk is wood grain. The cork board is actual cork. Paper has a subtle fiber texture. Whiteboards have faint eraser streaks. Nothing is flat and clean unless it is brand new (which it never is in an indie film office). Textures are subtle (never louder than 15% opacity overlays) but always present.

**DO show evidence of use.**
Coffee stains on scripts. Thumbtack holes in the cork board where photos used to be. Worn spots on the desk where the player's forearm rests. A phone with a coiled cord that is slightly tangled. These are not decoration. These are proof that this office is inhabited. Every surface tells the story of work.

**DO use diegetic UI exclusively.**
There are no floating health bars. There are no abstract progress wheels. Every piece of information exists as a physical object in the office. The budget is a spreadsheet on a monitor. The shooting schedule is a whiteboard. Talent stats are handwritten notes on the backs of headshots. If you cannot imagine touching it with your hand, it does not belong on screen.

**DO respect period-accurate technology.**
This is 2005. CRT monitors, not flatscreens. Landline phones with cords. Whiteboards and cork boards, not Trello and Asana. If a laptop appears, it is a chunky ThinkPad or PowerBook G4, not a MacBook Air. DVD cases, not streaming thumbnails. Film canisters, not hard drives. The tech is transitional — digital cameras are debated, but film is still king. Get the technology wrong and the entire world collapses.

**DO layer information with progressive disclosure.**
A script on the desk shows title and author. Hover and you see the logline. Click and the full coverage report unfolds. A headshot shows the actor's face. Hover and their name appears. Click and their stats bloom outward. The first glance is simple. The deep dive reveals complexity. This respects the player's attention.

**DO use color as emotional punctuation, not decoration.**
Sundance Red appears when something is urgent or wrong. Cannes Blue appears when something is prestigious or aspirational. Money Green appears when cash flows in. These colors are narrative signals. They mean something. They are never used casually. If a button is green but does not involve money, the button is lying.

**DO animate with physicality.**
Objects have weight. Scripts do not teleport — they slide across the desk. Headshots do not pop in — they are pinned to the board with a pushpin animation (0.2s). The camera does not cut — it pans smoothly (0.6-1.0s). When a budget line updates, the numbers roll like an odometer, not blink like a digital clock. Everything moves like a physical object in a physical space.

**DO create spatial memory.**
The Greenlight Table is always center-left. The Talent Web is always on the right wall. The Ledger is always bottom-right. The player learns the space. They know where to look for information without hunting. Spatial consistency reduces cognitive load and makes the player feel like they inhabit the office, not just use it.

**DO use typography as characterization.**
Scripts are in Courier (industry standard). Business documents are in Helvetica (corporate neutrality). Handwritten notes are in a natural handwriting font (personality). Festival programs are in Garamond or Baskerville (prestige). The font tells you what you are reading before you read a word.

**DO test readability at 1080p.**
This is the minimum supported resolution. If text is not legible at 1080p, it does not ship. Body text minimum is 12pt, UI labels minimum is 10pt. Test on a 24-inch monitor at 1080p from 24 inches away (average viewing distance). If you have to squint, it fails.

**DO embrace asymmetry.**
The office is not a grid. Stacks of scripts are not perfectly aligned. Photos on the cork board overlap at irregular angles. The whiteboard schedule is not perfectly centered in its frame. This is not a Wes Anderson film. This is a working space. Asymmetry signals authenticity.

**DO use lighting to create depth.**
Desk lamps cast pools of light. The CRT monitor glows in a dim corner. Sunlight streams through the window at an angle, creating long shadows. Lighting is not even. It is directional and warm. The brightest spot on screen is always the focal point (the current decision). Lighting guides the eye.

### 4.2 DON'Ts

**DON'T use pure black (`#000000`) or pure white (`#FFFFFF`).**
Pure black is dead. Pure white is sterile. This office has character. The darkest color is Espresso (`#2C1810`). The lightest is Cream (`#F5E6C8`). If pure black or white appears anywhere in the final assets, it is a mistake.

**DON'T use neon or saturated colors outside the defined palette.**
No hot pink. No electric cyan. No lime green. The palette is warm, muted, and grounded in reality. If a color screams for attention, it does not belong. The only exception is Award Gold, and it is used so sparingly that it never dominates.

**DON'T use drop shadows on text.**
Text on paper does not have drop shadows. Text on monitors does not have drop shadows. Drop shadows make text harder to read, not easier. If contrast is insufficient without a drop shadow, fix the background color or add a subtle background plate behind the text.

**DON'T animate for animation's sake.**
Every animation must have a reason. If an animation does not communicate state change, provide feedback, or guide the eye, it is cut. No idle animations. No bouncing buttons. No spinners unless something is genuinely loading. The office does not fidget.

**DON'T use icons without labels (unless the icon is universal).**
A floppy disk icon for "save" is not universal to this audience. A trash can for "delete" is borderline. Always pair icons with text labels unless the icon is genuinely unambiguous (e.g., an X for close). When in doubt, label it.

**DON'T break the fourth wall.**
The player is a producer in an office, not a player in a game. There are no achievement pop-ups that say "Achievement Unlocked." There are no UI elements that say "Press X to continue." Everything is diegetic. If a tutorial is needed, it comes from a mentor character's handwritten note, not a floating tooltip.

**DON'T use comic sans, papyrus, or any novelty font.**
This should be obvious, but it is worth stating. The typefaces in this game are Courier, Helvetica, Garamond, a clean handwriting font (League Script or Caveat), and nothing else. Every font must be licensable for commercial use and must render cleanly at 12pt+.

**DON'T layer more than 5 elements deep in a single screen zone.**
Background > static objects > documents > interactive elements > notifications. That is five layers maximum. More than five and the depth becomes mud. Parallax scrolling is forbidden — the office is a fixed space, not an infinite plane.

**DON'T use particle effects, bloom, or lens flare.**
This is not a AAA action game. This is a production office. The most dramatic visual effect in the game is a coffee stain spreading on a script (a 2-second alpha-blended texture animation). If an effect would not happen in a real office, it does not happen in this office.

**DON'T make the player hunt for critical information.**
The current budget is always visible (bottom-right Ledger). The current production phase is always visible (whiteboard or Avid monitor). The current decision prompt is always in the center third of the screen. The player should never ask "Where is my money?" or "What phase am I in?" If playtesting reveals confusion, the UI has failed.

**DON'T use memes or anachronistic references.**
This is 2005. "Best film ever. Five stars. Would watch again." is a 2010s meme format. Keep all generated text, all in-world flavor text, and all UI language period-appropriate. References to MySpace are fine. References to Twitter are forbidden.

**DON'T use red/green as the only differentiator.**
Colorblind players exist. If a budget line is green for positive and red for negative, there must also be an icon (up arrow for positive, down arrow for negative) or a text label (+$50K / -$20K). Color is reinforcement, not the sole carrier of meaning.

---

## 5. Typography Specification

Typography is 50% of the interface. The wrong font kills immersion. The right font is invisible.

### 5.1 Primary Typefaces

| Typeface | Usage | Weights Used | Rationale |
|---|---|---|---|
| **Courier Prime** | All screenplay text, script pages, coverage reports | Regular (400) | Industry-standard screenplay font. Free, open-source, renders cleanly at all sizes. Monospace creates rhythm. |
| **Helvetica Neue** | Business documents, budget spreadsheets, contracts, agent emails, UI labels | Regular (400), Medium (500), Bold (700) | Neutral, corporate, ubiquitous in 2000s business software. Fallback: Arial if Helvetica licensing is prohibitive. |
| **Garamond** | Festival programs, prestige documents, awards ceremony text, critical reviews | Regular (400), Italic (400), Bold (700) | Serif typeface with cultural prestige. Signals high art, intellectual seriousness. Used sparingly. |
| **Caveat** | Handwritten notes, margin annotations, post-it reminders, personal messages | Regular (400), Bold (700) | Warm, human, imperfect. Feels like someone actually wrote this with a pen. Free Google Font. |
| **Inter** | Fallback UI font for dynamic text (generated names, numbers, real-time updates) | Regular (400), Medium (500), Semibold (600) | Clean, highly legible, supports extended Latin + Cyrillic. Renders well at small sizes. Modern but not anachronistic. |

All typefaces must be licensed for commercial use in games. Courier Prime, Caveat, and Inter are free and open-source. Helvetica Neue requires licensing or must be replaced with Arial (acceptable fallback). Garamond is widely available.

### 5.2 Type Scale and Hierarchy

| Element | Typeface | Size | Weight | Line Height | Color | Usage |
|---|---|---|---|---|---|---|
| **H1: Section Header** | Helvetica Neue | 28pt | Bold (700) | 1.2 | Espresso | Screen titles (e.g., "GREENLIGHT TABLE") |
| **H2: Subsection Header** | Helvetica Neue | 20pt | Medium (500) | 1.3 | Espresso | Panel headers (e.g., "Incoming Scripts") |
| **Body Text (Script)** | Courier Prime | 12pt | Regular (400) | 1.6 | Espresso | Screenplay text, coverage reports |
| **Body Text (Document)** | Helvetica Neue | 12pt | Regular (400) | 1.5 | Espresso | Contracts, budget sheets, emails |
| **Body Text (Review/Article)** | Garamond | 13pt | Regular (400) | 1.6 | Espresso | Festival reviews, press clippings |
| **UI Label** | Helvetica Neue | 10pt | Medium (500) | 1.4 | Espresso or Cannes Blue | Button labels, field labels, stat names |
| **UI Value** | Helvetica Neue | 11pt | Regular (400) | 1.4 | Cannes Blue or Money Green/Sundance Red | Numbers, percentages, dates |
| **Handwritten Note** | Caveat | 14pt | Regular (400) | 1.5 | Blue Pen Ink | Margin notes, post-its, annotations |
| **Small Print** | Helvetica Neue | 9pt | Regular (400) | 1.4 | Espresso at 70% opacity | Footnotes, timestamps, metadata |
| **Emphasis (in-body)** | Same as body | Same as body | Bold (700) | Same as body | Sundance Red or Cannes Blue | Important keywords in documents |

**Minimum readable sizes**:
- Body text: 12pt (11pt acceptable for Garamond due to larger x-height)
- UI labels: 10pt
- Metadata: 9pt
- Never use text smaller than 9pt for any reason

### 5.3 Text Hierarchy in Context

**Example: Script Coverage Report**

```
[H1] GREENLIGHT TABLE                                    [Helvetica 28pt Bold, Espresso]

[H2] Coverage Report: "The Deaf Saxophonist"            [Helvetica 20pt Medium, Espresso]

[Body Script] LOGLINE:                                   [Courier 12pt, Espresso]
A once-famous saxophonist loses his hearing and         [Courier 12pt, Espresso]
retreats to Reno, where he forms an unlikely bond       [Courier 12pt, Espresso]
with a teenage blackjack dealer who communicates        [Courier 12pt, Espresso]
through improvised sign language.                       [Courier 12pt, Espresso]

[Body Script] READER NOTES:                              [Courier 12pt, Espresso]
Ambitious. Possibly pretentious. [Emphasis]Festival     [Sundance Red, Bold]
bait[End Emphasis] with genuine guts. The structure     [Courier 12pt, Espresso]
is non-linear, which will either sing or collapse       [Courier 12pt, Espresso]
depending on execution...                               [Courier 12pt, Espresso]

[Handwritten note in margin] "Cast carefully.           [Caveat 14pt, Blue Pen Ink]
Lead must carry the silence." — M.                      [Caveat 14pt, Blue Pen Ink]

[UI Label] BUDGET DEMAND:                                [Helvetica 10pt Medium, Espresso]
[UI Value] Low ($200K-$350K)                            [Helvetica 11pt, Money Green]

[UI Label] GENRE:                                        [Helvetica 10pt Medium, Espresso]
[UI Value] Drama                                        [Helvetica 11pt, Cannes Blue]
```

The hierarchy is clear: title > section header > body text > metadata. The eye flows naturally from top to bottom. The handwritten note breaks the formality, adding human texture. The UI labels are small but legible. The budget value uses color to reinforce its category (green = financial, positive).

### 5.4 Typographic Don'ts

- **Never center-align body text.** Left-aligned only (standard for Western reading). Center-alignment is for headers and titles only.
- **Never use all-caps for body text.** All-caps reduces readability by 30%. Use it sparingly for headers or labels only.
- **Never stack more than 3 type sizes in a single paragraph.** Hierarchy requires consistency.
- **Never use type smaller than 9pt.** If it is not readable, it is not usable.
- **Never use decorative fonts for functional text.** Garamond is acceptable for reviews because reviews are read slowly. It is forbidden for UI labels because labels are scanned quickly.
- **Never use faux-bold or faux-italic.** Use actual bold/italic font weights. Faux styling renders poorly and looks amateurish.

---

## 6. Asset Pipeline Overview

A production-ready pipeline for creating, naming, organizing, and implementing all visual assets.

### 6.1 Pipeline Stages

**Stage 1: Concept / Reference Gathering**
- **Owner**: Art Director (PIXEL) + Lead Artist
- **Deliverable**: Mood board per asset category (e.g., "Scripts," "Headshots," "Office Props")
- **Tools**: Pinterest boards, Figma boards, physical reference photos
- **Approval Gate**: Visual identity alignment check. Does this reference match the defined color palette and shape language?

**Stage 2: Blockout / Grayscale Mockup**
- **Owner**: Lead Artist
- **Deliverable**: Grayscale composition mockups (no color, no texture, shapes only)
- **Tools**: Figma (UI elements), Blender or Maya (3D assets if needed), Photoshop (textures)
- **Approval Gate**: Silhouette test. Can the asset be identified from shape alone?

**Stage 3: Color and Texture Pass**
- **Owner**: Lead Artist + Texture Artist
- **Deliverable**: Full-color, textured assets in final resolution
- **Tools**: Photoshop (2D assets), Substance Painter (3D textures)
- **Approval Gate**: Palette adherence check. Does this use only approved hex codes? Does texture noise exceed 15% opacity?

**Stage 4: Integration and Polish**
- **Owner**: UI Engineer + Lead Artist
- **Deliverable**: Asset integrated into engine (Unity or Godot), animated if needed
- **Tools**: Unity or Godot, After Effects (for animated textures like coffee stains)
- **Approval Gate**: Readability test at 1080p. Is all text legible? Are interactive elements >44px?

**Stage 5: Playtesting and Iteration**
- **Owner**: Full team
- **Deliverable**: Revised assets based on player feedback
- **Approval Gate**: Player comprehension. Can testers identify object affordances without tutorial prompts?

### 6.2 Naming Conventions

Consistent naming prevents chaos in a 500+ asset library.

**Format**: `[category]_[object]_[variant]_[state]_[resolution].ext`

**Examples**:
- `ui_script_thriller_default_2x.png` (UI category, script object, thriller variant, default state, 2x resolution)
- `talent_headshot_female_middle_age_hover.png` (Talent category, headshot, demographic variant, hover state)
- `prop_coffee_cup_empty_default.png` (Prop category, coffee cup, empty variant, default state)
- `bg_desk_surface_oak_2k.jpg` (Background category, desk surface, oak wood variant, 2048x2048 resolution)

**Categories**:
- `ui_` = Interface elements (buttons, panels, borders, windows)
- `doc_` = Documents (scripts, contracts, spreadsheets, reports)
- `talent_` = Talent-related assets (headshots, bios, stat cards)
- `prop_` = Office props (coffee cups, phones, film canisters, pens)
- `bg_` = Backgrounds and surfaces (desk, walls, floors, cork boards)
- `vfx_` = Visual effects (coffee stain animations, paper crumpling, light blooms)
- `font_` = Typeface files
- `audio_` = Sound effects and music (though this is an art doc, audio is part of the asset pipeline)

**Variants**: Describe the specific visual version (e.g., `red`, `blue`, `worn`, `new`, `landscape`, `portrait`)

**States**: `default`, `hover`, `active`, `disabled`, `selected`

**Resolution**: `1x` (base 1080p), `2x` (1440p/4K), `4x` (ultra-high-DPI for future-proofing). Export all UI assets at 2x minimum.

### 6.3 File Formats and Specs

| Asset Type | Format | Resolution | Color Mode | Compression | Alpha Channel |
|---|---|---|---|---|---|
| **UI Elements** | PNG | 2x native size (e.g., 360x480 for a 180x240 element) | sRGB | Lossless | Yes (transparency required) |
| **Backgrounds** | JPG | 2048x2048 (tiled) or 3840x2160 (full-screen) | sRGB | 85% quality | No |
| **Textures (overlays)** | PNG | 1024x1024 or 2048x2048 | sRGB | Lossless | Yes (for blend modes) |
| **Photos (headshots)** | PNG | 512x614 (1:1.2 ratio at 2x) | sRGB | Lossless | Yes (rounded corners) |
| **Documents (scripts)** | PNG | 1200x1560 (letter size at 150 DPI) | sRGB | Lossless | Yes |
| **Fonts** | WOFF2 (web), TTF (desktop) | Vector | N/A | N/A | N/A |
| **VFX (animated)** | PNG sequence or WebM | Varies | sRGB | Lossless (PNG), 90% (WebM) | Yes |

**Color Profile**: All assets must be exported in sRGB color space (standard for games and web). Do not use Adobe RGB or ProPhoto RGB.

**DPI**: All raster assets are created at 72 DPI or 150 DPI (for document readability). Higher DPI is unnecessary for screen display.

**Layered Source Files**: All assets must have Photoshop (.psd) or Figma source files stored in the `source_assets/` folder with the same naming convention. Never flatten source files.

### 6.4 Quality Assurance Checklist

Before any asset is marked as final, it must pass this checklist.

| Check | Pass Criteria | Tested By |
|---|---|---|
| **Palette Adherence** | Uses only approved hex codes from Section 2 | Art Director |
| **Shape Language** | Matches one of the three shape families from Section 3 | Art Director |
| **Silhouette Recognition** | >70% recognition rate in blind silhouette test | QA team |
| **Readability at 1080p** | All text >9pt, all interactive elements >44px | QA team |
| **File Size** | UI elements <500KB, Backgrounds <2MB, VFX <5MB | Tech Lead |
| **Colorblind Safe** | Passes all three colorblind modes without information loss | Accessibility Lead |
| **Naming Convention** | Matches the defined format exactly | Asset Manager |
| **Source File Archived** | Layered PSD/Figma file exists in `source_assets/` | Asset Manager |

Any asset that fails any check is returned to the artist for revision. No exceptions.

### 6.5 Directory Structure

Organized folders prevent asset hell.

```
/assets/
  /ui/
    /buttons/
    /panels/
    /icons/
    /borders/
  /documents/
    /scripts/
    /contracts/
    /spreadsheets/
    /reports/
  /talent/
    /headshots/
      /male/
      /female/
      /nonbinary/
    /bio_cards/
  /props/
    /desk_items/
    /office_equipment/
    /film_equipment/
  /backgrounds/
    /desk_surfaces/
    /walls/
    /windows/
  /vfx/
    /coffee_stains/
    /paper_crumple/
    /lighting_effects/
  /fonts/
    /courier_prime/
    /helvetica/
    /garamond/
    /caveat/
    /inter/
  /audio/
    /sfx/
      /office_ambience/
      /ui_interactions/
    /music/
      /menu_themes/
      /festival_themes/

/source_assets/
  [Mirror of /assets/ structure, containing PSD/Figma files]

/references/
  /mood_boards/
  /style_studies/
  /period_photography/
```

All artists work from this structure. No exceptions. Deviate and the build breaks.

---

## 7. Animation Principles

Animation in BACKLOT is not about spectacle. It is about physicality, feedback, and guiding the player's eye. Every animation must feel like something happening in a real space.

### 7.1 Core Principles

**Principle 1: Weight and Inertia**
Objects have mass. A script sliding across a desk accelerates slowly and decelerates gradually (ease-in-out curve). A pushpin being pressed into a cork board has a quick snap (ease-in, no ease-out). A coffee cup being set down has a slight bounce (overshoot by 5%, settle over 0.2s). Nothing teleports. Nothing moves at constant velocity.

**Principle 2: Cause and Effect**
Every animation has a trigger. The player drags a headshot — the photo lifts (scale 1.05x, shadow increases to 16px blur). The player releases — the photo settles (scale returns to 1.0, shadow reduces to 8px blur, slight rotation snaps to 0). No animation plays without player action or system feedback.

**Principle 3: Overlapping Action**
When the camera pans from the Greenlight Table to the Talent Web, the camera moves first (0.6s), then the UI elements fade in (0.4s starting at 0.3s into the pan). This overlap feels organic. Simultaneous transitions feel robotic.

**Principle 4: Anticipation and Follow-Through**
A whiteboard marker erasing a completed shoot day: slight upward lift (anticipation, 0.1s), fast horizontal stroke (action, 0.3s), slight downward press at the end (follow-through, 0.1s). Total: 0.5s. This three-part structure makes the action feel intentional, not automatic.

**Principle 5: Economy of Motion**
Less is more. A button press is 0.1s of scale reduction (0.95x) and a 10% brightness drop. That is enough. No need for glow, pulse, particle effects, or sound (unless the button is a phone ringing or a critical greenlight decision). If the animation does not communicate essential feedback, cut it.

### 7.2 Timing Standards

All animations use a consistent timing language.

| Action | Duration | Easing Curve | Rationale |
|---|---|---|---|
| **Button press** | 0.1s | Ease-in | Immediate feedback, snappy |
| **Hover state** | 0.2s | Ease-out | Smooth transition, not jarring |
| **Drag object** | Instant on grab, 0.3s on release | Ease-out on release | Object follows cursor instantly, settles gradually |
| **Panel open/close** | 0.4s | Ease-in-out | Panel has weight, should not snap |
| **Camera pan** | 0.6-0.8s | Ease-in-out | Human eye tracking speed |
| **Page turn** | 0.5s | Custom (slow-fast-slow) | Mimics physical page flip |
| **Notification pop-in** | 0.3s | Ease-out with slight overshoot (1.05x peak scale) | Draws attention without being obnoxious |
| **Fade in/out** | 0.4s | Linear (no easing) | Fades should be smooth and even |
| **Number roll (odometer)** | 0.6-1.2s (depends on magnitude of change) | Ease-out | Larger changes take longer, adds weight to money |
| **Coffee stain spread** | 2.0s | Ease-out (rapid start, slow stop) | Liquid diffusion mimics real physics |

**Global Rule**: No animation longer than 1.2s except for rare, dramatic events (festival award ceremony, final film premiere). Long animations become unskippable cutscenes, and unskippable cutscenes kill replay value.

### 7.3 Camera Movement

The camera is not a disembodied observer. It is the player's POV — a person sitting at this desk, looking around this office.

**Camera Pan** (moving between UI zones):
- **Speed**: 0.6-0.8s depending on distance
- **Path**: Smooth arc, not straight line (mimics head turn)
- **Easing**: Ease-in-out (accelerate, coast, decelerate)
- **Accompanying action**: Blur the departing zone slightly (2px Gaussian, 0.2s fade-in), sharpen the arriving zone

**Camera Zoom** (focusing on a document or detail):
- **Speed**: 0.5s
- **Magnification**: 1.2x to 1.5x (subtle, not cinematic)
- **Easing**: Ease-in-out
- **Accompanying action**: Vignette the edges slightly (darken by 15%, 40px radial gradient), fade out background noise (audio + visual)

**Camera Reset** (returning to default overview):
- **Speed**: 0.7s
- **Easing**: Ease-in-out
- **Trigger**: Player presses ESC or clicks "Back" button
- **Accompanying action**: Reverse zoom/pan, restore ambient audio to full volume

**No camera shake, no dutch angles, no fish-eye distortion.** This is a grounded, human perspective. The most dramatic camera move in the game is a slow push-in on a festival laurel when the player wins Cannes. That is it.

### 7.4 Micro-Interactions

The smallest animations create the most delight.

| Interaction | Animation | Duration | Purpose |
|---|---|---|---|
| **Script hover** | Slight lift (2px translate-y, shadow increase to 8px blur) | 0.2s | Indicates draggability |
| **Headshot click** | Polaroid flips over to reveal stats on back | 0.4s (card flip) | Reveals hidden information |
| **Budget update** | Numbers roll like odometer, green flash on positive, red pulse on negative | 0.8s | Emotional feedback on financial change |
| **Coffee cup idle** | Occasional steam wisp (PNG sequence, 3s loop, 30% opacity) | 3s loop | Adds life to static scene |
| **Phone ring** | Handset vibrates (2px horizontal shake, 0.2s interval) + visual ring indicator (expanding circle, 1.0s fade) | Loops until answered | Creates urgency without being annoying |
| **Festival result** | Laurel pins itself to wall (pushpin drops from top, 0.3s, slight bounce on impact) | 0.5s total | Celebratory but understated |
| **Talent relationship change** | Connection string color shifts (red <-> green, 0.5s gradient transition) | 0.5s | Visualizes social dynamics |
| **Whiteboard schedule update** | Dry-erase marker writes date (3-frame animation: marker approaches, writes, lifts) | 0.6s | Reinforces handmade aesthetic |

Every micro-interaction passes the "does this feel like a real action?" test. If a physical equivalent does not exist, the animation is cut.

### 7.5 Animation Budget

Not every element needs to animate. Animation is expensive (dev time + performance). Prioritize impact.

**High Priority** (must animate):
- All player-triggered interactions (button presses, drags, clicks)
- All critical feedback moments (money in/out, relationship changes, festival results)
- Camera transitions between UI zones

**Medium Priority** (animate if budget allows):
- Idle loops (steam from coffee, monitor screen flicker, ambient office life)
- Micro-interactions (hover states, tooltip appearances, page turns)
- Seasonal transitions (office lighting shifts subtly between winter/spring/summer/fall)

**Low Priority** (animate only if time permits):
- Background props (a plant swaying slightly, a poster peeling at the corner)
- Rare Easter eggs (a mouse running across the desk at 2AM in-game time)
- Title screen flourishes (a film reel spinning slowly in the background)

**Cut Entirely** (do not animate):
- Static backgrounds (desk surface, walls, floors)
- Text (except number rolls and typewriter effects for dramatic reveals)
- Photos and documents when not being interacted with

If in doubt, cut the animation. A static, polished interface beats a janky, over-animated one.

---

## 8. Readability Checklist

A game is unplayable if the player cannot read the screen. This checklist must be passed for every major screen before it ships.

### 8.1 Text Readability

| Test | Pass Criteria | How to Test |
|---|---|---|
| **Minimum Size** | No text smaller than 9pt | Measure all text in final build |
| **Contrast Ratio** | Body text >7:1, UI labels >4.5:1 | Use WebAIM Contrast Checker on all text/background pairs |
| **Font Legibility** | All fonts render clearly at 12pt on 1080p display | Print screen, view at arm's length |
| **Line Length** | Body text lines 50-75 characters max | Count characters in longest body text block |
| **Line Height** | Minimum 1.4x font size | Measure in Figma/Photoshop |
| **Alignment** | Body text left-aligned, headers can be centered | Visual inspection |

**Failure Resolution**: If any text fails contrast, either change text color or add a subtle background plate (50-80% opacity Cream or Espresso rectangle, 8px padding).

### 8.2 Visual Hierarchy

| Test | Pass Criteria | How to Test |
|---|---|---|
| **Focal Point** | Player identifies primary action within 2 seconds | Eye-tracking or timed tester prompts |
| **Information Density** | Maximum 7 distinct elements competing for attention in any screen | Count UI elements, group related items |
| **Silhouette Test** | Key elements recognizable in silhouette (>70% tester recognition) | Convert screen to black/white silhouettes, test with blind participants |
| **Squint Test** | Screen hierarchy legible when squinting (blurs details) | Squint at screen from 6 feet away — can you still identify zones? |

**Failure Resolution**: If focal point is unclear, increase size of primary element by 20% and reduce size of secondary elements by 10%. If hierarchy fails squint test, increase contrast between zones (lighting, color saturation, scale).

### 8.3 Color Accessibility

| Test | Pass Criteria | How to Test |
|---|---|---|
| **Colorblind Modes** | All information conveyed by color also conveyed by icon, pattern, or text | Test in all three colorblind modes (protanopia, deuteranopia, tritanopia) |
| **Red/Green Distinction** | Never rely solely on red vs. green | Replace with up/down arrows, +/- signs, or distinct icons |
| **Color Contrast** | All interactive elements distinguishable by 20% contrast difference | Use color picker to compare adjacent elements |

**Failure Resolution**: Add icons to all color-coded elements. Example: green budget line has an up arrow, red budget line has a down arrow.

### 8.4 Interactive Element Clarity

| Test | Pass Criteria | How to Test |
|---|---|---|
| **Minimum Target Size** | All interactive elements >44x44px (iOS standard) | Measure in Figma |
| **Hover State** | All interactive elements have distinct hover state | Hover over every element, verify visual change |
| **Affordance** | 80%+ testers correctly identify clickable vs. static elements without prompting | Show screenshots, ask "What can you click?" |
| **Feedback Loop** | Every interaction triggers visual feedback within 0.1s | Test in build, verify immediate response |

**Failure Resolution**: If affordance is unclear, add visual cues (drop shadow on interactive elements, cursor change to pointer, subtle glow on hover).

### 8.5 Spatial Clarity

| Test | Pass Criteria | How to Test |
|---|---|---|
| **Zone Definition** | Player can name the six UI zones (Greenlight Table, Talent Web, Production Clock, Avid Bay, Ledger, Festival Wall) after one session | Post-session interview, ask "What were the main areas of the screen?" |
| **Navigation Logic** | Player can return to any major screen within 2 clicks from any other screen | Path analysis in build |
| **Spatial Memory** | Player looks to correct screen zone without hunting by third session | Eye-tracking or observation notes |

**Failure Resolution**: If zones are unclear, add stronger visual boundaries (borders, color shifts, lighting changes). If navigation is confusing, add a persistent mini-map or breadcrumb trail (diegetically: a cork board with pins showing current workflow).

### 8.6 Performance Readability

| Test | Pass Criteria | How to Test |
|---|---|---|
| **Framerate** | 60fps minimum at 1080p on mid-tier hardware (GTX 1060 / RX 580 equivalent) | Performance profiling in Unity/Godot |
| **Load Times** | Screen transitions <0.8s | Measure with stopwatch in build |
| **Animation Stutter** | No dropped frames during animations | Visual inspection + framerate graph |

**Failure Resolution**: Optimize asset sizes (reduce PNG resolution, compress textures), reduce shadow complexity (bake shadows where possible), limit simultaneous animations (max 5 animating elements on screen at once).

### 8.7 Testing Protocol

**When to Test**: After every major art milestone (blockout complete, color pass complete, animation pass complete, final polish complete).

**Who Tests**:
- Art Director (self-review)
- 3 internal playtesters (team members not on art team)
- 5 external playtesters (target audience, no game dev experience)

**Pass Threshold**: 80% of external testers must pass all criteria. If any test fails with >20% of testers, that screen returns to art team for revision.

**Iteration Cap**: Maximum 3 revision rounds per screen. If a screen fails after 3 rounds, escalate to full team design review (something fundamental is broken).

---

## 9. Reference List

Good art direction does not invent from nothing. It synthesizes, remixes, and refines. These references form the visual DNA of BACKLOT.

### 9.1 Film References

**Primary Visual References** (lighting, color, composition):

1. **The Player (1992, dir. Robert Altman)**
   - Reference: The Hollywood production office interiors, cork boards with headshots, the material culture of film industry work spaces
   - What to study: Lighting (warm practicals, deep shadows), composition (cluttered frames that still read clearly), color (desaturated 90s office tones, we push warmer)

2. **Adaptation (2002, dir. Spike Jonze)**
   - Reference: The writing process, the creative struggle, the physicality of screenplay pages
   - What to study: How script pages are shot (tight close-ups, typewriter font clarity), the neurotic energy of creative work

3. **Almost Famous (2000, dir. Cameron Crowe)**
   - Reference: The tactile nature of creative industries in the analog-to-digital transition (we are 5 years later, same transition)
   - What to study: Warm nostalgic lighting, the clutter of a working creative (records, papers, Polaroids), emotional color palette (golds, deep blues)

4. **Living in Oblivion (1995, dir. Tom DiCillo)**
   - Reference: The chaos of low-budget film production, the personalities on set
   - What to study: Black-and-white sequences (high contrast, clear silhouettes), production design (minimal but characterful)

5. **Mulholland Drive (2001, dir. David Lynch)**
   - Reference: The dream and nightmare of Hollywood, the gap between aspiration and reality
   - What to study: The contrast between warm (hopeful) and cold (nightmare) lighting, the use of red as danger/passion

**Secondary References** (mood, tone, world-building):

6. **Lost in Translation (2003, dir. Sofia Coppola)** — Isolation in a foreign system (film festivals feel like this)
7. **Barton Fink (1991, dir. Coen Brothers)** — The horror of creative compromise, the Hollywood Hotel as prison
8. **Birdman (2014, dir. Alejandro González Iñárritu)** — The backstage chaos, the prestige desperation (though our tone is less manic)
9. **Get Shorty (1995, dir. Barry Sonnenfeld)** — Hollywood as a con game, but we play it straighter
10. **Ed Wood (1994, dir. Tim Burton)** — The beautiful delusion of artists who believe against all evidence

### 9.2 Game References

**UI/UX Design References**:

1. **Return of the Obra Dinn (2017)**
   - Reference: Diegetic UI excellence — every interface element exists in the world
   - What to study: Logbook as primary UI, handwritten annotations, period-appropriate typography

2. **Papers, Please (2013)**
   - Reference: Desk-based gameplay, document inspection, time pressure without action mechanics
   - What to study: Top-down desk view, spatial organization of documents, stamping as satisfying interaction

3. **Wilmot's Warehouse (2019)**
   - Reference: Spatial organization as core mechanic, clean visual hierarchy despite density
   - What to study: Color coding, visual clarity in chaos, satisfying dragging and sorting

4. **Game Dev Tycoon (2012)**
   - Reference: Creative industry simulation, the loop of create-release-assess-repeat
   - What to study: How to abstract complex systems into readable UI, pacing of decision points

5. **Disco Elysium (2019)**
   - Reference: Text-heavy game that remains visually engaging, personality as mechanic
   - What to study: Portrait integration with dialogue, color-coded text for different voices, handwritten UI elements

6. **Pentiment (2022)**
   - Reference: Period-accurate material culture, every visual detail serves world-building
   - What to study: Manuscript aesthetics, typeface as characterization, commitment to historical specificity

**Secondary Game References**:
7. **Her Story** — Database investigation as gameplay
8. **Unpacking** — Objects as storytelling
9. **A Mortician's Tale** — Understated, human-scale storytelling in a management frame
10. **Strange Horticulture** — Desk-based gameplay, object examination

### 9.3 Art and Design Movements

**Primary Movement**: **Mid-Century Modernism meets 2000s Indie Aesthetic**
- The office furniture, the desk lamp, the landline phone — these are mid-century design (Eames chairs, Noguchi lamps, clean lines with warm wood). But the clutter, the DIY energy, the festival posters taped to walls — this is 2000s indie scrappiness. The collision of these two aesthetics is the visual identity.

**Influences**:
1. **Saul Bass Title Design** — Geometric clarity, bold color blocks, modernist simplicity (we reference this for festival branding and title cards)
2. **Swiss Graphic Design / International Typographic Style** — Helvetica, grid systems, hierarchy through scale and weight (we use this for business documents and UI labels)
3. **Criterion Collection Cover Design** — Prestige through restraint, intelligent use of white space, film-as-art positioning (we channel this for festival programs and award aesthetics)
4. **Polaroid Photography Aesthetic** — The square format, the white border, the slightly washed-out colors, the instant nostalgia (we use this for headshots and in-world photography)
5. **Newspaper Classified Ads / Zine Layouts** — Dense information, minimal decoration, DIY punk energy (we reference this for budget spreadsheets and shooting schedules)

### 9.4 Photography References

**Mood and Lighting Studies**:

1. **Gregory Crewdson** — Cinematic lighting in mundane spaces, the uncanny in the everyday (we steal his use of warm practicals in dim rooms)
2. **Stephen Shore** — Everyday American spaces shot with formal clarity, color saturation that is real but heightened (we reference his diner and office interiors)
3. **William Eggleston** — The epic in the ordinary, color as subject, democratic approach to composition (we study his use of reds and greens)
4. **Saul Leiter** — Layered compositions, reflections, urban warmth, the beauty of imperfect framing (we channel this for window views and environmental depth)
5. **Todd Hido** — Nocturnal suburban melancholy, warm windows in cold darkness (we reference this for late-night office scenes)

**Documentary References** (for office and production authenticity):

6. **Lost in La Mancha (2002)** — Terry Gilliam's production disaster, the reality of film chaos
7. **Hearts of Darkness (1991)** — Apocalypse Now's making-of, the madness of ambitious production
8. **Burden of Dreams (1982)** — Werner Herzog's Fitzcarraldo, obsession and compromise
9. **A Decade Under the Influence (2003)** — 1970s American cinema history, the golden age we are nostalgic for
10. **Easy Riders, Raging Bulls (documentary and book)** — The indie film movement of the 70s, the template for 2000s indie resurgence

### 9.5 Cultural Touchstones (2000s Indie Film Scene)

To accurately depict the mid-2000s indie film world, these films and entities define the period:

**Key Films of the Era** (visual and cultural references):
- **Eternal Sunshine of the Spotless Mind (2004)** — High-concept indie hitting mainstream
- **Sideways (2004)** — Sundance darling, small-scale character study
- **Brokeback Mountain (2005)** — Indie film as cultural flashpoint
- **Capote (2005)** — Awards bait, performance-driven prestige
- **Little Miss Sunshine (2006)** — Quirky indie formula perfected
- **Juno (2007)** — Peak indie aesthetic (for better or worse)
- **There Will Be Blood (2007)** — Auteur vision with scale
- **The Diving Bell and the Butterfly (2007)** — International prestige play
- **Wendy and Lucy (2008)** — Mumblecore maturity, Kelly Reichardt's arrival
- **500 Days of Summer (2009)** — Indie-to-mainstream crossover

**Festivals as Visual Brands**:
- **Sundance**: Red and white branding, snow and parkas, Park City main street, the mythos
- **Cannes**: Palais des Festivals stairs, red carpet, golden Palme, French Riviera glamour
- **Toronto (TIFF)**: Accessible and industry-focused, less glamour, more deal-making
- **Venice**: Oldest festival, Golden Lion, lagoon setting, European prestige
- **Berlin**: Golden Bear, February snow, political edge

**Distributors as Cultural Forces** (visual identities we reference):
- **Miramax** (dying but still haunting) — Purple and gold logo, prestige and predation
- **Focus Features** (ascendant) — Clean, modern, literary
- **Fox Searchlight** (indie arm of major) — Sophisticated, awards-focused
- **IFC Films** (truly independent) — Scrappy, auteur-friendly
- **The Weinstein Company** (2005-2017) — Doomed from birth, awards obsession

### 9.6 Music and Audio Mood References

Though this is an art direction document, the audio landscape shapes the visual one. These references define the sonic palette.

**Diegetic Music** (music that exists in the world, playing from sources in the office):

1. **Explosions in the Sky** — Post-rock instrumentals, the sound of contemplative creative work (plays from laptop speakers during late-night editing)
2. **The National** — Melancholic indie rock, the sound of 2000s festival after-parties (plays during office scenes)
3. **Iron & Wine** — Warm acoustic folk, the sound of earnest indie film soundtracks (temp score for dramas)
4. **Clint Mansell** — "Lux Aeterna" and Requiem for a Dream scoring, peak 2000s prestige (referenced in festival sequences)
5. **Sigur Rós** — Ethereal, emotional, the sound of art films that want to be important (temp score for ambitious projects)

**Ambient Office Sounds**:
- Phones ringing two rooms over (muffled, never answered)
- Laptop fan hum (2005 MacBook Pros were loud)
- Street noise through open windows (New York or LA traffic)
- Coffee maker gurgling
- Keyboard typing in short bursts (emails, notes)
- Papers shuffling
- The distant hum of a film projector (in the editing suite only)

**Menu Music** (non-diegetic):
- Acoustic guitar, finger-picking style (think José González or Nick Drake)
- Warm, slightly melancholic, contemplative
- No lyrics (lyrics anchor mood too specifically)
- 90-110 BPM (resting heart rate, calming but not sleepy)

### 9.7 Typography References

**Screenplay Formatting**:
- **The Academy of Motion Picture Arts and Sciences Screenplay Format Guide** — Industry standard
- Courier 12pt, specific margin rules, scene header formatting
- We adhere strictly to real screenplay formatting for immersion

**Business/Office Fonts of the 2000s**:
- **Arial and Helvetica** dominated corporate docs (we use Helvetica for authenticity)
- **Times New Roman** for formal contracts (we use Garamond as a more elegant serif alternative)
- **Verdana** for screen legibility (we avoid it — too web-2.0)

**Festival/Prestige Typography**:
- **Criterion Collection spine fonts** — Helvetica Neue for titles, clean and confident
- **TIFF** historically used Futura (bold geometric sans-serif) — we avoid exact replication but channel the vibe
- **Cannes** uses elegant serifs (we use Garamond for all Cannes-related materials)

**Handwriting References**:
- Real producer notes (scrawled, urgent, abbreviated)
- Script coverage reader notes (neater, more academic)
- We use Caveat font for handwriting — it is imperfect enough to feel human but legible enough to read at 12pt

---

## 10. Technical Constraints Summary

Art direction without technical grounding is fantasy. These constraints define what is possible.

### 10.1 Platform and Performance Targets

**Primary Platform**: PC (Windows/Mac/Linux via Steam)
**Secondary Platform**: Nintendo Switch
**Stretch Platform**: iPad (iOS)

**Resolution Targets**:
| Platform | Minimum Resolution | Target Resolution | UI Scale Factor |
|---|---|---|---|
| **PC** | 1920x1080 (1080p) | 2560x1440 (1440p) | 1x at 1080p, 1.33x at 1440p, 2x at 4K |
| **Nintendo Switch** | 1280x720 (handheld) | 1920x1080 (docked) | 0.66x handheld, 1x docked |
| **iPad** | 2048x2732 (iPad Pro) | 2048x2732 | 2x (Retina) |

**Framerate Targets**:
- **PC**: 60fps minimum, 120fps stretch goal
- **Switch**: 30fps minimum (handheld), 60fps target (docked)
- **iPad**: 60fps minimum

**Performance Budget per Frame** (at 60fps = 16.67ms per frame):
- Rendering: <8ms
- Game logic: <4ms
- UI updates: <2ms
- Audio: <1ms
- Overhead: <1.67ms

**Asset Memory Budget**:
- **PC**: 2GB VRAM, 4GB System RAM
- **Switch**: 512MB VRAM (shared with system), 3GB available RAM
- **iPad**: 1GB VRAM, 2GB available RAM

All assets must fit within Switch constraints (smallest target). This means aggressive texture atlasing, asset streaming, and no 4K uncompressed textures.

### 10.2 Engine and Tools

**Primary Engine**: **Unity 2022 LTS** (or **Godot 4.x** as open-source alternative)
- Rationale: 2D-optimized, excellent UI tools, robust asset pipeline, multi-platform export

**Art Tools**:
- **Photoshop CC** (or **Affinity Photo**) — Primary 2D asset creation
- **Figma** — UI mockups, layout design, component libraries
- **Blender** — 3D asset creation if needed (unlikely, but available for complex prop modeling)
- **After Effects** (or **Cavalry**) — Animated texture creation (coffee stains, paper effects)
- **Aseprite** — Pixel art / low-res animated elements if needed

**Font Management**:
- All fonts must be licensed for commercial game use (perpetual license, not subscription)
- Web fonts (WOFF2) for UI
- Desktop fonts (TTF/OTF) for source files
- Store all licensed fonts in `/assets/fonts/` with license documents in `/licenses/`

### 10.3 Texture and Sprite Specifications

**Texture Atlas Strategy**:
All UI elements are packed into texture atlases to minimize draw calls. Target: <10 draw calls per screen.

| Atlas | Size | Contents | Compression |
|---|---|---|---|
| **UI_Common** | 2048x2048 | Buttons, borders, panels, icons | ASTC (mobile), DXT5 (PC) |
| **Documents** | 2048x2048 | Script pages, contract templates, budget sheets | ASTC, DXT5 |
| **Headshots** | 4096x4096 | All talent headshots (procedurally placed) | ASTC, DXT5 |
| **Props** | 2048x2048 | Coffee cups, phones, pens, office clutter | ASTC, DXT5 |
| **Backgrounds** | 4096x4096 (multiple atlases) | Desk surfaces, walls, cork boards, windows | ASTC, DXT1 (no alpha) |

**Sprite Batching**:
- Unity's Sprite Atlas feature for automatic batching
- All sprites share same material to enable batching
- Maximum 4 texture atlases active per screen to stay within mobile GPU limits

**Compression Settings**:
- **Alpha-Required Assets**: ASTC 6x6 (mobile), DXT5 (PC)
- **No-Alpha Assets**: ASTC 8x8 (mobile), DXT1 (PC)
- **Text-Heavy Assets** (scripts, documents): Lower compression (ASTC 4x4) to preserve readability
- Never use uncompressed formats in final build

### 10.4 Rendering Constraints

**Shader Complexity**:
- No custom shaders except for specific effects (coffee stain spread, lighting overlays)
- Use Unity's built-in Sprite shaders for 99% of assets
- Maximum 5 shader passes per frame
- No real-time lighting (baked lighting only)

**Shadow and Lighting**:
- All shadows are baked into sprite textures (drop shadows pre-rendered)
- Lighting is environmental (baked ambient occlusion, painted highlights)
- Dynamic lighting only for hover states and notifications (simple additive glow, no raytracing)

**Transparency and Overdraw**:
- Minimize alpha blending (expensive on mobile GPUs)
- Maximum 3 layers of transparency per pixel (e.g., desk > paper > coffee stain)
- Use alpha cutout where possible instead of alpha blend

**Post-Processing**:
- Minimal post-processing to maintain performance
- Allowed: Subtle vignette (baked into background), color grading (LUT-based, single texture lookup)
- Forbidden: Bloom, motion blur, depth of field, screen-space reflections (too expensive for this art style)

### 10.5 Animation Constraints

**Sprite Animation**:
- Maximum 30fps for sprite sheet animations (sufficient for stylized motion)
- Maximum 12 frames per animation loop
- Total sprite sheet memory budget: 512MB across all animations

**UI Animation**:
- Use Unity's UI animation system (Animator + Animation Clips)
- Tweening via DOTween or similar library (more efficient than Animator for simple transforms)
- Maximum 10 simultaneous UI animations at any time

**Particle Systems**:
- Avoid Unity's particle systems (too heavy for 2D)
- Use sprite sheet animations for effects (coffee steam, paper flutter)
- Maximum 3 active VFX at once

### 10.6 Localization Constraints

**Text Expansion**:
- UI must accommodate 30% text expansion for German, French (longer words)
- All UI labels use dynamic text boxes (auto-resize within bounds)
- Minimum font size remains 10pt even with longer text (if text does not fit, abbreviate)

**Font Support**:
- Latin Extended (Western European languages)
- Cyrillic (Russian, Ukrainian)
- CJK (Chinese, Japanese, Korean) requires separate font files (large file sizes)
- Arabic/Hebrew (right-to-left) not supported in v1.0 (complex layout requirements)

**Localization-Safe Design**:
- Never embed text in images (must be extractable for translation)
- Use text components, not text textures
- All UI strings stored in external JSON files for easy translation

### 10.7 Accessibility Constraints

**Colorblind Support**:
- Three colorblind modes (protanopia, deuteranopia, tritanopia) via palette swaps
- All color-coded information also conveyed via icon or pattern
- Colorblind mode toggle in Settings, persists across sessions

**Font Scaling**:
- UI must support 100%, 125%, 150% font scaling
- Test at all three scales to ensure no text clipping
- Minimum readable size at 150% scaling: 18pt (12pt * 1.5)

**High Contrast Mode**:
- Optional high-contrast mode: Espresso and Cream only, all mid-tones removed
- For players with low vision or playing in bright environments
- Toggle in Settings

**Screen Reader Support**:
- Not implemented in v1.0 (complex for image-heavy UI)
- Alt-text for all interactive elements for potential future support

### 10.8 File Size Budget

**Total Game Size Target**: <2GB (comfortable for Switch cartridge, fast Steam download)

| Category | Budget | Notes |
|---|---|---|
| **Art Assets** | 800MB | Textures, sprites, backgrounds |
| **Audio** | 400MB | Music, SFX, ambient loops |
| **Fonts** | 20MB | Five typeface families with multiple weights |
| **Code and Engine** | 600MB | Unity runtime, game logic, plugins |
| **Misc** | 180MB | Localization files, save data templates, config |

**Compression Strategy**:
- All textures compressed (ASTC/DXT)
- Audio compressed (Vorbis OGG, 128kbps for music, 64kbps for SFX)
- Fonts subsetted (only include glyphs for supported languages)
- Asset bundles streamed where possible (future optimization)

If total size exceeds 2GB, cut in this order:
1. Reduce background texture resolution (4096 -> 2048)
2. Reduce audio bitrate (128kbps -> 96kbps for music)
3. Cut idle animations and rare VFX
4. Reduce headshot texture atlas size (4096 -> 2048, fewer unique headshots)

### 10.9 Testing Hardware Targets

All visual assets must be tested on this range of hardware before shipping:

**PC**:
- **Low-End**: Intel i5-7400, GTX 1050 Ti, 8GB RAM, 1080p monitor
- **Mid-Tier**: AMD Ryzen 5 3600, GTX 1660, 16GB RAM, 1440p monitor
- **High-End**: Intel i7-12700K, RTX 3070, 32GB RAM, 4K monitor

**Switch**:
- Test on actual Switch hardware (not just emulator)
- Test in handheld mode (worst-case performance and visibility)

**iPad**:
- iPad Pro 11" (2021 or newer)
- iPad Air (for lower-end target)

If performance fails on low-end hardware, art fidelity is reduced (texture resolution, shadow complexity, animation quantity) until 60fps is achieved.

---

## 11. Production Milestones and Deliverables

Art direction is not complete until the art exists. This section defines the production schedule and deliverables.

### 11.1 Phase 1: Concept and Proof-of-Concept (Weeks 1-4)

**Goal**: Validate the visual identity with a single fully-realized screen.

**Deliverables**:
1. **Mood Board** (Week 1)
   - 40-60 reference images organized by category (lighting, color, composition, UI, typography)
   - Figma board or Pinterest collection
   - Approval by Art Director + Game Director

2. **Color Palette Test** (Week 1)
   - All primary and secondary colors rendered as swatches
   - Contrast ratio test results documented
   - Colorblind mode swatches generated

3. **Typography Test** (Week 2)
   - All five typefaces rendered at key sizes (9pt, 10pt, 12pt, 14pt, 20pt, 28pt)
   - Sample script page, sample budget sheet, sample UI panel with labels
   - Legibility test at 1080p

4. **Greenlight Table Mockup** (Weeks 2-3)
   - Fully realized single screen (Greenlight Table with 3 scripts visible)
   - Grayscale blockout > color pass > texture pass > final polish
   - Interactive prototype in Figma (hover states, click interactions)

5. **Animation Test** (Week 3)
   - Three key animations: script drag, camera pan, coffee stain spread
   - Rendered as video or Unity prototype
   - Timing and easing validated against Section 7 specs

6. **Playtest and Iterate** (Week 4)
   - Internal playtest with 5 team members
   - External playtest with 3 target audience members
   - Readability checklist (Section 8) applied
   - Revision based on feedback

**Approval Gate**: If the Greenlight Table mockup passes readability tests and receives 80%+ positive feedback, proceed to Phase 2. If not, revise and re-test (maximum 2 revision rounds).

### 11.2 Phase 2: Core UI Screens (Weeks 5-12)

**Goal**: Build all six major UI zones to final quality.

**Deliverables**:
1. **Talent Web Screen** (Weeks 5-6)
   - Cork board with 10 headshots, connection strings, stat cards
   - Interactive prototype (click headshot to flip, hover to see relationships)

2. **Production Clock Screen** (Weeks 7-8)
   - Whiteboard with shooting schedule, day-by-day tracking, crisis event overlays
   - Interactive prototype (mark days complete, trigger crisis events)

3. **Avid Bay Screen** (Weeks 9-10)
   - CRT monitor with editing timeline, scene cards, editorial approach UI
   - Interactive prototype (drag scene cards, apply color grade, preview changes)

4. **Ledger Screen** (Week 11)
   - CRT monitor with spreadsheet, burn-rate visualization, revenue notifications
   - Interactive prototype (budget line updates, number roll animations)

5. **Festival Wall Screen** (Week 12)
   - Wall with festival programs, laurels, distribution deal documents
   - Interactive prototype (pin laurel animation, festival result sequence)

**Approval Gate**: Each screen passes readability checklist and silhouette test before moving to next screen. If any screen fails twice, escalate to design review (may indicate systemic UI problem).

### 11.3 Phase 3: Asset Production (Weeks 13-20)

**Goal**: Generate all in-game assets at scale (scripts, headshots, props, backgrounds).

**Deliverables**:
1. **Script Templates** (Week 13)
   - 50 unique script cover designs (procedurally generated from 10 base templates)
   - 5 script page layouts (different screenplay formats)
   - Script texture atlas built

2. **Headshot Photography** (Weeks 14-16)
   - 80-120 unique headshots (hire actors/models for photo shoot, or use stock photography with commercial license)
   - Processed to match color palette and lighting
   - Headshot texture atlas built

3. **Props and Office Objects** (Week 17)
   - 30-40 unique props (coffee cups, phones, pens, staplers, film canisters, etc.)
   - Modeled in 3D or illustrated in 2D, depending on complexity
   - Props texture atlas built

4. **Backgrounds and Surfaces** (Week 18)
   - Desk surface (oak, walnut, metal variants)
   - Wall surfaces (painted drywall, exposed brick)
   - Cork board, whiteboard, window view
   - Background texture atlas built

5. **VFX and Animated Textures** (Week 19)
   - Coffee stain spread (PNG sequence, 12 frames)
   - Paper crumple (4 frames)
   - Steam wisp (8 frames, looping)
   - Phone ring indicator (6 frames, looping)

6. **UI Components Library** (Week 20)
   - All buttons, borders, panels, icons
   - Packaged as Figma component library + Unity prefabs
   - UI texture atlas built

**Approval Gate**: All assets pass QA checklist (Section 6.4) before integration.

### 11.4 Phase 4: Animation and Polish (Weeks 21-24)

**Goal**: Bring the office to life with animation and micro-interactions.

**Deliverables**:
1. **Camera Transitions** (Week 21)
   - All camera pans between UI zones (6 zones = 15 unique transitions)
   - Smooth easing, correct timing (0.6-0.8s)

2. **UI Micro-Interactions** (Week 22)
   - All hover states, click feedback, drag-and-drop animations
   - Implemented in Unity with DOTween

3. **Notification and Feedback Animations** (Week 23)
   - Budget updates (number roll, color flash)
   - Relationship changes (string color shift)
   - Festival results (laurel pin animation)

4. **Environmental Idle Loops** (Week 24)
   - Coffee steam (looping, subtle)
   - Monitor flicker (occasional, rare)
   - Ambient office details (plant sway, poster peel — only if time permits)

**Approval Gate**: Animation budget check (Section 7.5). If frame rate drops below 60fps on mid-tier hardware, cut lowest-priority animations.

### 11.5 Phase 5: Localization and Accessibility (Weeks 25-28)

**Goal**: Ensure the game is playable and readable for all target audiences.

**Deliverables**:
1. **Colorblind Modes** (Week 25)
   - Implement three palette swaps (protanopia, deuteranopia, tritanopia)
   - Test all UI screens in each mode

2. **Font Scaling** (Week 26)
   - Implement 100%, 125%, 150% scaling options
   - Test all screens at each scale, fix text clipping

3. **High Contrast Mode** (Week 27)
   - Implement Espresso/Cream-only palette swap
   - Test readability in bright lighting conditions

4. **Localization Prep** (Week 28)
   - Extract all UI strings to JSON
   - Mark all text fields as localizable
   - Provide translation kit to localization team (spreadsheet with context for each string)

**Approval Gate**: Accessibility checklist (Section 8.3) passes at 100%. No shipping without colorblind support and font scaling.

### 11.6 Phase 6: Bug Fixing and Optimization (Weeks 29-32)

**Goal**: Achieve stable 60fps and fix all visual bugs.

**Deliverables**:
1. **Performance Profiling** (Week 29)
   - Profile on all target hardware (PC low/mid/high, Switch handheld/docked, iPad)
   - Identify bottlenecks (draw calls, texture memory, animation overhead)

2. **Optimization Pass** (Week 30)
   - Reduce texture atlas sizes if memory budget exceeded
   - Batch sprites more aggressively
   - Cut or simplify animations causing frame drops

3. **Visual Bug Fixing** (Week 31)
   - Fix z-sorting issues (elements rendering in wrong order)
   - Fix texture seams and atlas bleeding
   - Fix animation stutters and timing issues

4. **Final QA** (Week 32)
   - Full playthrough on all platforms
   - Verify all assets render correctly
   - Verify all readability checks pass
   - Verify all accessibility features function

**Approval Gate**: 60fps on all platforms, zero critical visual bugs, all readability tests passing. If any test fails, extend this phase by 1 week and re-test.

### 11.7 Post-Launch Content (Ongoing)

**Goal**: Expand asset library for variety and replayability.

**Potential Deliverables** (prioritized by impact):
1. **Seasonal Office Variations** (4 versions: winter, spring, summer, fall)
   - Lighting shifts (cooler in winter, warmer in summer)
   - Environmental details (snow outside window, open window with breeze, autumn leaves)

2. **Office Upgrades** (3 tiers: scrappy startup, established studio, prestige powerhouse)
   - Better furniture, framed one-sheets, awards on shelves
   - Visual progression tied to Reputation tiers (Section 5.1 in GDD)

3. **Additional Headshot Sets** (50-100 more unique headshots)
   - Increases talent pool variety for long playthroughs

4. **Festival Venue Art** (interior views of Sundance theater, Cannes Palais, TIFF venue)
   - Rare, dramatic moments (premiere sequences, award ceremonies)

5. **Historical Industry Events** (DLC potential)
   - Digital camera debate UI (film vs. digital choice screen)
   - Streaming platform emergence (new distribution option UI)

---

## 12. Final Notes from PIXEL

This document is the contract between vision and execution. Every hex code, every typeface choice, every animation timing — these are not suggestions. These are specifications. The visual identity of BACKLOT lives or dies on consistency.

Here is what I need from the team:

**From Engineers**: Do not add UI elements that are not in this spec without consulting me. Do not use colors outside the palette. Do not change font sizes for "just this one screen." Every deviation fragments the identity. If the spec is insufficient, tell me and I will revise it. Do not improvise.

**From Artists**: Reference this document daily. When in doubt, check the Do's and Don'ts. When the deadline is tight and you are tempted to cut corners, remember: a few clean, polished screens beat a dozen janky ones. Quality over quantity. Consistency over novelty.

**From QA**: The readability checklist is not optional. Every screen must pass before it ships. If a tester squints, we fail. If a colorblind player cannot distinguish budget states, we fail. Accessibility is not a stretch goal. It is table stakes.

**From Marketing**: Every screenshot, every trailer frame, every Steam capsule image must represent this visual identity. Do not cherry-pick half-finished screens because they "look cool." Wait for the polished ones. The first screenshot a player sees defines their expectations. We get one chance to make that promise. Do not waste it.

This game's visual identity is its first and loudest statement. It says: "This is a game about making films, and we have made a film-quality game." It says: "We respect your intelligence and your taste." It says: "This is not a spreadsheet with a film industry skin. This is a world you can inhabit."

If we execute this spec with discipline and craft, the player will sit at that desk, pin that headshot to that cork board, and greenlight that script about a deaf saxophonist in Reno — and they will feel like a producer. Not like someone playing a producer. Like a producer.

That is the bar.

Show me, don't tell me.

Make it read.

Make it real.

— **PIXEL**

---

**End of Art Direction Document**
**BACKLOT v1.0**
**Total Word Count: ~15,800 words**