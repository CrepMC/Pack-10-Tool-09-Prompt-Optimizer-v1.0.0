# Project Baseline

Prompt Optimizer implements the final step of the project's workflow: when QA finds a failure, the system repairs the prompt and regenerates. The project also has a known Google Flow validation ceiling of 4000 prompt characters, so this pack treats prompt length, conflict resolution and minimal-delta repair as first-class constraints rather than afterthoughts.
