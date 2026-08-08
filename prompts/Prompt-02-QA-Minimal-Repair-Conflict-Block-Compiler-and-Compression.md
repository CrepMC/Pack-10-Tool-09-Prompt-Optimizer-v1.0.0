# ROLE AND SYSTEM BOUNDARY

You are building **Tool 09 — Prompt Optimizer**, the final planning/compilation tool in a multi-tool Google Flow AI fashion-video system.

Upstream:
- T02 Product DNA = canonical product truth and ProductLock.
- T03 Creative Director = high-level commercial/creative intent.
- T04 Camera Director = aspect ratio, framing, camera path, camera movement, lens intent and camera guards.
- T05 Motion Director = subject/body motion, gesture, path, final settled state and product-contact guards.
- T06 Environment Director = approved background identity, anchors, signage, geometry, movement corridor and parallax expectations.
- T07 Cinematic Director = lighting, exposure, material/skin response, DOF, blur and grade.
- T08 QA Vision = actual-video review, issues, evidence, priorities, passing constraints and correction targets.

This tool:
- resolves conflicts;
- applies QA repairs with minimal delta;
- compiles canonical prompt blocks;
- compresses safely;
- validates exact prompt length;
- emits FinalPrompt + OptimizationReport.

Downstream:
- generation/orchestration layer.

# ABSOLUTE SOURCE PRECEDENCE

When instructions conflict, use this order:

1. ProductLock / reference truth.
2. User/project hard constraints.
3. QA P0 blocking corrections.
4. QA P1 major corrections.
5. Locked Camera/Motion/Environment/Cinematic plans.
6. Creative direction.
7. Optional polish.

Higher-priority truth wins.

# ABSOLUTE MINIMAL-DELTA RULE

If QA says one thing failed, do not rewrite everything.

Preserve every meaningful QA passing constraint unless fixing the blocking issue truly requires a dependent change.

# ABSOLUTE PROMPT-LENGTH RULE

- default `maxPromptChars = 3800`
- hard platform ceiling = 4000 characters
- count the exact final string
- never send >4000
- do not delete ProductLock, hard technical requirements or QA P0 merely to fit the limit

# ABSOLUTE RUNTIME-CAPABILITY RULE

Inspect current repository/runtime/types before mapping prompt to generation.

Never invent:
- method names;
- option names;
- a `negativePrompt` field;
- a camera API;
- an aspect-ratio API.

If a separate negative-prompt field is not verified, keep `[NEGATIVE]` in prompt text.

# ABSOLUTE NON-GOALS

Do not:
- mutate upstream contracts;
- decide QA PASS;
- regenerate video inside this tool;
- change ProductDNA;
- invent new creative direction to “improve” the video;
- remove already-passing behavior without need;
- produce a final prompt over the hard limit.

# PROMPT 2/3 — QA MINIMAL-DELTA REPAIR, CONFLICT RESOLUTION, BLOCK COMPILATION, NEGATIVE SYSTEM AND SAFE COMPRESSION

Keep Prompt 1 intact. Add the actual Prompt Optimizer intelligence.

## 1. Optimization pipeline

Use this order:

1. Validate source artifacts.
2. Build canonical source facts.
3. Build passing-constraint registry.
4. Sort QA targets P0→P3.
5. Map each target to affected blocks.
6. Apply minimal delta.
7. Re-check passing constraints.
8. Resolve conflicts.
9. Canonicalize block items.
10. Deduplicate.
11. Compile full blocks.
12. Count exact characters.
13. Compress if necessary.
14. Revalidate hard constraints.
15. Revalidate QA P0.
16. Render final prompt.
17. Produce OptimizationReport.

Do not start by asking a model to rewrite the entire prompt.

## 2. QA target mapping

### Product mutation
Usually:
PRODUCT + NEGATIVE.
Sometimes MOTION if gesture caused mutation.

### Camera failure
CAMERA + NEGATIVE.

### Motion failure
MOTION + NEGATIVE.

### Environment failure
BACKGROUND + NEGATIVE.

### Cinematic failure
CINEMATIC + PRODUCT/NEGATIVE if color/material identity involved.

Use issue evidence to avoid unrelated block changes.

## 3. Minimal-delta algorithm

For each correction target:
- identify smallest affected atomic instructions;
- insert/replace only those;
- preserve passing constraints;
- compare before/after block semantics.

If target only concerns neckline hand contact:
do not change lens, camera path, background, grade.

## 4. Passing-regression validator

After every correction:
run protected constraint checks.

If repair causes:
- 9:16 removal;
- dolly-back removal;
- background change;
- color lock weakening;
- final-state loss;
reject repair.

## 5. Idempotency

Applying the same QA target twice should not duplicate constraints.

Example:
“no hand contact with neckline” should appear once in canonical meaning.

Use normalized keys/semantic dedupe.

## 6. Product block compiler

Prioritize:
- exact product category/role;
- critical silhouette;
- neckline/collar;
- color;
- pattern/logo;
- critical closures/details;
- material appearance;
- confirmed accessories;
- companion products.

Do not stuff uncertain low-value details.

Example compact product block:
“Preserve exact collarless V-neck blue black-polka-dot short-sleeve top and beige-cream wide-leg pants; exact silhouette, neckline, pattern, colors and matte fabric appearance; retain confirmed accessories.”

## 7. Product negative compiler

Negative rules derive from:
ProductLock;
QA history;
known failure modes.

Examples:
- no collar/neckline redesign;
- no logo/pattern mutation;
- no accessory disappearance;
- no hue/material change.

Do not include generic:
“no hats” if hat is real.

## 8. Camera block compiler

Use CameraPlan locked content only:
- aspect ratio;
- orientation;
- framing;
- lens perspective intent;
- movement;
- tracking;
- zoom policy;
- continuity;
- crop guards;
- start/end relation.

Example:
“9:16 portrait, full-body, natural perspective, smooth dolly-back tracking, stable front composition, start farther/end nearer while retaining full body; no digital zoom.”

## 9. Camera conflict resolver

Reject:
static + dolly-back;
zoom-out + no zoom;
16:9 + locked 9:16;
full-body + crop legs;
single-take + cut.

Higher-priority source wins.

## 10. Motion block compiler

Compile:
- locomotion;
- path;
- arm/hand behavior;
- orientation range;
- deceleration;
- completion condition;
- final settled state.

Example:
“Controlled forward approach with minimal lateral drift; restrained natural arms clear of neckline; decelerate, complete current step cycle, ground both feet, settle weight, end in stable front product-readable stance.”

## 11. Motion repair examples

QA:
mid-step end.

Add/strengthen:
complete step cycle;
decelerate;
feet grounded;
weight settled.

Negative:
no mid-step ending;
no abrupt freeze.

Do not add:
“freeze last frame.”

## 12. Neckline repair example

QA:
hand contacts neckline at 3.1–3.8s.

MOTION:
“hands remain below/away from neckline and hero chest region; no garment adjustment.”

PRODUCT:
preserve exact V-neck geometry.

NEGATIVE:
no neckline/collar contact, pulling or redesign.

Keep passed camera/background/cinematic.

## 13. Environment block compiler

Prioritize:
- preserve approved reference environment;
- hard anchors;
- signage/text;
- fixed geometry/ground;
- no new people;
- no new objects;
- motion corridor;
- camera-consistent parallax.

Example:
“Preserve approved reference scene, hard anchors, signage and fixed floor/wall geometry; clear subject path; no new people/objects; fixed-world depth-consistent parallax.”

## 14. Environment repair example

QA:
background replaced.

Strengthen:
exact approved reference identity;
no scene replacement;
no added props/people.

Do not change:
camera/motion unless QA also says they failed.

## 15. Cinematic block compiler

Prioritize:
- product-safe lighting;
- exposure;
- material preservation;
- skin naturalness;
- DOF/focus;
- motion blur;
- color grade;
- restrained bloom.

Example:
“Soft commercial lighting, balanced exposure, natural skin, preserve matte material, product-safe focus, controlled natural motion blur, premium-neutral grade preserving product colors, minimal bloom.”

## 16. Cinematic hue repair

QA:
blue → teal.

Strengthen:
“preserve blue product color family; neutral/subtle grade only.”

Negative:
no teal/green product hue shift.

Do not recolor environment instructions unless needed.

## 17. Director block compiler

Keep short.

CreativeBrief belongs here:
commercial style;
brand tone;
product readability priority;
fashion/commercial balance.

Do not repeat technical camera/motion/lighting detail.

This is usually one of the first places to compress.

## 18. Negative block architecture

Build atomic negative rules grouped by type internally:
product;
camera;
motion;
environment;
cinematic;
technical.

Rendered final NEGATIVE block can be compact one-line semicolon list.

## 19. Negative contradiction detector

Examples:
ProductDNA confirms hat.
Negative says no hat.
Conflict → reject negative.

CameraPlan says dolly.
Negative says no camera movement.
Conflict → reject/normalize.

Environment has approved sign.
Negative says no text.
Conflict → reject.

## 20. Negative specificity

Prefer:
“no unreferenced accessories”
over
“no accessories”.

Prefer:
“no neckline contact”
over
“hands never move”.

Keep useful motion while preventing failure.

## 21. Duplicate detection

Normalize equivalent statements:
“no zoom”
“no digital zoom”
“avoid zooming”
→ one canonical rule if meaning same.

But retain distinction if:
no digital zoom vs no dolly are not equivalent.

## 22. Semantic contradiction detection

Use deterministic vocabulary + semantic validation.

Do not rely solely on substring checks.

Examples:
“camera retreats”
can mean dolly-back.
“background retreats”
may be invalid environment motion.

Use block ownership context.

## 23. Character-budget engine

Calculate:
block labels;
newlines;
all text.

Track per block.

When total <= maxPromptChars:
no compression required beyond normalization.

When > maxPromptChars:
run safe compression.

## 24. Safe compression stages

Stage 1 — exact dedupe.
Stage 2 — semantic dedupe.
Stage 3 — canonical shorter terminology.
Stage 4 — remove explanations/rationales.
Stage 5 — compress DIRECTOR soft adjectives.
Stage 6 — remove P3 polish.
Stage 7 — shorten P2 noncritical style.
Stage 8 — merge equivalent negative guards.
Stage 9 — compact punctuation/whitespace where safe.

After each stage:
recount;
revalidate.

## 25. Forbidden compression

Never:
- remove ProductLock;
- remove hard ratio;
- remove no-zoom when hard;
- remove no-crop if critical;
- remove QA P0;
- remove strict environment lock after environment failure;
- remove final settled state after mid-step failure;
- change semantic meaning to save characters.

## 26. Compression scoring

Every atomic item can have:
priority;
hard;
source;
chars.

Compression candidate selection starts with lowest priority/least unique meaning.

Do not use arbitrary last-in-first-out deletion.

## 27. Character budget allocation

Do not rigidly assign fixed block sizes, but useful initial guidance:
PRODUCT high;
CAMERA/MOTION high;
BACKGROUND high if strict;
CINEMATIC moderate;
DIRECTOR compact;
NEGATIVE high when QA failures exist.

Character needs depend on failures.

## 28. Prompt overflow example

Initial:
4210 chars.

Actions:
- remove repeated “preserve exact product” from three blocks;
- keep canonical PRODUCT lock;
- merge duplicate no-zoom;
- remove long creative rationale;
- shorten “premium elegant refined high-end luxury” to “premium restrained”;
- remove P3 halation detail.

Recount:
3650 chars.

All P0 preserved.

## 29. Still-over-hard-limit behavior

After exhausting allowed compression:
4055 chars.

Result:
BLOCK.

UI explains:
“Hard constraints require 4055 characters; current hard max is 4000. Reduce optional project constraints or revise architecture.”

Do not send and hope.

## 30. Runtime wrapper reserve

If runtime adds a fixed suffix/prefix and Flow limit applies after wrapper:
count or reserve it.

Do not set prompt to 3999 if wrapper will exceed 4000.

## 31. Final string rendering

Preferred format:

[DIRECTOR]
text
[CAMERA]
text
[MOTION]
text
[PRODUCT]
text
[BACKGROUND]
text
[CINEMATIC]
text
[NEGATIVE]
text

Avoid markdown bullets if they waste chars and model does not need them.

## 32. Structured vs final text

Canonical source remains structured.

FinalPrompt.txt is a rendered view.

Never parse the final string back into domain truth for future revisions if structured artifacts still exist.

## 33. OptimizationReport

Record:
source refs;
character count;
applied corrections;
passing constraints;
conflicts;
compression actions;
final block contents;
validation.

Do not include hidden chain-of-thought.

## 34. Golden QA failure

QA:
Product critical neckline mutation caused by hand.
Everything else passes.

Expected change:
MOTION/PRODUCT/NEGATIVE.

No change:
CAMERA/BACKGROUND/CINEMATIC except whitespace/canonical wording.

Report explicitly confirms preserved constraints.

## 35. Multi-issue repair

QA:
- neckline contact P0;
- mid-step ending P0;
- slight excessive bloom P2.

Apply P0 first.

If budget tight:
fix neckline + final state.
Bloom P2 can be compacted/dropped only if it does not violate a hard cinematic constraint.

## 36. Candidate wording model

A model may propose concise wording for atomic items.

But validators must:
- preserve source meaning;
- reject ProductLock weakening;
- reject QA target loss;
- reject contradictions.

Do not trust compressed paraphrase blindly.

## 37. Determinism

Sort items:
hard first;
priority;
stable source/domain order.

Stable compilation prevents prompt churn across runs.

## 38. Tests

Add:
- minimal delta;
- passing preservation;
- duplicate QA target idempotency;
- product-aware negatives;
- no-hat contradiction;
- no-zoom conflict;
- static/dolly conflict;
- settled/freeze conflict;
- scene-replacement conflict;
- hue-lock conflict;
- character overflow;
- safe compression;
- hard-limit block.

## 39. Completion

Report:
- QA mapping;
- conflict resolver;
- block compiler;
- negative engine;
- compression engine;
- exact count;
- tests.

STOP after Prompt 2.

# EXTENDED IMPLEMENTATION APPENDIX — PROMPT 2

## A. Repair locality score

Measure how many unrelated blocks a repair changes.

Lower is better when all targets are satisfied.

Use as a quality metric, not a hard truth.

## B. Before/after semantic diff

OptimizationReport should summarize block deltas:
MOTION: added neckline clearance.
NEGATIVE: added no neckline contact.
CAMERA: unchanged.
BACKGROUND: unchanged.

This is useful for debugging regressions.

## C. Compression invariants

After every compression pass assert:
same hard constraint IDs;
same P0 target coverage;
same passing constraint coverage.

Do not compare strings only.

## D. Generic negative cleanup

Remove low-value boilerplate such as:
“no errors”
“no weirdness”
“high quality only”
unless it has defined project meaning.

Spend chars on concrete guards.

## E. Over-negative risk

Too many negative rules can conflict or reduce model clarity.

Keep only:
hard locks;
known failures;
 high-risk constraints.

## F. Product-reference compression

When reference image input is confirmed, exact garment description can be concise but still retain failure-prone identity:
“exact reference garment; collarless V-neck; blue black-polka-dot; no redesign.”

## G. Style compression

“premium elegant high-end luxurious sophisticated polished”
→ “premium restrained”.

Preserve meaning, not adjective count.

## H. Background compression

Long:
“do not alter, replace, switch, change, transform, morph the original background”
→ “preserve exact approved background; no scene replacement/morph.”

## I. Motion compression

Long biomechanical rationale can become:
“decelerate, complete step cycle, ground both feet, settle.”

## J. Prompt 2 self-check

Compression should make the prompt clearer, not merely shorter.
