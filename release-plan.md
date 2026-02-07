# BACKLOT — Release Plan

**SHIP, Release Manager**
**Status: Pre-Production Release Readiness v1.0**
**Target Platform: PC (Steam Primary), Nintendo Switch (Secondary, post-launch)**
**Estimated Launch Window: Q3 2026 (assuming 8-month core dev + 3-month polish/QA)**

---

## 1. Executive Summary

BACKLOT is a PC-first, UI-heavy management sim with zero tolerance for launch-day surprises. We are targeting Steam as primary platform with a potential Switch port 3-6 months post-launch. This is not a live-service game. This is not an early access game. We ship 1.0 when it is ready, and "ready" means the checklist is complete.

**Core Release Challenges**:
1. **Steam Store Page Optimization** — Management sims live or die by capsule art and first 30 seconds of trailer
2. **Day-One Stability** — No game-breaking bugs in first 3 films (where 80% of players will be)
3. **Save System Integrity** — If a player loses 10 hours to a corrupted save, we are dead
4. **Procedural Content Quality** — Coverage reports must feel authored, not algorithmic
5. **Age Ratings** — ESRB/PEGI submission requires 6-8 weeks lead time minimum

**What Could Go Wrong**:
- Save file corruption on edge cases (bankruptcy during phase transition, quit during autosave)
- Procedural script generation produces offensive/incoherent content (needs content filtering)
- Performance drops on min-spec hardware (2019 laptops with integrated graphics)
- Steam Deck compatibility issues (UI readability at 800p, input handling)
- Festival jury scoring feels random (players cannot learn the system)
- First-time-user-experience overwhelm (too much information, too fast)

**Launch Day Success Criteria**:
- 95%+ of players complete Film 1 without hitting a blocking bug
- Zero save file corruption reports in first 48 hours
- Metacritic User Score above 7.0 in first week
- Steam review sentiment "Very Positive" (80%+ positive)
- Zero ESRB/PEGI compliance issues flagged
- Server uptime 99.9%+ (Steam Cloud Saves sync)

This document is the checklist. If it is not on the checklist, it does not happen. If it is on the checklist and not checked, we do not ship.

---

## 2. Master Launch Checklist

### 2.1 BUILD PIPELINE

**Code Complete Milestone** (Milestone 4 in tech doc: Week 32)

- [ ] All feature pillars implemented and tested (Greenlight, Talent Web, Production Clock, Avid Bay, Festival Circuit, Ledger)
- [ ] All stretch goals evaluated and cut/deferred if not production-ready
- [ ] Code freeze date set (2 weeks before gold master)
- [ ] Final commit tagged in Git (`v1.0-release-candidate`)
- [ ] Build versioning system implemented (semantic versioning: 1.0.0)
- [ ] Debug logs and development cheats disabled in release build
- [ ] Profanity filter implemented for procedural text generation (script titles, press quotes)
- [ ] Offensive content screening pass complete (no slurs, no real-world figure names in procedural generation)

**Build Automation** (Week 32-34)

- [ ] Automated build pipeline functional (GitHub Actions exports Windows/Linux/macOS on commit)
- [ ] Smoke test suite runs on every build (load game, simulate 1 film, save/load, exit cleanly)
- [ ] Build artifacts stored with version tags and timestamps
- [ ] Release build optimization flags enabled (strip debug symbols, compress assets)
- [ ] Build size under 500MB (target: 350-450MB installed)
- [ ] Crash reporter integrated (error logs written to user directory, instructions to submit)

**Platform-Specific Builds** (Week 34-36)

- [ ] **Windows 10/11 (64-bit)**: Exported, tested on clean VM (no dev tools installed)
- [ ] **Linux (Ubuntu 20.04+, SteamOS 3.0)**: Exported, tested on clean VM and Steam Deck
- [ ] **macOS (10.15+, Intel + Apple Silicon)**: Exported, notarized with Apple, tested on both architectures
- [ ] Steam Deck verified on all three platforms (input, performance, UI readability)
- [ ] Controller support functional on all platforms (Xbox, PlayStation, Switch Pro tested)
- [ ] Minimum spec validation: Game runs at 30 FPS minimum on 2019 Intel i5 + integrated graphics at 1280x720

**Gold Master Candidate** (Week 36)

- [ ] Release Candidate 1 (RC1) built and distributed to QA
- [ ] RC1 tested for 72 hours minimum (full playthroughs, edge cases, stress tests)
- [ ] All P0 bugs fixed (blocking, crashes, save corruption)
- [ ] All P1 bugs fixed or documented as Known Issues (visual glitches, minor balance issues)
- [ ] P2 bugs triaged for post-launch patch (nice-to-haves, stretch feature bugs)
- [ ] RC2 built if P0/P1 bugs found in RC1 testing
- [ ] Final Gold Master approved by Lead Programmer (BYTE) and QA Lead (CRASH)
- [ ] Gold Master SHA hash recorded (for rollback verification)

---

### 2.2 PLATFORM CONFIGURATION (STEAM)

**Steamworks Setup** (Week 30-32, begins before code complete)

- [ ] Steamworks developer account active and billing configured
- [ ] App ID reserved and configured (store page URL locked)
- [ ] Depot structure defined (base game, Windows/Linux/macOS depots)
- [ ] Steam Cloud Save enabled (save files sync to cloud, 100MB quota sufficient)
- [ ] Steam Cloud Save tested across platforms (save on Windows, load on Linux, verify integrity)
- [ ] Steam Overlay functional in-game (Shift+Tab)
- [ ] Steam Input API integrated (controller glyphs match connected controller)
- [ ] SteamAPI initialization and shutdown clean (no leaks, no crashes on exit)

**Store Page Configuration** (Week 28-30, can begin early)

- [ ] Store page copy written and reviewed (follows Steam guidelines, no prohibited claims)
- [ ] Short description (300 characters): hook and core loop clear
- [ ] Long description (detailed feature list, comparables, tone)
- [ ] Capsule images created and uploaded:
  - [ ] Header capsule (460x215): Must read at thumbnail size
  - [ ] Small capsule (231x87): High contrast, readable text
  - [ ] Main capsule (616x353): Primary storefront image
  - [ ] Hero capsule (1920x620): Featured section image
- [ ] Screenshots (minimum 5, target 8-10):
  - [ ] Greenlight Table with script coverage visible
  - [ ] Talent Web relationship graph
  - [ ] Production Clock crisis decision
  - [ ] Avid Bay editorial selection
  - [ ] Festival results screen (positive outcome)
  - [ ] Ledger financial UI
  - [ ] Studio office overview (diegetic UI showcase)
  - [ ] Cork board with headshots and red string
- [ ] Trailer video uploaded (1:30-2:00 runtime, hook in first 10 seconds)
- [ ] Store tags selected (minimum 10, maximum 20):
  - Management, Simulation, Indie, Strategy, Singleplayer
  - Character-Driven, Story Rich, Choices Matter, Resource Management
  - Replay Value, Atmospheric, Stylized, 2D, Point & Click
- [ ] Age rating set (see Section 4 for ESRB/PEGI submission)
- [ ] Release date set (hard date, not "Coming Soon")
- [ ] Pricing configured (regional pricing set via Steam recommendations)
- [ ] Pre-purchase options evaluated (Yes/No decision, discount tier if Yes)
- [ ] Launch discount configured (10-20% for first week, standard practice)

**Community Hub and Features** (Week 32-34)

- [ ] Community Hub activated
- [ ] Discussion forums configured (General, Bug Reports, Suggestions)
- [ ] Workshop disabled (not applicable for this game)
- [ ] Community moderators identified (minimum 2: developer + trusted community member)
- [ ] Bug report template pinned in forums
- [ ] FAQ document written and pinned (common questions, known issues, system requirements)
- [ ] Steam News feed configured (announcements, patch notes)

**Achievements** (Week 30-32)

- [ ] Achievement list finalized (target: 20-30 achievements, mix of progression and challenge)
- [ ] Achievement icons created (64x64 locked/unlocked states)
- [ ] Achievements integrated in code (SteamAPI calls, unlock conditions tested)
- [ ] Hidden achievements flagged (spoiler-heavy, discovered through play)
- [ ] Achievement rarity balanced (aim for 10-20% ultra-rare, 40-60% common)
- [ ] Example achievement structure:
  - "First Frame" — Complete your first film
  - "Sundance Darling" — Win a Sundance jury prize
  - "Palme d'Or" — Win the top prize at Cannes
  - "Comeback Kid" — Successfully cast a Comeback-flagged talent
  - "Muse" — Develop a Muse bond between actor and director
  - "Bankrupt But Not Broken" — Recover from bankruptcy
  - "Auteur" — Maintain Artistic Identity above 80 for 5 years
  - "Commercial King" — Earn $5M lifetime revenue
  - "Festival Circuit" — Submit to all 5 major festivals in one playthrough
  - "Legacy" — Complete 20 films

**Trading Cards (Optional, Low Priority)** (Post-Launch)

- [ ] Decision: Yes/No on trading cards (requires 6-9 card designs + badges)
- [ ] Card art commissioned (film-themed: director's chair, festival laurel, script pages, etc.)
- [ ] Steam Trading Card program application submitted
- [ ] Badge levels configured

---

### 2.3 PLATFORM CONFIGURATION (NINTENDO SWITCH — POST-LAUNCH)

This section applies only if Switch port is greenlit post-launch. Target: Q1 2027 (3-6 months after PC launch).

**Nintendo Developer Program** (Begin 3-4 months before Switch launch)

- [ ] Nintendo Developer Portal account created
- [ ] Switch DevKit acquired (2-4 week lead time)
- [ ] Lotcheck submission guidelines reviewed (Nintendo's QA requirements)
- [ ] Age rating obtained (IARC system or direct ESRB/PEGI submission, see Section 4)

**Switch Build Configuration** (4-6 weeks before Switch launch)

- [ ] Godot Switch export template configured (official Nintendo SDK required)
- [ ] Controller input remapped for Joy-Con and Pro Controller (no mouse references in UI)
- [ ] UI scaled for 720p handheld mode (minimum font size 16pt, tested on actual hardware)
- [ ] Performance target met (30 FPS minimum, 60 FPS target for docked mode)
- [ ] Save data integration with Nintendo Account cloud saves
- [ ] Playtime tracking functional (Nintendo Switch Parental Controls)
- [ ] eShop metadata configured (screenshots, trailer, description)
- [ ] eShop icon created (256x256, readable at small sizes)
- [ ] Nintendo Lotcheck submission passed (Nintendo QA, 2-4 week turnaround)

---

### 2.4 AGE RATINGS (ESRB / PEGI / IARC)

**Required for Launch** (Begin 8 weeks before launch)

BACKLOT contains:
- Alcohol references (talent trait: Hard Drinker; industry party events)
- Drug references (possible event: talent in rehab, reference to substance use)
- Mild language (possible in procedural press quotes: "a baffling misfire" is fine; profanity filter prevents worse)
- No violence, no sexual content, no gambling

**Expected Ratings**:
- ESRB: **T for Teen** (13+) — Alcohol/Drug Reference, Language
- PEGI: **PEGI 12** — Alcohol/Drug Reference, Bad Language
- IARC: Equivalent to above

**Submission Process (IARC — Fastest Option)** (Week 30-32)

- [ ] IARC questionnaire completed (via Steamworks or direct submission)
- [ ] Gameplay footage prepared (30-60 minutes showing all content types: talent events, press quotes, UI)
- [ ] Content descriptor list compiled (all potentially sensitive content documented)
- [ ] IARC certificate received (typically 1-2 business days)
- [ ] ESRB/PEGI ratings assigned automatically via IARC (no separate submission needed for digital-only)
- [ ] Rating icons downloaded and added to store page and game boot screen

**Alternative: Direct ESRB Submission** (If IARC unavailable or physical release planned) (Week 28-32)

- [ ] ESRB application submitted (online form, gameplay footage, content description)
- [ ] Submission fee paid ($800-$4000 depending on budget tier)
- [ ] Review period (4-6 weeks typical)
- [ ] Rating certificate received
- [ ] Rating icon integrated into marketing materials and game boot screen

**Content Filtering Pass** (Week 30, before rating submission)

- [ ] Profanity filter tested in procedural text generation (script titles, press quotes, character names)
- [ ] Substance references reviewed (ensure contextual, not glamorizing)
- [ ] All talent trait event text reviewed for age-appropriateness (rehab references acceptable; explicit drug use descriptions not acceptable)
- [ ] Press quote library reviewed for prohibited language
- [ ] Edge cases tested (does random name generation ever produce offensive combinations?)

**Rating Display Compliance** (Week 36, final build)

- [ ] Rating icon displayed on boot screen (ESRB/PEGI logo, 3 seconds minimum)
- [ ] Rating descriptor text included (e.g., "Alcohol Reference, Language")
- [ ] Store page updated with rating icons
- [ ] Trailer/marketing materials include rating bug in corner (required for YouTube/TV ads)

---

### 2.5 QUALITY ASSURANCE AND BUG TRIAGE

**QA Phases** (Week 28-36)

**Alpha QA** (Week 28-30, after Milestone 3)

- [ ] Internal QA begins (CRASH + 1-2 external testers)
- [ ] Focus: Core loop stability (Greenlight -> Festival completion without crashes)
- [ ] Focus: Save/load integrity (save at every phase, load, verify state)
- [ ] Focus: Procedural content quality (coverage reports, press quotes, event text)
- [ ] P0 bugs logged and fixed immediately (blockers)
- [ ] P1 bugs logged for pre-launch fix (major issues, balance problems)
- [ ] P2 bugs logged for post-launch patch (minor issues, polish)

**Beta QA** (Week 32-34, after Milestone 4)

- [ ] External beta (50-100 trusted testers via Steam playtesting feature or closed keys)
- [ ] Beta NDA and feedback form distributed
- [ ] Focus: Edge cases (bankruptcy during phase transition, quit during autosave)
- [ ] Focus: Long-play stability (10+ films completed without crash or corruption)
- [ ] Focus: Platform coverage (Windows, Linux, macOS, Steam Deck tested)
- [ ] Focus: Accessibility (controller support, font readability, colorblind-friendly UI)
- [ ] Community feedback aggregated (balance, pacing, clarity)
- [ ] P0/P1 bugs from beta fixed in RC1

**Release Candidate QA** (Week 35-36)

- [ ] RC1 tested for 72 hours minimum (full playthroughs, stress tests)
- [ ] Regression testing (ensure bug fixes did not break other systems)
- [ ] Edge case matrix tested (see Section 6.2)
- [ ] Performance profiling on min-spec hardware (30 FPS floor verified)
- [ ] Save file compatibility tested (old saves load correctly in new build)
- [ ] RC2 built if critical bugs found; repeat QA cycle
- [ ] Final sign-off from QA Lead (CRASH) required for Gold Master

**Bug Triage Criteria**

| Priority | Definition | Examples | Action |
|---|---|---|---|
| **P0** | Blocks core loop or causes data loss | Crash during save, infinite loop in Production Clock, save file corruption | Fix immediately, delay launch if needed |
| **P1** | Major functional or balance issue | Festival scoring broken, talent negotiation always fails, UI unreadable on Steam Deck | Fix before launch |
| **P2** | Minor issue, does not block play | Typo in press quote, UI animation glitch, achievement not unlocking | Fix in post-launch patch |
| **P3** | Polish, nice-to-have | Additional sound effects, UI color tweak, tooltip clarification | Deferred to future update |

**Known Issues Document** (Week 36, before launch)

- [ ] All P2/P3 bugs documented in Known Issues list
- [ ] Known Issues posted to Steam Community Hub and FAQ
- [ ] Workarounds provided where applicable (e.g., "If achievement does not unlock, restart game")

---

### 2.6 ROLLBACK AND HOTFIX PROCEDURES

**What is the rollback plan?** This is the question I ask before every launch. Here is the answer.

**Pre-Launch Preparation** (Week 36)

- [ ] Gold Master SHA hash recorded and stored securely (rollback reference)
- [ ] Steam depot rollback procedure documented (Steamworks allows depot rollback per-platform)
- [ ] Emergency contact list created (Lead Programmer, QA Lead, Steamworks admin, PR contact)
- [ ] Hotfix build pipeline tested (can we build, test, and deploy a patch in 24 hours?)
- [ ] Communication templates prepared (Steam News post, Twitter/social announcement, email to press)

**Launch Day Monitoring Plan** (Launch Day + 72 hours)

- [ ] Launch day "war room" scheduled (all hands available for 8-hour window during launch)
- [ ] Steam Community Hub monitored every 2 hours (bug reports, player feedback)
- [ ] Crash logs monitored (check user-submitted logs in designated forum thread or email)
- [ ] Player sentiment tracked (Steam reviews, social media mentions, Reddit threads)
- [ ] Metrics dashboard active (Steam player count, session length, completion rates via Steamworks stats)

**Hotfix Trigger Criteria** (Decision Tree)

A hotfix is deployed if ANY of the following occur in first 48 hours:

1. **P0 Bug Confirmed by 3+ Players**: Save corruption, crash-on-launch, infinite loop
2. **Completion Rate Below 60%**: If fewer than 60% of players complete Film 1, core loop is broken
3. **Review Sentiment Below 50% Positive**: If Steam reviews drop below 50% positive, critical issue present
4. **Data Loss Reports**: Any report of lost save files or progress

**Hotfix Deployment Process** (24-48 Hour Turnaround)

- [ ] Bug confirmed and reproduced by QA (CRASH)
- [ ] Fix implemented by Lead Programmer (BYTE)
- [ ] Hotfix build created (version bump: 1.0.0 -> 1.0.1)
- [ ] Hotfix tested on all platforms (Windows, Linux, macOS) minimum 2 hours each
- [ ] Hotfix uploaded to Steam (separate depot or patch branch)
- [ ] Steam News post published ("Hotfix 1.0.1 - Fixes [specific issue]")
- [ ] Community notified (Reddit, Twitter, Discord if applicable)
- [ ] Monitoring resumes for 24 hours post-hotfix

**Rollback Procedure** (Last Resort, IF Hotfix Fails)

- [ ] Steam depot reverted to Gold Master build (Steamworks console, per-platform)
- [ ] Store page updated with notice ("Temporary rollback to resolve critical issue")
- [ ] Refund policy communicated (Steam allows refunds within 2 weeks / 2 hours playtime)
- [ ] Post-mortem scheduled within 48 hours (what went wrong, how do we prevent this)

**Communication Templates (Pre-Written)** (Week 36)

**Template: Hotfix Announcement (Steam News)**

```
BACKLOT - Hotfix 1.0.1 Now Live

We've deployed a hotfix to address the following issues reported by players:

- [Specific bug description]
- [Specific bug description]
- [Specific bug description]

The update will download automatically. If you continue to experience issues, please verify game files (Steam > Library > Right-click BACKLOT > Properties > Local Files > Verify Integrity).

Thank you for your patience and for reporting these issues. We're monitoring feedback closely and will continue to address bugs as they arise.

- The BACKLOT Team
```

**Template: Rollback Announcement (Emergency)**

```
BACKLOT - Temporary Rollback to Resolve Critical Issue

We've temporarily reverted BACKLOT to the previous stable build while we investigate a critical issue affecting save file integrity. We sincerely apologize for the disruption.

If you've experienced data loss, please contact us at [support email] with your save file location so we can attempt recovery.

We expect to have a corrected build live within 24-48 hours. Updates will be posted here as we have them.

- The BACKLOT Team
```

---

### 2.7 POST-LAUNCH MONITORING AND PATCH ROADMAP

**First Week Post-Launch**

- [ ] Daily monitoring (Steam reviews, forums, social media, crash logs)
- [ ] Player completion rate tracked (via Steamworks stats: % who complete Film 1, Film 5, Film 10)
- [ ] Average session length tracked (target: 60-90 minutes per session)
- [ ] Peak concurrent players noted (for server capacity planning if future features require)
- [ ] Community sentiment summary compiled (positive, negative, neutral themes)

**First Month Post-Launch**

- [ ] Patch 1.1 scoped based on player feedback (balance tweaks, P2 bug fixes, QOL improvements)
- [ ] Patch 1.1 features documented:
  - Bug fixes from Known Issues list
  - Balance adjustments (e.g., Production Clock pacing, festival jury scoring clarity)
  - UI/UX improvements (e.g., additional tooltips, faster animations)
  - Performance optimizations if needed
- [ ] Patch 1.1 developed, tested, and deployed within 4 weeks of launch
- [ ] Patch notes published (Steam News, community forums)

**Post-Launch Content Roadmap (Optional, Low Priority)** (Month 2-6)

IF the game is stable and well-received, evaluate DLC or free content updates:

- [ ] **Free Update 1.2**: Industry Shift Events (Year 5+ events: digital cameras replace film, DVD collapse, streaming emerges)
- [ ] **Free Update 1.3**: Rival Studio system (AI-controlled competitors, talent poaching, festival competition)
- [ ] **DLC Consideration**: "The Awards Season" expansion (Oscar campaign simulation, guild politics, FYC ads)

**Metrics to Track** (Ongoing)

- Steam player retention (% who return after 1 week, 1 month)
- Average films completed per player (target: 5+)
- Review sentiment trend (positive/negative ratio over time)
- Refund rate (Steam refunds within 2 weeks, target: <5%)
- Community engagement (forum activity, Discord activity if applicable)

---

## 3. Build Pipeline and Deployment

### 3.1 Version Control and Branching Strategy

**Git Branches** (Established Week 1 of development)

- `main`: Always stable, always builds. Tagged releases only. Protected branch.
- `develop`: Integration branch for features. All feature branches merge here first.
- `feature/*`: Individual systems (e.g., `feature/talent-web`, `feature/festival-circuit`)
- `hotfix/*`: Emergency fixes branched from `main`, merged back to `main` and `develop`
- `release/*`: Release candidate branches (e.g., `release/1.0`, `release/1.1`)

**Release Tagging** (Week 36)

- [ ] `v1.0-rc1`: Release Candidate 1 (submitted to QA)
- [ ] `v1.0-rc2`: Release Candidate 2 (if needed after QA fixes)
- [ ] `v1.0-gold`: Gold Master (final approved build, deployed to Steam)
- [ ] `v1.0.1`: Hotfix 1 (if needed post-launch)

### 3.2 Build Automation (GitHub Actions)

**CI/CD Pipeline** (Configured Week 8-10)

- [ ] GitHub Actions workflow configured (see tech doc Section 9.1)
- [ ] Automated exports on commit to `develop` and `release/*` branches
- [ ] Smoke tests run automatically (load game, simulate 1 film, save/load, exit)
- [ ] Build artifacts uploaded to GitHub Releases (Windows, Linux, macOS ZIPs)
- [ ] Discord/Slack notification on build success or failure (optional but helpful)

**Manual Build Process** (Gold Master, Week 36)

- [ ] Lead Programmer (BYTE) manually triggers final export from `release/1.0` branch
- [ ] Exports generated for all platforms (Windows, Linux, macOS)
- [ ] File integrity verified (SHA256 hashes generated and recorded)
- [ ] Builds uploaded to secure storage (Google Drive, Dropbox, or private server)
- [ ] QA receives builds for final RC testing

### 3.3 Steam Deployment (Steamworks)

**Steamworks Depot Upload** (Week 36)

- [ ] Steamworks SDK configured locally (steamcmd or Steamworks GUI uploader)
- [ ] Depots uploaded per platform:
  - Depot 1: Windows 64-bit
  - Depot 2: Linux 64-bit
  - Depot 3: macOS (Universal binary: Intel + Apple Silicon)
- [ ] Depot builds marked as "default" branch (live release)
- [ ] Beta branch configured (optional, for testing patches before public release)
- [ ] Upload verified (download build from Steam, run smoke test)

**Launch Day Deployment** (Launch Day, 10:00 AM PST typical)

- [ ] Steam store page set to "Released" (no longer "Coming Soon")
- [ ] Launch discount activated (10-20% for first week)
- [ ] Community Hub unlocked (forums, discussions, screenshots)
- [ ] Steam News post published ("BACKLOT is now available!")
- [ ] Developer presence in forums for first 8 hours (respond to questions, monitor bugs)

---

## 4. Launch Day Timeline (Hour-by-Hour)

**Target Launch Time: 10:00 AM Pacific (Steam standard launch window)**

### Pre-Launch (T-24 to T-0)

**T-24 Hours** (Day Before Launch)

- [ ] Final build verification (Gold Master tested one last time on clean machines)
- [ ] Steam store page reviewed (no typos, correct pricing, correct release date/time)
- [ ] Press embargo lifted (if review copies sent to press, embargo ends at launch)
- [ ] Social media posts scheduled (launch announcement, trailer, store link)
- [ ] Team briefed (roles and responsibilities for launch day monitoring)

**T-4 Hours** (Morning of Launch)

- [ ] War room active (all hands available: BYTE, CRASH, SHIP, HYPE)
- [ ] Steam Community Hub checked (preemptive moderation, ensure clean state)
- [ ] Monitoring dashboard live (Steam stats, review sentiment, forum activity)
- [ ] Communication channels open (Discord, Slack, email)

**T-1 Hour**

- [ ] Final store page check (release time confirmed: 10:00 AM PST)
- [ ] Social media posts queued (launch announcement goes live at T-0)

### Launch Window (T-0 to T+8)

**T-0: 10:00 AM PST — LAUNCH**

- [ ] Store page goes live (players can purchase and download)
- [ ] Social media posts published (Twitter, Reddit, Discord, Facebook)
- [ ] Steam News post published ("BACKLOT is now available!")
- [ ] Team begins monitoring (every 30 minutes for first 2 hours, then hourly)

**T+1 Hour**

- [ ] Check Steam reviews (any negative reviews flagged for investigation)
- [ ] Check forums (any bug reports triaged immediately)
- [ ] Check player count (Steam Charts or Steamworks stats)
- [ ] Check crash logs (any user-submitted logs reviewed)

**T+2 Hours**

- [ ] First sentiment summary (positive/negative/neutral ratio, common themes)
- [ ] If P0 bugs reported by 3+ players: Initiate hotfix process (see Section 2.6)
- [ ] If launch is smooth: Continue monitoring, reduce frequency to every 2 hours

**T+4 Hours**

- [ ] Mid-day check (review count, player count, forum activity)
- [ ] Respond to high-visibility threads (top forum posts, Reddit threads)
- [ ] Social media engagement (respond to @mentions, retweet fan posts)

**T+8 Hours**

- [ ] End of war room shift (handoff to rotating monitoring schedule)
- [ ] Daily summary report compiled (reviews, bugs, player count, sentiment)
- [ ] Decision: Continue war room for Day 2, or shift to daily monitoring?

### Post-Launch (T+24 to T+72)

**Day 2-3**

- [ ] Monitoring frequency: Every 4 hours
- [ ] Continue bug triage (P0 bugs trigger hotfix, P1 bugs logged for Patch 1.1)
- [ ] Community engagement (respond to questions, thank positive reviewers)
- [ ] Metrics tracking (completion rate, session length, refund rate)

**End of Week 1**

- [ ] Week 1 post-mortem (what went well, what went wrong, lessons learned)
- [ ] Patch 1.1 planning begins (based on Week 1 feedback)
- [ ] Press follow-up (respond to any outlet requests for interviews, statements)

---

## 5. Marketing and Community Management

**Pre-Launch Marketing** (Week 20-36, led by HYPE)

- [ ] Steam page live 3-6 months before launch (wishlist building)
- [ ] Trailer released 1-2 months before launch (posted to YouTube, Twitter, Reddit)
- [ ] Demo consideration: Yes/No decision (see pitch doc: single production cycle, ends at festival premiere)
- [ ] Press outreach (email press list with review keys 2 weeks before launch)
- [ ] Influencer outreach (reach out to management sim YouTubers, film enthusiasts)
- [ ] Reddit marketing (post to r/tycoon, r/BaseBuildingGames, r/indiegaming, r/TrueFilm)
- [ ] Twitter/social media campaign (weekly posts building to launch: dev diaries, GIFs, screenshots)

**Launch Day Marketing** (Launch Day)

- [ ] Launch announcement posts (Twitter, Reddit, Facebook, Discord)
- [ ] Store link shared everywhere (Steam store page URL)
- [ ] Trailer re-shared (YouTube, Twitter, embedded in Reddit post)
- [ ] Press embargo lifts (reviews go live, share positive reviews on social media)

**Community Management (Ongoing)**

- [ ] Steam forums moderated daily (bug reports, questions, feedback)
- [ ] Reddit presence maintained (respond to threads on r/BACKLOT if sub exists, or r/indiegaming)
- [ ] Discord server (optional, low priority — only if community demands it)
- [ ] Patch notes posted to Steam News (every update, clear communication)

---

## 6. Risk Mitigation and Edge Case Testing

### 6.1 High-Risk Scenarios

**Scenario 1: Save File Corruption During Autosave**

**Risk**: Player quits or crashes during autosave write operation. Save file partially written, unreadable on next load.

**Mitigation**:
- [ ] Autosave writes to temporary file first (`autosave.sav.tmp`)
- [ ] After successful write, temp file renamed to `autosave.sav` (atomic operation on most filesystems)
- [ ] If corruption detected on load, fallback to previous autosave (`autosave.sav.bak`)
- [ ] QA tests: Force-quit during autosave 20 times, verify fallback works

**Scenario 2: Procedural Text Generation Produces Offensive Content**

**Risk**: Random combination of words produces slur, offensive phrase, or real-world figure name.

**Mitigation**:
- [ ] Profanity filter implemented (blacklist of prohibited words)
- [ ] Real-world figure name blacklist (no "Weinstein", "Polanski", etc. in generated names)
- [ ] QA tests: Generate 10,000 scripts, 10,000 press quotes, manually review flagged content
- [ ] Player reporting system (in-game button: "Report Inappropriate Content", sends log to developers)

**Scenario 3: Festival Jury Scoring Feels Random**

**Risk**: Players cannot learn the system. Jury taste shifts are too volatile, or feedback is unclear.

**Mitigation**:
- [ ] Post-festival breakdown UI shows score components (Taste Alignment, Quality, Buzz)
- [ ] Coverage reports hint at festival fit ("This feels like a Cannes film" for high cinematography)
- [ ] Jury taste shifts limited to 10-20% per year (not 50%+)
- [ ] QA tests: Submit same film to same festival 10 times, verify consistent outcome percentile

**Scenario 4: First-Time-User-Experience Overwhelm**

**Risk**: New players hit the Greenlight Table and are paralyzed by information overload. Bounce rate is high.

**Mitigation**:
- [ ] Tutorial system implemented (optional, skippable for experienced players)
- [ ] First film is simplified (Production Clock has fewer crises, fewer cast members)
- [ ] Tooltips everywhere (hover over any stat for explanation)
- [ ] QA tests: Watch 10 new players (no management sim experience) play first 30 minutes, note confusion points

**Scenario 5: Performance Drops on Min-Spec Hardware**

**Risk**: Game runs at 15 FPS on 2019 laptops with integrated graphics. Refund requests spike.

**Mitigation**:
- [ ] Performance profiling on min-spec hardware (Week 34-36)
- [ ] Godot's low-quality rendering mode enabled (reduces visual fidelity, boosts FPS)
- [ ] Talent Web graph rendering optimized (background thread, 10 FPS layout updates)
- [ ] QA tests: Run on 2019 Intel i5 + Intel UHD 620 graphics at 1280x720, verify 30 FPS floor

### 6.2 Edge Case Testing Matrix

| Edge Case | Test Procedure | Pass Criteria |
|---|---|---|
| **Bankruptcy during phase transition** | Trigger bankruptcy while transitioning from Production to Post-Production | Game enters Crisis State cleanly, no crash, UI updates correctly |
| **Save during event resolution** | Save game immediately after choosing a crisis event option | Save completes, reload shows correct post-decision state |
| **Quit during festival results** | Force-quit (Alt+F4) during festival outcome screen | Autosave prevents progress loss, festival outcome persists |
| **120 talents, full relationship graph** | Generate max talent count, have all work together at least once | Game runs at 60 FPS, relationship lookups instant (<5ms) |
| **20+ completed films** | Complete 20 films, verify save file size | Save file under 500KB, load time under 2 seconds |
| **All festivals submitted in one year** | Submit same film to all 5 festivals via save/load | No duplicate outcomes, festival shelf life penalty applies correctly |
| **Talent poached mid-casting** | Cast a talent, save, trigger rival studio poach event via debug | Casting UI updates, talent becomes unavailable, error handling clean |
| **Revenue stream pays out during bankruptcy** | Trigger bankruptcy, verify pending revenue streams still pay | Revenue arrives, bankruptcy resolved if revenue > debt |
| **Procedural content edge cases** | Generate 10,000 scripts, check for: empty strings, null titles, duplicate loglines | Zero errors, all scripts have valid coverage text |

---

## 7. Post-Launch Support Plan

### 7.1 Support Channels

- [ ] Email support address created (support@[studio domain].com)
- [ ] Steam Community Hub monitored daily (Bug Reports forum pinned)
- [ ] FAQ document maintained and updated (common issues, workarounds)
- [ ] Response time target: 24-48 hours for non-critical issues, 2-4 hours for P0 bugs

### 7.2 Patch Cadence

| Patch | Timing | Content |
|---|---|---|
| **Hotfix 1.0.1** | Week 1 (if needed) | Critical P0 bugs only |
| **Patch 1.1** | Month 1 | P1 bugs, balance tweaks, QOL improvements |
| **Patch 1.2** | Month 3 | Additional content (Industry Shift Events), performance optimizations |
| **Patch 1.3** | Month 6 | Stretch features (Rival Studio system, Muse dynamics) if scope allows |

### 7.3 Community Feedback Loop

- [ ] Monthly community survey (Google Form: What do you love? What's frustrating? What's missing?)
- [ ] Feature request tracking (public Trello board or GitHub issues, prioritized by votes)
- [ ] Transparency in roadmap (Steam News posts: "Here's what we're working on")

---

## 8. Success Metrics and KPIs

### 8.1 Launch Week Targets

| Metric | Target | Measurement |
|---|---|---|
| **Steam Reviews (Positive %)** | 80%+ (Very Positive) | Steam store page, Day 7 |
| **Player Completion Rate (Film 1)** | 95%+ | Steamworks stats, Achievement unlock rate |
| **Player Completion Rate (Film 5)** | 60%+ | Steamworks stats, Achievement unlock rate |
| **Average Session Length** | 60-90 minutes | Steamworks playtime stats |
| **Refund Rate** | <5% | Steam analytics (private, developer-only) |
| **Peak Concurrent Players** | 500+ (modest indie target) | SteamCharts, Steam stats |
| **Wishlist Conversion** | 20-30% | Wishlist count vs. Week 1 sales |

### 8.2 Long-Term Targets (6 Months)

| Metric | Target | Measurement |
|---|---|---|
| **Total Units Sold** | 10,000+ (break-even estimate) | Steam sales data |
| **Review Count** | 500+ | Steam store page |
| **Positive Review Ratio** | 75%+ sustained | Steam store page |
| **Community Engagement** | 1,000+ forum posts | Steam Community Hub |
| **Content Updates Released** | 2-3 patches | Patch notes archive |

---

## 9. Lessons Learned From Past Launches (Wound Context)

**Why am I so paranoid about launch day? Here is why.**

**The Worst Launch I Ever Shipped**:
- **The Game**: A narrative-driven puzzle platformer, 2018
- **What Went Wrong**:
  - Save system bug: If player paused on a specific level and quit, save file corrupted. Not caught in QA because pause-quit combo was rare.
  - Result: 200+ refund requests in first 48 hours. Steam review score dropped to 40% positive.
  - We deployed a hotfix in 36 hours, but the damage was done. First impressions are permanent.
- **What I Learned**:
  - Test every possible quit point. Players quit in ways QA never imagines.
  - Autosave to temp file, rename on success. Atomic saves are non-negotiable.
  - Have the rollback plan ready BEFORE launch. We did not. We scrambled.

**The Second-Worst Launch**:
- **The Game**: A roguelike deckbuilder, 2020
- **What Went Wrong**:
  - Performance issue on integrated graphics. Game ran fine on test machines (all had dedicated GPUs). Min-spec claim was a lie.
  - Result: "Unplayable on my laptop" reviews. We had to lower min-spec post-launch and add a low-quality mode.
- **What I Learned**:
  - Test on actual min-spec hardware. Laptops, not desktops. Integrated graphics, not dedicated.
  - Performance budget is sacred. If you claim 30 FPS, deliver 30 FPS.

**The Launch That Went Right**:
- **The Game**: A city-builder sim, 2021
- **What Went Right**:
  - 6 weeks of beta testing. 100+ testers. Every edge case documented.
  - Save system rock-solid. Autosave, manual save, cloud save — all tested to death.
  - Launch day: Zero P0 bugs. 85% positive reviews. Peak concurrent 2,000 players.
- **What I Learned**:
  - Boring launch days are good launch days. If nothing goes wrong, we did our job.
  - Checklists work. Follow the checklist. Trust the process.

**BACKLOT will be a boring launch day. That is the goal.**

---

## 10. Final Pre-Launch Checklist (The Big One)

This is the master checklist. Every item must be checked before Gold Master is approved. If it is not checked, we do not ship.

### 10.1 Code and Build

- [ ] All feature pillars implemented and tested
- [ ] All stretch goals evaluated (cut or deferred)
- [ ] Code freeze date set and honored
- [ ] Final commit tagged (`v1.0-gold`)
- [ ] Debug logs disabled in release build
- [ ] Profanity filter implemented and tested
- [ ] Crash reporter integrated
- [ ] Build automation functional
- [ ] Smoke tests pass on all platforms
- [ ] Gold Master SHA hash recorded

### 10.2 Platform and Store

- [ ] Steamworks configured (App ID, depots, cloud saves)
- [ ] Store page complete (copy, images, trailer, tags, pricing)
- [ ] Age rating obtained (ESRB/PEGI via IARC)
- [ ] Achievements implemented and tested
- [ ] Steam Deck verified (input, performance, UI)
- [ ] Controller support tested (Xbox, PlayStation, Switch Pro)
- [ ] Minimum spec validated (30 FPS on 2019 i5 + integrated graphics)

### 10.3 Quality Assurance

- [ ] Alpha QA complete (core loop stable)
- [ ] Beta QA complete (edge cases tested, long-play stable)
- [ ] Release Candidate QA complete (72-hour soak test passed)
- [ ] All P0 bugs fixed
- [ ] All P1 bugs fixed or documented in Known Issues
- [ ] Edge case matrix tested (see Section 6.2)
- [ ] Performance profiling complete (60 FPS on recommended spec, 30 FPS on min spec)

### 10.4 Launch Readiness

- [ ] Launch date set (hard date, not "Coming Soon")
- [ ] Launch discount configured (10-20% for first week)
- [ ] War room scheduled (launch day + 72 hours)
- [ ] Monitoring dashboard configured (Steam stats, reviews, forums)
- [ ] Hotfix pipeline tested (24-hour deployment capability verified)
- [ ] Rollback plan documented (depot rollback procedure)
- [ ] Communication templates prepared (hotfix announcement, rollback announcement)
- [ ] Emergency contact list finalized (BYTE, CRASH, SHIP, HYPE)

### 10.5 Marketing and Community

- [ ] Trailer released (1-2 months before launch)
- [ ] Press outreach complete (review keys sent 2 weeks before launch)
- [ ] Social media campaign active (weekly posts building to launch)
- [ ] Reddit marketing posts scheduled (r/tycoon, r/indiegaming, r/TrueFilm)
- [ ] Steam Community Hub configured (forums, moderators)
- [ ] FAQ document published (pinned in forums)
- [ ] Bug report template pinned (clear submission guidelines)

### 10.6 Post-Launch

- [ ] Week 1 monitoring plan active (daily sentiment summaries)
- [ ] Patch 1.1 scoped (P2 bugs, balance tweaks, QOL improvements)
- [ ] Support channels active (email, Steam forums)
- [ ] Community feedback loop established (monthly survey, feature request tracking)

---

## 11. Rollback Plan (The Nuclear Option)

**When do we rollback?** Only if the hotfix fails or the issue is catastrophic and unfixable within 48 hours.

**Rollback Procedure**:

1. **Confirm Decision** (BYTE + SHIP consensus required)
2. **Steam Depot Revert** (Steamworks console: revert to Gold Master depot per platform)
3. **Store Page Notice** ("Temporary rollback to resolve critical issue. Expected resolution: 24-48 hours.")
4. **Community Announcement** (Steam News, Reddit, Twitter: full transparency, apologize, explain timeline)
5. **Refund Policy** (Communicate Steam's 2-week / 2-hour refund window, offer no-questions-asked refunds)
6. **Post-Mortem** (Within 48 hours: what went wrong, how do we prevent this, when do we re-deploy?)

**Rollback Communication Template** (Pre-Written, Week 36):

```
BACKLOT - Emergency Rollback Notice

We've made the difficult decision to temporarily revert BACKLOT to the previous stable build (v1.0) while we address a critical issue affecting [specific system: save files / performance / game-breaking bug].

We understand how frustrating this is, especially for players who've already invested time in the game. If you've experienced data loss or other issues, please contact us at support@[studio].com with details. We'll do everything we can to help.

What happens next:
- We're working on a corrected build and expect to have it live within 24-48 hours.
- We'll post updates every 12 hours until the issue is resolved.
- If you'd prefer a refund, Steam's standard refund policy applies (2 weeks, <2 hours playtime). We will honor refund requests beyond that window on a case-by-case basis — email us.

We're deeply sorry for this disruption. Launch day is supposed to be a celebration, and we've let you down. We'll make this right.

- The BACKLOT Team
```

**I hope we never have to use that template. But it is written, just in case.**

---

## 12. Closing Notes

This document is not aspirational. It is operational. Every checklist item is actionable. Every timeline is realistic. Every risk has a mitigation plan.

**Launch day is not the finish line. It is the starting line.** The game we ship on Day 1 is the foundation. The game we support over the next 6 months is the legacy.

**Three principles for launch**:

1. **Boring is good.** If nothing goes wrong, we did our job. The best launch is one where players play the game and we monitor quietly in the background.

2. **Checklists prevent disasters.** I have seen studios skip the checklist because "we know what we're doing." Those studios have catastrophic launches. Follow the checklist. Trust the process.

3. **First impressions are permanent.** A player who hits a save corruption bug on Day 1 will never trust us again. They will refund, leave a negative review, and tell their friends to avoid the game. There are no second chances.

**The rollback plan exists because I respect the player's time.** If we ship a broken game, we owe them transparency, speed, and a fix. Not excuses.

**BACKLOT will launch when the checklist is complete. Not before. Not after. When it is ready.**

**Is it on the checklist? If not, it does not happen. If yes, it gets done.**

**Launch day will be boring. That is the goal.**

---

**SHIP out.**
