# Handoff: eldukeni-ai

Дата подготовки: 2026-05-28

## Назначение проекта

`eldukeni-ai` - статическое веб-приложение для генерации карточек товаров, описаний, ракурсов, баннеров и логотипов для El Dukeni. Frontend находится в `index.html`, backend-логика вынесена в Supabase Edge Functions.

## Текущий статус

Рабочая версия приложения находится в `index.html`.

Что уже есть:

- Login через Supabase Auth.
- Роли `admin`, `viewer` и обычные пользователи через таблицу `profiles`.
- Генерация карточек товара.
- Пакетная обработка фото.
- Генерация нескольких ракурсов.
- Поиск фото через backend-функции.
- Admin dashboard.
- Учет генераций, токенов и стоимости.
- Интеграция с продавцами через Apps Script API URL.

## Как запустить локально

```bash
python -m http.server 8080
```

Открыть:

```text
http://localhost:8080/index.html
```

## Что проверить при приемке

1. Открывается login screen.
2. Пользователь может войти через Supabase Auth.
3. Профиль пользователя находится в `profiles`.
4. Генерация карточки проходит успешно.
5. Edge Functions отвечают без 401/403/500.
6. Запись генерации появляется в `generations`.
7. Admin dashboard открывается для роли `admin`.
8. Google Apps Script URL сохраняется и возвращает список продавцов.
9. Production URL работает по HTTPS.

## Supabase

Project URL:

```text
https://plgoehremyeeueweoxrt.supabase.co
```

Frontend использует публичный anon key из `index.html`.

Нужно передать новому владельцу:

- Supabase organization или project ownership.
- Доступ к Auth users.
- Таблицы и RLS policies.
- Edge Functions.
- Function secrets.
- Логи Edge Functions.

Edge Functions, которые должен проверить новый владелец:

- `generate-card`
- `generate-views`
- `generate-description`
- `search-product`
- `generate-banner`
- `generate-logo`
- `lens-search`
- `process-found-image`
- `scrape-page-images`

Приватные ключи, которые нельзя хранить в GitHub:

- Supabase service role key.
- Gemini / Google AI API keys.
- OpenAI / Anthropic / other AI provider keys.
- Любые backend-only tokens.

## Google / Billing

Проверить и передать:

- Google Apps Script Web App, который используется для базы продавцов.
- Связанные Google Sheets / Drive folders.
- Google Cloud project, если Apps Script или Google APIs используют Cloud project.
- Google Billing account, если расходы идут с личной карты.
- API keys / OAuth consent screen / service accounts, если они есть.

Важно: не передавать личный Google account. Нужно добавить нового владельца и перевести billing на аккаунт компании.

## GitHub

Перед передачей:

- Добавить нового ответственного как collaborator с admin-доступом или перенести repository в organization.
- Проверить, что новый ответственный может push/pull.
- Убедиться, что в репозитории нет приватных ключей.
- После приемки удалить личные deploy tokens, если они использовались.

Рекомендуемые настройки:

- Default branch: `main`.
- Require pull request before merge для `main`.
- Require status checks, если появятся CI checks.
- Запрет force push в `main`.
- Issues включены для задач и багов.

## Хостинг и домен

Проект можно держать на любом static hosting.

Передать:

- Hosting project ownership.
- Домен и DNS.
- Доступ к production deploy.
- Историю deploy.
- Настройки CORS / allowed origins, если они задавались в Supabase.

## Известные технические особенности

- Проект сейчас без сборщика и без `package.json`.
- Основная логика находится в одном большом `index.html`.
- `index.html.html` выглядит как старая/альтернативная версия и требует ручной проверки перед удалением.
- Некоторые строки в HTML могут отображаться некорректно в терминале из-за кодировки, но браузер должен читать файл как UTF-8.
- URL Apps Script хранится у пользователя локально в браузере (`localStorage`).

## Что улучшить следующим этапом

- Разбить `index.html` на отдельные файлы: `styles.css`, `app.js`, модули для Supabase/API/admin.
- Добавить `SECURITY.md`.
- Добавить минимальные smoke tests для доступности функций.
- Настроить GitHub Pages или Vercel preview.
- Добавить backup/export схемы Supabase.
- Описать схему базы данных и RLS policies отдельным файлом.

