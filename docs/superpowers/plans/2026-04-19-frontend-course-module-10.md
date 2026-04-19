# Frontend Course — Module 10 (React экосистема) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: superpowers:subagent-driven-development. Контентный проект.

**Goal:** Наполнить модуль 10 «React экосистема»: обзор + 7 уроков + мини-проект (SPA-магазин) + дополнить MOC-React + обновить Start-Here.

**Architecture:** Структура модулей 01–09. Шаблон урока (6 секций), средняя глубина. Фокус — экосистема вокруг базового React: маршрутизация, глобальный state (Context, useReducer), оптимизация (useMemo/useCallback/useRef), кастомные хуки, серверный state (TanStack Query), формы (React Hook Form + zod). TypeScript НЕ вводим — он в модуле 11.

**Базовые пути:**
- Vault: `/Users/luckyme/Desktop/maloyfront/FrontendCourse/`
- Модуль: `FrontendCourse/10-React-экосистема/`

---

## File Structure

```
FrontendCourse/
├── 00-Start-Here.md                                  (правка: убрать «_(скоро)_»)
├── 10-React-экосистема/
│   ├── 00-Обзор-модуля.md                            (новый)
│   ├── 10.1-React-Router.md                          (новый)
│   ├── 10.2-Context.md                               (новый)
│   ├── 10.3-useReducer.md                            (новый)
│   ├── 10.4-useMemo-useCallback-useRef.md            (новый)
│   ├── 10.5-Кастомные-хуки.md                        (новый)
│   ├── 10.6-TanStack-Query.md                        (новый)
│   └── 10.7-Формы-RHF-и-zod.md                       (новый)
├── Проекты/Мини/
│   └── M10-SPA-магазин.md                            (новый)
└── MOC/
    └── MOC-React.md                                  (правка: заполнить раздел «Экосистема»)
```

Итого: **10 новых файлов**, 2 правки (Start-Here + MOC-React).

---

## Task 1: Обзор модуля 10

**Create:** `FrontendCourse/10-React-экосистема/00-Обзор-модуля.md`

```markdown
---
тип: обзор-модуля
модуль: 10-React-экосистема
статус: not-started
roadmap: https://roadmap.sh/react
---

# Модуль 10 — React экосистема

**roadmap.sh:** [React roadmap](https://roadmap.sh/react)

Ты уже знаешь базу: JSX, props, `useState`, `useEffect`, lifting state. Для простой формы и Todo — этого хватает. Но как только приложение становится SPA (страницы, глобальная корзина, серверные данные, сложные формы) — голый `useState` уже тесен. В этом модуле — экосистема, на которой пишутся реальные React-приложения: React Router, Context, TanStack Query, React Hook Form, кастомные хуки.

## Что изучаем
- React Router — маршрутизация, Link, параметры, вложенные роуты.
- Context — глобальный state без prop drilling.
- `useReducer` — сложная логика state в одном месте.
- `useMemo`, `useCallback`, `useRef` — оптимизация рендеров и работа с DOM.
- Кастомные хуки — выделение логики в переиспользуемые функции.
- TanStack Query — серверный state: cache, refetch, инвалидация.
- React Hook Form + zod — производительные формы и валидация по схеме.

## Уроки
- [ ] [[10.1-React-Router]]
- [ ] [[10.2-Context]]
- [ ] [[10.3-useReducer]]
- [ ] [[10.4-useMemo-useCallback-useRef]]
- [ ] [[10.5-Кастомные-хуки]]
- [ ] [[10.6-TanStack-Query]]
- [ ] [[10.7-Формы-RHF-и-zod]]

## Итоговая практика
- [ ] Мини-проект: [[M10-SPA-магазин]] — SPA-магазин с роутами, Context-корзиной, TanStack Query для каталога и RHF+zod для оформления. Интегрирует все темы модуля.

## Связанные MOC
- [[MOC-React]] — карта React: база (модуль 09), экосистема (этот модуль), Next.js (модуль 13).

## Чек-лист завершения
- [ ] все 7 уроков прочитаны
- [ ] мини-проект задеплоен: SPA с 4+ роутами, Context для корзины, TanStack Query для данных, RHF+zod для формы
- [ ] понимаешь разницу между клиентским и серверным state
- [ ] умеешь вытаскивать логику в кастомный хук
- [ ] знаешь, когда нужен `useMemo`/`useCallback`, а когда нет
- [ ] узлы React Router, State Management, React Hook Form в roadmap.sh закрыты
```

---

## Task 2: Урок 10.1 — React Router

**Create:** `FrontendCourse/10-React-экосистема/10.1-React-Router.md`

**Frontmatter:**
```yaml
---
модуль: 10-React-экосистема
тема: React Router
статус: to-read
roadmap: https://roadmap.sh/react
связано: [[10.2-Context]]
---
```

**Заголовок:** `# React Router`

**`## Зачем это нужно`:** Без Router SPA — одна страница, всё внутри неё. С Router ты получаешь настоящие URL: `/products`, `/products/42`, `/cart`. Переходы без перезагрузки, но с полноценной историей, закладками и кнопкой «Назад». Это стандарт для любого React-приложения больше одного экрана.

**`## Главное` (~340-420 слов):** подразделы `###`:
- **Установка и версия.** `npm install react-router-dom`. Актуальная версия — v6/v7 (синтаксис отличается от v5 — старые гайды могут путать).
- **BrowserRouter.** Обёртка вокруг приложения, должна быть в `main.jsx`: `<BrowserRouter><App /></BrowserRouter>`. Даёт доступ к URL и history.
- **Routes и Route.** `<Routes>` — контейнер. `<Route path="/" element={<Home />} />` — одна маршрутизация. Первый совпавший — рендерится.
- **Link vs `<a>`.** Всегда `<Link to="/products">Каталог</Link>`. Обычный `<a>` — полная перезагрузка, потеря state. `<NavLink>` — тот же Link + автоматический `className` на активной странице.
- **useNavigate.** Программный переход: `const navigate = useNavigate(); navigate("/cart")`. После сабмита формы, после логина.
- **useParams.** Динамический сегмент — `path="/products/:id"`. Внутри компонента: `const { id } = useParams();`. Параметр — всегда строка.
- **useSearchParams.** Query string: `?page=2&sort=price`. `const [params, setParams] = useSearchParams();`. `params.get("page")`. Удобно для фильтров, пагинации.
- **Вложенные роуты.** `<Route path="/dashboard" element={<Layout />}> <Route path="stats" element={<Stats />} /> </Route>`. В `Layout` — `<Outlet />` — место, куда подставится дочерний роут.
- **Защищённые маршруты.** Обёртка-компонент: `if (!user) return <Navigate to="/login" replace />`. Оборачиваешь нужные роуты — пользователь без авторизации не попадёт.
- **404 страница.** `<Route path="*" element={<NotFound />} />` — последний роут, ловит всё несовпавшее.

**`## Пример кода`** — блок ```jsx:
```jsx
// main.jsx
import { BrowserRouter } from "react-router-dom";
createRoot(document.getElementById("root")).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);

// App.jsx
import { Routes, Route, Link, NavLink, useParams, useNavigate, Navigate, Outlet } from "react-router-dom";

function Nav() {
  return (
    <nav>
      <NavLink to="/" end>Главная</NavLink>
      <NavLink to="/products">Каталог</NavLink>
      <NavLink to="/cart">Корзина</NavLink>
    </nav>
  );
}

function ProductPage() {
  const { id } = useParams();
  const navigate = useNavigate();
  return (
    <>
      <h2>Товар {id}</h2>
      <button onClick={() => navigate(-1)}>Назад</button>
    </>
  );
}

function Protected({ user, children }) {
  if (!user) return <Navigate to="/login" replace />;
  return children;
}

function Layout() {
  return (
    <>
      <Nav />
      <main><Outlet /></main>
    </>
  );
}

function App() {
  const user = null; // из Context в реальном проекте
  return (
    <Routes>
      <Route path="/" element={<Layout />}>
        <Route index element={<h1>Главная</h1>} />
        <Route path="products" element={<h1>Каталог</h1>} />
        <Route path="products/:id" element={<ProductPage />} />
        <Route path="cart" element={<Protected user={user}><h1>Корзина</h1></Protected>} />
        <Route path="*" element={<h1>404</h1>} />
      </Route>
    </Routes>
  );
}
```

**`## Частые ошибки`** — 4 буллета:
- Использовать `<a href="...">` вместо `<Link to="...">` — полная перезагрузка страницы, теряется state.
- Забыть `BrowserRouter` в `main.jsx` — `useNavigate`/`useParams` упадут с ошибкой «must be used within a Router».
- `useParams` ожидает число: параметр всегда строка. `Number(id)` — руками.
- Порядок роутов — более общие сверху перекрывают конкретные. В v6 это решено, но в именованных сегментах (`:id` vs `new`) — всё равно следи.

**`## Задания`:**
- [ ] Проект с 4 роутами: `/`, `/about`, `/products`, `/products/:id`. Navigation через `NavLink`.
- [ ] Добавь защищённый роут `/profile` (через флаг `isLoggedIn`).
- [ ] Фильтр каталога через `useSearchParams`: `?category=books`.
- [ ] Вложенные роуты: `/admin` → `/admin/users`, `/admin/orders`. С общим `Layout` и `<Outlet />`.

**`## Что почитать`:**
- [React Router docs](https://reactrouter.com/en/main)
- [React Router — Tutorial](https://reactrouter.com/en/main/start/tutorial)
- [React Router — useParams](https://reactrouter.com/en/main/hooks/use-params)
- [React Router — Data APIs (loaders/actions)](https://reactrouter.com/en/main/route/loader)

Блок — `jsx`.

---

## Task 3: Урок 10.2 — Context

**Create:** `FrontendCourse/10-React-экосистема/10.2-Context.md`

**Frontmatter:**
```yaml
---
модуль: 10-React-экосистема
тема: Context
статус: to-read
roadmap: https://roadmap.sh/react
связано: [[10.1-React-Router]], [[10.3-useReducer]]
---
```

**Заголовок:** `# Context`

**`## Зачем это нужно`:** Пропсы через 5 уровней — боль (prop drilling). Context — способ «пробросить» значение глубоко вниз без передачи через каждого посредника. Типичное применение — тема, текущий пользователь, локаль, корзина. Это встроенная в React альтернатива Redux для простых случаев.

**`## Главное` (~320-400 слов):** подразделы `###`:
- **Три шага.** Создать контекст `createContext(defaultValue)`, обернуть часть дерева в `<Context.Provider value={...}>`, читать в дочерних компонентах через `useContext(Context)`.
- **`createContext`.** Возвращает объект с `Provider` и `Consumer`. Default value — используется, если нет Provider выше (обычно — `null` или заглушка).
- **Provider.** `<ThemeContext.Provider value={theme}>`. Всё, что внутри, может читать `value`. Несколько Provider-ов вложенно — никаких проблем.
- **useContext.** `const theme = useContext(ThemeContext)`. Хук возвращает текущее значение ближайшего Provider-а сверху.
- **Когда использовать Context.** Данные «сквозные»: текущий пользователь, тема, локаль, корзина. НЕ используй Context для всего подряд — props справляются лучше, когда уровней 1-2.
- **Кастомный провайдер + хук.** Типовой паттерн: собственный `ThemeProvider` со своим state + `useTheme` хук вместо голого `useContext`. Удобно и даёт защиту: если нет Provider — `useTheme` может бросить ошибку с внятным сообщением.
- **Context и ре-рендеры.** Любое изменение `value` → ре-рендер ВСЕХ потребителей. Если положить туда объект, который меняется часто → тормоза. Для больших глобальных state-ов — Redux Toolkit/Zustand.
- **Разделение контекстов.** Один контекст — одна смысловая штука. «Тема + пользователь + корзина» в одном — перерендеры будут трогать всё. Раздели.
- **Context + useReducer.** Часто используются вместе (см. 10.3): reducer держит сложный state, Context прокидывает его вниз.
- **Context vs Redux/Zustand.** Context — для «редко меняющегося глобального» (тема, user). Для частых обновлений (real-time, сложное состояние) — внешний store. Для новичков в 90% случаев Context достаточен.

**`## Пример кода`** — блок ```jsx:
```jsx
import { createContext, useContext, useState } from "react";

// 1. Создать контекст
const ThemeContext = createContext(null);

// 2. Кастомный провайдер
export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");
  const toggle = () => setTheme(t => t === "light" ? "dark" : "light");
  return (
    <ThemeContext.Provider value={{ theme, toggle }}>
      {children}
    </ThemeContext.Provider>
  );
}

// 3. Кастомный хук с защитой
export function useTheme() {
  const ctx = useContext(ThemeContext);
  if (!ctx) throw new Error("useTheme должен быть внутри ThemeProvider");
  return ctx;
}

// Использование
function Button() {
  const { theme, toggle } = useTheme();
  return (
    <button
      onClick={toggle}
      className={theme === "dark" ? "dark" : "light"}
    >
      Тема: {theme}
    </button>
  );
}

function App() {
  return (
    <ThemeProvider>
      <Button />
    </ThemeProvider>
  );
}
```

**`## Частые ошибки`** — 4 буллета:
- Использовать `useContext` без Provider сверху — получишь default value (часто `null`), а потом `Cannot read property` где-нибудь глубже.
- Класть всё приложение в один Context — любое изменение ре-рендерит всё. Разделяй по смыслу.
- Передавать в `value` новый объект каждый рендер: `value={{ a, b }}` — ссылка меняется каждый раз, все потребители перерендерятся. Мемоизируй через `useMemo`.
- Использовать Context для часто меняющегося state (каждые 100ms) — будут тормоза. Подумай о Zustand/Redux.

**`## Задания`:**
- [ ] `ThemeProvider` с переключением light/dark. Хук `useTheme`. Применить в 2-3 компонентах.
- [ ] `AuthContext` — текущий пользователь, методы `login(user)` / `logout()`. Защищённый роут через `useAuth`.
- [ ] Вложи два Provider-а (тема + auth) в `main.jsx`. Убедись, что оба работают независимо.
- [ ] Мемоизируй `value` через `useMemo` — посмотри, как меняется поведение в React DevTools.

**`## Что почитать`:**
- [React docs — Passing Data Deeply with Context](https://react.dev/learn/passing-data-deeply-with-context)
- [React docs — useContext reference](https://react.dev/reference/react/useContext)
- [React docs — Scaling Up with Reducer and Context](https://react.dev/learn/scaling-up-with-reducer-and-context)
- [Kent C. Dodds — How to use React Context effectively](https://kentcdodds.com/blog/how-to-use-react-context-effectively)

Блок — `jsx`.

---

## Task 4: Урок 10.3 — useReducer

**Create:** `FrontendCourse/10-React-экосистема/10.3-useReducer.md`

**Frontmatter:**
```yaml
---
модуль: 10-React-экосистема
тема: useReducer
статус: to-read
roadmap: https://roadmap.sh/react
связано: [[10.2-Context]], [[10.4-useMemo-useCallback-useRef]]
---
```

**Заголовок:** `# useReducer`

**`## Зачем это нужно`:** Когда state сложный (много полей, разная логика обновления) — 10 разных `useState` + обработчиков превращаются в кашу. `useReducer` собирает всё в одну функцию: «на такое событие — такое новое состояние». Паттерн Redux, но встроенный в React, без библиотек.

**`## Главное` (~320-400 слов):** подразделы `###`:
- **Синтаксис.** `const [state, dispatch] = useReducer(reducer, initialState)`. `dispatch(action)` → React вызывает `reducer(state, action)` → получает новый state.
- **Reducer — чистая функция.** `function reducer(state, action) { switch (action.type) { ... } }`. Не мутирует state, возвращает новый. Не делает side-effects.
- **Action — обычный объект.** Минимум: `{ type: "ADD_TODO" }`. Чаще с данными: `{ type: "ADD_TODO", payload: { text: "..." } }`. Соглашение `type` — строка в SCREAMING_SNAKE_CASE.
- **Когда useReducer, а когда useState.** Один-два независимых значения → `useState`. Много связанных полей + сложные переходы (форма, корзина, undo/redo) → `useReducer`.
- **Иммутабельность.** Как и в `useState`, возвращай новый объект: `{ ...state, count: state.count + 1 }`, `[...state.items, newItem]`. Ни в коем случае не `state.items.push(x)`.
- **default в switch.** Всегда пиши `default: return state;` — защита от опечатки в action.type. Или `throw new Error("Unknown action: " + action.type)` — для строгости.
- **Инициализация.** Третий аргумент `useReducer(reducer, initialArg, init)` — функция ленивой инициализации: `init(initialArg)` будет вызвана один раз. Полезно, чтобы не считать тяжёлое значение каждый рендер.
- **Reducer + Context.** Классический паттерн: reducer в Context, глобальный state + dispatch доступны везде. Близко к Redux, но без зависимости.
- **Почему не всегда reducer.** Для простых случаев — оверхед. Но если обработчиков больше 3-4 и они связаны (add/remove/toggle/clear todos) — reducer выигрывает.
- **Отладка.** Все переходы централизованы в reducer — проще логировать (`console.log(action, state)`), ставить breakpoint, писать тесты чистой функции.

**`## Пример кода`** — блок ```jsx:
```jsx
import { useReducer } from "react";

// Reducer
function todosReducer(state, action) {
  switch (action.type) {
    case "ADD":
      return [...state, {
        id: crypto.randomUUID(),
        text: action.payload,
        done: false,
      }];
    case "TOGGLE":
      return state.map(t =>
        t.id === action.payload ? { ...t, done: !t.done } : t
      );
    case "REMOVE":
      return state.filter(t => t.id !== action.payload);
    case "CLEAR_DONE":
      return state.filter(t => !t.done);
    default:
      throw new Error("Unknown action: " + action.type);
  }
}

function TodoApp() {
  const [todos, dispatch] = useReducer(todosReducer, []);

  return (
    <>
      <button onClick={() => dispatch({ type: "ADD", payload: "New" })}>
        Добавить
      </button>
      <ul>
        {todos.map(t => (
          <li key={t.id}>
            <span onClick={() => dispatch({ type: "TOGGLE", payload: t.id })}>
              {t.done ? "✓" : "○"} {t.text}
            </span>
            <button onClick={() => dispatch({ type: "REMOVE", payload: t.id })}>
              ✕
            </button>
          </li>
        ))}
      </ul>
      <button onClick={() => dispatch({ type: "CLEAR_DONE" })}>
        Очистить завершённые
      </button>
    </>
  );
}
```

**`## Частые ошибки`** — 4 буллета:
- Мутировать state в reducer: `state.items.push(x); return state` — React не увидит изменений (та же ссылка).
- Делать side-effects в reducer (fetch, setTimeout) — reducer должен быть чистым. Side-effects — в `useEffect` или обработчиках.
- Забыть `default` в switch — опечатка в `action.type` тихо вернёт `undefined`, и state станет `undefined`.
- Использовать reducer для одной-двух переменных — усложнение без пользы. Начни с `useState`.

**`## Задания`:**
- [ ] Переписать `Todos` из 09.3 на `useReducer` с action-ами ADD/TOGGLE/REMOVE/CLEAR_DONE.
- [ ] Счётчик: INCREMENT/DECREMENT/RESET/SET. Разные action-ы через один dispatch.
- [ ] Корзина: ADD_ITEM/REMOVE_ITEM/CHANGE_QTY/CLEAR — state — массив объектов. Проверь иммутабельность.
- [ ] Положи reducer в Context (см. 10.2) — получи «маленький Redux» без зависимостей.

**`## Что почитать`:**
- [React docs — Extracting State Logic into a Reducer](https://react.dev/learn/extracting-state-logic-into-a-reducer)
- [React docs — useReducer reference](https://react.dev/reference/react/useReducer)
- [React docs — Scaling Up with Reducer and Context](https://react.dev/learn/scaling-up-with-reducer-and-context)
- [Kent C. Dodds — Should I useState or useReducer?](https://kentcdodds.com/blog/should-i-usestate-or-usereducer)

Блок — `jsx`.

---

## Task 5: Урок 10.4 — useMemo, useCallback, useRef

**Create:** `FrontendCourse/10-React-экосистема/10.4-useMemo-useCallback-useRef.md`

**Frontmatter:**
```yaml
---
модуль: 10-React-экосистема
тема: useMemo, useCallback, useRef
статус: to-read
roadmap: https://roadmap.sh/react
связано: [[10.3-useReducer]], [[10.5-Кастомные-хуки]]
---
```

**Заголовок:** `# useMemo, useCallback, useRef`

**`## Зачем это нужно`:** Компоненты ре-рендерятся чаще, чем хотелось бы. Три хука — инструменты точечной оптимизации и работы с не-реактивными данными. `useMemo` кеширует значение, `useCallback` — функцию, `useRef` — хранит ссылку между рендерами без ре-рендера при изменении.

**`## Главное` (~340-420 слов):** подразделы `###`:
- **useMemo: синтаксис.** `const value = useMemo(() => compute(a, b), [a, b])`. Пересчитывает `value` только когда `a` или `b` изменились. Иначе возвращает закешированное.
- **useMemo: когда.** Дорогое вычисление (фильтр большого массива, парсинг) ИЛИ стабильная ссылка для `useEffect` deps / props дочернего компонента. Для `x + 1` — не нужен.
- **useCallback: синтаксис.** `const handle = useCallback(() => {...}, [deps])`. Возвращает ту же функцию между рендерами, пока deps не изменились.
- **useCallback: когда.** Функцию передаёшь в `React.memo`-компонент или в deps другого хука. Иначе — не нужен: обычная функция пересоздаётся бесплатно.
- **React.memo.** Обёртка компонента: `export default memo(Child)`. Компонент ре-рендерится только если props изменились (по shallow compare). Вместе с `useCallback`/`useMemo` — защита от лишних рендеров.
- **useRef: синтаксис.** `const ref = useRef(initial)`. `ref.current` — мутабельное значение. Изменение НЕ вызывает ре-рендер.
- **useRef для DOM.** `<input ref={inputRef} />` + `inputRef.current.focus()`. Прямой доступ к элементу — для фокуса, скролла, измерений.
- **useRef для «переменных между рендерами».** ID таймера, предыдущее значение prop, флаг «первый рендер». Всё, что нужно сохранить, но не показывать в UI.
- **Не оптимизируй заранее.** React быстрый. В 90% случаев `useMemo`/`useCallback` не нужны и делают код сложнее. Добавляй, когда замерил тормоза через React DevTools Profiler.
- **Правильные deps.** Линтер `react-hooks/exhaustive-deps` — всегда указывает правильные зависимости. Не обманывай его пустым массивом — получишь баги со stale closure.

**`## Пример кода`** — блок ```jsx:
```jsx
import { useState, useMemo, useCallback, useRef, memo, useEffect } from "react";

// Дорогая фильтрация — через useMemo
function ProductList({ products, query }) {
  const filtered = useMemo(
    () => products.filter(p => p.name.toLowerCase().includes(query.toLowerCase())),
    [products, query]
  );
  return <ul>{filtered.map(p => <li key={p.id}>{p.name}</li>)}</ul>;
}

// Стабильная функция для memo-дочки
const ChildButton = memo(function ChildButton({ onClick, label }) {
  console.log("render ChildButton");
  return <button onClick={onClick}>{label}</button>;
});

function Parent() {
  const [count, setCount] = useState(0);
  const handleClick = useCallback(() => setCount(c => c + 1), []);
  return (
    <>
      <p>{count}</p>
      <ChildButton onClick={handleClick} label="+" />
    </>
  );
}

// useRef: DOM и таймер
function SearchInput() {
  const inputRef = useRef(null);
  const timerRef = useRef(null);
  const [text, setText] = useState("");

  useEffect(() => {
    inputRef.current.focus();
  }, []);

  function handleChange(e) {
    setText(e.target.value);
    clearTimeout(timerRef.current);
    timerRef.current = setTimeout(() => console.log("search:", e.target.value), 500);
  }

  return <input ref={inputRef} value={text} onChange={handleChange} />;
}
```

**`## Частые ошибки`** — 4 буллета:
- Использовать `useMemo` для простого выражения: `useMemo(() => a + b, [a, b])` — оверхед больше, чем вычисление. Только для дорогих операций.
- `useCallback` без `React.memo` на дочернем — бесполезен: child всё равно ре-рендерится от родителя.
- Писать в `ref.current` и ждать ре-рендер — нет, `useRef` не триггерит. Для реактивных значений — `useState`.
- Пустой массив deps в `useEffect`/`useCallback`, когда внутри используется state/props — stale closure, бьёт всегда старыми значениями. Слушай линтер.

**`## Задания`:**
- [ ] Медленный поиск: массив 10000 элементов + `filter` в рендере. Обернул в `useMemo` — сравни FPS в Profiler.
- [ ] Родитель + 5 `memo`-дочерей с callback-prop. Без `useCallback` — все рендерятся. С ним — только нужные.
- [ ] Input с автофокусом при маунте — через `useRef`.
- [ ] Debounce-поиск через `useRef` на `setTimeout` (не через библиотеку, а руками).

**`## Что почитать`:**
- [React docs — useMemo](https://react.dev/reference/react/useMemo)
- [React docs — useCallback](https://react.dev/reference/react/useCallback)
- [React docs — useRef](https://react.dev/reference/react/useRef)
- [React docs — Manipulating the DOM with Refs](https://react.dev/learn/manipulating-the-dom-with-refs)

Блок — `jsx`.

---

## Task 6: Урок 10.5 — Кастомные хуки

**Create:** `FrontendCourse/10-React-экосистема/10.5-Кастомные-хуки.md`

**Frontmatter:**
```yaml
---
модуль: 10-React-экосистема
тема: Кастомные хуки
статус: to-read
roadmap: https://roadmap.sh/react
связано: [[10.4-useMemo-useCallback-useRef]], [[10.6-TanStack-Query]]
---
```

**Заголовок:** `# Кастомные хуки`

**`## Зачем это нужно`:** Если в двух компонентах одинаковая логика (подписка на resize, чтение localStorage, fetch-обвязка) — вынеси в функцию `useSomething`. Получишь переиспользование без копипасты. Кастомные хуки — главный способ делиться логикой между компонентами, заменяющий HOC и render-props.

**`## Главное` (~320-400 слов):** подразделы `###`:
- **Правило одно.** Функция с именем на `use`, которая внутри вызывает другие хуки. Всё — это и есть кастомный хук. Не магия — просто соглашение.
- **Возвращать можно что угодно.** Объект `{ data, loading, error }`, массив `[value, setValue]`, одно значение. Удобно — так, как логично для использования.
- **Типичный пример: useLocalStorage.** `const [val, setVal] = useLocalStorage("key", defaultVal)`. Внутри — `useState` + `useEffect` для синхронизации.
- **useFetch.** Базовый хук: берёт URL, возвращает `{ data, loading, error }`. Внутри — `useState` + `useEffect` с `AbortController`. Реальный проект — `TanStack Query` (10.6), но свой `useFetch` писал каждый.
- **useDebounce.** Значение, обновляющееся с задержкой. Полезно для поиска. `const debounced = useDebounce(query, 300)`.
- **useMediaQuery.** `const isMobile = useMediaQuery("(max-width: 768px)")`. Подписка на `matchMedia`, ре-рендер при изменении.
- **useToggle.** Утилитарный: `const [isOpen, toggle] = useToggle(false)`. Минимальный, но удобный для модалок.
- **Правила хуков в своих хуках.** Внутри кастомного хука — те же правила: верхний уровень функции, без условий. Линтер не делает исключений.
- **Когда выносить в хук.** Если логика повторилась ≥2 раз ИЛИ компонент перегружен `useEffect`/`useState` и ты хочешь сфокусировать его на UI.
- **Именование.** Всегда `use<Name>` — линтер React хуков ищет именно префикс `use`. Без него он решит, что это обычная функция, и пропустит проверки.
- **Кастомный хук — не общий state.** Каждый вызов хука — свой state. `useLocalStorage("x")` в двух компонентах — два отдельных state с синхронизацией через localStorage, не единый source of truth. Для общего — Context.

**`## Пример кода`** — блок ```jsx:
```jsx
import { useState, useEffect, useCallback } from "react";

// useLocalStorage
export function useLocalStorage(key, initial) {
  const [val, setVal] = useState(() => {
    const raw = localStorage.getItem(key);
    return raw ? JSON.parse(raw) : initial;
  });
  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(val));
  }, [key, val]);
  return [val, setVal];
}

// useDebounce
export function useDebounce(value, delay = 300) {
  const [debounced, setDebounced] = useState(value);
  useEffect(() => {
    const id = setTimeout(() => setDebounced(value), delay);
    return () => clearTimeout(id);
  }, [value, delay]);
  return debounced;
}

// useToggle
export function useToggle(initial = false) {
  const [on, setOn] = useState(initial);
  const toggle = useCallback(() => setOn(v => !v), []);
  return [on, toggle, setOn];
}

// useFetch (учебный, боевой — TanStack Query)
export function useFetch(url) {
  const [state, setState] = useState({ data: null, loading: true, error: null });
  useEffect(() => {
    const ctrl = new AbortController();
    setState({ data: null, loading: true, error: null });
    fetch(url, { signal: ctrl.signal })
      .then(r => r.json())
      .then(data => setState({ data, loading: false, error: null }))
      .catch(err => {
        if (err.name !== "AbortError") {
          setState({ data: null, loading: false, error: err });
        }
      });
    return () => ctrl.abort();
  }, [url]);
  return state;
}

// Использование
function Profile({ userId }) {
  const { data, loading, error } = useFetch(`/api/users/${userId}`);
  if (loading) return <p>Загрузка…</p>;
  if (error) return <p>Ошибка: {error.message}</p>;
  return <h2>{data.name}</h2>;
}
```

**`## Частые ошибки`** — 4 буллета:
- Имя без `use`: `function getLocalStorage()` — линтер не проверит, React-правила нарушатся тихо.
- Вызывать обычную функцию так же, как хук (или наоборот) — это разные вещи. Хук — содержит хуки, обычная функция — нет.
- Ожидать общего state между вызовами одного хука — каждый вызов независим. Для общего — Context.
- Копировать логику между двумя компонентами «ещё разок» — уже на 2-й раз время выносить в хук.

**`## Задания`:**
- [ ] Напиши `useLocalStorage(key, initial)` — state + автосохранение в localStorage.
- [ ] Напиши `useDebounce(value, delay)` — и собери поиск с задержкой на 300ms.
- [ ] Напиши `useMediaQuery(query)` — переключай лэйаут между mobile и desktop.
- [ ] Вытащи всю логику загрузки из компонента `UserProfile` в `useUser(id)` — компонент станет «тонким».

**`## Что почитать`:**
- [React docs — Reusing Logic with Custom Hooks](https://react.dev/learn/reusing-logic-with-custom-hooks)
- [React docs — The use prefix](https://react.dev/learn/reusing-logic-with-custom-hooks#hook-names-always-start-with-use)
- [usehooks.com — коллекция готовых хуков](https://usehooks.com/)
- [Kent C. Dodds — When to useState vs useReducer](https://kentcdodds.com/blog/should-i-usestate-or-usereducer)

Блок — `jsx`.

---

## Task 7: Урок 10.6 — TanStack Query

**Create:** `FrontendCourse/10-React-экосистема/10.6-TanStack-Query.md`

**Frontmatter:**
```yaml
---
модуль: 10-React-экосистема
тема: TanStack Query
статус: to-read
roadmap: https://roadmap.sh/react
связано: [[10.5-Кастомные-хуки]], [[10.7-Формы-RHF-и-zod]]
---
```

**Заголовок:** `# TanStack Query`

**`## Зачем это нужно`:** Fetch руками через `useEffect` → boilerplate: loading, error, отмена, cache, refetch, синхронизация между компонентами. TanStack Query (бывший React Query) решает всё это одной строкой `useQuery`. Это индустриальный стандарт работы с серверным state в React.

**`## Главное` (~340-420 слов):** подразделы `###`:
- **Серверный vs клиентский state.** Клиентский — твой UI (модалка, выбранный таб). Серверный — копия данных с бэка, которые могут устареть. Это разные вещи, и `useState` — не лучший инструмент для серверных.
- **Установка.** `npm install @tanstack/react-query`. В `main.jsx` — обёртка `<QueryClientProvider client={queryClient}>` и инстанс `new QueryClient()`.
- **useQuery.** `const { data, isLoading, error } = useQuery({ queryKey: ["users"], queryFn: fetchUsers })`. Всё готово: cache, автоматический refetch при фокусе окна, дедупликация одинаковых запросов.
- **queryKey.** Массив, уникально идентифицирующий запрос. Зависит от параметров: `["user", userId]`. При изменении ключа — новый запрос.
- **Состояния.** `isLoading` — первичная загрузка, `isFetching` — любой fetch (включая background), `isError` — ошибка, `error` — объект ошибки, `data` — результат.
- **Cache и stale time.** По умолчанию данные считаются устаревшими сразу (`staleTime: 0`). `staleTime: 60_000` — свежие в течение минуты, refetch не происходит. `gcTime` (бывший `cacheTime`) — сколько держать в памяти после unmount.
- **useMutation.** Для POST/PUT/DELETE: `const { mutate } = useMutation({ mutationFn: (data) => fetch(...) })`. Дальше `mutate(payload)` в обработчике.
- **Инвалидация.** После mutation — обнови связанные запросы: `queryClient.invalidateQueries({ queryKey: ["todos"] })`. Тогда TanStack сам перезапросит свежие данные.
- **Optimistic updates.** Можно сразу обновить кеш до ответа сервера (`onMutate`), при ошибке откатить (`onError`). Даёт мгновенный UI-отклик.
- **DevTools.** `@tanstack/react-query-devtools` — overlay, где видишь все запросы, их состояние, данные. Обязательно поставь в dev-сборке.
- **Что даёт из коробки.** Cache, дедупликация, автоматический refetch при фокусе/реконнекте, background refetch, отмена устаревших запросов, retry при ошибке. Всё то, что руками писать — неделя.

**`## Пример кода`** — блок ```jsx:
```jsx
// main.jsx
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
const queryClient = new QueryClient();

createRoot(document.getElementById("root")).render(
  <QueryClientProvider client={queryClient}>
    <App />
  </QueryClientProvider>
);

// hooks/useUsers.js
import { useQuery, useMutation, useQueryClient } from "@tanstack/react-query";

export function useUsers() {
  return useQuery({
    queryKey: ["users"],
    queryFn: () => fetch("/api/users").then(r => r.json()),
    staleTime: 60_000, // свежие минуту
  });
}

export function useCreateUser() {
  const qc = useQueryClient();
  return useMutation({
    mutationFn: (user) =>
      fetch("/api/users", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(user),
      }).then(r => r.json()),
    onSuccess: () => qc.invalidateQueries({ queryKey: ["users"] }),
  });
}

// components/UsersList.jsx
function UsersList() {
  const { data, isLoading, error } = useUsers();
  const createUser = useCreateUser();

  if (isLoading) return <p>Загрузка…</p>;
  if (error) return <p>Ошибка: {error.message}</p>;

  return (
    <>
      <ul>
        {data.map(u => <li key={u.id}>{u.name}</li>)}
      </ul>
      <button
        onClick={() => createUser.mutate({ name: "Новый" })}
        disabled={createUser.isPending}
      >
        Добавить
      </button>
    </>
  );
}
```

**`## Частые ошибки`** — 4 буллета:
- Забыть `queryKey` — без него TanStack не может кешировать и дедуплицировать запросы.
- Менять `queryKey` через объект без стабильной структуры — кеш не попадает, каждый раз новый запрос.
- Делать fetch в `useEffect` и дублировать с `useQuery` — выбирай что-то одно, синхронизация сломается.
- Не инвалидировать запросы после mutation — UI показывает старые данные до ручного refresh.

**`## Задания`:**
- [ ] Поставь TanStack Query + DevTools. Сделай запрос к [dummyjson.com/products](https://dummyjson.com/products) через `useQuery`.
- [ ] Добавь `staleTime: 60_000` — открой DevTools, посмотри, как запрос становится «fresh».
- [ ] Сделай `useMutation` для добавления продукта (POST, пусть mock через dummyjson) + invalidateQueries.
- [ ] Сделай запрос с параметром: `useQuery({ queryKey: ["product", id], queryFn: ... })`. При смене `id` — новый запрос.

**`## Что почитать`:**
- [TanStack Query docs](https://tanstack.com/query/latest/docs)
- [TanStack Query — Quick Start](https://tanstack.com/query/latest/docs/framework/react/quick-start)
- [TanStack Query — Mutations](https://tanstack.com/query/latest/docs/framework/react/guides/mutations)
- [TkDodo — Practical React Query](https://tkdodo.eu/blog/practical-react-query)

Блок — `jsx`.

---

## Task 8: Урок 10.7 — Формы: React Hook Form + zod

**Create:** `FrontendCourse/10-React-экосистема/10.7-Формы-RHF-и-zod.md`

**Frontmatter:**
```yaml
---
модуль: 10-React-экосистема
тема: Формы — React Hook Form + zod
статус: to-read
roadmap: https://roadmap.sh/react
связано: [[10.6-TanStack-Query]]
---
```

**Заголовок:** `# Формы — React Hook Form + zod`

**`## Зачем это нужно`:** Controlled inputs через `useState` работают, но для сложной формы (10 полей, валидация, ошибки) — 100 строк boilerplate. React Hook Form + zod — индустриальный стандарт: минимум кода, максимум производительности, валидация по схеме. Плюс zod даёт одну истину для валидации и формы, и API-ответа.

**`## Главное` (~340-420 слов):** подразделы `###`:
- **Установка.** `npm install react-hook-form zod @hookform/resolvers`. Три отдельных пакета: RHF, zod (валидация), резолвер-мост.
- **useForm.** `const { register, handleSubmit, formState } = useForm({ resolver: zodResolver(schema) })`. Хук отдаёт API для работы с полями.
- **register.** `<input {...register("email")} />` — привязка поля. RHF сам подставляет `name`, `onChange`, `onBlur`, `ref`. Uncontrolled под капотом — быстро, мало ре-рендеров.
- **handleSubmit.** `<form onSubmit={handleSubmit(onValid, onInvalid)}>`. RHF сам сделает `preventDefault`, валидирует, вызовет `onValid(data)` только если всё ок.
- **formState.** `errors` — объект ошибок по полям, `isSubmitting` — идёт ли submit, `isDirty` — менялось ли поле. Рендер индикаторов — через это.
- **Zod-схема.** `const schema = z.object({ email: z.string().email(), age: z.number().min(18) })`. Описываешь правила, получаешь TypeScript-тип + валидатор из одного источника.
- **Zod → RHF через resolver.** `zodResolver(schema)` — мост: RHF дёргает zod, zod возвращает ошибки, RHF кладёт в `formState.errors`. Одной строкой.
- **Отображение ошибок.** `{errors.email && <span>{errors.email.message}</span>}`. Сообщения приходят из zod (пиши на русском в схеме: `z.string().email("Неверный email")`).
- **Controller для неконтролируемых.** Для сторонних библиотек (react-select, date-picker), которые не умеют `register` — `<Controller name="date" control={control} render={...} />`.
- **watch / setValue / reset.** `watch("email")` — подписка на значение. `setValue("email", "x")` — программная запись. `reset()` — сброс после успеха.
- **Производительность.** RHF минимизирует ре-рендеры: большинство полей — uncontrolled. Печать в одно поле не ре-рендерит всю форму (в отличие от `useState`-подхода).

**`## Пример кода`** — блок ```jsx:
```jsx
import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { z } from "zod";

const schema = z.object({
  email: z.string().email("Неверный email"),
  password: z.string().min(8, "Минимум 8 символов"),
  age: z.coerce.number().int().min(18, "Только для совершеннолетних"),
  subscribe: z.boolean().optional(),
});

function SignupForm() {
  const {
    register,
    handleSubmit,
    reset,
    formState: { errors, isSubmitting },
  } = useForm({
    resolver: zodResolver(schema),
    defaultValues: { email: "", password: "", age: 0, subscribe: false },
  });

  async function onSubmit(data) {
    await fetch("/api/signup", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(data),
    });
    reset();
  }

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <label>
        Email
        <input {...register("email")} />
        {errors.email && <span className="err">{errors.email.message}</span>}
      </label>

      <label>
        Пароль
        <input type="password" {...register("password")} />
        {errors.password && <span className="err">{errors.password.message}</span>}
      </label>

      <label>
        Возраст
        <input type="number" {...register("age")} />
        {errors.age && <span className="err">{errors.age.message}</span>}
      </label>

      <label>
        <input type="checkbox" {...register("subscribe")} />
        Подписка
      </label>

      <button type="submit" disabled={isSubmitting}>
        {isSubmitting ? "Отправка…" : "Зарегистрироваться"}
      </button>
    </form>
  );
}
```

**`## Частые ошибки`** — 4 буллета:
- Забыть `resolver: zodResolver(schema)` — RHF работает без валидации, поля без проверки.
- Читать `formState.errors` как строку: `{errors.email}` — это объект, нужно `errors.email.message`.
- Для чисел использовать `z.number()` — input-ы отдают строки, нужен `z.coerce.number()` или явный `valueAsNumber: true` в `register`.
- Использовать RHF как `useState`: `const email = watch("email")` + ре-рендер — теряешь главный плюс uncontrolled. Подписывайся только там, где надо.

**`## Задания`:**
- [ ] Форма регистрации с 4 полями (email, password, age, subscribe) + zod-схема + резолвер. Ошибки под каждым полем.
- [ ] Добавь `confirmPassword` — валидация через `z.refine`: `password === confirmPassword`.
- [ ] После успешного submit — `reset()` + сообщение «Зарегистрировано».
- [ ] Сделай форму адреса (city, street, zip) — через `z.object` вложенный в основной schema. Разнеси поля по fieldset-ам.

**`## Что почитать`:**
- [React Hook Form docs](https://react-hook-form.com/)
- [React Hook Form — Get Started](https://react-hook-form.com/get-started)
- [Zod docs](https://zod.dev/)
- [Zod + RHF integration](https://react-hook-form.com/get-started#SchemaValidation)

Блок — `jsx`.

---

## Task 9: Мини-проект M10 — SPA-магазин

**Create:** `FrontendCourse/Проекты/Мини/M10-SPA-магазин.md`

**Exact content:**

```markdown
---
тип: мини-проект
модуль: 10-React-экосистема
статус: not-started
---

# M10 — SPA-магазин

Мини-проект после модуля 10. SPA-магазин на React + Vite, интегрирующий все темы модуля: React Router (роуты), Context (корзина), TanStack Query (каталог с API), React Hook Form + zod (оформление заказа). Это первый «серьёзный» проект — по структуре близкий к тому, что делают на реальной работе.

## Задача

Маленький интернет-магазин с 4 роутами: каталог, страница товара, корзина, checkout. Данные — с публичного API [dummyjson.com/products](https://dummyjson.com/products). Корзина — в Context с персистом в localStorage. Checkout — форма с валидацией через RHF + zod, отправка — mock POST (консоль или dummyjson).

## Требования

### Функциональность
1. **Роуты:** `/` (редирект на /products), `/products` (каталог), `/products/:id` (деталь), `/cart` (корзина), `/checkout` (форма). 404 для всего остального.
2. **Каталог** — 20+ товаров из dummyjson, карточки с картинкой/названием/ценой, кнопкой «В корзину».
3. **Поиск и фильтр** — по названию (debounce 300мс через `useDebounce`), по категории — через `useSearchParams`.
4. **Страница товара** — полная информация, кнопка «В корзину», «Назад к каталогу».
5. **Корзина (Context)** — добавление, удаление, изменение количества, подсчёт суммы, очистка. Персист в localStorage.
6. **Счётчик в навбаре** — сколько товаров в корзине, в реальном времени.
7. **Checkout** — форма с 5-6 полями (имя, email, телефон, город, адрес, комментарий): RHF + zod.
8. **Валидация формы** — email, телефон (regex), все обязательные поля, минимальные длины. Ошибки под полями.
9. **После успеха** — редирект на `/success` с поздравлением, очистка корзины.
10. **Деплой** — Vercel, прод-URL.

### Технические правила
- `npm create vite@latest ... -- --template react`, без TypeScript.
- React Router v6/v7, `BrowserRouter`.
- Состояние корзины — только в Context (никаких Redux/Zustand).
- Данные — только через TanStack Query (никаких голых `fetch` в `useEffect`).
- Форма — только RHF + zod (никаких `useState` для полей).
- Минимум один кастомный хук (например, `useCart`, `useDebounce`, или `useProducts`).
- `React Query DevTools` — в dev-сборке.
- `.gitignore` (node_modules, dist, .env).
- README: ссылка на прод, скриншоты, краткое «архитектура».

### Структура проекта (ориентир)
```
src/
├── main.jsx              # BrowserRouter + QueryClientProvider + CartProvider
├── App.jsx               # Routes
├── pages/
│   ├── ProductsPage.jsx
│   ├── ProductPage.jsx
│   ├── CartPage.jsx
│   ├── CheckoutPage.jsx
│   └── SuccessPage.jsx
├── components/
│   ├── Nav.jsx           # с счётчиком корзины
│   ├── ProductCard.jsx
│   └── CheckoutForm.jsx  # RHF + zod
├── context/
│   └── CartContext.jsx   # useCart + провайдер
└── hooks/
    ├── useProducts.js    # TanStack Query
    └── useDebounce.js
```

## Чего НЕ должно быть

- Голых `fetch` в компонентах (всё через TanStack Query).
- Локальных `useState` для полей формы checkout (RHF + zod).
- Redux/Zustand — Context достаточно.
- UI-библиотек (MUI, Chakra) — пиши свои компоненты + чистый CSS.
- TypeScript — будет в модуле 11.
- `key={index}` в списках (используй `product.id`).

## Этапы

1. Vite + React, поставить: `react-router-dom`, `@tanstack/react-query`, `@tanstack/react-query-devtools`, `react-hook-form`, `zod`, `@hookform/resolvers`.
2. Скелет роутов: 5 страниц + 404. `BrowserRouter` в main.
3. `CartProvider` + `useCart` хук. Persist в localStorage.
4. `useProducts` / `useProduct(id)` через TanStack Query + dummyjson.
5. Каталог: карточки, поиск с debounce, фильтр по категории через searchParams.
6. Страница товара + кнопка «В корзину».
7. Корзина: список, изменение qty, удаление, сумма.
8. Checkout форма: 5-6 полей, zod-схема, обработка submit.
9. Success-страница, reset корзины.
10. Стили: CSS Modules или просто CSS. Адаптивный layout.
11. Деплой на Vercel.

## Сдача

1. Публичный GitHub-репозиторий.
2. Прод-URL (HTTPS, Vercel/Netlify).
3. README: ссылка на деплой, 2-3 скриншота, «стек», «структура папок», «что сложного».
4. На созвоне — смотрим код по слоям: роуты → Context → TanStack Query → форма.

## Критерии приёмки ревью

- [ ] 5 рабочих роутов + 404.
- [ ] Каталог загружается через TanStack Query, есть loader и error-состояния.
- [ ] Поиск с debounce работает (проверяется в Network — нет запроса на каждый keystroke).
- [ ] Фильтр категории через `useSearchParams` — URL меняется, shareable.
- [ ] Context-корзина: add/remove/qty/clear, сумма корректная.
- [ ] Корзина сохраняется в localStorage (F5 не очищает).
- [ ] Счётчик в навбаре обновляется в реальном времени.
- [ ] Checkout — RHF + zod, валидация работает, ошибки отображаются.
- [ ] После submit — редирект на /success, корзина очищена.
- [ ] Минимум один кастомный хук в `src/hooks/`.
- [ ] React Query DevTools установлен (виден overlay в dev).
- [ ] Нет `useState` для полей формы checkout.
- [ ] Нет голых `fetch` в компонентах.
- [ ] Прод-URL работает.

## Что дальше
Дальше — **модуль 11 TypeScript**: типизация props, state, API-ответов, generics. Перепишешь этот магазин на TS — увидишь, как ошибки ловятся до запуска.
```

---

## Task 10: Заполнить раздел «Экосистема» в MOC-React

**Modify:** `FrontendCourse/MOC/MOC-React.md`

Заменить полностью — добавить 7 уроков в «Экосистема» и ссылку на M10 в «Практика».

**Exact content:**

```markdown
---
тип: MOC
тема: React
---

# MOC — React

Карта знаний по React: база (модуль 09), экосистема и роутинг (модуль 10), Next.js (модуль 13).

## База (модуль 09)
- [[09.1-JSX-и-компоненты]]
- [[09.2-Props]]
- [[09.3-State-и-useState]]
- [[09.4-События-и-формы]]
- [[09.5-Списки-и-условный-рендеринг]]
- [[09.6-useEffect]]
- [[09.7-Lifting-state-и-композиция]]

## Экосистема (модуль 10)
- [[10.1-React-Router]]
- [[10.2-Context]]
- [[10.3-useReducer]]
- [[10.4-useMemo-useCallback-useRef]]
- [[10.5-Кастомные-хуки]]
- [[10.6-TanStack-Query]]
- [[10.7-Формы-RHF-и-zod]]

## Next.js (модуль 13 — скоро)
- _App Router, Server Components, Server Actions, routing, layouts_

## Практика
- [[M09-Todo-на-React]] — первая переработка vanilla-проекта на React.
- [[M10-SPA-магазин]] — SPA с роутами, Context, TanStack Query, RHF+zod.
```

---

## Task 11: Обновить 00-Start-Here.md

**Modify:** `FrontendCourse/00-Start-Here.md`

Убрать «_(скоро)_» у модуля 10:
`- [[10-React-экосистема/00-Обзор-модуля|Модуль 10 — React экосистема]] _(скоро)_` → `- [[10-React-экосистема/00-Обзор-модуля|Модуль 10 — React экосистема]]`.

---

## Task 12: Верификация

- [ ] `FrontendCourse/10-React-экосистема/` содержит 8 `.md` файлов.
- [ ] `M10-SPA-магазин.md` существует в `Проекты/Мини/`.
- [ ] `MOC-React.md` содержит 7 ссылок на уроки 10.1–10.7 и ссылку на `M10-SPA-магазин`.
- [ ] В `00-Start-Here.md` у модуля 10 нет «_(скоро)_».
- [ ] Отчитаться: модуль 10 готов.

---

## Out of Scope

- TypeScript с React — модуль 11.
- Тестирование React (Vitest, Testing Library) — модуль 12.
- Server Components, Next.js, SSR — модуль 13.
- Zustand / Redux Toolkit — обзорно в модуле 13/14, но не сейчас.
- Storybook — модуль 12 (опционально).
