# Overhaul Iteration Rubric

Two improvement passes per case study after the initial overhaul. Each pass: score against
this rubric → fix everything scored weak → render-verify light+dark → log.

## Pass 1 focus: fidelity to the pivot feedback (did we actually do what it asked?)

Score each item hit / partial / miss, with evidence (section id + what's on screen):

1. Hero reads as "How I transformed [technical constraint] into [user solution]", not "I built".
2. Overview TL;DR has exactly Problem / Solution / Role / quantified Impact, impact numbers real.
3. Constraints formalized: technical + business + ethical, each concrete, each traceable to a
   later design decision (spot-check 2 links).
4. Archetypes section exists, contrasts the pair, and states what each forces the design to do.
5. IA diagram present, plain-language, actually shows data hierarchy/movement (not decoration).
6. User flow diagram maps the feedback's named journey step by step.
7. Gray-box wireframe: truly gray (no palette leakage), annotations explain grouping rationale.
8. Failure story foregrounded with real evidence; explains exactly how feedback drove iteration.
9. Final screens each tie back to a named constraint. NDA/recreation labeling intact.
10. Component/UI-kit exhibit shows typography, spacing, color logic (enterprise scalability).
11. Accessibility: zero disclaimers anywhere; SV carries the working grayscale + contrast proof.
12. Solo-hacker vibe gone (no overnight-agents flexing); collaboration/bridge framing present.
13. Enterprise vocabulary woven naturally (secure / scalable / agent-native / unified compute),
    zero keyword salad.
14. Piece-specific mandates:
    - SB: audit hook kept; why-data-valuable prose cut; V1-vs-V2 side by side; insight-card
      anatomy with annotation lines; trust-architecture diagram with structural boundary.
    - SV: 6-rebuilds flex + sleep quotes gone; Worked state machine (Default/Hover/Expanded/
      Error); semantic-vocabulary UI kit; Flow autopsy with the split decision drawn.
    - LD: no company name-calling; over-budget + 50-team edge states shown; three confidence
      states broken down (type/icon/layout/action per state).

## Pass 2 focus: craft quality (would a design team showcase this?)

1. Read the whole page top to bottom as a stranger: does each section earn the next? Any
   duplicated content left over from restructuring (the #1 risk of section moves)? Kill dupes.
2. Narrative continuity: constraints named in §2 are the SAME ones referenced in §6 captions;
   archetypes named in §3 reappear in flows/edge states; no orphan concepts.
3. Visual QA on renders (light AND dark, every new artifact):
   - new ov- components: spacing rhythm matches neighbors, borders/hairlines correct in dark,
     no white boxes in dark mode, no clipped/overflowing diagram, arrows/connectors aligned;
   - gray-box wireframes read as wireframes at a glance;
   - screenshots not cropped (D41), captions present, tryit links present.
4. Copy QA: no em dashes outside verbatim quotes; no filler ("delve", "seamless", "robust"); no
   invented numbers; verbatim quotes byte-identical to source; honest-limits still honest.
5. Multi-altitude test: 60-second read works from hero + overview alone; nav pills land on the
   right anchors; section eyebrows scannable.
6. Consistency across the trilogy: same seven sections, same nav labels, same role line, same
   signature; cross-links resolve to the -overhaul siblings; visual language still per-piece.
7. Structural validation green (verify.py) and originals untouched.

## Logging

Each pass appends to ITERATIONS.md (what was found, what changed, how verified) and the whole
overhaul lands as one DECISIONS.md entry at the end.
