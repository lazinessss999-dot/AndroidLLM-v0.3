# Third-party components

- AndroidX / Jetpack Compose — Apache License 2.0
- Kotlin / kotlinx.coroutines — Apache License 2.0
- LiteRT-LM 0.16.1 — Apache License 2.0
- llama.cpp commit `c060ca974c773c7c3d17fd1b66dc9d312bc292c0` — MIT License
- Arm AI Chat Android JNI example files from `ggml-org/llama.cpp/examples/llama.android/lib` — distributed with the llama.cpp repository; modified for AndroidLLM context size, sampler temperature, stop, static ARM linking and APK size reduction.

The llama.cpp MIT text is included in `engine/gguf/LLAMA_CPP_LICENSE`.
No code or assets are copied from the originally analyzed APK.

Model files are not bundled in the APK. Each model keeps its own license; AndroidLLM links to the corresponding model card before download.
