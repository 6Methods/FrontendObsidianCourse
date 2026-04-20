# Frontend Advanced Course — Design Spec

**Date:** 2026-04-20
**Author:** Иван (с Claude Opus)
**Status:** draft — ждёт твоего ревью

---

## Цель

Продвинутая версия курса поверх базового `FrontendObsidianCourse`. Для тех, кто уже прошёл базовый ИЛИ имеет 1–2 года реального опыта React+TS и целится в middle → senior (продуктовые команды, международный найм, сильные инженерные культуры).

**НЕ дублировать:** базовый курс (HTML/CSS/JS/TS-basic/React-basic/Next-basic) и твой `claudemind/engineering-os` (там уже хорошо: Fiber-обзор, System Design кейсы, Practice tasks 20+, CRUD паттерны).

**Дополняет:** глубину, которой нет ни там, ни там — internals, архитектура масштаба, инфра без Vercel, алгоритмы, команда.

---

## Prerequisites

- Пройден `FrontendObsidianCourse` (14 модулей, P1/P2/P3) ИЛИ
- 1+ год реального опыта с React+TypeScript в команде
- Комфортен с Git, PR, терминалом, npm/pnpm

---

## Формат и инфраструктура

- **Отдельный vault:** `FrontendAdvanced/` — отдельный Obsidian-репозиторий, не подмешиваем к базовому.
- **Структура урока:** те же 6 секций (Зачем → Главное → Пример кода → Частые ошибки → Задания → Что почитать), но объём «Главное» — **500–1000 слов** (глубокие темы требуют места). Код-примеры — длиннее, реалистичнее.
- **Tone:** «ты», ментор-практик, но без упрощений. Средний читатель — middle с 1–2 годами опыта.
- **Длительность на прохождение:** 9–12 месяцев в режиме 10–15 часов/неделю.

---

## Структура: 6 треков, 20 модулей + 4 больших проекта

### Track 1: Deep Frontend (4 модуля)
Что происходит под капотом и как использовать это в бою.
- **A1.1 Browser Rendering Pipeline** — parse → style → layout → paint → composite, reflow vs repaint, composite layers, `will-change` правильно, Chrome Rendering tab, почему transform/opacity дешёвые.
- **A1.2 Event Loop и Concurrency** — macrotasks vs microtasks, `queueMicrotask`, starvation, `requestIdleCallback`, Scheduler API, Web Workers, `SharedArrayBuffer`, `Atomics`, когда выносить работу в worker.
- **A1.3 Memory и GC** — V8 heap/stack, hidden classes, young/old generation, типичные утечки (closures, listeners, detached DOM), Chrome Memory profiler, heap snapshot diff.
- **A1.4 Performance в React (2026)** — React Compiler (что делает, где ломается), Suspense streaming, selective hydration, `useTransition` глубже, profiler, флеймграфы.

### Track 2: TypeScript Mastery (3 модуля)
Типы как инструмент дизайна, не как декорация.
- **A2.1 Type-level Programming** — conditional types, `infer`, distributive unions, template literal types, recursive types, deep mapped types.
- **A2.2 Precision Types** — branded types, `Result`/`Option` вместо исключений, exhaustive matching, `satisfies` vs `as`, discriminated unions как state machine.
- **A2.3 Библиотечный DX** — как проектировать публичные API: overloads, generics с умным инференсом, declaration merging, `jsdoc` для IDE, `@ts-expect-error` с комментариями.

### Track 3: Архитектура и масштаб (4 модуля)
Что делают сеньоры в командах 10+ человек.
- **A3.1 Architecture Patterns** — Feature-Sliced Design (layers, slices, segments), hexagonal, DDD для фронта, когда что выбирать, антипаттерны.
- **A3.2 Monorepo** — Turborepo, pnpm workspaces, shared packages, build graph, incremental builds, remote cache, deploy стратегии монорепо.
- **A3.3 Micro-frontends** — Module Federation (Webpack 5/Rspack), ESM import maps, Single-SPA, когда оно **не нужно** (чаще, чем кажется), контракты между фронтами.
- **A3.4 Legacy и Refactoring** — читать чужой код системно, codemods (ast-grep, jscodeshift), strangler fig pattern, безопасные миграции JS→TS, feature flags для миграций, «как перестать бояться 200k-строчного проекта».

### Track 4: Инфра, DevOps, SQL (4 модуля)
Что нужно знать, когда Vercel недостаточно.
- **A4.1 Docker для фронтендера** — multi-stage builds, Next.js standalone output, docker-compose для dev, размер образа, healthchecks.
- **A4.2 Self-hosting без Vercel** — Caddy, Nginx как reverse proxy, Fly.io, Railway, Cloudflare Tunnel, bare VPS. Когда и зачем съезжать.
- **A4.3 CI/CD глубже** — matrix builds, параллелизация, cache стратегии, Lighthouse CI с гейтами, visual regression (Chromatic), blue-green и canary через платформы.
- **A4.4 SQL для фронтендера** — `explain analyze`, индексы (B-tree/hash/GIN/BRIN), N+1, keyset vs offset пагинация, транзакции, isolation levels, connection pooling (pgBouncer).
- **A4.5 Observability** — structured logging (pino), OpenTelemetry, distributed tracing, custom metrics, SLO/SLI/error budget, Grafana/Prometheus vs SaaS.

> _Track 4 — 5 модулей, не 4. Оставить все или слить observability в A4.3?_

### Track 5: Алгоритмы и структуры данных (2 модуля)
Не LeetCode-гринд, а применимо.
- **A5.1 Структуры данных с фронтовыми кейсами** — hash map, set, linked list, stack/queue, heap, trie. Применения: виртуализация списков, fuzzy search, undo/redo, priority queue для scheduler.
- **A5.2 Деревья, графы, DP** — BFS/DFS, topological sort, shortest paths. Применения: DOM-обход, dependency graph, диффинг деревьев, layout-алгоритмы.

### Track 6: Команда и культура (3 модуля)
Что отличает senior от middle+.
- **A6.1 Tech Writing** — ADR, RFC, дизайн-доки, postmortem. Шаблоны, структура, когда какой документ.
- **A6.2 Senior Code Review и коммуникация** — как блокировать плохой PR мягко, как аргументировать решения, как спорить с сеньором-ревьюером, культура review-диалога.
- **A6.3 Open Source** — первый merged PR в React/Next/популярную либу. Как читать issue tracker, RFC-процесс, CLA, как стать maintainer-ом, конфликты в community.

---

## Проекты (4 больших)

- **A-P1 Performance Rescue.** После Track 1. Дан медленный репо (я подготовлю или выберем реальный open-source проект). Цель: Lighthouse 60 → 95+, LCP < 1.5s, бандл < 200KB. Сдача: before/after метрики, PR с объяснениями каждой оптимизации.

- **A-P2 Monorepo Platform.** После Track 3. Turborepo, 2 приложения (маркетинг-сайт + приложение) + shared design system + shared utils. Версионирование через changesets. Деплой как отдельные Vercel-проекты из одного репо.

- **A-P3 Self-hosted Production.** После Track 4. Задеплоить Next.js-приложение **без Vercel**: Docker + VPS (Hetzner/DigitalOcean) + Caddy + Postgres + OTel. Сравнить стоимость и опыт с Vercel.

- **A-P4 OSS Contribution.** После Track 6. Реальный merged PR в популярный OSS-репо (React, Next.js, Tailwind, tanstack, любая либа с 5k+ звёзд). Документировать процесс: как нашёл issue, обсуждение, PR, review, merge.

---

## Приложения

- **Алгоритмы-advanced.md** — 50 задач medium+ (расширение базового приложения с 30 easy-задач).
- **Чтение-чужого-кода.md** — методология: как войти в legacy-проект за 2 дня и не сойти с ума.
- **Senior-собес.md** — типичные вопросы на middle/senior (system design light, trade-off обсуждения, scenario-questions).

---

## Out of Scope (намеренно)

- **Vue/Svelte/Solid** — фокус остаётся React-центричный.
- **Mobile (React Native)** — это отдельная специализация.
- **GraphQL как основной транспорт** — упомянуть в A2.3 (типизация), но не углубляться.
- **Design patterns GoF** — переоценены, возьмём только реально применимые.
- **LeetCode Hard** — потолок — medium+ с практическим применением.
- **AI/LLM тема** — у тебя уже есть отдельный `ai-engineer` трек в claudemind.
- **CS-теория ради теории** — никакой формальной computer science, только то, что применяешь.

---

## Открытые вопросы (нужен твой ответ)

1. **Observability модуль (A4.5)** — оставить отдельным или слить в A4.3 CI/CD? Я бы оставил, тема большая и самостоятельная.
2. **Проект A-P3 (Self-hosted)** — обязательный или опциональный? Кому-то карьерно не нужен (если пойдёт в Vercel-first команду), но кругозор даёт сильно.
3. **Нумерация модулей** — `A1.1 / A1.2 / ...` как сейчас (трек + номер), или сквозная `01–20`? Трековая яснее структурно, сквозная проще читать.
4. **Vault-репозиторий** — отдельный GitHub-репо `FrontendAdvanced` или ветка `advanced` в текущем `FrontendObsidianCourse`? Отдельный чище, но два репо = две точки поддержки.
5. **Когда запускаем** — сейчас сразу после базового, или после «обкатки» базового и сбора фидбэка?

---

## Риски

- **Перегруз автора.** 20 модулей глубокого материала — это в 2–3 раза плотнее базового курса. Пилить придётся долго (~2–3 месяца даже в интенсивном темпе).
- **Узкая аудитория.** Базовый курс нужен всем junior-стремящимся. Продвинутый — только тем, кто уже работает и хочет расти. Аудитория в разы меньше.
- **Быстрое устаревание.** React Compiler, Next.js internals, Module Federation в 2026 — быстро меняющиеся темы. Потребуются ежеквартальные пересмотры.
- **Частичное пересечение с `engineering-os`.** Советую перед стартом пройтись и явно разграничить: что там (recall/practice tasks) vs что здесь (deep understanding + архитектура).

---

## Следующие шаги

Если спека ок — следующий этап: `writing-plans` по треку-1 (Deep Frontend), как MVP. Попробуем качество на 4 модулях, если зайдёт — двинем дальше. Если нет — скорректируем формат.

Если хочешь что-то поменять — скажи, перепишу.
