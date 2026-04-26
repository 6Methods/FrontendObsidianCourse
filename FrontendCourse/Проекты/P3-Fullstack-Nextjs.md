---
тип: большой-проект
модуль: 14-Деплой-и-финал
статус: not-started
---

# P3 — Fullstack Next.js

Финальный проект курса. Расширение M13 «Заметки» до продуктового уровня. Цель — не «сделать ещё фич», а довести до состояния, которое не стыдно положить в резюме: комментарии, теги, поиск, профили, Lighthouse ≥ 90, Sentry, security headers, preview-деплои на PR, README с архитектурой и скринами.

## Задача

Взять M13 «Заметки» и довести до продуктового состояния. Добавить социальные фичи (комментарии, теги, поиск, профили), monitoring (Sentry), SEO, безопасность, CI/CD пайплайн с Lighthouse.

## Требования

### Новая функциональность
1. Комментарии под каждой публичной заметкой. Server Action создания, RLS на чтение (все) и запись (только залогиненные).
2. Теги — many-to-many с заметками. Фильтр ленты по тегу: `/tag/[slug]`.
3. Поиск — full-text по заметкам. Postgres `ts_vector` + `tsquery` или Supabase FTS. Input + URL `?q=...`.
4. Профили `/u/[username]`: публичные заметки юзера, аватарка (`next/image`), bio, счётчики.
5. Настройки `/me/settings` — смена username, bio, загрузка аватарки в Supabase Storage.

### Производительность
- `next/image` везде: аватарки, картинки в заметках.
- `next/font` для шрифта, `display: swap`.
- `priority` на LCP-элементе главной.
- Lighthouse ≥ 90 на Performance, Accessibility, Best Practices, SEO — на главной и странице заметки.
- Core Web Vitals: LCP ≤ 2.5s, INP ≤ 200ms, CLS ≤ 0.1.
- Vercel Speed Insights подключён.

### Мониторинг
- Sentry на frontend и server. Source maps. Уведомления на email или Slack.
- Vercel Analytics — базовая аналитика посетителей.

### Безопасность
- CSP headers в `next.config.js` или middleware.
- Rate limit на Server Actions создания (Upstash Ratelimit, бесплатный tier).
- Vercel BotID на форму логина и создания.
- RLS проверена: ни одна приватная заметка или комментарий не видна чужому.
- OAuth redirect URLs прописаны в Google Cloud Console для прод-домена.
- `npm audit` в CI, Dependabot включён.

### CI/CD
- GitHub Actions: `lint → typecheck → unit → build → e2e` (Playwright headless).
- Lighthouse CI блокирует PR, если Performance < 85.
- Vercel preview deployments на каждый PR.
- Required status checks на main.

### SEO
- `generateMetadata` на заметке, теге, профиле.
- `sitemap.ts` и `robots.ts` в `app/`.
- Open Graph картинки через `opengraph-image.tsx`.

## Чего НЕ должно быть
- Ручных API для CRUD (используем Server Actions).
- Pages Router.
- Секретов с префиксом `NEXT_PUBLIC_*`.
- Пропущенного Lighthouse-прогона.
- «TODO» в проде — всё доделано или вынесено в issues.

## Этапы

1. Форкни M13 в новый репо `notes-app-pro` (или продолжи в том же, создав ветку).
2. Добавь схему `comments` (Drizzle migration). RLS-политики.
3. Server Action и форма комментария под `/notes/[id]`. Revalidate path.
4. Схема `tags` + `notes_tags`. Страница `/tag/[slug]` — Server Component с лентой.
5. Full-text поиск: `tsvector` колонка на `notes`, `GENERATED ALWAYS AS (to_tsvector('russian', title || ' ' || body)) STORED`. Страница `/search?q=...`.
6. Профили: `/u/[username]`, запросы к `notes` по `userId`. Supabase Storage для аватарок.
7. Заменить все `<img>` на `<Image>`. Настроить `remotePatterns` для Supabase Storage.
8. Подключить `@vercel/speed-insights/next` и `@vercel/analytics/next`.
9. Подключить Sentry (`@sentry/nextjs`), тестовая ошибка отловлена.
10. CSP в middleware, security headers в `next.config.js`.
11. Upstash Ratelimit на Server Action создания заметки и комментария.
12. Playwright: smoke e2e (логин, создать, опубликовать, увидеть в ленте, прокомментить, удалить).
13. Lighthouse CI в GitHub Actions.
14. Prod-деплой на Vercel с кастомным доменом или `.vercel.app`.
15. README: архитектура (схема БД, структура роутов), стек, live URL, Lighthouse-скрины, env-vars.

## Сдача
1. Публичный GitHub-репо.
2. Prod-URL с HTTPS.
3. README с:
   - описанием продукта и стека,
   - схемой БД,
   - инструкцией запуска локально,
   - скриншотами (главная, профиль, заметка с комментариями, поиск),
   - Lighthouse-скорами (screenshot или badge),
   - списком env-vars (имена без значений),
   - ссылками на Vercel preview и прод.
4. Live Sentry issue как доказательство подключения.

## Критерии приёмки ревью
- [ ] Комментарии работают через Server Action, видны только на публичных заметках.
- [ ] Теги: заметка → 0..N тегов, страница тега показывает все публичные заметки с этим тегом.
- [ ] Поиск работает по title и body (русский язык).
- [ ] Профиль `/u/[username]` показывает аватарку и публичные заметки.
- [ ] Lighthouse Performance ≥ 90 на главной.
- [ ] Speed Insights подключён, есть данные.
- [ ] Sentry ловит тестовую ошибку.
- [ ] CSP header присутствует в ответе.
- [ ] Rate limit работает (повторный спам блокируется).
- [ ] RLS: из инкогнито не видна чужая приватная заметка.
- [ ] Lighthouse CI в Actions блокирует PR при падении ниже порога.
- [ ] README с архитектурой, скринами и live URL.

## Что дальше
Курс пройден. Три проекта в портфолио (P1 лендинг, P2 React SPA, P3 fullstack). Дальше — оффер, реальный прод, backend/DevOps-углубление, open-source. [[14.9-Финал-резюме-и-дальше]] расскажет, как упаковать это в резюме.
