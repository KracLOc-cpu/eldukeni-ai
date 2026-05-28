# Service Transfer Checklist

Используйте этот чеклист при передаче проекта новому владельцу.

## GitHub

- [ ] Новый владелец добавлен в repository collaborators.
- [ ] Новый владелец имеет admin-доступ.
- [ ] Repository перенесен в organization, если компания требует владение.
- [ ] Новый владелец смог выполнить `git clone`.
- [ ] Новый владелец смог сделать test branch и push.
- [ ] Включены Issues.
- [ ] Включена защита `main`, если проект продолжат развивать через PR.

## Supabase

- [ ] Новый владелец добавлен в Supabase organization/project.
- [ ] Проверен доступ к Auth users.
- [ ] Проверен доступ к Database.
- [ ] Проверен доступ к Edge Functions.
- [ ] Проверен доступ к Function secrets.
- [ ] Проверены RLS policies.
- [ ] Проверены таблицы `profiles`, `generations`, `sellers`, `model_prices`.
- [ ] Проверены Edge Functions из `HANDOFF.md`.
- [ ] После приемки выполнен rotation service role key и AI provider keys.

## Google

- [ ] Найден Google Apps Script project для sellers API.
- [ ] Новый владелец добавлен как owner/editor.
- [ ] Переданы связанные Google Sheets / Drive folders.
- [ ] Проверен Web App deployment URL.
- [ ] Проверены доступы к Google Cloud project.
- [ ] Billing переключен на аккаунт компании.
- [ ] Личная карта больше не оплачивает проект.

## Hosting / Domain

- [ ] Найден production hosting project.
- [ ] Новый владелец добавлен как owner/admin.
- [ ] Проверен production URL.
- [ ] Проверены domain/DNS настройки.
- [ ] Проверен HTTPS.
- [ ] Проверены allowed origins/CORS, если используются.

## Acceptance Test

- [ ] Новый владелец открыл production.
- [ ] Новый владелец вошел в приложение.
- [ ] Новый владелец запустил тестовую генерацию.
- [ ] Новая генерация появилась в Supabase.
- [ ] Admin dashboard открывается для роли `admin`.
- [ ] Sellers integration работает с Apps Script URL.

## После подтверждения

- [ ] Удалить личные токены.
- [ ] Убрать личные аккаунты из billing.
- [ ] Убрать лишние admin-доступы.
- [ ] Сохранить финальный список переданных сервисов.

