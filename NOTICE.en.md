[中文](NOTICE.md) · English

# NOTICE — Sources, Attribution, and License

This plugin (`dsh-breeze-tts`) merges two existing plugins and adds an AI-configurable channel on top. Where we used other people's work, we say so, item by item.

---

## Part One: Borrowed (complete list)

### ① localtts — the main body of merged code

| Item | Value |
|---|---|
| Plugin name (npm package) | `@dsh-external/dsh-plugin-local-ai-tts` |
| GitHub | **https://github.com/abbccdd/dsh-localtts** |
| Author | `abbccdd` |
| Version used | `0.1.12-rc.5` |
| Pinned commit | `d17b68363166d2b442c77eb8b09248d3827a7250` |
| License | **MIT** |
| What was used | Host/client registration skeleton, message-event subscription and dedup, Auto Read toggle, Edge TTS synthesis, RVC synthesis, long-read chunked playback, settings persistence, theme and translation, diagnostic routes |

### ② dsh-plugin-tts — upstream of localtts (must also be declared under MIT)

| Item | Value |
|---|---|
| Plugin name | `dsh-plugin-tts` |
| GitHub | **https://github.com/1624318455/dsh-plugin-tts** |
| Baseline commit | `ec0cf87ef52abb81ae91681a966aa3096365e631` |
| License | **MIT** |
| Copyright line | `Copyright (c) 2026 dsh-plugin-tts contributors` |
| Relationship | localtts is itself a derivative of this project; MIT requires declaration layer by layer |

### ③ Breeze TTS 2 — service called only, no code copied (both layers stated)

**③-1 Model and weights (official)**

| Item | Value |
|---|---|
| Project | Breeze TTS 2 |
| Official GitHub | **https://github.com/breezeblue-ai/breeze-tts** |
| Publisher | BreezeBlue (Shanghai Weifenglan Technology) |
| HuggingFace weights | `BreezeBlue/breeze-tts-2` |
| License | Code **Apache-2.0**; **model weights, checkpoints, adapters, derivatives, self-hosted outputs = BreezeBlue Research and Non-Commercial License** |

**③-2 The C++ server actually run (the object this plugin truly connects to)**

| Item | Value |
|---|---|
| Project | **Breeze-TTS-2.cpp** |
| GitHub | **https://github.com/HoppouAI/Breeze-TTS-2.cpp** |
| Description | C++/GGUF/ggml rewrite based on BreezeBlue/Breeze-TTS-2 weights, Vulkan backend, Windows/Linux x64 |
| Model download | **https://huggingface.co/HoppouAI/Breeze-TTS-2.cpp** (must include `audio_tokenizer/`) |
| License | Code **Apache-2.0**; MP3 encoder (`third_party/shine`) **LGPL-2.0**; weights retain the BreezeBlue non-commercial license |
| What was used | **Only calls its runtime service over HTTP API (`/health`, `/v1/voices`, `/v1/audio/speech`); no code or model weights were copied, modified, or redistributed** |

> ★ **Two mandatory statements**:
> 1. **This plugin contains no Breeze TTS 2 model weights — it is a client that calls a Breeze service deployed by the user.**
> 2. **Breeze-TTS-2.cpp code is Apache-2.0, its bundled MP3 encoder (`third_party/shine`) is LGPL-2.0, and the model weights are under the BreezeBlue Research and Non-Commercial License. All of these are independent of this plugin's MIT license.**

---

## Part Two: Developed by us

- **`dsh-breeze-voices` plugin body** (developed from scratch, merged into this package): three tabs (voice design / voice cloning / existing voices), Breeze API integration, voice registration flow, top-bar health check.
- **Fix for silent playback in preview**: Web Audio synchronous unlock + `decodeAudioData` playback + `<audio>` fallback (browser autoplay restriction).
- **Candidate-route logic for the voice dropdown**: `listVoices()` supports both `/v1/voices` and `/v1/audio/voices` (built into source, replacing an external patch).
- **Merge and adaptation of the two plugins**: unified factory, dual-slot registration, updater removal, original-plugin coexistence warning.
- **FR-5 AI-configurable channel**: host-side config storage (`~/.dsh/dsh-breeze-tts/config.json`) + 8 REST routes + auth matrix (local no-token / remote 403·401 / escape hatch) + host-side WAV header fix + `AI_SETUP.md`.
- This README / NOTICE documentation.

---

## Part Three: Attribution

```
Maintainer: OldQin Family
Implementation: Xiao Niu
AI operation testing: Ning Ning
Closeout / verification: Xiao Shu

Based on:
  - @dsh-external/dsh-plugin-local-ai-tts (MIT)
    https://github.com/abbccdd/dsh-localtts
  - dsh-plugin-tts (MIT)
    https://github.com/1624318455/dsh-plugin-tts
Runtime service (called only, no code copied):
  - Breeze-TTS-2.cpp (Apache-2.0; MP3 encoder LGPL-2.0)
    https://github.com/HoppouAI/Breeze-TTS-2.cpp
  - Breeze TTS 2 model weights (BreezeBlue Research and Non-Commercial)
    https://github.com/breezeblue-ai/breeze-tts
    https://huggingface.co/BreezeBlue/breeze-tts-2
    (weights are not distributed with this plugin)
```

---

## Part Four: LICENSE

This plugin uses **MIT** (see [LICENSE](LICENSE)). The `LICENSE` file **retains verbatim** the two upstream MIT texts and copyright lines (`abbccdd/dsh-localtts`, `1624318455/dsh-plugin-tts`) — this is a mandatory legal requirement of MIT. Our own contributions are appended at the end; no original copyright line was altered or removed.
