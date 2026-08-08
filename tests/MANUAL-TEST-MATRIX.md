# Manual Test Matrix

| Case | Expected |
|---|---|
| clean PASS QA | compile without unnecessary repair |
| neckline failure | motion/product/negative delta |
| 16:9 failure | hard 9:16 camera repair |
| mid-step failure | settled end repair |
| background fail | background/negative repair |
| hue drift | cinematic/product color lock |
| 4100 chars | safe compression |
| >4000 after safe compression | blocked |
| no native negative field | merge into prompt |
