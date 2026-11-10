# shef-ai-providers

Как подключить модель к [shef.toolsai](https://b24-crm-tools-ai.bx-shef.by/toolsai) — модулю для коробочного Битрикс24, который подключает AI к звонкам, сделкам, чатам и письмам. Через shef.toolsai модель работает и для AI-агента [shef.cowork](https://github.com/bx-shef/shef-cowork-tools).

Страницы продукта: [описание](https://b24-crm-tools-ai.bx-shef.by/) · [shef.toolsai](https://b24-crm-tools-ai.bx-shef.by/toolsai) · [инструменты shef.cowork](https://github.com/bx-shef/shef-cowork-tools).

Сверка моделей и адресов с официальными страницами провайдеров: **2026-11-10**. Цен здесь нет: актуальные цены — на странице цен провайдера (ссылки на страницах провайдеров).

## Что выбрать

| Провайдер | Что умеет | Где взять ключ | Куда уходят данные |
|---|---|---|---|
| [DeepSeek](providers/deepseek.md) | текст | [platform.deepseek.com/api_keys](https://platform.deepseek.com/api_keys) | наружу, на серверы DeepSeek |
| [ChatGPT (OpenAI)](providers/openai.md) | распознавание, текст | кабинет OpenAI Platform (раздел API keys) | наружу, на серверы OpenAI |
| [Claude (Anthropic)](providers/anthropic-claude.md) | текст | [platform.claude.com/settings/keys](https://platform.claude.com/settings/keys) | наружу, на серверы Anthropic |
| [Google (Gemini)](providers/gemini.md) | текст | [aistudio.google.com/apikey](https://aistudio.google.com/apikey) | наружу, на серверы Google |
| [Яндекс (YandexGPT, Yandex AI Studio)](providers/yandexgpt.md) | текст | API-ключ сервисного аккаунта Yandex Cloud + ID каталога | наружу, в Yandex Cloud |
| [BitrixGPT Вайбкод](providers/bitrixgpt-vibecode.md) | распознавание, текст | личный ключ Вайбкод ([страница моделей](https://vibecode.bitrix24.tech/ai-models)) | наружу, в облако Битрикс24 |
| [Свой сервер](own-server.md) (OpenAI-совместимый: vLLM, Ollama, LocalAI, whisper) | распознавание, текст — что поднимете | ключ задаёте сами (или без ключа на 127.0.0.1) | остаются у вас, если сервер ваш |

Распознавание речи (`audio/transcriptions`) в каталоге shef.toolsai есть у ChatGPT (OpenAI), BitrixGPT Вайбкод и у своего сервера. Для DeepSeek, Claude, Gemini и Яндекса у модуля нет OpenAI-совместимого метода распознавания: берите распознавание у другого провайдера или на своём сервере — у каждого направления свой провайдер.

Провайдеры с постоянным ключом и обычным запросом `Authorization: Bearer` подключаются настройкой, без кода. Сбер GigaChat в каталоге нет: ключ доступа живёт 30 минут и выписывается отдельным запросом; подключается через переходник на «Свой адрес».

## Как устроено

1. В «Общих настройках» shef.toolsai, вкладка «API», у направления («Распознавание», «Текст», «Анализ сделок», «Чат AI-помощника») выберите «Провайдер» и «Модель» (быстрая, основная, мощная).
2. Впишите ключ провайдера в поле ключа направления (или общий ключ).
3. В разделе «Расход и включение» нажмите «Проверить и включить» и убедитесь, что в журнале расхода появился запрос.

Свои поля направления (адрес, модель, цены) главнее каталога. Ключ откатывается к общему только вместе с адресом.

## Содержимое

- [providers/](providers/) — по странице на провайдера: ключ, адрес, модель, поля, проверка, ошибки.
- [own-server.md](own-server.md) — свой сервер, адрес на 127.0.0.1.
- [examples/](examples/) — наборы настроек и проверочный запрос curl.
- [CHANGELOG.md](CHANGELOG.md).

Модели и адреса меняются. Перед подключением сверьтесь со страницей провайдера. Лицензия — MIT.
