---
тип: мини-проект
модуль: 13-Nextjs-и-backend
статус: not-started
---

# M13 — Fullstack заметки

Мини-проект после модуля 13. Fullstack-приложение на Next.js 15/16: заметки пользователя с авторизацией, базой и публичной лентой. Главный шаг от SPA к продуктовому приложению — здесь всё сразу: App Router, Server Components, Server Actions, Supabase, auth.js, Vercel-деплой.

## Задача

Приложение «Заметки»: пользователь логинится, создаёт/редактирует/удаляет свои заметки. Может сделать заметку публичной — она появляется в общей ленте на главной. Всё — на Server Components и Server Actions, без API-роутов (кроме auth.js callback).

## Требования

### Функциональность
1. **Главная `/`** — публичная лента (Server Component, `revalidate: 60`). Карточка: автор, title, preview.
2. **`/login`** — вход через Google (или email-link) через auth.js.
3. **`/me`** — личный кабинет, список своих заметок (публичные + приватные). Защищено session-check.
4. **`/notes/new`** — форма создания. Server Action создаёт запись.
5. **`/notes/[id]`** — публичная просмотрщица заметки. `generateMetadata` с title + description.
6. **`/notes/[id]/edit`** — редактирование (только автор). Server Action.
7. **Удаление** — Server Action с подтверждением (client `confirm`).
8. **404** — `not-found.tsx`.
9. **Loading/error** UI на страницах с асинхронными данными.

### Технический стек
- Next.js 15 или 16, App Router.
- TypeScript, `strict: true`.
- Supabase (Postgres) + Drizzle ORM.
- auth.js v5 (`next-auth@beta`), Google provider.
- Zod для валидации input в Server Actions.
- CSS Modules или Tailwind — выбор на вкус.

### Схема БД (Drizzle)
```
notes: id (uuid), userId (fk), title (text), body (text), isPublic (bool), createdAt (timestamp).
users: берём из auth.js (schema adapter).
```

### RLS (Row Level Security)
- Свои строки: `user_id = auth.uid()`.
- Публичный read: `is_public = true`.

### Правила
- Все мутации — через **Server Actions**, не через Route Handlers.
- После мутации — `revalidatePath` или `revalidateTag`.
- Никаких секретов с префиксом `NEXT_PUBLIC_*`.
- Валидация форм — Zod-схема, ошибки в `useActionState`.
- Нет `"use client"` там, где не нужно (правило: листья-дерева — клиент).

## Чего НЕ должно быть
- Ручных API-роутов для CRUD (используй Server Actions).
- Redux/Zustand — Next.js App Router не требует глобального state.
- `fetch` внутри client-компонента для серверных данных — используй Server Components.
- `NEXT_PUBLIC_` для секретов (ключ БД, OAuth client_secret).
- Pages Router — только App Router.

## Этапы

1. `npx create-next-app@latest notes-app` (App Router, TS, ESLint, Tailwind/CSS — на выбор).
2. Подключи Supabase: создай проект, скопируй URL + anon key в `.env.local`.
3. Настрой Drizzle: `drizzle-orm`, `drizzle-kit`, schema + migrations.
4. Схема `notes` + генерация миграций: `npx drizzle-kit push`.
5. auth.js v5: `next-auth@beta`, Google OAuth provider, adapter для БД.
6. `middleware.ts` — редирект на `/login` для приватных роутов.
7. Главная лента `/` — Server Component, `revalidate: 60`.
8. `/me` — auth-check + список своих заметок.
9. Формы create/edit — Server Actions + Zod validation.
10. RLS в Supabase — через SQL Editor или через Drizzle policies.
11. `loading.tsx`, `error.tsx`, `not-found.tsx`.
12. `generateMetadata` на `/notes/[id]`.
13. Деплой на Vercel. Env-vars в Project Settings. Google OAuth redirect URL — на прод-домен.
14. Тестовый прогон: создать, опубликовать, прочитать из инкогнито, удалить.

## Сдача
1. Публичный GitHub-репозиторий.
2. Prod-URL (HTTPS на Vercel).
3. README: стек, схема БД, как развернуть локально, env-vars (имена).
4. Скриншоты главной, личного кабинета, формы.

## Критерии приёмки ревью
- [ ] Логин через auth.js работает.
- [ ] CRUD заметок работает через Server Actions.
- [ ] Публичная лента на `/` — Server Component с revalidate.
- [ ] `generateMetadata` на странице заметки.
- [ ] Приватные роуты защищены middleware или layout-check.
- [ ] Loading/error/not-found UI.
- [ ] RLS включён в Supabase, приватные заметки не видны чужим.
- [ ] Нет Route Handlers для CRUD (только auth callback).
- [ ] Деплой рабочий, HTTPS.
- [ ] README с шагами запуска.

## Что дальше
Дальше — **модуль 14 Деплой и финал**: расширение до P3 (комментарии, теги, поиск), оптимизация Vercel (Image, Font, edge), финальные метрики Lighthouse, готовность к резюме.
