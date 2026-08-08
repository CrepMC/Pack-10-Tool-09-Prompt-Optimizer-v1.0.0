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

# PROMPT 1/3 — FOUNDATION, SOURCE INGEST, PRIORITY RESOLVER, BLOCK CONTRACT, UI AND VALIDATION SHELL

Implement the foundation of Tool 09 while preserving all completed T02–T08 behavior.

## 1. Architecture

Create or equivalent separated modules:
- `domain/promptOptimizerInput`
- `domain/promptBlock`
- `domain/sourcePriority`
- `domain/conflictRecord`
- `domain/correctionApplication`
- `domain/passingConstraintRegistry`
- `domain/promptBudget`
- `domain/optimizationReport`
- `domain/errors`
- `adapters/qaReportAdapter`
- `adapters/runtimePromptCapabilityAdapter`
- `services/inputValidator`
- `services/sourcePriorityResolver`
- `services/passingConstraintService`
- `services/qaCorrectionService`
- `services/blockCompilerService`
- `services/conflictResolver`
- `services/promptBudgetService`
- `services/finalValidationService`
- `services/exportService`
- `state/promptOptimizerStateMachine`
- UI components for source status, QA issues, passing constraints, priority stack, conflicts, block preview, character budget, validation, final prompt and export.

Do not implement this as one `compilePrompt()` file with hidden business logic.

## 2. Input contract

Require exact source refs/payloads:
- ProductDNA;
- CreativeBrief;
- CameraPlan;
- MotionPlan;
- EnvironmentPlan;
- CinematicPlan;
- QAReport;
- optimizer config.

Validate:
- schema versions;
- source project IDs;
- status/lock state where required;
- stale QA;
- QAReport video/source linkage;
- current upstream hashes/versions;
- correction targets exist when FAIL requires repair.

If QAReport belongs to a different video/source set:
BLOCK.

## 3. PASS QA behavior

If QA overall PASS:
the optimizer may still compile the canonical final prompt package, but it must not invent corrections.

It can:
- normalize blocks;
- remove duplicates;
- validate length;
- preserve passing constraints.

It cannot:
“improve” a passing prompt by changing camera/motion/environment.

## 4. FAIL QA behavior

If QA FAIL:
load:
- P0 targets first;
- P1 second;
- P2 optional;
- P3 only if character budget remains.

A P0 issue is a release-critical prompt-repair requirement.

## 5. Source priority registry

Represent source precedence explicitly in code.

Recommended enum/rank:
PRODUCT_LOCK = 700
USER_HARD_CONSTRAINT = 600
QA_P0 = 500
QA_P1 = 450
LOCKED_EXECUTION_PLAN = 400
CREATIVE_DIRECTION = 300
QA_P2 = 250
OPTIONAL_POLISH = 100

Exact numeric values can differ, but order must not.

Do not average conflicts.

## 6. Priority resolver

The resolver should accept normalized facts/instructions with:
- source;
- source_ref;
- domain;
- statement;
- priority;
- hard/soft;
- constraint ID.

It returns:
- accepted;
- rejected;
- conflicts;
- reason.

## 7. Product truth compilation

ProductDNA/ProductLock produces canonical hard instructions:
- primary product identity;
- silhouette;
- neckline/collar;
- sleeve;
- closures/buttons/pockets where critical;
- color family;
- pattern/logo;
- material appearance;
- confirmed accessories;
- do_not_infer;
- forbidden mutations.

Do not include every low-confidence field.

Prioritize identity-critical information.

## 8. User/project hard constraints

Compile explicit project hard requirements such as:
- 9:16 portrait;
- no zoom;
- single continuous take;
- strict background;
- max prompt length;
- final settled state.

Do not infer new hard requirements from style adjectives.

## 9. QA correction ingestion

Each correction target includes:
- priority;
- objective;
- issue refs;
- passing constraints to preserve;
- do-not-change list.

Convert correction target into a normalized repair requirement.

Do not convert it directly into a long freeform prompt.

## 10. Passing constraint registry

Build a protected registry from QA.

Examples:
`cam_ratio_9x16`
`cam_dolly_back`
`env_scene_identity`
`cine_blue_lock`
`motion_final_settled`

When later repair changes a block, run a preservation check against this registry.

## 11. Canonical prompt blocks

Create seven first-class block objects:

DIRECTOR
CAMERA
MOTION
PRODUCT
BACKGROUND
CINEMATIC
NEGATIVE

Each block has:
- name;
- content/items;
- minimum priority;
- source refs;
- hard constraints;
- soft instructions;
- character count.

## 12. Block ownership

DIRECTOR:
high-level creative/commercial intent only.

CAMERA:
ratio, framing, lens intent, camera movement, continuity, crop/zoom guards.

MOTION:
subject path, gestures, turn range, settled final state.

PRODUCT:
exact product identity and fidelity locks.

BACKGROUND:
environment identity, anchors, signage, geometry, occupancy, parallax.

CINEMATIC:
lighting/exposure/material/skin/DOF/blur/grade.

NEGATIVE:
cross-domain prohibitions/known failure guards.

Do not mix responsibilities unless a QA repair necessarily links two domains.

## 13. Fixed block order

Always output:
[DIRECTOR]
[CAMERA]
[MOTION]
[PRODUCT]
[BACKGROUND]
[CINEMATIC]
[NEGATIVE]

Stable order improves review and reproducibility.

## 14. Block content model

Internally prefer lists of normalized atomic instructions.

Example CAMERA items:
- 9:16 portrait;
- full-body framing;
- smooth dolly-back tracking;
- stable front composition;
- no digital zoom.

Only render into compact text at the final compilation step.

## 15. Conflict examples

### Camera
Accepted:
dolly-back.

Rejected:
static camera, if CameraPlan locked dolly-back.

### Product
Accepted:
collarless V-neck.

Rejected:
collared shirt.

### Motion
Accepted:
complete step cycle and settle.

Rejected:
freeze mid-step.

### Environment
Accepted:
approved reference scene.

Rejected:
new marble lobby.

### Cinematic
Accepted:
premium-neutral grade preserving blue.

Rejected:
teal shift changing blue product identity.

## 16. Conflict record

Store:
conflict_id;
sources;
winner;
loser;
rule;
resolution.

This becomes part of OptimizationReport.

## 17. Runtime capability adapter shell

The optimizer must inspect actual repository/runtime support before generation mapping.

Capability profile may include:
- prompt text field;
- aspect ratio field if verified;
- negative prompt field if verified;
- model-specific prompt character limit if available;
- wrappers/prefixes added downstream.

Prompt 1 establishes the adapter interface; Prompt 3 hardens it.

## 18. Negative-prompt policy

Internally maintain NEGATIVE block regardless of runtime.

If a native negative field is later verified:
adapter may map it separately.

If not:
render it inside final prompt text.

Do not delete NEGATIVE just because an API field is absent.

## 19. Character budget shell

Config:
`maxPromptChars` default 3800.
`hardMaxPromptChars` fixed 4000.

Create live count:
- block chars;
- labels;
- separators;
- total exact rendered chars.

Prompt 1 should already block >4000.

Full compression engine arrives Prompt 2.

## 20. Character-count correctness

Count exact Unicode string length according to the actual validation path used by the project.

If existing Flow validation counts JavaScript string length:
match that.

Do not guess token count.

Add unit tests for accented Vietnamese/Unicode if final prompt language can include it.

## 21. Wrapper budget

If downstream generation layer prepends/appends fixed text:
allow config `runtimeWrapperReserveChars`.

Then effective user prompt target must account for that.

Do not discover this only after Flow rejects the prompt.

## 22. UI

Panels:
1. Source Status
2. QA Result
3. P0/P1 Correction Targets
4. Passing Constraints
5. Priority Stack
6. Conflict Resolver
7. Block Preview
8. Character Budget
9. Validation
10. Final Prompt
11. Optimization Report
12. Export/Generation Handoff

Show exact character count live.

## 23. Character budget visualization

Show:
- used;
- target;
- hard max;
- remaining.

Example:
`3214 / 3800 target — 586 chars available — hard max 4000`.

Do not show only percentage.

## 24. State machine

WAITING_INPUT
VALIDATING_INPUT
BLOCKED
RESOLVING_PRIORITIES
APPLYING_QA_REPAIRS
BUILDING_BLOCKS
RESOLVING_CONFLICTS
COMPRESSING
VALIDATING_FINAL_PROMPT
READY_FOR_GENERATION
LOCKED
EXPORTED.

No READY state if unresolved hard conflict.

## 25. Error catalog

At minimum:
OPT_INPUT_SCHEMA_INVALID
OPT_INPUT_STALE
OPT_QA_SOURCE_MISMATCH
OPT_PRODUCT_LOCK_CONFLICT
OPT_HARD_CONSTRAINT_CONFLICT
OPT_PASSING_CONSTRAINT_REGRESSION
OPT_UNRESOLVED_CONFLICT
OPT_BLOCK_OWNERSHIP_VIOLATION
OPT_PROMPT_TOO_LONG
OPT_HARD_MAX_EXCEEDED
OPT_QA_P0_MISSING
OPT_PRODUCT_LOCK_MISSING
OPT_UNSUPPORTED_RUNTIME_FIELD
OPT_NEGATIVE_FIELD_UNVERIFIED
OPT_FINAL_VALIDATION_FAILED
OPT_HANDOFF_FAILED.

## 26. User edits

User can edit soft wording.

Hard instructions should display lock badges.

If user tries to delete:
ProductLock;
9:16 hard constraint;
QA P0;
show blocking reason.

Do not silently allow hard-lock removal.

## 27. Auditability

For each final instruction, retain source refs internally.

The user does not need chain-of-thought.

They do need:
“this line is from ProductDNA”;
“this correction is from QA issue X”.

## 28. Deterministic rendering

Normalize:
whitespace;
block labels;
separator;
punctuation;
list join style.

Same atomic items should render stably.

## 29. Prompt language

Use concise English generation language by default if existing project prompts/models perform best that way.

UI/docs can remain Vietnamese.

Do not translate product brand/logo text unless required.

## 30. Prompt 1 tests

Test:
1. valid source set;
2. stale QA;
3. QA source mismatch;
4. ProductLock priority;
5. hard 9:16 priority;
6. passing constraint registry;
7. P0 correction ingestion;
8. seven blocks;
9. fixed order;
10. conflict record;
11. exact char count;
12. >4000 blocked;
13. unverified negative field not used;
14. locked instruction cannot be removed.

## 31. Definition of Done

A maintainer can load the golden QA failure:
neckline mutation caused by hand.

The tool should show:
- ProductLock;
- QA P0;
- passing camera/background/color;
- affected MOTION/NEGATIVE blocks;
- exact prompt count;
without regenerating video.

Run build/typecheck/tests.

STOP after Prompt 1.

# EXTENDED IMPLEMENTATION APPENDIX — PROMPT 1

## A. Canonical atomic instruction model

Each instruction should preferably have:
`id`
`domain`
`source`
`source_ref`
`priority`
`hard`
`text/canonical meaning`
`block`
`protected`
`qa_issue_refs`
`passing_constraint_refs`.

This supports deterministic repair and compression.

## B. Source provenance UI

When a user selects an instruction:
show:
“Source: ProductDNA”
“Source: QA P0 issue qa_issue_001”
“Source: CameraPlan”.

No chain-of-thought.

## C. Soft vs hard creative content

Creative adjective:
“premium”
soft.

Product color:
“blue”
hard.

Camera ratio:
“9:16”
hard.

This distinction drives compression.

## D. Block minimum content

DIRECTOR may be very short.

PRODUCT cannot be empty if product reference text is required.

CAMERA cannot omit hard ratio if not natively enforced.

NEGATIVE may be empty only when there are truly no needed prohibitions and no project guard requires it.

## E. Readiness shell

`ready_for_generation=false` until:
source valid;
hard locks;
P0;
length;
conflicts all pass.

UI should never infer readiness from “prompt exists”.

## F. Draft vs canonical prompt

Users may view a draft.
Only canonical validated render becomes FinalPrompt.

## G. Prompt language normalization

Prefer concise imperative/descriptive fragments.

Avoid long polite prose:
“Please make sure that...”

Use:
“Preserve exact...”
“No...”
“Maintain...”

## H. Prompt 1 self-check

The golden neckline failure should show exactly why only motion/product/negative are affected.
