# Build status

**Version:** 0.5.0-debug (versionCode 5)  
**Stage:** LiteRT-LM + llama.cpp GGUF + custom import + device presets + per-model settings + Markdown + simple RAG  
**Build result:** SUCCESS  
**llama.cpp:** `c060ca974c773c7c3d17fd1b66dc9d312bc292c0` (prebuilt `libai-chat.so` in `engine/gguf/src/main/jniLibs`)  
**APK:** `releases/AndroidLLM-0.5.0-debug.apk`  
**Size:** 64894514 bytes  
**SHA-256:** `5ca3e472d41d75b0ab84c202a402e028ad524d521e3cffb6ff1979d23e45073f`

Included:

- LiteRT-LM 0.16.1: CPU, GPU OpenCL, AUTO fallback, text and VLM.
- llama.cpp: statically linked baseline ARM CPU backend, GGUF text.
- Public catalog with 1-2B Instruct and VLM models.
- Persistent custom imports for `.gguf` and `.litertlm`.
- Device performance presets by RAM tier (Auto / Low / Medium / High / Flagship).
- Per-model overrides: context, max output, temperature, top-p, top-k, backend, thinking.
- Markdown rendering for chat messages (toggleable).
- Simple RAG: attach `.md`/`.txt` documents; relevant excerpts are injected into the prompt (offline, lexical scoring, no embeddings).

The mock engine module was removed in 0.5.0.

