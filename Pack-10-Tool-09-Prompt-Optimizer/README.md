# Pack 10 — Tool 09: Prompt Optimizer

**Version:** 1.0.0  
**Upstream:** T08 QA Vision + T07 Cinematic + T06 Environment + T05 Motion + T04 Camera + T03 Creative + T02 Product DNA  
**Downstream:** Generation/Orchestration Layer  
**Primary artifacts:** `FinalPrompt.txt` + `OptimizationReport.json`

## Mục tiêu

Prompt Optimizer là assembler + repair engine cuối cùng. Nó không tự nghĩ lại toàn bộ creative direction. Nó nhận mọi contract upstream, QA Report và correction targets, rồi tạo một prompt generation **ngắn, không mâu thuẫn, đúng priority, giữ ProductLock và hard constraints**.

Tool này chịu trách nhiệm:
- ingest toàn bộ artifacts T02→T08;
- resolve conflicts bằng precedence rules;
- preserve QA passing constraints;
- sửa failing constraints theo minimal delta;
- compile các block:
  `[DIRECTOR]`
  `[CAMERA]`
  `[MOTION]`
  `[PRODUCT]`
  `[BACKGROUND]`
  `[CINEMATIC]`
  `[NEGATIVE]`;
- compact wording;
- loại duplicate/contradiction;
- quản lý negative constraints;
- enforce output ratio/hard technical rules;
- kiểm soát prompt length;
- produce final prompt + optimization report;
- expose exactly what changed and why.

Tool này KHÔNG:
- sửa ProductDNA;
- sửa CameraPlan/MotionPlan/EnvironmentPlan/CinematicPlan;
- tự regenerate video;
- tự PASS QA;
- invent API methods/options;
- bỏ hard lock chỉ để prompt ngắn hơn;
- viết prompt >4000 characters.

## Priority tuyệt đối

1. ProductLock / reference truth
2. User/project hard constraints
3. QA P0 corrections
4. QA P1 corrections
5. Camera/Motion/Environment/Cinematic locked plans
6. Creative style
7. Optional polish

Nếu conflict:
priority cao hơn thắng.

## Prompt length

- `maxPromptChars` default: **3800**
- hard platform limit: **4000**
- never exceed 4000
- reserve margin cho runtime wrappers nếu project cần
- compression không được xóa ProductLock/hard constraints/QA P0

## Negative prompt

Không invent một API field `negativePrompt` nếu runtime chưa chứng minh có field riêng.

Nếu runtime chỉ nhận một prompt text:
merge `[NEGATIVE]` vào prompt text.

## Definition of Done

- nhận artifacts hợp lệ;
- preserve passing constraints;
- P0/P1 repairs applied;
- no contradictions;
- 9:16/hard ratio preserved;
- final prompt <= configured max and never >4000;
- blocks structured;
- negative rules product-aware;
- output stable/deterministic enough;
- OptimizationReport describes deltas;
- no hidden regeneration;
- build/typecheck/tests pass.
