# Frontend Obsidian Course

Приветикс. Курс свой сделал в целом кайфовый, покрыть все темы не удалось, но сомневаюсь что оно имеет значение
Часть материалов были найдены с помощью Perplexity и отрефакторены Claude

Два курса в одном репозитории: **базовый** (с нуля до junior) и **продвинутый** (middle → senior). Формат — Obsidian-vault: теория, задания, карты знаний, шаблоны заметок.

---

## Навигация

- [Для кого](#для-кого)
- [Как начать](#как-начать)
- [Базовый курс — FrontendCourse](#базовый-курс--frontenddevelopers)
  - [Модули](#модули)
  - [Проекты](#проекты)
- [Продвинутый курс — FrontendAdvanced](#продвинутый-курс--frontendadvanced)
  - [Треки и модули](#треки-и-модули)
  - [Проекты продвинутого курса](#проекты-продвинутого-курса)
- [Стек](#стек)
- [Структура репозитория](#структура-репозитория)

---

## Для кого

**Базовый курс** подходит, если ты:
- Начинаешь с нуля и хочешь стать junior frontend / fullstack React-разработчиком.
- Дизайнер в Figma и хочешь понять, как макет превращается в работающий сайт.
- Знаешь отдельные куски, но нет цельной картины и маршрута.

**Продвинутый курс** подходит, если ты:
- Прошёл базовый курс или имеешь 1+ год опыта с React + TypeScript.
- Хочешь вырасти с middle до middle+ / senior.
- Целишься в сильные продуктовые команды.

---

## Как начать

1. Установи [Obsidian](https://obsidian.md) (бесплатно).
2. Клонируй репозиторий:
   ```bash
   git clone git@github.com:6Methods/FrontendObsidianCourse.git
   ```
3. В Obsidian: **Open folder as vault** → выбери `FrontendCourse/` (базовый) или `FrontendAdvanced/` (продвинутый).
4. Открой `00-Start-Here.md` — точка входа в каждом vault.
5. **Начинай с модуля 00 — Установка:** поставь VS Code, Node.js, зарегистрируйся на GitHub.
6. Опциональные плагины Obsidian: Templater, Dataview, Tasks, Kanban.
7. Заведи аккаунт на [roadmap.sh/frontend](https://roadmap.sh/frontend) — отмечай узлы по ходу курса.

> **Ты дизайнер?** После модуля 00 читай уроки `01.4` и `01.5` — там разобрано, как макет из Figma превращается в HTML и CSS, с таблицами соответствий и полным примером карточки.

---

## Базовый курс — FrontendDevelopers

**`FrontendCourse/`** — путь с нуля до junior. 15 модулей, 3 больших проекта, 12+ мини-проектов.

Каждый урок — 6 фиксированных секций: **Зачем → Главное → Пример кода → Частые ошибки → Задания → Что почитать.**

### Модули

| # | Модуль | Что внутри |
|---|--------|------------|
| **00** | [Установка](FrontendCourse/00-Установка/00-Обзор-модуля.md) | Пошаговая установка VS Code, расширения, Format on Save; Node.js LTS и npm; терминал с нуля — анатомия промта, навигация по папкам, проверка установки |
| **01** | [Setup](FrontendCourse/01-Setup/00-Обзор-модуля.md) | Инструменты и контекст: зачем каждый инструмент; как учиться; DevTools-минимум. **Для дизайнеров:** три слоя сайта через аналогии с комнатой; Figma → HTML → CSS → браузер с таблицей соответствий |
| **02** | [HTML](FrontendCourse/02-HTML/00-Обзор-модуля.md) | Семантика, структура документа, формы, базовая доступность |
| **03** | [CSS база](FrontendCourse/03-CSS-база/00-Обзор-модуля.md) | Блочная модель, Flexbox, Grid, адаптивный дизайн, media queries |
| **04** | [CSS продвинутый](FrontendCourse/04-CSS-продвинутый/00-Обзор-модуля.md) | Custom properties, анимации, Tailwind CSS, методология BEM → **P1** |
| **05** | [JS база](FrontendCourse/05-JS-база/00-Обзор-модуля.md) | Типы, функции, массивы и объекты, async/await, работа с DOM |
| **06** | [JS продвинутый](FrontendCourse/06-JS-продвинутый/00-Обзор-модуля.md) | Замыкания, `this`, прототипы, event loop, fetch, паттерны проектирования |
| **07** | [Веб-архитектура](FrontendCourse/07-Веб-архитектура/00-Обзор-модуля.md) | HTTP, REST, CORS, cookies и JWT, браузерные хранилища |
| **08** | [Git и DevTools](FrontendCourse/08-Git-и-DevTools/00-Обзор-модуля.md) | Git, Pull Request, Chrome DevTools углублённо |
| **09** | [React база](FrontendCourse/09-React-база/00-Обзор-модуля.md) | JSX, props, state, хуки, события, условный рендер |
| **10** | [React экосистема](FrontendCourse/10-React-экосистема/00-Обзор-модуля.md) | Router, Context, useReducer, мемоизация, кастомные хуки, TanStack Query, React Hook Form + Zod → **P2** |
| **11** | [TypeScript](FrontendCourse/11-TypeScript/00-Обзор-модуля.md) | Базовые типы, generics, utility types, TS + React, Zod inference |
| **12** | [Build tools и тестирование](FrontendCourse/12-Build-tools-и-тестирование/00-Обзор-модуля.md) | Vite, ESLint 9, Prettier, Vitest, Testing Library, Playwright, GitHub Actions |
| **13** | [Next.js и backend](FrontendCourse/13-Nextjs-и-backend/00-Обзор-модуля.md) | App Router, Server vs Client Components, data fetching, Route Handlers, Server Actions, Supabase + Drizzle + auth.js |
| **14** | [Деплой и финал](FrontendCourse/14-Деплой-и-финал/00-Обзор-модуля.md) | Vercel, next/image + next/font, Core Web Vitals, кеш, мониторинг, безопасность, a11y 2.0, AI-инструменты, резюме и портфолио → **P3** |

### Проекты

| Проект | После | Что делаем |
|--------|-------|------------|
| **P1 — Лендинг по макету Figma** | Модуль 04 | Верстаем лендинг по готовому Figma-макету: HTML-семантика, CSS/Tailwind, адаптив, деплой на Vercel |
| **P2 — React SPA** | Модуль 10 | Одностраничное приложение: React Router, TanStack Query, React Hook Form + Zod, публичный API |
| **P3 — Fullstack на Next.js** | Модуль 14 | Fullstack-приложение: Next.js App Router, Supabase + Drizzle + auth.js, Lighthouse CI, мониторинг, production URL в портфолио |

12+ мини-проектов — по одному в конце каждого модуля.

---

## Продвинутый курс — FrontendAdvanced

**`FrontendAdvanced/`** — слой поверх базового. 6 треков, 32 модуля. Для middle, целящихся в middle+ / senior.

**Предпосылка:** базовый курс пройден или 1+ год реального опыта с React + TypeScript.

### Треки и модули

#### Track 1 — Deep Frontend

| Модуль | Что внутри |
|--------|------------|
| [A1.1 Browser Rendering](FrontendAdvanced/A1-Deep-Frontend/A1.1-Browser-Rendering/00-Обзор-модуля.md) | Critical rendering path, DOM/CSSOM, layout, paint, composite; как браузер рисует пиксели |
| [A1.2 Event Loop и Concurrency](FrontendAdvanced/A1-Deep-Frontend/A1.2-Event-Loop-и-Concurrency/00-Обзор-модуля.md) | Microtask/macrotask, scheduler, Web Workers, SharedArrayBuffer |
| [A1.3 Memory и GC](FrontendAdvanced/A1-Deep-Frontend/A1.3-Memory-и-GC/00-Обзор-модуля.md) | V8 heap, garbage collection, memory leaks, профилирование в DevTools |
| [A1.4 React Performance 2026](FrontendAdvanced/A1-Deep-Frontend/A1.4-React-Performance-2026/00-Обзор-модуля.md) | React Compiler, Suspense streaming, selective hydration, профилировщик |

#### Track 2 — TypeScript Mastery

| Модуль | Что внутри |
|--------|------------|
| [A2.1 Type-level Programming](FrontendAdvanced/A2-TypeScript-Mastery/A2.1-Type-level-Programming/00-Обзор-модуля.md) | Conditional types, template literal types, infer, mapped types глубоко |
| [A2.2 Precision Types](FrontendAdvanced/A2-TypeScript-Mastery/A2.2-Precision-Types/00-Обзор-модуля.md) | Branded types, discriminated unions, `satisfies`, опциональные чейны в типах |
| [A2.3 Библиотечный DX](FrontendAdvanced/A2-TypeScript-Mastery/A2.3-Библиотечный-DX/00-Обзор-модуля.md) | Публичное API библиотеки, декларации, генерация типов, versioning |

#### Track 3 — Архитектура и масштаб

| Модуль | Что внутри |
|--------|------------|
| [A3.1 Feature-Sliced Design](FrontendAdvanced/A3-Архитектура-и-масштаб/A3.1-Feature-Sliced-Design/00-Обзор-модуля.md) | FSD методология, слои и слайсы, миграция с других архитектур |
| [A3.2 Monorepo на Turborepo](FrontendAdvanced/A3-Архитектура-и-масштаб/A3.2-Monorepo-на-Turborepo/00-Обзор-модуля.md) | Turborepo, workspace, changesets, shared пакеты, инкрементальные сборки |
| [A3.3 Micro-frontends](FrontendAdvanced/A3-Архитектура-и-масштаб/A3.3-Micro-frontends/00-Обзор-модуля.md) | Module Federation, shell + remote, когда применять и когда нет |
| [A3.4 Legacy и рефакторинг](FrontendAdvanced/A3-Архитектура-и-масштаб/A3.4-Legacy-и-рефакторинг/00-Обзор-модуля.md) | Стратегии постепенной миграции, strangler fig, метрики здоровья кода |
| [A3.5 Testing strategy](FrontendAdvanced/A3-Архитектура-и-масштаб/A3.5-Testing-strategy/00-Обзор-модуля.md) | Testing pyramid для фронта, Vitest / Playwright / MSW, тестирование RSC |
| [A3.6 Accessibility](FrontendAdvanced/A3-Архитектура-и-масштаб/A3.6-Accessibility/00-Обзор-модуля.md) | WCAG 2.2, семантика, ARIA, фокус, screen reader тестирование |
| [A3.7 Data fetching, RSC, Actions](FrontendAdvanced/A3-Архитектура-и-масштаб/A3.7-Data-fetching-RSC-Actions/00-Обзор-модуля.md) | Server Components глубоко, streaming, Server Actions, optimistic updates |
| [A3.8 Design system](FrontendAdvanced/A3-Архитектура-и-масштаб/A3.8-Design-system/00-Обзор-модуля.md) | Токены, компонентная библиотека, Storybook, документация, versioning |

#### Track 4 — Инфра, DevOps, SQL

| Модуль | Что внутри |
|--------|------------|
| [A4.1 Docker для фронтендера](FrontendAdvanced/A4-Инфра-DevOps-SQL/A4.1-Docker-для-фронтендера/00-Обзор-модуля.md) | Контейнеры, Dockerfile для Next.js, docker-compose, локальная БД |
| [A4.2 Self-hosting без Vercel](FrontendAdvanced/A4-Инфра-DevOps-SQL/A4.2-Self-hosting-без-Vercel/00-Обзор-модуля.md) | VPS + Caddy, HTTPS, zero-downtime deploy, мониторинг uptime |
| [A4.3 CI/CD глубже](FrontendAdvanced/A4-Инфра-DevOps-SQL/A4.3-CI-CD-глубже/00-Обзор-модуля.md) | GitHub Actions продвинутые паттерны, matrix, кеши, деплой по окружениям |
| [A4.4 SQL для фронтендера](FrontendAdvanced/A4-Инфра-DevOps-SQL/A4.4-SQL-для-фронтендера/00-Обзор-модуля.md) | PostgreSQL, EXPLAIN ANALYZE, индексы, N+1, Drizzle ORM глубоко |
| [A4.5 Observability](FrontendAdvanced/A4-Инфра-DevOps-SQL/A4.5-Observability/00-Обзор-модуля.md) | OpenTelemetry, pino, Sentry, трейсинг запросов от клиента до БД |
| [A4.6 Web Security](FrontendAdvanced/A4-Инфра-DevOps-SQL/A4.6-Web-Security/00-Обзор-модуля.md) | XSS и CSP, CSRF и CORS, OAuth 2.0 / OIDC / JWT, security headers |
| [A4.7 i18n](FrontendAdvanced/A4-Инфра-DevOps-SQL/A4.7-i18n/00-Обзор-модуля.md) | Интернационализация в Next.js, next-intl, RTL, форматирование дат/чисел |

#### Track 5 — Алгоритмы и структуры данных

| Модуль | Что внутри |
|--------|------------|
| [A5.1 Сложность и измерения](FrontendAdvanced/A5-Алгоритмы-и-структуры-данных/A5.1-Сложность-и-измерения/00-Обзор-модуля.md) | Big-O амортизация, бенчмарки в браузере, реальные примеры из фронтенда |
| [A5.2 Структуры данных для фронтенда](FrontendAdvanced/A5-Алгоритмы-и-структуры-данных/A5.2-Структуры-данных-для-фронтенда/00-Обзор-модуля.md) | LRU-кеш, Trie, Bloom filter — с применением в реальных задачах |
| [A5.3 Деревья](FrontendAdvanced/A5-Алгоритмы-и-структуры-данных/A5.3-Деревья/00-Обзор-модуля.md) | BST, обходы, DOM как дерево, задачи на деревья с фронтенд-контекстом |
| [A5.4 Графы](FrontendAdvanced/A5-Алгоритмы-и-структуры-данных/A5.4-Графы/00-Обзор-модуля.md) | BFS / DFS, топологическая сортировка, задачи на зависимости и маршруты |
| [A5.5 Dynamic Programming](FrontendAdvanced/A5-Алгоритмы-и-структуры-данных/A5.5-Dynamic-Programming/00-Обзор-модуля.md) | Memoization, табуляция, классические задачи DP со сложностью O(n) |

#### Track 6 — Команда и культура

| Модуль | Что внутри |
|--------|------------|
| [A6.1 Tech writing](FrontendAdvanced/A6-Команда-и-культура/A6.1-Tech-writing/00-Обзор-модуля.md) | ADR, RFC, postmortem — как писать, чтобы читали и принимали решения |
| [A6.2 Senior code review](FrontendAdvanced/A6-Команда-и-культура/A6.2-Senior-code-review/00-Обзор-модуля.md) | Что искать в ревью, как давать обратную связь, автоматизация через CI |
| [A6.3 Open source](FrontendAdvanced/A6-Команда-и-культура/A6.3-Open-source/00-Обзор-модуля.md) | Как найти задачу, сделать merged PR, вести свой OSS-проект |
| [A6.4 Команда и менторинг](FrontendAdvanced/A6-Команда-и-культура/A6.4-Команда-и-менторинг/00-Обзор-модуля.md) | 1:1, эскалация, онбординг новых людей, менторинг джунов |
| [A6.5 AI-augmented development](FrontendAdvanced/A6-Команда-и-культура/A6.5-AI-augmented-development/00-Обзор-модуля.md) | Как встроить AI-инструменты в рабочий процесс, не потеряв глубину |

### Проекты продвинутого курса

| Проект | Что делаем |
|--------|------------|
| **A-P1 Performance Rescue** | Берём реальное приложение с Lighthouse ~60 и доводим до 95+: профилирование, бандл, изображения, Core Web Vitals |
| **A-P2 Monorepo Platform** | Turborepo с несколькими приложениями и shared-пакетами, changesets, CI с кешированием |
| **A-P3 Self-hosted Production** | Next.js без Vercel: VPS, Docker, Caddy, HTTPS, zero-downtime deploy, мониторинг |
| **A-P4 OSS Contribution** | Merged PR в реальный open source проект — от выбора issue до ревью мейнтейнера |

**Темп:** 10–15 часов в неделю, 9–12 месяцев.

---

## Стек

```
HTML · CSS · Tailwind CSS
JavaScript · TypeScript
React 19 · Next.js 15/16 (App Router, Server Components, Server Actions)
Supabase · Drizzle ORM · auth.js
Vite · ESLint 9 · Prettier · Vitest · Testing Library · Playwright
GitHub Actions · Docker · Vercel
```

---

## Структура репозитория

```
FrontendCourse/              ← базовый курс, открывай как Obsidian-vault
├── 00-Start-Here.md         ← точка входа
├── 00-Установка/            ← старт: VS Code, Node.js, терминал
├── 01-Setup/
├── 02-HTML/ … 14-Деплой-и-финал/
├── MOC/                     ← карты знаний: CSS, JS, React, TS, Next.js
├── Проекты/                 ← P1, P2, P3 + мини-проекты
├── Приложения/              ← алгоритмы для собеса
├── Ресурсы/                 ← ссылки, книги, трекер прогресса
└── Шаблоны/                 ← шаблоны урока и обзора модуля

FrontendAdvanced/            ← продвинутый курс, отдельный Obsidian-vault
├── 00-Start-Here.md
├── A1-Deep-Frontend/
├── A2-TypeScript-Mastery/
├── A3-Архитектура-и-масштаб/
├── A4-Инфра-DevOps-SQL/
├── A5-Алгоритмы-и-структуры-данных/
├── A6-Команда-и-культура/
└── MOC/

docs/superpowers/            ← служебное, для прохождения не нужно
├── plans/                   ← планы реализации курса по модулям
└── specs/                   ← дизайн-спеки
```

---

## Лицензия

Материалы распространяются для личного обучения. Автор: [@6Methods](https://github.com/6Methods).
