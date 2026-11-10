# Проверочный запрос к OpenAI-совместимому API

Запросы выполняются на хосте портала до настройки shef.toolsai. Ключ берётся из переменной окружения, в файлах и журналах его нет.

```bash
export BASE_URL="https://api.openai.com/v1"   # адрес из страницы провайдера или http://127.0.0.1:8000/v1
export API_KEY="..."                            # свой ключ; для своего сервера без ключа пропустите заголовок
export MODEL="gpt-5.4-mini"                     # модель с вашего провайдера

# Список моделей (проверка адреса и ключа)
curl -sS "$BASE_URL/models" -H "Authorization: Bearer $API_KEY"

# Текст
curl -sS "$BASE_URL/chat/completions" \
  -H "Authorization: Bearer $API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model":"'"$MODEL"'","messages":[{"role":"user","content":"Ответь одним словом: работает?"}]}'

# Распознавание (если провайдер или свой сервер его умеет)
curl -sS "$BASE_URL/audio/transcriptions" \
  -H "Authorization: Bearer $API_KEY" \
  -F file=@record.mp3 -F model=whisper-1 -F response_format=verbose_json
```

Что смотреть:

- `200` и поле `choices[0].message.content` — всё работает.
- `401` — ключ неверный; `402` или сообщение о балансе — нет денег; `429` — лимит; `404` — неверный адрес или модель.
- У Яндекса модель — `gpt://<ID каталога>/aliceai-llm`, у Claude на `json_object` приходит 400 (см. страницы провайдеров).

Сверено: 2026-11-10.
