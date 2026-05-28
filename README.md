# eldukeni-ai

Веб-инструмент для генерации и обработки карточек товаров El Dukeni. Проект сделан как статическое HTML-приложение, которое работает через Supabase Auth, Supabase REST API и Supabase Edge Functions.

## Что делает проект

- Авторизация пользователей через Supabase Auth.
- Генерация карточек товаров по фото.
- Пакетная генерация карточек.
- Генерация 4 ракурсов товара.
- Генерация описаний, баннеров и логотипов.
- Поиск изображений товара через backend-функции.
- Админ-панель с историей генераций, пользователями, статистикой, токенами и стоимостью моделей.
- Интеграция с базой продавцов через Google Apps Script Web App URL.

## Структура

```text
.
├── index.html       # основная рабочая версия приложения
├── index.html.html  # старая/альтернативная версия интерфейса
└── README.md
```

## Локальный запуск

Проект не требует сборки. Достаточно открыть `index.html` в браузере.

Рекомендуемый вариант через локальный сервер:

```bash
python -m http.server 8080
```

После запуска открыть:

```text
http://localhost:8080/index.html
```

## Внешние сервисы

### Supabase

Проект использует Supabase project:

```text
https://plgoehremyeeueweoxrt.supabase.co
```

В `index.html` используются:

- Supabase Auth.
- Таблица `profiles`.
- Таблица `generations`.
- Таблица `sellers`.
- Таблица `model_prices`.
- Edge Function `generate-card`.
- Edge Function `generate-views`.
- Edge Function `generate-description`.
- Edge Function `search-product`.
- Edge Function `generate-banner`.
- Edge Function `generate-logo`.
- Edge Function `lens-search`.
- Edge Function `process-found-image`.
- Edge Function `scrape-page-images`.

Публичный Supabase anon key находится в frontend-коде. Это нормально для Supabase client-side приложений, если RLS настроен корректно. Service role key, AI API keys и другие приватные ключи должны храниться только в Supabase secrets / backend environment variables.

### Google

В проекте есть интеграция с Google Apps Script Web App для базы продавцов. URL сохраняется в `localStorage` под ключом:

```text
eldukeni_sellers_api_url
```

При передаче проекта нужно отдельно передать:

- Google Apps Script project.
- Доступ к Google Drive/Sheets, если Apps Script использует таблицы или файлы.
- Google Cloud Billing, если Apps Script, Gemini, Search API или другие Google API оплачиваются с личного аккаунта.
- Права владельца на связанные Google Cloud projects.

### Хостинг

Приложение можно разместить как обычный статический сайт: GitHub Pages, Netlify, Vercel или любой static hosting.

Для production нужно проверить:

- URL сайта.
- HTTPS.
- Redirect / domain settings.
- CORS и allowed origins в Supabase, если они настроены.
- Доступность всех Supabase Edge Functions.

## Передача проекта

Подробный чеклист передачи находится в [HANDOFF.md](HANDOFF.md).

Коротко:

1. Передать GitHub repository новому владельцу или организации.
2. Передать Supabase project / organization.
3. Передать hosting project и домен.
4. Передать Google Apps Script / Google Cloud Billing.
5. Проверить, что новый владелец может залогиниться, запустить сайт и вызвать генерацию.
6. После подтверждения доступа обновить приватные ключи и убрать личные аккаунты.

## Безопасность

- Не передавать личные пароли.
- Не публиковать service role key.
- Не хранить AI API keys в `index.html`.
- Проверить RLS policies в Supabase перед production-передачей.
- После передачи выполнить rotation всех приватных ключей.

