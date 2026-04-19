# Frontend Course — Module 13 (Next.js и backend) Implementation Plan

**Goal:** Модуль 13: обзор + 7 уроков (зачем Next.js, App Router, Server/Client Components, Data fetching, Route Handlers, Server Actions, БД+Auth) + мини-проект (fullstack на Next.js + Supabase + auth.js, деплой на Vercel) + MOC-Nextjs + Start-Here.

**Architecture:** Паттерн как в 01-12. 6 секций. «Главное» 340-420 слов. Tone — ментор-практик, «ты». Фокус на App Router + Server Components + Vercel deployment (2026-дефолт).

**Пути:**
- Vault: `FrontendCourse/`
- Модуль: `FrontendCourse/13-Nextjs-и-backend/`

---

## File Structure

```
FrontendCourse/
├── 00-Start-Here.md                          (правка)
├── 13-Nextjs-и-backend/
│   ├── 00-Обзор-модуля.md                    (новый)
│   ├── 13.1-Зачем-Nextjs.md                  (новый)
│   ├── 13.2-App-Router.md                    (новый)
│   ├── 13.3-Server-vs-Client-Components.md   (новый)
│   ├── 13.4-Data-fetching.md                 (новый)
│   ├── 13.5-Route-Handlers.md                (новый)
│   ├── 13.6-Server-Actions.md                (новый)
│   └── 13.7-База-данных-и-Auth.md            (новый)
├── Проекты/
│   ├── Мини/
│   │   └── M13-Fullstack-заметки.md          (новый)
│   └── P3-Fullstack-Nextjs.md                (правка: заполнить)
└── MOC/
    └── MOC-Nextjs.md                         (правка)
```

9 новых файлов + 3 правки.

---

## Темы уроков (подразделы «Главное»)

### 13.1 Зачем Next.js
- Что даёт Next.js поверх React.
- SSR, SSG, ISR, CSR — разница в одном абзаце.
- App Router vs Pages Router — App Router default, Pages legacy.
- SEO и метаданные на сервере.
- File-based routing.
- Производительность: streaming, partial rendering.
- Vercel как родной хостинг: zero-config.
- Next.js 15/16 и React 19 — Server Components, Actions.
- Когда Next.js не нужен (чистый SPA, admin-dashboard без SEO).
- Setup: `npx create-next-app@latest`.

### 13.2 App Router
- Файловая структура `app/`.
- `page.tsx` — страница.
- `layout.tsx` — обёртка, общий UI (хедер, меню). Корневой `layout` обязателен.
- `loading.tsx` — Suspense-граница, показывается пока страница грузится.
- `error.tsx` — граница ошибок (error boundary).
- `not-found.tsx` — 404.
- Вложенные роуты: папки + `page.tsx`.
- Dynamic segments: `[slug]`, `[...slug]`, `(group)` для группировки без URL.
- `Link` и `useRouter` (клиентский).
- Метаданные: `export const metadata` или `generateMetadata`.

### 13.3 Server vs Client Components
- Default — Server Component. «use client» — client.
- Что умеют Server Components: БД, секреты, async/await на верхнем уровне. Не умеют: state, effects, onClick.
- Client Components: интерактив (state, handlers). Не умеют: напрямую дёргать БД.
- Граница: где ставить `"use client"`. Правило: «листья дерева — клиент».
- Props из Server → Client сериализуются (JSON-safe, без функций).
- Рендер на сервере и гидратация на клиенте.
- Когда какой выбрать: отображение данных — server, формы и кнопки — client.
- Shared components: работают и там и там (если нет state/effects).
- `useRouter` (client) vs `redirect` (server).

### 13.4 Data fetching в Server Components
- `fetch` прямо в компоненте (async/await).
- Next.js расширяет fetch: `{ cache: "force-cache" | "no-store" }`, `{ next: { revalidate: 60 } }`.
- Static vs Dynamic rendering — выбирается автоматически по тому, что дергает компонент.
- `cookies()` / `headers()` из `next/headers` → автоматически dynamic.
- Revalidation: time-based (`revalidate: 60`), on-demand (`revalidatePath`, `revalidateTag`).
- Тэги (`next: { tags: ["posts"] }`) и invalidate по тэгу.
- Loading UI и streaming через `loading.tsx` + Suspense.
- Обработка ошибок: throw в Server Component → ближайший `error.tsx`.
- Параллельный fetch — `Promise.all([a, b])`.

### 13.5 Route Handlers
- Что такое: API-endpoint в `app/api/*/route.ts`.
- Методы: `export async function GET/POST/PUT/DELETE`.
- `Request`, `Response` — стандарт Web Fetch API (не Express).
- `NextRequest`/`NextResponse` — расширения с helper-ами.
- Params: `export async function GET(req, { params })` — `params` как Promise в Next 15+ (`await params`).
- Query: `new URL(req.url).searchParams`.
- Body: `await req.json()`.
- Статусы: `new Response(null, { status: 201 })` или `NextResponse.json(data, { status: 201 })`.
- Когда нужен Route Handler, а когда Server Action: API для внешних клиентов — handler; внутренние мутации — action.

### 13.6 Server Actions
- Что это: серверные функции, вызываемые с клиента, без ручного API.
- Маркер `"use server"` — в файле или в функции.
- Привязка к форме: `<form action={serverAction}>` — без JS на клиенте.
- Вызов из client: `await action(formData)` или через `useFormStatus`/`useActionState` (React 19).
- FormData: стандартный Web API, никаких JSON.
- Ревалидация после мутации: `revalidatePath("/posts")`.
- Редирект: `redirect("/posts")` из `next/navigation`.
- Защита: в action можно проверить auth, выбросить — попадёт на client как error.
- `useActionState` — state для формы (error, pending).

### 13.7 База данных и Auth
- Зачем БД: продуктовые приложения без состояния бесполезны.
- Supabase — Postgres + auth + storage как сервис. В 2026 — самый быстрый старт.
- Vercel + Supabase интеграция: env-vars автоматом.
- Подключение: `@supabase/supabase-js` или ORM (Drizzle, Prisma).
- Drizzle — лёгкий TS-ORM, хорошо работает с Server Components.
- Row Level Security (RLS) — безопасность на уровне БД.
- Auth.js (NextAuth v5) — стандарт OAuth/email-auth для Next.
- Session на сервере: `auth()` в Server Components/Actions.
- Protected routes: middleware или проверка session в layout.
- Env-vars: `.env.local`, `NEXT_PUBLIC_*` для клиента, остальные — только сервер.

---

## Мини-проект M13 — Fullstack заметки

Fullstack-приложение на Next.js 15/16: заметки (создание, редактирование, удаление, публичный view). Supabase + Drizzle + auth.js. Деплой на Vercel.

Требования:
1. **Auth.js** (Google или email-link). Защищённые роуты.
2. **Заметки**: CRUD через Server Actions.
3. **Главная** `/` — лента публичных заметок (Server Component, revalidate 60s).
4. **Личный кабинет** `/me` — только свои. Server Component + auth-check.
5. **Создание/редактирование** `/notes/new`, `/notes/[id]/edit` — form + Server Action.
6. **Удаление** — Server Action с `confirm`.
7. **Supabase + Drizzle**: схема `notes` (id, userId, title, body, isPublic, createdAt).
8. **RLS в Supabase** — юзер видит только свои приватные.
9. **SEO**: `generateMetadata` на `[id]` — title заметки + description.
10. **Loading/error UI** во всех нужных местах.
11. **Деплой на Vercel**: prod-URL с HTTPS.

---

## P3-Fullstack-Nextjs (заполнить заглушку)

Большой проект — расширение M13: добавить комментарии, теги, поиск, профили пользователей. Или альтернативно — маркетплейс/блог, но тот же стек. Рассмотрим в модуле 14.

---

## MOC-Nextjs

```markdown
---
тип: MOC
тема: Next.js
---

# MOC — Next.js

Карта по Next.js и бекенду: App Router, Server Components, Server Actions, data fetching, API, БД, auth.

## Основы (модуль 13)
- [[13.1-Зачем-Nextjs]]
- [[13.2-App-Router]]

## Server vs Client + данные (модуль 13)
- [[13.3-Server-vs-Client-Components]]
- [[13.4-Data-fetching]]

## API и мутации (модуль 13)
- [[13.5-Route-Handlers]]
- [[13.6-Server-Actions]]

## Backend: БД и Auth (модуль 13)
- [[13.7-База-данных-и-Auth]]

## Практика
- [[M13-Fullstack-заметки]] — fullstack Next.js + Supabase + auth.js.
- [[P3-Fullstack-Nextjs]] — расширенный fullstack проект (модуль 14).
```

---

## Start-Here — убрать «_(скоро)_» у модуля 13 и P3.

---

## Out of Scope
- Pages Router — только упомянуть как legacy.
- Edge runtime в деталях — Fluid Compute в 2026 default.
- tRPC, GraphQL — другие стеки, не трогаем.
- Docker/Kubernetes — деплой через Vercel, не нужен.
- Серверный рендеринг чужих фреймворков (Remix/SvelteKit) — для общего понимания достаточно Next.js.
