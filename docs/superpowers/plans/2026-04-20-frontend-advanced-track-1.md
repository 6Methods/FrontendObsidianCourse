# Frontend Advanced — Track 1 (Deep Frontend) Implementation Plan

> **For agentic workers:** execute task-by-task. Subagent-driven за счёт параллельных dispatch-ов уроков.

**Goal:** MVP продвинутого курса — Track 1 «Deep Frontend»: 4 модуля (Browser Rendering, Event Loop/Concurrency, Memory/GC, React Performance 2026) + vault-сетап + MOC-Internals. Если зайдёт формат — двигаемся по Track 2–6.

**Architecture:** Паттерн как в базовом курсе, но в отдельном vault-е `FrontendAdvanced/`. Формат уроков — те же 6 секций, но «Главное» 500–1000 слов, код-примеры реальнее и длиннее. Tone — ментор-практик, «ты», без упрощений, читатель — middle с 1–2 годами React/TS.

**Tech Stack:** Obsidian-vault, Markdown, YAML frontmatter. Темы — browser internals (V8, Blink), React 19+ (Compiler, Suspense streaming, Activity), Chrome DevTools (Performance/Memory/Rendering panels).

**Пути:**
- Vault: `FrontendAdvanced/`
- Track 1: `FrontendAdvanced/A1-Deep-Frontend/`

---

## File Structure

```
FrontendAdvanced/
├── 00-Start-Here.md
├── A1-Deep-Frontend/
│   ├── A1.1-Browser-Rendering/
│   │   ├── 00-Обзор-модуля.md
│   │   ├── A1.1.1-Parse-и-DOM.md
│   │   ├── A1.1.2-Style-и-CSSOM.md
│   │   ├── A1.1.3-Layout-и-reflow.md
│   │   ├── A1.1.4-Paint-и-composite.md
│   │   ├── A1.1.5-Reflow-vs-Repaint-vs-Composite.md
│   │   └── A1.1.6-Chrome-Rendering-tab.md
│   ├── A1.2-Event-Loop-и-Concurrency/
│   │   ├── 00-Обзор-модуля.md
│   │   ├── A1.2.1-Event-loop-в-деталях.md
│   │   ├── A1.2.2-Microtasks-vs-Macrotasks.md
│   │   ├── A1.2.3-Scheduler-и-idle-callback.md
│   │   ├── A1.2.4-Web-Workers.md
│   │   ├── A1.2.5-SharedArrayBuffer-и-Atomics.md
│   │   └── A1.2.6-Service-Workers-как-runtime.md
│   ├── A1.3-Memory-и-GC/
│   │   ├── 00-Обзор-модуля.md
│   │   ├── A1.3.1-Модель-памяти-JS.md
│   │   ├── A1.3.2-V8-hidden-classes.md
│   │   ├── A1.3.3-GC-алгоритмы.md
│   │   ├── A1.3.4-Memory-leaks.md
│   │   └── A1.3.5-Chrome-Memory-Profiler.md
│   └── A1.4-React-Performance-2026/
│       ├── 00-Обзор-модуля.md
│       ├── A1.4.1-React-Compiler-что-делает.md
│       ├── A1.4.2-Когда-Compiler-ломается.md
│       ├── A1.4.3-Suspense-streaming-глубже.md
│       ├── A1.4.4-Selective-hydration.md
│       ├── A1.4.5-useTransition-и-useDeferredValue.md
│       └── A1.4.6-React-Profiler-практика.md
└── MOC/
    └── MOC-Internals.md
```

**Итого:** 1 + 4 × (1 обзор + 5–6 уроков) + 1 MOC = **27 файлов**.

---

## Task 1: Vault-сетап + Start-Here + MOC-Internals

**Files:**
- Create: `FrontendAdvanced/00-Start-Here.md`
- Create: `FrontendAdvanced/MOC/MOC-Internals.md`

**Steps:**

- [ ] **Step 1:** Написать `00-Start-Here.md` — точка входа продвинутого vault-а.

Содержание:
- Frontmatter `тип: точка-входа`.
- Краткое позиционирование: «это не базовый курс, это поверх».
- Prerequisites (пройден базовый ИЛИ 1+ год React/TS).
- Как проходить: Track 1 → 2 → 3..., проекты A-P1/A-P2/A-P3/A-P4 между треками.
- Карта треков (пока только Track 1 заполнен, остальные — _скоро_).
- MOC-секция: MOC-Internals (заполнен), MOC-Types / MOC-Architecture / MOC-Infra / MOC-Algorithms / MOC-Senior — _скоро_.
- Приложения: _скоро_ (Алгоритмы-advanced, Чтение-чужого-кода, Senior-собес).

- [ ] **Step 2:** Написать `MOC/MOC-Internals.md`.

Содержание:
- Frontmatter `тип: MOC`, `тема: Browser и JS internals`.
- Краткий абзац позиционирования.
- Секции по модулям Track 1 с линками на все 22 урока.
- Секция «Практика» с ссылкой на будущий A-P1 Performance Rescue.

---

## Task 2: Модуль A1.1 — Browser Rendering Pipeline (обзор + 6 уроков)

**Файлы:** `FrontendAdvanced/A1-Deep-Frontend/A1.1-Browser-Rendering/` — 7 файлов.

**Темы уроков:**

### A1.1.1 Parse и DOM construction
- HTML-стриминг: как Blink парсит чанк за чанком.
- DOM tree, tokens, pre-load scanner.
- Почему `<script>` блокирует парсинг (без `async`/`defer`).
- `async` vs `defer` vs `type="module"` — точное поведение.
- Speculative parsing.
- Влияние блокирующих ресурсов на FCP.

### A1.1.2 Style и CSSOM, каскад глубже
- CSSOM construction параллельно с DOM.
- Render tree = DOM + CSSOM (без `display:none`).
- Каскад: specificity → source order → `!important` → layers → inline.
- CSS Cascade Layers (`@layer`) в 2026 — зачем.
- Как CSS блокирует rendering (`<link rel="stylesheet">` в head).
- `media=print` как оптимизация.

### A1.1.3 Layout (reflow) и box model под капотом
- Что такое layout: вычисление геометрии каждого элемента.
- Когда триггерится reflow: resize, insert DOM, read `offsetHeight`, класс-свитч с размерами.
- Layout thrashing: чтение + запись в цикле.
- `contain` CSS-свойство — изоляция layout.
- `content-visibility: auto` — не рендерить невидимое.
- Ridiculous facts: сколько layout-ов делает страница гугла (спойлер: много).

### A1.1.4 Paint и Composite слои
- Paint: растеризация пикселей.
- Composite: слои объединяются на GPU.
- Какие CSS-свойства промоутят элемент в отдельный слой (`transform`, `opacity`, `will-change`, `position: fixed`, `filter`).
- Почему `transform: translateZ(0)` — хак и антипаттерн сегодня.
- Memory cost слоёв.
- DevTools Layers panel.

### A1.1.5 Reflow vs Repaint vs Composite: как мерить
- Иерархия дороговизны: reflow > repaint > composite-only.
- Свойства по категориям: `width/height/margin` → reflow; `color/background` → repaint; `transform/opacity` → composite.
- `requestAnimationFrame` — как попадать в 16.6ms frame budget.
- Performance panel: interpret Main thread flame chart.
- `performance.measure` для custom метрик.
- Long tasks API.

### A1.1.6 Chrome Rendering tab — практика
- Paint flashing — что перерисовывается.
- Layer borders — какие слои существуют.
- Scrolling performance issues — где `will-change` нужен.
- FPS meter.
- CSS overlay для Core Web Vitals realtime.
- Practical workflow: находим медленный компонент за 10 минут.

**Структура каждого урока:** 6 секций, «Главное» 500–1000 слов, код-примеры + скриншоты-описания панелей DevTools.

**Обзор модуля:** зачем, что изучаем (6 буллетов), 6 уроков списком, связанные MOC, чек-лист завершения (6–8 пунктов: «умею читать Performance panel», «знаю, какие свойства триггерят reflow», и т.д.).

---

## Task 3: Модуль A1.2 — Event Loop и Concurrency (обзор + 6 уроков)

**Файлы:** `FrontendAdvanced/A1-Deep-Frontend/A1.2-Event-Loop-и-Concurrency/` — 7 файлов.

**Темы уроков:**

### A1.2.1 Event loop в деталях
- Модель: Call stack → Web APIs → Task queue → Event loop.
- Что такое task: script execution, setTimeout callback, fetch response, DOM event handler.
- Rendering steps between tasks: style → layout → paint.
- Почему долгий task блокирует UI.
- HTML spec terminology: task source, task queue.
- `scheduler.yield()` (2026).

### A1.2.2 Microtasks vs Macrotasks
- Microtask queue: Promise.then, queueMicrotask, MutationObserver.
- Microtasks дренируются полностью между макротасками.
- Почему `await` ведёт себя «как магия» — это микротаск.
- Starvation: бесконечные микротаски блокируют рендер.
- MutationObserver как инструмент.
- queueMicrotask: когда полезен.

### A1.2.3 Scheduler и idle callback
- `requestAnimationFrame`: 16.6ms перед paint.
- `requestIdleCallback`: когда браузер свободен (30-50ms слоты).
- Scheduler API 2026: `postTask` с приоритетами (`user-blocking`, `user-visible`, `background`).
- `scheduler.yield()`: явное уступание.
- Primes в React's internal scheduler: те же идеи.

### A1.2.4 Web Workers
- Параллелизм, не concurrency: реально другой поток.
- `new Worker('worker.js')`, postMessage, onmessage.
- Transferable objects (ArrayBuffer, OffscreenCanvas).
- Module workers: `new Worker(url, { type: 'module' })`.
- Когда стоит: тяжёлый parse JSON, image processing, crypto, ML inference.
- Когда НЕ стоит: мелкие операции, overhead перекрывает.
- Comlink library — postMessage как await.

### A1.2.5 SharedArrayBuffer и Atomics
- Shared memory между main и worker.
- COOP/COEP headers — обязательны в 2026.
- Atomics.load / Atomics.store / Atomics.wait / Atomics.notify.
- Race conditions без Atomics.
- Real-world: async iteration over shared buffer, WASM threads.
- Риски: сложность, deadlocks, debug ад.

### A1.2.6 Service Workers как runtime
- Не просто кеш: полноценный background-процесс между страницей и сетью.
- Жизненный цикл: install → activate → idle → fetch-event → terminate.
- Cache API, navigation preload.
- Background Sync, Push (нативные нотификации).
- Service Worker vs Web Worker: разные задачи.
- Workbox — high-level DSL.

**Обзор модуля:** чек-лист 7 пунктов: «различаю micro/macrotask», «знаю, когда нужен Web Worker», «могу дебажить long tasks», ...

---

## Task 4: Модуль A1.3 — Memory и GC (обзор + 5 уроков)

**Файлы:** `FrontendAdvanced/A1-Deep-Frontend/A1.3-Memory-и-GC/` — 6 файлов.

**Темы уроков:**

### A1.3.1 Модель памяти JS
- Stack: примитивы, frame-ы функций (fixed size).
- Heap: объекты, массивы, функции, строки (variable).
- Reference vs value.
- Что значит «функция — object» для памяти.
- Memory allocation: при каждом литерале/конструкторе.
- Почему `const obj = {...obj}` не копирует глубоко.

### A1.3.2 V8 hidden classes
- JS-объекты — dynamic, но V8 хочет static для скорости.
- Hidden class (Shape): структура объекта с полями в определённом порядке.
- Transition: `obj.x = 1; obj.y = 2` — отдельная hidden class на каждом шаге.
- Inline caches: после стабильного hidden class — fast path.
- Почему добавлять поля в разном порядке — плохо для perf.
- Monomorphic / polymorphic / megamorphic call sites.
- Rule: инициализируй все поля в конструкторе.

### A1.3.3 GC алгоритмы
- Mark-and-sweep базовый.
- Generational GC: young generation (short-lived) + old generation (long-lived).
- Minor GC (scavenge): young generation, быстрый, частый.
- Major GC (mark-sweep-compact): old generation, медленный, редкий.
- Incremental marking: GC работает в паузах между задачами.
- Concurrent marking в V8.
- «Stop-the-world» pauses как proxy for jank.

### A1.3.4 Memory leaks (closures, listeners, detached DOM)
- Leak 1: closures, которые держат большие данные в замыкании.
- Leak 2: event listeners без removeEventListener.
- Leak 3: detached DOM nodes (ссылка в JS держит удалённый из документа узел).
- Leak 4: setInterval без clearInterval.
- Leak 5: глобальные переменные (случайно).
- Leak 6: React: stale closures в useEffect без deps.
- Pattern: AbortController для комплексной отмены (listeners + fetch).

### A1.3.5 Chrome Memory Profiler в деталях
- Memory panel overview: Heap snapshot / Allocation timeline / Allocation sampling.
- Heap snapshot: retainers, shallow size, retained size.
- Три snapshot workflow: до / во время действия / после — diff.
- Allocation timeline: видно, какие функции allocate много.
- Detached DOM: search `Detached` в фильтре.
- Закрашенные строки (red): потенциальные leaks.
- Практика: найти leak в демо-приложении за 15 минут.

---

## Task 5: Модуль A1.4 — React Performance 2026 (обзор + 6 уроков)

**Файлы:** `FrontendAdvanced/A1-Deep-Frontend/A1.4-React-Performance-2026/` — 7 файлов.

**Темы уроков:**

### A1.4.1 React Compiler — что делает
- Что такое React Compiler (ex-Forget): анализ + автоматическая мемоизация.
- Babel-plugin, интегрирован в Next.js 15+, Vite (через plugin).
- Inference: компилятор смотрит на JSX и пропсы, решает, когда `useMemo`/`useCallback` нужны автоматически.
- Результат: ручной `React.memo`, `useMemo`, `useCallback` становятся не нужны в 95% случаев.
- eslint-plugin-react-compiler — подсвечивает code, который компилятор не может оптимизировать.
- Опт-ин через `"use memo"` или глобально.

### A1.4.2 Когда Compiler ломается
- Нарушение Rules of React: mutation props, чтение refs в render.
- Conditional hooks.
- Сложные closures с mutable state.
- Non-React values в deps (Date, Math.random в render).
- Read: `eslint-plugin-react-compiler` warnings — надо чинить, а не игнорить.
- Escape hatch: `// @bailout("reason")` — сознательный отказ.
- Debug: React DevTools → Compiler view показывает, что заоптимизировано.

### A1.4.3 Suspense streaming глубже
- RSC (React Server Components) + Suspense = streaming HTML.
- Server шлёт HTML в несколько chunk-ов: сначала скелет, потом asynchronously дозагружает.
- Boundary модель: каждый `<Suspense fallback>` — точка стриминга.
- Parallel data fetching: промисы стартуют одновременно, UI подгружается по мере готовности.
- Out-of-order streaming: часть страницы может прийти быстрее.
- Вложенные Suspense: shell first → details later.

### A1.4.4 Selective hydration
- Classic hydration: монолитно, вся страница целиком.
- React 18+: Suspense boundaries гидрируются независимо.
- User interaction prioritizes: клик в ещё не-гидрированный блок → React гидрирует его первым.
- Progressive enhancement: HTML работает без JS, потом hydration добавляет интерактив.
- Streaming SSR + selective hydration = минимальный TTI.
- Troubleshoot: hydration mismatch errors.

### A1.4.5 useTransition и useDeferredValue в продакшне
- `useTransition`: помечает update как non-urgent, React может прервать его ради user input.
- Use case: фильтрация большого списка, tab switch с тяжёлым содержимым.
- `startTransition` (вне хука) для императивных случаев.
- `useDeferredValue`: альтернатива для пропсов, которые пришли извне.
- Разница: `useTransition` для state setter в твоём коде; `useDeferredValue` для value извне.
- isPending → показывать скелетон/спиннер.

### A1.4.6 React Profiler — практика
- React DevTools → Profiler: recording session.
- Flame chart: время рендера каждого компонента.
- Ranked: сортировка по длительности.
- Commit view: сколько коммитов, почему они случились.
- Interactions: привязка к user actions.
- Find the bottleneck workflow.
- Why did this render: React DevTools показывает причину (props changed / context changed / parent rendered).
- Intersect with Browser Performance panel: когда React bottleneck, а когда browser.

---

## Task 6: MOC-Internals финализация + Start-Here обновление

- [ ] **Step 1:** Обновить `MOC/MOC-Internals.md` — добавить все 22 линка уроков.
- [ ] **Step 2:** Обновить `00-Start-Here.md` — убрать «скоро» у Track 1.

---

## Out of Scope (для Track 1)

- Deep React Fiber internals (reconciliation алгоритм строка-за-строкой) — в `engineering-os` уже есть.
- JavaScript engine alternative implementations (JavaScriptCore, SpiderMonkey) — фокус V8.
- Platform APIs из WHATWG draft-ов — только стабильные 2026.
- Mobile-specific rendering (iOS Safari quirks) — упомянуть вскользь.

---

## Acceptance

Track 1 считается закрытым, когда:
- 27 файлов написаны по формату (6 секций, «Главное» 500–1000 слов).
- MOC-Internals заполнен.
- Start-Here обновлён.
- Читатель после Track 1 умеет: читать Chrome Performance/Memory/Rendering tabs, находить reflow/paint issues, использовать Web Workers осознанно, понимать React Compiler и Suspense streaming.

---

## Next

После Track 1 — ретро. Если формат (глубина 500–1000 слов, 5–6 уроков в модуле) работает — Track 2 (TypeScript Mastery). Если нет — скорректировать формат/объём.
