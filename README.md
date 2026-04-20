# Frontend Obsidian Course

Два курса в одном репозитории: **базовый** (с нуля до junior) и **продвинутый** (middle → middle+/senior). Формат — Obsidian-vault: теория, заметки, чек-листы, карты знаний, шаблоны.

- **`FrontendCourse/`** — базовый, 14 модулей, 3 больших проекта, 12+ мини-проектов.
- **`FrontendAdvanced/`** — продвинутый, 6 треков, 28 модулей, 137 уроков, 4 больших проекта.

Стек 2026: HTML, CSS, Tailwind, JavaScript, TypeScript, React 19, Next.js 15/16 (App Router, Server Components, Server Actions), Supabase + Drizzle + auth.js, Vite, Vitest, Testing Library, Playwright, GitHub Actions, Vercel.

## Для кого

- Учишься с нуля, хочешь стать junior frontend / fullstack React-разработчиком.
- Знаешь отдельные куски, но нет цельной картины и маршрута.
- Хочешь не просто прочитать, а прорешать задания и собрать портфолио из трёх проектов.

## Как пользоваться

1. Установи [Obsidian](https://obsidian.md) (бесплатно).
2. Клонируй репозиторий:
   ```bash
   git clone git@github.com:6Methods/FrontendObsidianCourse.git
   ```
3. В Obsidian: `Open folder as vault` → выбери папку `FrontendCourse/`.
4. Открой `00-Start-Here.md` — это точка входа.
5. Поставь рекомендованные плагины: Templater, Dataview, Tasks, Kanban (опционально).
6. Заведи аккаунт на [roadmap.sh/frontend](https://roadmap.sh/frontend) — отмечай узлы по ходу курса.

## Структура репозитория

```
FrontendCourse/              <- базовый курс (0 → junior), открывай как Obsidian-vault
├── 00-Start-Here.md
├── 01-Setup/ ... 14-Деплой-и-финал/
├── MOC/                     <- карты знаний по темам
├── Проекты/ P1, P2, P3 + Мини/
├── Приложения/, Ресурсы/, Шаблоны/

FrontendAdvanced/            <- продвинутый курс (middle → middle+/senior)
├── 00-Start-Here.md
├── A1-Deep-Frontend/        <- Track 1: browser/V8 internals, event loop, memory, React 2026
├── A2-TypeScript-Mastery/   <- Track 2: type-level, precision types, библиотечный DX
├── A3-Архитектура-и-масштаб/ <- Track 3: FSD, monorepo, legacy, testing, a11y
├── A4-Инфра-DevOps-SQL/     <- Track 4: Docker, self-hosting, CI/CD, SQL, OTel, security
├── A5-Алгоритмы-и-структуры-данных/ <- Track 5: с прикладным уклоном
├── A6-Команда-и-культура/   <- Track 6: tech writing, code review, OSS, менторинг
└── MOC/                     <- 6 карт знаний по трекам

docs/                        <- служебное, не нужно для прохождения
└── superpowers/
    ├── plans/               <- планы реализации курса по модулям
    └── specs/               <- дизайн-спеки
```

## Как проходить

1. **По порядку.** Модули 01→14, не перепрыгивай — каждый опирается на предыдущий.
2. В каждом модуле сначала открой `00-Обзор-модуля.md` — там чек-лист, цель и ссылка на roadmap.sh.
3. Каждый урок — 6 секций: зачем → главное → пример кода → частые ошибки → 4 задания → 4 ссылки для углубления.
4. После каждого модуля — мини-проект. **Делай его, прежде чем идти дальше.** Курс без практики — потраченное время.
5. После ключевых модулей — большие проекты:
   - **P1** (после модуля 04) — лендинг по макету Figma.
   - **P2** (после модуля 10) — React SPA.
   - **P3** (после модуля 14) — fullstack на Next.js + Supabase с мониторингом и Lighthouse CI.
6. Пуш на GitHub. Обновляй `Ресурсы/Прогресс.md` после каждой вехи.
7. В `Приложения/Алгоритмы-для-собеса.md` — 30 типовых задач под собес, прорешай параллельно с модулями 09+.

## Что внутри по модулям

### Фундамент
- **01 Setup** — инструменты, терминал, VS Code, Node, браузерные DevTools.
- **02 HTML** — семантика, формы, базовый a11y.
- **03 CSS база** — модель блока, Flexbox, Grid, responsive.
- **04 CSS продвинутый** — custom properties, анимации, Tailwind, BEM. → **P1**

### JavaScript
- **05 JS база** — типы, функции, массивы/объекты, async/await, DOM.
- **06 JS продвинутый** — замыкания, this, прототипы, event loop, fetch, паттерны.

### Инструменты и веб
- **07 Веб-архитектура** — HTTP, REST, CORS, cookies/JWT, браузерные хранилища.
- **08 Git и DevTools** — git, PR, Chrome DevTools глубже.

### React-стек
- **09 React база** — JSX, props, state, hooks, события, условный рендер.
- **10 React экосистема** — Router, Context, useReducer, мемоизация, кастомные хуки, TanStack Query, React Hook Form + Zod. → **P2**

### TypeScript
- **11 TypeScript** — базовые типы, generics, utility types, TS+React, Zod inference.

### Прод-стек
- **12 Build tools и тестирование** — Vite, ESLint 9, Prettier, Vitest, Testing Library, Playwright, GitHub Actions.
- **13 Next.js и backend** — App Router, Server vs Client Components, data fetching, Route Handlers, Server Actions, Supabase + Drizzle + auth.js.
- **14 Деплой и финал** — Vercel, next/image + next/font, Core Web Vitals, кеш, monitoring, security, a11y 2.0, AI-инструменты и code review, резюме и портфолио. → **P3**

## Итог курса

После прохождения у тебя будет:
- Три живых проекта с production-URL в портфолио (P1, P2, P3).
- Резюме, GitHub-профиль и LinkedIn, оформленные под поиск работы.
- Фундамент для собесов: стек в руках + 30 прорешанных алгоритм-задач.
- Roadmap.sh с закрытыми узлами как визуальное доказательство прогресса.

## Продвинутая версия — `FrontendAdvanced/`

Второй vault в этом репозитории — **для middle+, целящихся в middle+/senior и сильные продуктовые команды**. Слой поверх базового курса: то, что отличает «умеющего писать React» от «проектирующего архитектуру на команду 10+ человек».

**Предпосылка:** базовый `FrontendCourse/` пройден **или** 1+ год реального опыта с React+TypeScript в команде.

**6 треков, 28 модулей, 137 уроков:**

- **Track 1 — Deep Frontend.** Browser rendering pipeline, event loop и concurrency, memory и GC, React performance 2026 (Compiler, Suspense streaming, selective hydration).
- **Track 2 — TypeScript Mastery.** Type-level programming, conditional и template literal types, precision types (branded, discriminated unions, `satisfies`), библиотечный DX.
- **Track 3 — Архитектура и масштаб.** Feature-Sliced Design, Turborepo monorepo, micro-frontends (advanced/optional), legacy и рефакторинг, testing strategy (Vitest/Playwright/MSW), accessibility.
- **Track 4 — Инфра, DevOps, SQL.** Docker для фронтендера, self-hosting без Vercel (VPS + Caddy), CI/CD глубже, PostgreSQL и EXPLAIN, observability (OpenTelemetry, pino, Sentry), web security (XSS/CSP, CSRF/CORS, OAuth/OIDC/JWT, security headers).
- **Track 5 — Алгоритмы и структуры данных.** Прикладной уклон: Big-O амортизация, структуры данных для фронта (LRU, Trie, Bloom), деревья, графы, DP.
- **Track 6 — Команда и культура.** ADR/RFC/postmortem, senior code review, open source contribution, менторинг, 1:1, эскалация.

**Практические проекты:** A-P1 Performance Rescue (Lighthouse 60 → 95+), A-P2 Monorepo Platform (Turborepo + changesets), A-P3 Self-hosted Production (Next.js без Vercel), A-P4 OSS Contribution (merged PR в реальный OSS).

**Темп:** 10–15 часов в неделю, 9–12 месяцев.

Открывай папку `FrontendAdvanced/` как отдельный Obsidian-vault, старт — `FrontendAdvanced/00-Start-Here.md`.

## Лицензия

Материалы распространяются для личного обучения. Автор: [@6Methods](https://github.com/6Methods).
