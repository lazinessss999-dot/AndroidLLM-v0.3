# AndroidLLM

Локальный Android-клиент для LiteRT-LM и GGUF/llama.cpp.

## Версия 0.5.0

### Runtime

- LiteRT-LM 0.16.1: CPU, GPU OpenCL, AUTO fallback, текст и изображения.
- llama.cpp commit `c060ca974c773c7c3d17fd1b66dc9d312bc292c0`: GGUF text generation на arm64 CPU.
- llama.cpp собран как один статически связанный baseline ARM backend; APK не содержит дублирующих CPU-вариантов.
- Одновременно загружается одна модель.

### Настройки

- **Профиль производительности** по объёму RAM: Авто / Низкий (2–3 ГБ) / Средний (4–5 ГБ) / Высокий (6–7 ГБ) / Флагман (8 ГБ+). Пресет задаёт контекст, максимум токенов ответа и backend по умолчанию. «Авто» определяет RAM устройства автоматически.
- **Глобальные параметры генерации:** температура, Top-p, Top-k, показ рассуждения, системный промпт, Markdown.
- **Настройки отдельной модели:** контекст, максимум ответа, температура, Top-p, Top-k, backend и рассуждение можно переопределить для выбранной модели; настройки сохраняются в `model_settings.json`.
- **Markdown:** ответы рендерятся с поддержкой `**жирный**`, `*курсив*`, `` `код` ``, блоков кода, списков, заголовков и цитат. Отключается в настройках.
- **Простой RAG:** кнопка 📎 в чате позволяет прикрепить `.md`/`.txt` (документацию, библиотеки). Файл разбивается на фрагменты, при каждом вопросе в промпт подставляются самые релевантные отрывки (лексический поиск, полностью офлайн, без эмбеддингов).

### Каталог

Лёгкие модели:

- Qwen3 0.6B LiteRT INT4;
- SmolVLM2 500M LiteRT VLM;
- Qwen2.5 0.5B GGUF Q4_K_M.

Модели 1–2B:

- Qwen2.5 1.5B Instruct LiteRT Q8;
- Qwen2.5 1.5B Instruct GGUF Q4_K_M;
- Qwen2.5 Coder 1.5B Instruct GGUF Q4_K_M;
- SmolLM2 1.7B Instruct GGUF Q4_K_M;
- Llama 3.2 1B Instruct GGUF Q4_K_M;
- Qwen2-VL 2B Instruct LiteRT VLM;
- SmolVLM2 2.2B LiteRT VLM.

Все прямые ссылки протестированы без Hugging Face-токена. Импорт каталогизированного файла проверяет размер и SHA-256.

### Собственные модели

На экране «Модели» доступны три варианта:

1. добавить текстовую `.gguf`;
2. добавить текстовую `.litertlm`;
3. добавить `.litertlm` VLM с изображениями.

Файл копируется в app-private storage. Для GGUF проверяется magic `GGUF`; для всех файлов вычисляется SHA-256. Пользовательские карточки сохраняются в `custom_models.json` и восстанавливаются после перезапуска.

GGUF VLM с отдельным `mmproj/mtmd` пока не реализован: VLM работает через LiteRT-LM. Обычные текстовые GGUF уже запускаются через llama.cpp.

## APK

`releases/AndroidLLM-0.5.0-debug.apk`

SHA-256: `5ca3e472d41d75b0ab84c202a402e028ad524d521e3cffb6ff1979d23e45073f`

## Сборка проекта

Быстрая сборка (использует prebuilt `libai-chat.so` из `engine/gguf/src/main/jniLibs`):

```bash
./gradlew :app:assembleDebug
```

Полная сборка нативной части llama.cpp из исходников:

```bash
bash scripts/setup_llama_cpp.sh
./gradlew :app:assembleDebug
```

Требуются JDK 17, Android SDK 37, NDK `29.0.13113456` и CMake `3.31.6` (для нативной сборки).

При сборке в среде с малой RAM CMake использует job pool из одного C++ compiler process.
