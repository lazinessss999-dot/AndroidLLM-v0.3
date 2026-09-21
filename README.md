AndroidLLM
A local Android client for LiteRT-LM and GGUF/llama.cpp.

Version 0.5.0
Runtime
LiteRT-LM 0.16.1: CPU, GPU OpenCL, AUTO fallback, text and images.

llama.cpp commit c060ca974c773c7c3d17fd1b66dc9d312bc292c0: GGUF text generation on arm64 CPU.

llama.cpp is built as a single statically linked baseline ARM backend; the APK does not contain duplicate CPU variants.

One model is loaded at a time.

Settings
Performance profile based on RAM size: Auto / Low (2–3 GB) / Medium (4–5 GB) / High (6–7 GB) / Flagship (8 GB+). The preset defines the context, maximum response tokens, and default backend. "Auto" detects the device's RAM automatically.

Global generation parameters: temperature, Top-p, Top-k, show reasoning, system prompt, Markdown.

Per-model settings: context, maximum response, temperature, Top-p, Top-k, backend, and reasoning can be overridden for the selected model; settings are saved to model_settings.json.

Markdown: responses are rendered with support for **bold**, *italic*, `code`, code blocks, lists, headings, and quotes. Can be disabled in settings.

Simple RAG: the 📎 button in chat lets you attach .md/.txt files (documentation, libraries). The file is split into chunks, and the most relevant excerpts are inserted into the prompt for each question (lexical search, fully offline, no embeddings).

Catalog
Lightweight models:

Qwen3 0.6B LiteRT INT4;

SmolVLM2 500M LiteRT VLM;

Qwen2.5 0.5B GGUF Q4_K_M.

1–2B models:

Qwen2.5 1.5B Instruct LiteRT Q8;

Qwen2.5 1.5B Instruct GGUF Q4_K_M;

Qwen2.5 Coder 1.5B Instruct GGUF Q4_K_M;

SmolLM2 1.7B Instruct GGUF Q4_K_M;

Llama 3.2 1B Instruct GGUF Q4_K_M;

Qwen2-VL 2B Instruct LiteRT VLM;

SmolVLM2 2.2B LiteRT VLM.

All direct links have been tested without a Hugging Face token. Importing a cataloged file verifies the size and SHA-256.

Custom models
The "Models" screen offers three options:

add a text .gguf;

add a text .litertlm;

add a .litertlm VLM with images.

The file is copied to app-private storage. For GGUF, the magic GGUF is verified; for all files, SHA-256 is computed. Custom cards are saved to custom_models.json and restored after restart.

GGUF VLM with a separate mmproj/mtmd is not implemented yet: VLM works via LiteRT-LM. Regular text GGUF models already run via llama.cpp.

APK
releases/AndroidLLM-0.5.0-debug.apk

SHA-256: 5ca3e472d41d75b0ab84c202a402e028ad524d521e3cffb6ff1979d23e45073f

Building the project
Quick build (uses the prebuilt libai-chat.so from engine/gguf/src/main/jniLibs):

bash
./gradlew :app:assembleDebug
Full build of the native llama.cpp part from source:

bash
bash scripts/setup_llama_cpp.sh
./gradlew :app:assembleDebug
Requires JDK 17, Android SDK 37, NDK 29.0.13113456, and CMake 3.31.6 (for the native build).

When building in an environment with low RAM, CMake uses a job pool of a single C++ compiler process.