# Frontend Obsidian Course

Полный курс frontend-разработки с нуля до junior-готовности. 14 модулей, 3 больших проекта, 12+ мини-проектов. Формат — Obsidian-vault: теория, заметки, чек-листы, карты знаний, шаблоны.

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
FrontendCourse/              <- сам курс, открывай как Obsidian-vault
├── 00-Start-Here.md         <- начни отсюда
├── 01-Setup/                <- модули по порядку
├── 02-HTML/
├── ...
├── 14-Деплой-и-финал/
├── MOC/                     <- карты знаний по темам (CSS, JS, React, TS, Next.js...)
├── Проекты/
│   ├── P1-Лендинг-по-Figma.md
│   ├── P3-Fullstack-Nextjs.md
│   └── Мини/                <- мини-проекты после каждого модуля
├── Приложения/              <- доп. материалы (алгоритмы для собеса)
├── Ресурсы/                 <- ссылки, книги, прогресс-лог
└── Шаблоны/                 <- шаблоны заметок (Templater)

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

## Продвинутая версия (скоро)

Эта версия — **для тех, кто идёт с нуля до junior-оффера**. Планируется отдельная продвинутая ветка для тех, кто уже прошёл базовый курс и целится в middle+ или сильные продуктовые команды. Там будет:

- Алгоритмы и структуры данных глубже (не только «для собеса»): деревья, графы, динамическое программирование, сложность.
- Node.js и классический backend: Express/Hono, REST-API отдельно от фреймворка, middlewares, логирование.
- System design для фронтенда: как устроены большие SPA, micro-frontends, кеш-слои, очередь задач, real-time.
- Архитектура React-приложений: feature-sliced, clean architecture, работа с большими кодовыми базами.
- Продвинутый TypeScript: conditional types, template literal types, type-level programming.
- Performance глубже: профилирование, React Compiler, Web Workers, SharedArrayBuffer.
- Безопасность: OWASP, supply chain, SBOM, advanced CSP, threat modeling.
- Чтение и рефакторинг legacy-кода, миграция JS→TS на больших проектах.
- Open-source: первый PR в React/Next/популярные библиотеки.

Анонс — после релиза базовой версии и сбора обратной связи.

## Лицензия

Материалы распространяются для личного обучения. Автор: [@6Methods](https://github.com/6Methods).
