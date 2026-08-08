# 12 — Runtime Capability Adapter

Before generation:
inspect current runtime's supported fields/options.

Do not invent:
- `negativePrompt`;
- `cameraPath`;
- `aspectRatio` field names;
- model functions.

If a native field is verified, map to it.
Otherwise compile semantic constraints into prompt text.
