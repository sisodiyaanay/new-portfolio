# Case Study Overhaul Spec (authoritative)

You are overhauling ONE of the three Second Brain case studies per the pivoting feedback in
`C:\learnings\second-brain-agents-experiment\reviews\the-case-study-overhaul.md` (READ IT FIRST, in full).
This spec translates that feedback into exact, checkable requirements. Where this spec and the
feedback file disagree, the feedback file wins.

## Inputs (read these)

- The feedback: `reviews\the-case-study-overhaul.md`
- Your deflated source HTML (base64 images replaced by `@@IMG_nnn@@` placeholders):
  `C:\Users\Anay\AppData\Local\Temp\claude\C--learnings-second-brain-agents-experiment\5cde4a8c-51f3-4965-8668-494db295c269\scratchpad\deflated\<name>.deflated.html`
  CAUTION: some lines are extremely long. Read in slices (offset/limit). NEVER read the
  `.images.json` files (megabytes of base64); the inflate step handles them.
- Evidence base (real quotes, real numbers, only source of truth for claims):
  `C:\learnings\second-brain-agents-experiment\case-study-builder\docs\case-study-findings.md`
- House anatomy (context on existing conventions): `case-study-builder\docs\case-study-structure.md`

## Output

Write your overhauled DEFLATED html to:
`...scratchpad\deflated\<name>.overhaul.deflated.html`  (keep the `@@IMG_nnn@@` placeholders where you reuse images)

Then inflate it into the final deliverable:
```
python "C:\Users\Anay\AppData\Local\Temp\claude\C--learnings-second-brain-agents-experiment\5cde4a8c-51f3-4965-8668-494db295c269\scratchpad\inflate.py" ^
  "<your overhaul.deflated.html>" ^
  "...scratchpad\deflated\<name>.images.json" ^
  "C:\learnings\second-brain-agents-experiment\case-study-builder\<name>-overhaul.html"
```
NEVER touch the original `case-study-builder\<name>.html` — the overhaul is a new sibling file.

## Non-negotiable house rules (violating any of these fails the task)

1. **Same visual design.** Keep the existing `<style>` block, CSS custom properties, fonts,
   component classes, theme toggle (light default), progress bar, toast, and footer. You may
   APPEND new CSS for new components; prefix every new class with `ov-` and build it strictly
   from the existing CSS variables (var(--ink), var(--hair), var(--soft), var(--accent),
   var(--ok)/(--no)/(--amber) etc.) so light AND dark themes both work. No new hardcoded hex
   colors except via existing vars. No external assets, fonts, scripts, or URLs. The page must
   stay fully self-contained.
2. **No em dashes (U+2014) in any prose you write.** Use commas, colons, or periods. Em dashes
   inside verbatim quote blocks (`.prompt`) are protected: leave them exactly as they are.
3. **Verbatim quotes stay verbatim.** Typos and all ("164 sessions in a single day is not
   justifyable"). You may CUT a quote entirely, you may not edit one.
4. **Nothing fabricated.** Every number and claim must already exist in the source case study or
   in `case-study-findings.md`. No invented user studies, no invented metrics. Recreated screens
   and diagrams use the established dummy-data universe (acme.dev, the payments dashboard,
   Aarav/Priya/Sharma) and are labeled as recreations/illustrations where the original did so.
   The honest-limits content survives (see rule on disclaimers below for the ONE exception).
5. **No IP/technical internals in visible prose or diagrams:** no pipeline internals, scoring
   formula internals, stack/framework/vendor names for the internal build. Diagrams speak in
   plain product language ("raw machine log", "translated once into readable events"), not
   implementation language.
6. **Keep relative links working.** The file lives in `case-study-builder\` next to the original,
   so all `mockups/...` links stay as they are. Cross-links to the OTHER two case studies must
   point to their `-overhaul.html` siblings (the overhauled trio links to itself).
7. **Images:** reuse the existing `@@IMG_nnn@@` placeholders in the same `.appshot`/`.evo`/`.shot`
   frame markup (keep `loading="lazy"`, keep `img.shotimg` classes, keep or improve alt text).
   Do not drop screenshots without a reason from the feedback (cuts listed per piece below are
   the reasons). If a screen no longer fits any section, it may be dropped; the inflate script
   reports unused images, that is acceptable when intentional.
8. **Balanced, valid HTML.** Every tag you open, you close. Validate before finishing (see
   Validation).

## The standardized layout (apply exactly this section order)

Nav pills (in this order, these labels):
`Overview · The problem · Research · Ideation & IA · Testing · Execution · Retrospective`

1. **`id="overview"` — Overview & impact (TL;DR).** Rework the existing "at a glance" grid into
   exactly four `.gcard`s: **Problem** / **Solution** / **My role** / **Impact**. Impact uses the
   piece's real, already-claimed numbers (see per-piece). Role framing: "I architected the
   interaction models and defined the system constraints" energy; designer-led, not solo-hacker.
2. **`id="problem"` — The complex problem.** The baseline pain, shown not told: keep the piece's
   strongest existing evidence artifact (per-piece below) and ADD the raw-data exhibit where
   specified. Then a **"The constraints I designed within"** block: three labeled groups as cards
   (reuse `.feas`/`.kv` styles or `ov-` cards): **Technical** (raw machine logs, local-first data,
   no ground-truth labels, legacy formats), **Business** (token spend, timeline, one designer
   crossing into engineering), **Ethical** (the surveillance fear, privacy boundaries,
   aggregates-only leadership). Pull the piece-specific constraints from its existing copy.
3. **`id="research"` — Research & empathy.** The verbatim working-record quotes ARE the user
   research; keep the existing "labeled as the project's real user research" framing. Then the
   **archetypes**: a dedicated two-card contrast section (reuse `.grid2`/`.pcardlite`), per-piece
   pairing below. Each archetype card: name, what they want, what they fear, what that means the
   design must do.
4. **`id="ia"` — Ideation & IA.** NEW artifacts, built as inline HTML/CSS+SVG diagrams in the
   design system (this is the "reverse-engineered IA" hack from the feedback):
   - an **information-architecture / system map** (how data moves, per-piece below),
   - a **user-flow diagram** (minimalist flowchart of one named journey, per-piece below),
   - **gray-box wireframes**: a deconstructed version of one key screen, all gray boxes
     (var(--cardbg)/var(--hair) fills, no color, no imagery) with numbered annotations explaining
     WHY elements are grouped/ordered as they are. Label honestly: "structural deconstruction of
     the shipped screen" (reverse-engineered, not a dug-up historical sketch) unless the piece
     genuinely has an earlier iteration image, in which case use that too.
   Diagrams must be responsive (flex/grid, wrap on mobile) and theme-correct in both themes.
5. **`id="testing"` — Prototyping & usability testing.** The failure story, foregrounded, with
   the piece's real iteration evidence (per-piece below). Keep/reuse the existing iteration
   strips (`.evo` images) and v1→feedback→v2 frames (`.iterrow`). Explain exactly how feedback
   drove each change. Failures are the spine; do not soften them.
6. **`id="execution"` — Final execution.** The polished screens (existing `.appshot` frames with
   their mockup links), each explicitly tied back to a named constraint from §2 in its caption
   or intro line ("this exists because of constraint X"). Keep the NDA/recreation note where the
   original had one. ADD the piece's **component-system / UI-kit exhibit** here (per-piece).
7. **`id="retrospective"` — Retrospective.** Existing reflections reframed under two headings:
   what I learned about **ethical design** and what I learned about **system architecture**.
   Keep the honest-limits paragraph and ownership line (reframed per the role rule), keep the
   closing/trilogy cross-links (pointing at `-overhaul.html` siblings).

Keep the hero, footer, scripts, toast, and "Made by Anay and his Second Brain" signature.
Sections beyond these seven: fold their content INTO the seven (nothing valuable dropped unless
listed as a cut). The old section ids may remain as extra anchors if needed, but nav shows the
seven.

## Global copy rules

- **Hero reframe:** headline becomes a "How I transformed [complex technical constraint] into
  [intuitive user solution]" statement (per-piece suggested lines below; keep the existing
  emotional sub-paragraph, trimmed to fit). Keep the meta pills; role pill reads
  "Product Designer · systems & interaction".
- **Nuke accessibility disclaimers:** delete every "accessibility is a live work-in-progress" /
  "a11y noted" style line. The SV piece replaces them with a real accessibility exhibit (see SV
  spec); SB and LD simply carry no disclaimer.
- **Reframe the solo hacker:** remove "sent agents to work overnight while I slept" flavor
  (including such verbatim quotes; cutting is allowed). Ownership lines become architecture
  framing: "I architected the interaction models and defined the system constraints; the
  execution ran inside guardrails I designed." Keep honesty (it was one person) without the
  lone-cowboy flex. Frame decisions as bridges between engineering realities and user needs.
- **Enterprise vocabulary, woven naturally (not stuffed):** secure, scalable, agent-native,
  unified view of compute. Use especially in the SB trust architecture and LD token economics
  rationale. At most once or twice each per piece; it must read as rationale, not keyword salad.
- **Tone:** what you designed, not what you coded.

## Per-piece specs

### 1. second-brain-case-study  →  second-brain-case-study-overhaul.html
- Hero: "How I transformed a nightly stream of vanishing AI session logs into evidence-linked
  intelligence a team can trust." (sub keeps the plain-language story, shorter).
- §2 problem: KEEP the honest audit (2,469 commands / 0 extracted / ~0% captured) as the lead
  exhibit. ADD a raw-data exhibit: one recreated, obviously-machine-shaped session-log row
  (mock data, dummy universe, labeled "recreated row, representative structure") inside a
  `.shot`-style dark frame, so the reader SEES the unreadable input. CUT most of the
  "why this data is valuable" explainer prose (the tools grid can shrink to one line + logos;
  readers already know data is valuable, per feedback).
- §3 archetypes: **The Privacy-Wary Developer** vs **The Board-Facing CTO** (the feedback's
  named pair). Source material: the existing "two developers" segmentation line + the leader
  persona. A third mini-card for "the mirror-wanting developer" is allowed if it reads clean.
- §4 IA: **Trust Architecture diagram**, the centerpiece: data flows from the developer's
  private mirror (full detail, evidence links) across a hard permission boundary (identity
  stripped, patterns only, no drill-down) into the leadership aggregate view. Visualize
  "privacy is the shape of the product": the boundary is drawn as a structural wall in the
  diagram. Language: secure by structure, scales from one developer to the whole org.
  User flow: a developer receives their daily mirror → expands an insight → verifies the
  evidence link → corrects it if wrong (the feedback names this exact flow).
  Gray-box wireframe: the mirror home, deconstructed.
- §5 testing: the **V1→V2 evolution side-by-side** is the centerpiece: left = V1 as a gray-box
  wireframe (the digest that claimed "164 sessions", floating claims, wrong voice; rebuild it
  as gray boxes with the bad copy visible), right = V2 (the real `@@IMG_005@@` screen or coach
  home `@@IMG_004@@`). Between them, the verbatim feedback quote ("164 sessions in a single day
  is not justifyable"). Then the **Anatomy of the Insight Card**: rebuild the insight card in
  HTML/CSS at component scale with numbered annotation callouts pointing at: the claim, the
  confidence treatment, the session chip, the verbatim receipt, the "this is wrong" action.
  Explain each annotation: how the receipt design builds trust. Keep the existing iteration
  strip (`.evo` images IMG_002-004) as the lineage exhibit.
- §6 execution: Screens 1-3 (IMG_005-007) with constraint tie-backs; component-system exhibit =
  the insight-card states + the tag/level chip vocabulary (PATTERN/DECISION/RHYTHM/BLIND SPOT +
  strong/new/watch/insight levels) presented as a small UI kit table (typography, spacing,
  color logic).
- §7 retrospective: reflections reframed (ethical design: the surveillance fear and
  subject-first disclosure; system architecture: evidence-linking as the product's epistemology).

### 2. session-viewer-case-study  →  session-viewer-case-study-overhaul.html
- Hero: "How I transformed the black box of autonomous AI work into a story any teammate can
  replay." Keep the black-box problem framing.
- CUTS (feedback-mandated): the "6 rebuilds · 6 weeks" journey stats flex and the
  went-to-sleep-while-agents-coded quotes (including verbatim ones; cut, don't rewrite them).
  The journey section content folds into §5 as the iteration story without the flex framing.
- §2 problem: keep the black-box/overnight-run pain grid (reframed: the runs are autonomous, the
  designer's job is making them inspectable; no sleep bragging). Raw-data exhibit: one recreated
  raw log line vs the same moment as a readable turn (the anti-dump thesis made visible).
- §3 archetypes: **The Privacy-Wary Developer** (owns the trace, fears a monitor) vs
  **The Reviewing Teammate / lead** (needs to audit an autonomous run without reading raw logs).
- §4 IA (this piece is the interaction heavyweight, give it the most):
  - **IA / system map**: raw machine log → translated once into readable events → grouped into
    turns ("one turn = your message + the reply", shown as a visual mapping with a bracket over
    a message pair) → the five views as leaves (Complete / Story / Flow / Story canvas /
    Waterfall), each labeled with the question it answers.
  - **The "Worked" strip state machine**: four state cards with transition arrows: Default
    (collapsed, one quiet line) → Hover (affordance surfaces) → Expanded (the full worked log,
    grouped by kind) → Error (a failed step surfaces itself even when collapsed). Use `ov-`
    state-card styles; name what changes in each state (elevation, color, density).
  - Gray-box wireframe: the Complete view, deconstructed with numbered annotations (why the
    timeline rail sits left, why turns are the spine, why detail lives in a side panel).
- §5 testing: **The Flow autopsy** as the centerpiece: Flow v1 recreated as a gray-box wireframe
  (beautiful but disorienting), the verbatim confusion evidence ("i loose the track"), then a
  minimalist decision-flow diagram showing the split: "what happened in what order?" → Story
  canvas; "where did the time go?" → Waterfall. Keep the views-lived-and-died strip and the
  lineage `.evo` images.
- §6 execution: the five view screens + playback (IMG_004-009) with constraint tie-backs and
  mockup links. **Semantic vocabulary UI kit** (feedback-mandated): a snapshot exhibit of the
  kind system: agents / skills / tools / questions / files as chips with their icon + color
  logic, plus spacing/typography tokens. Then the **accessibility exhibit** (the trilogy's
  dedicated one): the same chip row rendered in grayscale proving the vocabulary reads without
  color (shape + icon + weight carry the meaning), plus a small table of the palette's
  contrast ratios against its backgrounds (compute real ratios for the actual hex values used
  in the exhibit; state them as ratios like "5.2:1, passes AA"). No disclaimers; a working
  proof. Delete the old a11y-noted line.
- §7 retrospective: reflections reframed; keep honest limits (n=1, team's own daily use).

### 3. second-brain-leadership-case-study  →  second-brain-leadership-case-study-overhaul.html
- Hero: "How I transformed raw usage telemetry into confidence-weighted signals a CTO can act
  on in one morning." Keep motion-vs-judgment and the token reckoning as the hook.
- TONE-DOWN (feedback-mandated): remove Amazon/Meta/Uber name-calling; reframe as "an
  industry-wide enterprise challenge" (verbatim quotes that name companies get cut or replaced
  by the piece's own paraphrase OUTSIDE quote marks; never edit inside a verbatim block).
- §2 problem: status theater + token reckoning, with constraints cards (ethical: developers are
  the protected party; business: compute spend must map to outcomes; technical: signals are
  composed from noisy evidence).
- §3 archetypes: **The Hands-On Director** vs **The Board-Facing CTO** (existing segmentation),
  plus a third protected-party card: **The Observed Developer** (what the design owes them).
- §4 IA: system map of the leadership layer: developer mirrors (private) → composed signals
  with confidence attached → the console's twelve intelligences → one unified view of compute
  and outcomes for the org. User flow: the 8:14am session → composed signal clears confidence
  threshold → 9:00am the CTO acts (the existing story, drawn as a flow). Gray-box wireframe:
  the command center, deconstructed (why vital signs top-left, why attention items rank by
  confidence, why detail never surfaces).
- §5 testing: the iteration strip (concept story → console v1 → final, IMG_001-003) told as
  usability iterations with what each step fixed. Then **scalability & edge cases**
  (feedback-mandated, the centerpiece): two recreated stress states of the Token economics
  screen, built in `.appshot` style with `ov-` internals (no screenshots exist for these;
  label "designed edge state, illustrative data"):
  (a) **wildly over budget**: a team at ~240% of monthly budget; show exactly what the UI does
  (the over-budget row pins to top, the delta renders in the alert treatment, the "what it
  bought" column stays attached so spend never detaches from outcomes, a composed signal with
  High confidence proposes the next action);
  (b) **50 teams instead of 5**: density strategy: teams collapse into ranked groups by
  attention-worthiness, top movers surface, everything else rolls into an aggregate row,
  search/filter affordance appears. One line each on why the design survives scale (scalable,
  unified view of compute).
- §6 execution: the four console screens (IMG_004-007) with constraint tie-backs. Component
  exhibit (feedback-mandated): **the three confidence states** (High Confidence / Unsure /
  Below Threshold) broken down as components: for each, show typography (declarative sentence
  vs question form vs absent), iconography, color treatment, layout position, and the action
  affordance it does/doesn't offer; explain how the hierarchy guides attention without forcing
  action ("doesn't cry wolf"). Build as three annotated `ov-` cards.
- §7 retrospective: ethical design (leaderboard trap, subject-first disclosure kept), system
  architecture (confidence as a first-class UI primitive).

## Validation (run before you finish)

Write/reuse a tiny python check on your INFLATED output file:
1. No `@@IMG_` remains (inflate.py already enforces).
2. Tag balance: counts of `<section`/`</section>`, `<div`/`</div>`, `<figure`/`</figure>` match.
3. Zero U+2014 outside `.prompt` blocks (strip `<div class="prompt">...</div>` spans first, then
   search).
4. Zero occurrences of: http:// or https:// in `src=`/`href=` except `#` anchors, relative
   `mockups/`, the two sibling `-overhaul.html` links, and `mailto:` if present. (No external
   deps.)
5. The seven section ids all present, nav hrefs match them.
6. File opens: render is verified later by the orchestrator; your job is structural validity.

## Report back (your final message)

Concise: what you cut, what you added (each new artifact by name), file sizes, validation
results, any spec deviation with reasoning, plus anything you noticed that the orchestrator
should re-check.
