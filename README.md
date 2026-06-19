# Snake Local Model Benchmark

A side-by-side benchmark of several local/coding models generating the same premium single-file Snake game.

The model outputs are the `*.html` files in this repo. They are intended for comparison, not as a hand-polished final game.

## Play / view

Open:

https://mmhorda.github.io/snake-local-model-benchmark/

Or clone/download the repo and open any generated HTML file directly in a browser.

## Included model outputs and exact model/quant used

| File | Model | Quant / variant | Compute backend | Runtime | Notes |
|---|---|---|---|---|---|
| `gemma4-12b.html` | Gemma 4 12B IT | QAT Unsloth UD Q4_K_XL | CUDA SM120 | llama.cpp | local quantized run |
| `glm52.html` | GLM 5.2 | cloud model | cloud | OpenRouter | cloud model, not a local quant |
| `qwen36-27b-rocm.html` | Qwen3.6 27B | Q4_K_M | ROCm | llama.cpp | local quantized run |
| `qwen36-27b-rpc.html` | Qwen3.6 27B | Q6_K | local GPU offload | llama.cpp | local quantized run |
| `qwen36-35b-a3b.html` | Qwen3.6 35B A3B | INT4 | OpenVINO | OpenVINO Model Server / OVMS | local OpenVINO run |

For `glm52.html`, the result came from the cloud model GLM 5.2 via OpenRouter. It was not a local quantized model.

## Exact prompt used

See [`PROMPT.md`](PROMPT.md). The prompt was the same except the requested output path/filename changed per model.

```text
Build a premium single-file Snake game using HTML, CSS, and vanilla JavaScript.

Deliver exactly one complete HTML document with embedded CSS and JS. Do not use external assets, frameworks, libraries, or network requests.

Game features:
1. Responsive canvas-based Snake game that scales cleanly on desktop and mobile.
2. Keyboard controls: Arrow keys and WASD.
3. Mobile controls: swipe gestures plus visible touch D-pad.
4. Start menu with title, difficulty selector, instructions, mute toggle, and start button.
5. Pause/resume with Escape or Space.
6. Game-over overlay showing score, high score, difficulty, and restart button.
7. High score persisted in localStorage separately per difficulty.
8. Difficulty levels:
   - Chill: slower speed, no wall death; snake wraps around edges.
   - Classic: medium speed, wall collision ends game.
   - Insane: fast speed, wall collision, occasional bonus food.
9. Food must never spawn on the snake.
10. Prevent immediate 180-degree reversal.
11. Use requestAnimationFrame with fixed-step timing so the game speed is stable.
12. Include particle effects when food is eaten.
13. Include animated neon grid background and glowing snake/food visuals.
14. Include subtle sound effects generated with the Web Audio API, no audio files.
15. Include mute/unmute.
16. Include accessibility basics: readable contrast, buttons with labels, focus states, and reduced-motion support.
17. Keep the code organized into clear functions/classes with comments.

Visual style:
Create a beautiful futuristic cyberpunk arcade look: dark background, neon gradients, glassmorphism UI panels, glowing canvas border, animated title, smooth transitions, and polished typography using system fonts only.

Output rules:
save it at ./outputs/<MODEL-FILENAME>.html
No explanations.
No markdown fences.
```

## Publish-time verification

I did not alter the model-generated HTML files for gameplay fixes. I only added this README, `PROMPT.md`, `VERIFICATION.json`, `.nojekyll`, and a landing `index.html` for sharing.

Syntax check results:

| File | Bytes | Inline script found | `node --check` exit |
|---|---:|---|---:|
| `gemma4-12b.html` | 17678 | yes | 0 |
| `glm52.html` | 41752 | yes | 0 |
| `qwen36-27b-rocm.html` | 24608 | yes | 0 |
| `qwen36-27b-rpc.html` | 29261 | yes | 0 |
| `qwen36-35b-a3b.html` | 35436 | yes | 0 |

## Notes

Use the exact prompt above if you want to compare another model apples-to-apples. The filename in the output rule should be changed for each model so results do not overwrite each other.
