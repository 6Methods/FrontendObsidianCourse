# Frontend Course — Module 09 (React база) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: superpowers:subagent-driven-development. Контентный проект.

**Goal:** Наполнить модуль 09 «React база»: обзор + 7 уроков + мини-проект (Todo на React) + создать MOC-React (заполнение) + обновить Start-Here.

**Architecture:** Структура модулей 01–08. Шаблон урока (6 секций), средняя глубина. Фокус — пять хуков базы: `useState`, `useEffect`, и базовая композиция. React 18+/19, функциональные компоненты, Vite как инструмент. TypeScript НЕ вводим — он в модуле 11.

**Базовые пути:**
- Vault: `/Users/luckyme/Desktop/maloyfront/FrontendCourse/`
- Модуль: `FrontendCourse/09-React-база/`

---

## File Structure

```
FrontendCourse/
├── 00-Start-Here.md                               (правка: убрать «_(скоро)_»)
├── 09-React-база/
│   ├── 00-Обзор-модуля.md                         (новый)
│   ├── 09.1-JSX-и-компоненты.md                   (новый)
│   ├── 09.2-Props.md                              (новый)
│   ├── 09.3-State-и-useState.md                   (новый)
│   ├── 09.4-События-и-формы.md                    (новый)
│   ├── 09.5-Списки-и-условный-рендеринг.md        (новый)
│   ├── 09.6-useEffect.md                          (новый)
│   └── 09.7-Lifting-state-и-композиция.md         (новый)
├── Проекты/Мини/
│   └── M09-Todo-на-React.md                       (новый)
└── MOC/
    └── MOC-React.md                               (правка: заполнить раздел «База»)
```

Итого: **10 новых файлов**, 2 правки (Start-Here + MOC-React).

---

## Task 1: Обзор модуля 09

**Create:** `FrontendCourse/09-React-база/00-Обзор-модуля.md`

**Exact content:**

```markdown
---
тип: обзор-модуля
модуль: 09-React-база
статус: not-started
roadmap: https://roadmap.sh/react
---

# Модуль 09 — React база

**roadmap.sh:** [React roadmap](https://roadmap.sh/react)

Ты уже умеешь vanilla JS с DOM. Но как только проект больше одной страницы — DOM превращается в кашу: ручное обновление, синхронизация состояния, забытые listener-ы. React решает это декларативно: описываешь «как выглядит UI при таком-то state», React сам ставит и убирает правильное. Этот модуль — про переход от «императивного DOM» к «декларативному UI» и пять базовых инструментов (`useState`, `useEffect`, props, events, композиция).

## Что изучаем
- JSX и функциональные компоненты — как писать UI внутри JS.
- Props — передача данных сверху вниз, children.
- `useState` — локальное состояние компонента.
- События и формы — controlled inputs, обработчики.
- Списки (`.map` + `key`) и условный рендеринг.
- `useEffect` — сайд-эффекты, зависимости, cleanup.
- Lifting state up — подъём состояния, композиция, «дырка» для children.

## Уроки
- [ ] [[09.1-JSX-и-компоненты]]
- [ ] [[09.2-Props]]
- [ ] [[09.3-State-и-useState]]
- [ ] [[09.4-События-и-формы]]
- [ ] [[09.5-Списки-и-условный-рендеринг]]
- [ ] [[09.6-useEffect]]
- [ ] [[09.7-Lifting-state-и-композиция]]

## Итоговая практика
- [ ] Мини-проект: [[M09-Todo-на-React]] — переписать M05 ToDo на React + Vite. Разделение на компоненты, useState, useEffect для localStorage, формы.

## Связанные MOC
- [[MOC-React]] — карта React: база (этот модуль), экосистема (модуль 10), Next.js (модуль 13).

## Чек-лист завершения
- [ ] все 7 уроков прочитаны
- [ ] мини-проект задеплоен, работает, компоненты разделены, нет прямой работы с DOM
- [ ] умеешь поставить Vite + React проект с нуля
- [ ] понимаешь разницу между «состояние» и «пропсы», умеешь поднимать state вверх
- [ ] знаешь, когда нужен `useEffect`, а когда обычного выражения достаточно
- [ ] узлы React → Basics на roadmap.sh закрыты
```

---

## Task 2: Урок 09.1 — JSX и компоненты

**Create:** `FrontendCourse/09-React-база/09.1-JSX-и-компоненты.md`

**Frontmatter:**
```yaml
---
модуль: 09-React-база
тема: JSX и компоненты
статус: to-read
roadmap: https://roadmap.sh/react
связано: "[[09.2-Props]]"
---
```

**Заголовок:** `# JSX и компоненты`

**`## Зачем это нужно`:** React построен на одной идее: UI — это функция от state. Компонент принимает данные, возвращает разметку. JSX — синтаксис, который позволяет писать HTML прямо внутри JS. Без понимания JSX и компонента как единицы переиспользования — никуда.

**`## Главное` (~320–400 слов):** подразделы `###`:
- **Функциональный компонент.** Обычная JS-функция, возвращающая JSX. Имя — с большой буквы (`Button`, не `button`), иначе React сочтёт за HTML-тег. Возвращает один корневой элемент (или Fragment `<>...</>` если несколько).
- **Что такое JSX.** Синтаксический сахар над `React.createElement`. Под капотом `<h1>Привет</h1>` превращается в `React.createElement("h1", null, "Привет")`. Компилирует — Vite/Babel.
- **HTML vs JSX — отличия.** `class` → `className`, `for` → `htmlFor`, все атрибуты в camelCase (`onClick`, `tabIndex`). Само-закрывающиеся теги обязательны: `<img />`, `<br />`. Числовые значения — через `{}`, строковые можно через `""`.
- **Выражения в JSX через `{}`.** Любое JS-выражение внутри фигурных скобок: `{user.name}`, `{count + 1}`, `{items.map(...)}`. НЕ выражения — `if`, `for` (используй тернарники и `.map`).
- **Множественные элементы и Fragment.** Функция возвращает ОДИН элемент. Если надо несколько — оберни в `<div>` или в Fragment `<>...</>` (не создаёт лишнего DOM-узла).
- **Импорты и экспорты.** Компонент обычно — один на файл. `export default function Button() {...}`. Импорт — `import Button from "./Button.jsx"`. По соглашению — файл называется как компонент.
- **Vite + React.** Стандартный старт: `npm create vite@latest my-app -- --template react`. Получаешь готовую структуру, hot reload, быстрый бандлер. В 99% случаев современного React-проекта — Vite.
- **Что запускается, когда React рендерит.** Первый рендер — компонент вызывается, возвращает дерево элементов, React кладёт в DOM. При изменении state — функция вызывается ЗАНОВО, React сравнивает старое дерево с новым (diff), обновляет только то, что изменилось.
- **Привычки.** Один компонент — одна ответственность. Файлы `.jsx` (или `.tsx` в TS). Именование: `PascalCase` для компонентов, `camelCase` для пропсов и функций.

**`## Пример кода`** — блок ```jsx```:
```jsx
// Button.jsx
function Button() {
  return <button className="btn">Нажми</button>;
}

export default Button;

// App.jsx
import Button from "./Button.jsx";

function App() {
  const user = { name: "Иван", age: 25 };
  const isAdmin = true;

  return (
    <>
      <h1 className="title">Привет, {user.name}!</h1>
      <p>Возраст: {user.age}</p>
      {isAdmin && <span>Ты админ</span>}
      <Button />
    </>
  );
}

export default App;

// main.jsx — точка входа (Vite генерирует автоматически)
import { createRoot } from "react-dom/client";
import App from "./App.jsx";

createRoot(document.getElementById("root")).render(<App />);
```

**`## Частые ошибки`** — 4 bullet-а:
- Писать компонент с маленькой буквы (`button`) — React решит, что это HTML-тег, и ничего не отрендерит.
- Возвращать несколько элементов без Fragment: `return <h1>...</h1><p>...</p>` — синтаксическая ошибка.
- Путать `class` и `className` — стили не применятся.
- Пихать `if` внутрь JSX: `<div>if (x) ...</div>` — не работает. Условия — через тернарник `{cond ? a : b}` или `&&`.

**`## Задания`:**
- [ ] Создай проект: `npm create vite@latest my-first-react -- --template react`, запусти `npm install && npm run dev`.
- [ ] Создай компонент `Card` с заголовком, текстом и кнопкой; используй его дважды в App.
- [ ] Вставь в разметку выражение `{new Date().toLocaleDateString()}` — увидишь сегодняшнюю дату.
- [ ] Попробуй Fragment: верни два элемента из компонента без обёртки `<div>`.

**`## Что почитать`:**
- [React docs — Your first component](https://react.dev/learn/your-first-component)
- [React docs — Writing markup with JSX](https://react.dev/learn/writing-markup-with-jsx)
- [React docs — JavaScript in JSX with curly braces](https://react.dev/learn/javascript-in-jsx-with-curly-braces)
- [Vite — React starter](https://vite.dev/guide/)

Блок — `jsx`.

---

## Task 3: Урок 09.2 — Props

**Create:** `FrontendCourse/09-React-база/09.2-Props.md`

**Frontmatter:**
```yaml
---
модуль: 09-React-база
тема: Props
статус: to-read
roadmap: https://roadmap.sh/react
связано: "[[09.1-JSX-и-компоненты]], [[09.3-State-и-useState]]"
---
```

**Заголовок:** `# Props`

**`## Зачем это нужно`:** Компонент без пропсов — статичная картинка. Пропсы — как аргументы функции: передаёшь данные сверху вниз, компонент рендерит то, что ты дал. Без понимания пропсов невозможна переиспользуемость.

**`## Главное` (~320–400 слов):** подразделы `###`:
- **Что такое props.** Первый аргумент функции-компонента. Объект с данными, переданными от родителя. `function Button(props) { return <button>{props.label}</button>; }` → `<Button label="Ок" />`.
- **Деструктуризация.** Обычно сразу разбирают: `function Button({ label, onClick }) {...}` — короче и яснее, какие props используешь.
- **Типы значений.** Любой JS: строки, числа, boolean, массивы, объекты, функции, JSX-элементы. Пропсы-не-строки через `{}`: `<User age={25} isAdmin={true} items={[1,2,3]} />`. Строки — можно в кавычках или в `{}`.
- **Значения по умолчанию.** Через деструктуризацию: `function Button({ label = "OK", size = "md" }) {...}`. Если проп не передан — возьмётся дефолт.
- **children — особый prop.** Всё, что между открывающим и закрывающим тегом: `<Card>содержимое</Card>`. Внутри компонента это `props.children`. Позволяет делать «контейнеры» (Card, Modal, Section).
- **Props — read-only.** НЕЛЬЗЯ менять props внутри компонента. `props.name = "Иван"` — антипаттерн. Если нужно менять — поднимай в state родителя (урок 09.7).
- **Передача обработчиков.** Функции тоже props. `<Button onClick={handleClick} />` — передаёшь функцию, компонент Button зовёт её на внутренний клик. Стандартный приём «Button ничего не знает, что произойдёт — решает родитель».
- **Спред пропсов.** `<input {...inputProps} />` — передать все свойства объекта как props. Удобно для обёрток над нативными элементами, но осторожно: прозрачность потерянная.
- **Именование.** Пропсы — `camelCase`. Булевы пропсы без значения — `<Button disabled />` (эквивалент `disabled={true}`).
- **Композиция через props.** Не наследование, а передача элементов: `<Layout header={<Header />} sidebar={<Nav />}>...</Layout>`. React предпочитает композицию классам.

**`## Пример кода`** — блок ```jsx```:
```jsx
function Card({ title, children, footer }) {
  return (
    <div className="card">
      <h3>{title}</h3>
      <div>{children}</div>
      {footer && <div className="footer">{footer}</div>}
    </div>
  );
}

function Button({ label = "OK", onClick, disabled = false }) {
  return (
    <button onClick={onClick} disabled={disabled}>
      {label}
    </button>
  );
}

function App() {
  const user = { name: "Иван", age: 25 };

  return (
    <>
      <Card title="Профиль" footer={<small>обновлено сегодня</small>}>
        <p>Имя: {user.name}</p>
        <p>Возраст: {user.age}</p>
        <Button
          label="Редактировать"
          onClick={() => console.log("edit")}
        />
      </Card>

      <Card title="Другая карточка">
        <p>Без футера.</p>
        <Button label="OK" disabled />
      </Card>
    </>
  );
}
```

**`## Частые ошибки`** — 4 bullet-а:
- Писать в props: `props.count++` — не работает и плохая идея. Props — read-only.
- Забывать `{}` для не-строк: `<Button disabled="true" />` — строка `"true"` вместо булева. Правильно: `<Button disabled={true} />` или `<Button disabled />`.
- Пропуск `onClick={handleClick}` vs `onClick={handleClick()}` — второе ВЫЗОВЕТ функцию при рендере, не при клике. Нужно передавать ссылку.
- Сотни props на один компонент — знак, что компонент перегружен. Разбей на части или используй children.

**`## Задания`:**
- [ ] Сделай компонент `Button` с props `label`, `variant` (`primary`/`secondary`), `onClick`. Используй его 3 раза с разными вариантами.
- [ ] Сделай `Card` с `children` — внутрь можно класть любой JSX.
- [ ] Добавь дефолтное значение prop и убедись, что оно применяется, когда prop не передан.
- [ ] Попробуй спред: `<input type="text" {...inputProps} />`. Создай объект с `value`, `onChange`, `placeholder`.

**`## Что почитать`:**
- [React docs — Passing Props to a Component](https://react.dev/learn/passing-props-to-a-component)
- [React docs — Passing JSX as children](https://react.dev/learn/passing-props-to-a-component#passing-jsx-as-children)
- [React docs — Props as snapshots](https://react.dev/learn/state-as-a-snapshot)
- [Thinking in React](https://react.dev/learn/thinking-in-react)

Блок — `jsx`.

---

## Task 4: Урок 09.3 — State и useState

**Create:** `FrontendCourse/09-React-база/09.3-State-и-useState.md`

**Frontmatter:**
```yaml
---
модуль: 09-React-база
тема: State и useState
статус: to-read
roadmap: https://roadmap.sh/react
связано: "[[09.2-Props]], [[09.4-События-и-формы]]"
---
```

**Заголовок:** `# State и useState`

**`## Зачем это нужно`:** Props приходят извне и статичны для компонента. State — переменная, которой компонент владеет и может менять. Без state UI не интерактивен. `useState` — первый и главный хук React, с него начинается реальная работа.

**`## Главное` (~340–420 слов):** подразделы `###`:
- **Синтаксис.** `const [count, setCount] = useState(0)`. Первое — текущее значение, второе — функция обновления, `0` — начальное. Деструктуризация массива — чисто соглашение, имена выбираешь ты.
- **Что делает `useState`.** Сохраняет значение между рендерами. Обычная `let count = 0` сбрасывалась бы при каждом вызове компонента; `useState` запоминает.
- **Обновление и ре-рендер.** Вызов `setCount(1)` → React помечает компонент как «нужен новый рендер» → функция-компонент вызывается снова, `count` уже `1`. Это **не** меняет существующую переменную — создаётся новый рендер с новыми значениями.
- **Асинхронность setState.** `setCount(count + 1); console.log(count);` — выведет СТАРОЕ значение. Обновление применится к следующему рендеру, не сразу.
- **Функциональная форма.** Если новое состояние зависит от старого — `setCount(prev => prev + 1)`. Гарантирует, что возьмёшь актуальное, даже если несколько `setCount` подряд.
- **Иммутабельность.** React сравнивает ссылки для определения «нужно ли перерендерить». Для объектов/массивов — создавай новый, не мутируй старый. НЕЛЬЗЯ: `arr.push(x); setArr(arr)`. МОЖНО: `setArr([...arr, x])`.
- **Правила обновления объекта.** `setUser({ ...user, name: "Иван" })` — копия + перезапись поля. `setItems(items.filter(i => i.id !== id))` — удаление. `setItems(items.map(i => i.id === id ? {...i, done: true} : i))` — правка одного элемента.
- **Несколько useState vs один объект.** Лучше несколько отдельных `useState` для независимых значений (counter и modal — разные вещи). Один объект — когда поля связаны логически (форма с 5 полями).
- **Правила хуков.** Хуки вызываются **только на верхнем уровне функции** и **только в React-компонентах** (или других хуках). Никаких `if`/`for`/`while` вокруг `useState`. Порядок вызовов должен быть стабильным между рендерами.
- **Ленивая инициализация.** Если начальное значение требует вычислений — `useState(() => expensiveCompute())`. Функция вызывается ОДИН раз, при первом рендере.

**`## Пример кода`** — блок ```jsx```:
```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Значение: {count}</p>
      <button onClick={() => setCount(count + 1)}>+1</button>
      <button onClick={() => setCount(prev => prev - 1)}>-1</button>
      <button onClick={() => setCount(0)}>Сбросить</button>
    </div>
  );
}

function UserForm() {
  const [user, setUser] = useState({ name: "", age: 0 });

  return (
    <>
      <input
        value={user.name}
        onChange={e => setUser({ ...user, name: e.target.value })}
      />
      <input
        type="number"
        value={user.age}
        onChange={e => setUser({ ...user, age: Number(e.target.value) })}
      />
      <pre>{JSON.stringify(user)}</pre>
    </>
  );
}

function Todos() {
  const [todos, setTodos] = useState([]);

  function addTodo(text) {
    setTodos(prev => [...prev, { id: Date.now(), text, done: false }]);
  }

  function toggle(id) {
    setTodos(prev =>
      prev.map(t => (t.id === id ? { ...t, done: !t.done } : t))
    );
  }

  function remove(id) {
    setTodos(prev => prev.filter(t => t.id !== id));
  }

  return null; // заглушка для краткости
}
```

**`## Частые ошибки`** — 4 bullet-а:
- Мутировать массив/объект: `items.push(x); setItems(items)` — React не увидит изменений. Всегда новая ссылка.
- Ожидать синхронности: `setCount(1); console.log(count)` — всё ещё старое значение. Новое — в следующем рендере.
- Вызывать хук внутри условия: `if (cond) useState(0)` — сломает порядок хуков, React упадёт.
- Использовать `setCount(count + 1)` несколько раз подряд — получишь +1, не +3. Для таких случаев — функциональная форма.

**`## Задания`:**
- [ ] Сделай `Counter` с `+`, `-`, `Reset`. Добавь кнопку `+10` через функциональную форму.
- [ ] Сделай `NameForm`: два поля (имя, фамилия) в одном объекте через `useState`. Выведи полное имя.
- [ ] Сделай список задач: `add`, `remove`, `toggleDone`. Только иммутабельно.
- [ ] Попробуй ленивую инициализацию: `useState(() => JSON.parse(localStorage.getItem("x") ?? "null"))`.

**`## Что почитать`:**
- [React docs — State: A component's memory](https://react.dev/learn/state-a-components-memory)
- [React docs — useState reference](https://react.dev/reference/react/useState)
- [React docs — Updating objects in state](https://react.dev/learn/updating-objects-in-state)
- [React docs — Updating arrays in state](https://react.dev/learn/updating-arrays-in-state)

Блок — `jsx`.

---

## Task 5: Урок 09.4 — События и формы

**Create:** `FrontendCourse/09-React-база/09.4-События-и-формы.md`

**Frontmatter:**
```yaml
---
модуль: 09-React-база
тема: События и формы
статус: to-read
roadmap: https://roadmap.sh/react
связано: "[[09.3-State-и-useState]], [[09.5-Списки-и-условный-рендеринг]]"
---
```

**Заголовок:** `# События и формы`

**`## Зачем это нужно`:** Пользователь взаимодействует через клики, ввод, submit. В React — всё через `onClick`, `onChange`, `onSubmit`. Отдельно — controlled inputs: React полностью владеет содержимым `<input>` через state. Это основа всех форм.

**`## Главное` (~340–420 слов):** подразделы `###`:
- **Синтаксис обработчика.** `<button onClick={handleClick}>`. Имя — в `camelCase` (`onClick`, `onChange`, `onSubmit`). Значение — функция (НЕ вызов): `onClick={handle}`, а не `onClick={handle()}`.
- **Inline-функции.** `onClick={() => setCount(c => c + 1)}` — коротко и понятно. Для сложной логики — вынести в функцию. `onClick={() => remove(id)}` — типовой паттерн с параметром.
- **Событие (event object).** В обработчик React передаёт `SyntheticEvent` — обёртку над нативным. `e.target.value` — что в input, `e.currentTarget` — элемент с обработчиком, `e.preventDefault()` — отменить дефолт (сабмит формы, переход по ссылке).
- **Controlled input.** `<input value={text} onChange={e => setText(e.target.value)} />`. Всё содержимое input управляется state. При каждом keystroke — ре-рендер. Плюс: всегда знаешь текущее значение, можно валидировать на лету.
- **Uncontrolled — кратко.** Альтернатива — `useRef` + `defaultValue`. Для сложных форм (file upload, редкое обновление) уместно. По умолчанию — controlled.
- **Form + onSubmit.** `<form onSubmit={handleSubmit}>`. Внутри `handleSubmit`: **первое** — `e.preventDefault()` (иначе браузер перезагрузит страницу). Затем — валидация и обработка.
- **Разные типы input.** `text`/`email`/`number`/`password` — через `value`. `checkbox`/`radio` — через `checked`. `select` — `value` на `<select>`, options — через `.map`. Textarea — `value` (в отличие от HTML, где контент между тегами).
- **Важность `name`.** Для логической группировки (особенно radio) и если сабмитишь форму браузерной `FormData`. Каждый input в форме — с уникальным `name`.
- **Один обработчик для многих полей.** `onChange={e => setForm({...form, [e.target.name]: e.target.value})}`. Через имена полей — универсальный обработчик. Не плоди 10 функций для 10 полей.
- **Клавиатура.** `onKeyDown`/`onKeyUp`: `e.key === "Enter"` — поймать Enter. Полезно в полях поиска с ручным сабмитом по Enter.
- **Фокус и blur.** `onFocus`/`onBlur`. Часто — для валидации: показываем ошибку только когда поле потеряло фокус, не при каждом keystroke.

**`## Пример кода`** — блок ```jsx```:
```jsx
import { useState } from "react";

function SearchBar() {
  const [q, setQ] = useState("");

  function handleSubmit(e) {
    e.preventDefault();
    console.log("искать:", q);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={q}
        onChange={e => setQ(e.target.value)}
        placeholder="Поиск..."
      />
      <button type="submit">Найти</button>
    </form>
  );
}

function SignupForm() {
  const [form, setForm] = useState({
    name: "",
    email: "",
    subscribe: false,
    plan: "free",
  });

  function handleChange(e) {
    const { name, value, type, checked } = e.target;
    setForm(prev => ({
      ...prev,
      [name]: type === "checkbox" ? checked : value,
    }));
  }

  function handleSubmit(e) {
    e.preventDefault();
    if (!form.email.includes("@")) return;
    console.log("регистрация:", form);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input name="name" value={form.name} onChange={handleChange} />
      <input name="email" value={form.email} onChange={handleChange} />
      <label>
        <input
          name="subscribe"
          type="checkbox"
          checked={form.subscribe}
          onChange={handleChange}
        />
        Подписка
      </label>
      <select name="plan" value={form.plan} onChange={handleChange}>
        <option value="free">Free</option>
        <option value="pro">Pro</option>
      </select>
      <button type="submit">OK</button>
    </form>
  );
}
```

**`## Частые ошибки`** — 4 bullet-а:
- Забыть `e.preventDefault()` в `onSubmit` — страница перезагружается, state теряется.
- `onClick={handleClick()}` — функция выполняется при рендере, не при клике. Правильно: `onClick={handleClick}` или `onClick={() => handleClick(arg)}`.
- Input без `onChange`, только с `value` — поле становится read-only (warning в консоли). Нужен либо `onChange`, либо `readOnly`.
- Controlled + `defaultValue` одновременно — React ругается. Выбирай один подход.

**`## Задания`:**
- [ ] Сделай счётчик с полем ввода: вводишь число → на кнопке `+` прибавляется это число.
- [ ] Форма регистрации с 4 полями (name, email, password, subscribe checkbox). Один `handleChange` через `e.target.name`.
- [ ] Добавь `onKeyDown` на поле поиска — сабмит по Enter.
- [ ] Валидация на blur: email без `@` → подсветить поле красным (через className).

**`## Что почитать`:**
- [React docs — Responding to Events](https://react.dev/learn/responding-to-events)
- [React docs — Reacting to input with state](https://react.dev/learn/reacting-to-input-with-state)
- [React docs — Sharing State Between Components](https://react.dev/learn/sharing-state-between-components)
- [React docs — SyntheticEvent](https://react.dev/reference/react-dom/components/common#react-event-object)

Блок — `jsx`.

---

## Task 6: Урок 09.5 — Списки и условный рендеринг

**Create:** `FrontendCourse/09-React-база/09.5-Списки-и-условный-рендеринг.md`

**Frontmatter:**
```yaml
---
модуль: 09-React-база
тема: Списки и условный рендеринг
статус: to-read
roadmap: https://roadmap.sh/react
связано: "[[09.4-События-и-формы]], [[09.6-useEffect]]"
---
```

**Заголовок:** `# Списки и условный рендеринг`

**`## Зачем это нужно`:** В реальном UI почти всегда есть два паттерна: «отрендерь массив» (список постов, задач, товаров) и «покажи это, если…» (loader, пустое состояние, ошибка). Оба делаются JS-выражениями внутри JSX — без специальных директив, как во Vue или Angular.

**`## Главное` (~320–400 слов):** подразделы `###`:
- **Списки через `.map`.** `items.map(item => <li>{item.name}</li>)` внутри JSX. Возвращается массив JSX-элементов, React рендерит каждый. Никаких `for` — только `.map`.
- **Атрибут `key`.** Обязателен для каждого элемента списка. `items.map(item => <li key={item.id}>...</li>)`. React использует key, чтобы эффективно обновлять DOM при изменении массива (добавление/удаление/перестановка).
- **Как выбирать key.** Уникальный, стабильный: `id` из базы, `Date.now()` при создании, `crypto.randomUUID()`. НЕ используй `index` массива, если список меняется (сортировка, удаление) — приведёт к багам со state внутренних компонентов.
- **Пустой список.** Если `items.length === 0` — покажи «Пусто». Условный рендеринг внутри компонента: `{items.length === 0 ? <Empty /> : items.map(...)}`.
- **Условный рендеринг: `&&`.** `{isLoading && <Spinner />}`. Если `isLoading` истина — отрендерит `<Spinner />`, иначе ничего.
- **Подводный камень `&&` с числом.** `{items.length && <List />}` — если `items.length === 0`, то `0 && <List />` = `0`, и React отрендерит... `0`! Правильно: `items.length > 0 && <List />` или тернарник.
- **Тернарник `? :`.** `{isLoggedIn ? <Profile /> : <LoginForm />}` — две ветки. Удобнее, когда нужны два разных варианта.
- **Ранний возврат.** Для большого ветвления — лучше `if` перед `return`: `if (!user) return <LoginForm />`. Разгружает JSX и понятнее.
- **Фильтр + map.** `items.filter(i => !i.done).map(i => <Item ... />)` — цепочки. Работают так же, как в vanilla.
- **Стили в условии.** `<div className={isActive ? "tab active" : "tab"}>`. Или через `clsx`/`classnames` для нескольких классов. Не делай всё через inline `style={{...}}`.
- **Вынесение в переменную.** Если условная JSX громоздкая — `const content = isLoading ? <Spinner /> : <List .../>`, потом `return <>{content}</>`. Читается лучше.

**`## Пример кода`** — блок ```jsx```:
```jsx
function TodoList({ todos, onToggle, onDelete }) {
  if (todos.length === 0) {
    return <p className="empty">Задач пока нет 🌱</p>;
  }

  return (
    <ul>
      {todos.map(todo => (
        <li key={todo.id} className={todo.done ? "done" : ""}>
          <input
            type="checkbox"
            checked={todo.done}
            onChange={() => onToggle(todo.id)}
          />
          <span>{todo.text}</span>
          <button onClick={() => onDelete(todo.id)}>✕</button>
        </li>
      ))}
    </ul>
  );
}

function App({ user, isLoading, error, todos }) {
  if (isLoading) return <Spinner />;
  if (error) return <ErrorBox message={error} />;
  if (!user) return <LoginForm />;

  const activeTodos = todos.filter(t => !t.done);
  const stats = `${activeTodos.length} из ${todos.length} в работе`;

  return (
    <div>
      <header>
        Привет, {user.name}!
        {activeTodos.length > 0 && <span> У тебя {activeTodos.length} дел.</span>}
      </header>
      <TodoList
        todos={todos}
        onToggle={/* ... */}
        onDelete={/* ... */}
      />
      <footer>{stats}</footer>
    </div>
  );
}
```

**`## Частые ошибки`** — 4 bullet-а:
- `key={index}` в динамическом списке. При сортировке/удалении React путает состояние внутренних компонентов (фокус, input-значения сбиваются).
- `{items.length && <List />}` вместо `items.length > 0 && <List />` → на пустом списке увидишь `0` в UI.
- Не обрабатывать пустое состояние — пользователь видит просто пустоту, не понимая, что всё в порядке.
- Логика в JSX через `map` + `if` + `else if` — разбей на функцию/переменную: JSX должен быть читаемым.

**`## Задания`:**
- [ ] Список из массива строк через `.map` с `key`.
- [ ] Три состояния компонента: `isLoading`, `error`, `data` — через ранние возвраты и тернарники.
- [ ] Фильтр: переключение «все / активные / завершённые» через state + `filter`.
- [ ] Попробуй `key={index}`, потом удали элемент в середине, посмотри, что ломается.

**`## Что почитать`:**
- [React docs — Rendering Lists](https://react.dev/learn/rendering-lists)
- [React docs — Conditional Rendering](https://react.dev/learn/conditional-rendering)
- [React docs — Keeping components pure](https://react.dev/learn/keeping-components-pure)
- [React docs — Understanding Your UI as a Tree](https://react.dev/learn/understanding-your-ui-as-a-tree)

Блок — `jsx`.

---

## Task 7: Урок 09.6 — useEffect

**Create:** `FrontendCourse/09-React-база/09.6-useEffect.md`

**Frontmatter:**
```yaml
---
модуль: 09-React-база
тема: useEffect
статус: to-read
roadmap: https://roadmap.sh/react
связано: "[[09.5-Списки-и-условный-рендеринг]], [[09.7-Lifting-state-и-композиция]]"
---
```

**Заголовок:** `# useEffect`

**`## Зачем это нужно`:** `useState` хранит данные, но сам компонент — чистая функция. Работа с «внешним миром» (сеть, DOM, таймеры, localStorage) называется сайд-эффектом и делается в `useEffect`. Без него невозможен fetch-запрос после маунта или подписка на window.

**`## Главное` (~340–420 слов):** подразделы `###`:
- **Синтаксис.** `useEffect(() => { ... }, [deps])`. Первый аргумент — функция-эффект, второй — массив зависимостей. Эффект вызывается ПОСЛЕ рендера.
- **Три варианта массива зависимостей.**
    - `[]` — эффект один раз, после первого рендера.
    - `[a, b]` — каждый раз, когда `a` или `b` изменились.
    - Без массива — после каждого рендера (почти всегда ошибка, бесконечный цикл).
- **Cleanup.** Эффект может вернуть функцию — она вызовется перед следующим эффектом или при размонтировании. Для отмены: `clearInterval`, `removeEventListener`, `AbortController`.
- **Типичный паттерн: fetch.** `useEffect(() => { fetch("...").then(r => r.json()).then(setData); }, [])`. Загрузка при первом рендере. С обработкой отмены — `AbortController` в cleanup.
- **Зависимости — что туда класть.** Всё, что используется внутри эффекта и может измениться: props, state, функции. Линтер `react-hooks/exhaustive-deps` подскажет.
- **StrictMode и двойной вызов.** В dev-режиме React 18+ вызывает эффекты ДВАЖДЫ, чтобы отловить плохой cleanup. Это фича, не баг. В проде вызовется один раз.
- **Чего НЕ делать в useEffect.** Не клади туда вычисления, которые можно сделать в рендере напрямую: `const doubled = count * 2` — не эффект. Не дублируй state. Не используй `useEffect` ради синхронизации, если `useMemo` или просто вычисление подойдёт.
- **Синхронизация, а не "lifecycle".** Ментальная модель: «эффект синхронизирует компонент с чем-то внешним». Не «что-то делать при маунте», а «держать внешнее в актуальном состоянии». Такое мышление предотвращает лишние эффекты.
- **Подписки и таймеры.** `useEffect(() => { const id = setInterval(tick, 1000); return () => clearInterval(id); }, [])`. Таймер живёт пока живёт компонент.
- **localStorage.** Чтение — в инициализации `useState(() => JSON.parse(localStorage.getItem("x") ?? "null"))`. Запись — в `useEffect(() => { localStorage.setItem("x", JSON.stringify(x)); }, [x])`.
- **Event listeners на window/document.** Ставить в эффекте, снимать в cleanup. Иначе — утечки при размонтировании.

**`## Пример кода`** — блок ```jsx```:
```jsx
import { useState, useEffect } from "react";

// 1. Fetch при маунте с cleanup через AbortController
function UserProfile({ userId }) {
  const [user, setUser] = useState(null);

  useEffect(() => {
    const ctrl = new AbortController();

    fetch(`/api/users/${userId}`, { signal: ctrl.signal })
      .then(r => r.json())
      .then(setUser)
      .catch(err => {
        if (err.name !== "AbortError") console.error(err);
      });

    return () => ctrl.abort();
  }, [userId]);

  if (!user) return <p>Загрузка…</p>;
  return <h2>{user.name}</h2>;
}

// 2. Таймер
function Clock() {
  const [time, setTime] = useState(new Date());

  useEffect(() => {
    const id = setInterval(() => setTime(new Date()), 1000);
    return () => clearInterval(id);
  }, []);

  return <time>{time.toLocaleTimeString()}</time>;
}

// 3. Синхронизация с localStorage
function useLocalStorage(key, initial) {
  const [val, setVal] = useState(() => {
    const raw = localStorage.getItem(key);
    return raw ? JSON.parse(raw) : initial;
  });

  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(val));
  }, [key, val]);

  return [val, setVal];
}

// 4. Listener на window
function useWindowSize() {
  const [size, setSize] = useState({ w: window.innerWidth, h: window.innerHeight });

  useEffect(() => {
    const onResize = () => setSize({ w: window.innerWidth, h: window.innerHeight });
    window.addEventListener("resize", onResize);
    return () => window.removeEventListener("resize", onResize);
  }, []);

  return size;
}
```

**`## Частые ошибки`** — 4 bullet-а:
- Забыть массив зависимостей — эффект срабатывает на каждый рендер, часто бесконечно.
- Не сделать cleanup для таймеров/listener-ов/fetch — утечки памяти, старые запросы пишут в размонтированный компонент.
- Класть `setState` в эффект без условий — бесконечный цикл (setState → rerender → effect → setState).
- Использовать `useEffect` для вычислений: «мне надо `doubled` из `count`» — просто `const doubled = count * 2`, не эффект.

**`## Задания`:**
- [ ] Компонент `Clock`, показывает текущее время, обновляется каждую секунду.
- [ ] Fetch пользователя по id из props; при смене `userId` — новый запрос, со своим `AbortController`.
- [ ] Свой хук `useLocalStorage(key, initial)` — синхронизирует state с localStorage.
- [ ] Показывай ширину окна в реальном времени (resize listener).

**`## Что почитать`:**
- [React docs — Synchronizing with Effects](https://react.dev/learn/synchronizing-with-effects)
- [React docs — You Might Not Need an Effect](https://react.dev/learn/you-might-not-need-an-effect)
- [React docs — useEffect reference](https://react.dev/reference/react/useEffect)
- [React docs — Lifecycle of Reactive Effects](https://react.dev/learn/lifecycle-of-reactive-effects)

Блок — `jsx`.

---

## Task 8: Урок 09.7 — Lifting state и композиция

**Create:** `FrontendCourse/09-React-база/09.7-Lifting-state-и-композиция.md`

**Frontmatter:**
```yaml
---
модуль: 09-React-база
тема: Lifting state up и композиция
статус: to-read
roadmap: https://roadmap.sh/react
связано: "[[09.6-useEffect]]"
---
```

**Заголовок:** `# Lifting state up и композиция`

**`## Зачем это нужно`:** Два компонента должны «видеть» одно значение — как быть? Ответ: поднять state в ближайшего общего родителя и спустить данные через props. Плюс композиция — через `children` и компоненты как props. Это две главные архитектурные техники React.

**`## Главное` (~340–420 слов):** подразделы `###`:
- **Поток данных сверху вниз.** React — one-way data flow. Данные текут от родителя к детям через props. Дети «сообщают» наверх через callback-props (`onClick`, `onChange`), но сами не меняют данные родителя.
- **Когда поднимать state.** Два компонента зависят от одного и того же — `state` должен жить в их общем родителе. Например, поле поиска и список товаров оба зависят от `query` — значит, `query` лежит в родителе.
- **Паттерн.** Родитель владеет state + передаёт вниз: (а) значение через `value`/`selected`, (б) обработчик через `onChange`. Ребёнок не хранит ничего — только рендерит данное и зовёт переданную функцию.
- **Props drilling — и как с ним жить.** Если state нужно протащить через 4-5 уровней — это признак проблемы. Решения: композиция через `children`, Context (не в этом модуле — см. модуль 10), переносить компоненты.
- **Композиция: children.** Вместо того чтобы передавать всё через props, передавай готовый JSX. `<Card>{children}</Card>` — внутри можно положить что угодно. Компонент-контейнер не знает, что внутри.
- **Композиция: slot pattern.** Несколько «дырок»: `<Layout header={...} sidebar={...}>content</Layout>`. Каждая дырка — отдельный prop с JSX.
- **Именование callback-props.** Соглашение — `on<Event>`: `onSelect`, `onClose`, `onChange`. Внутри компонента — часто `handle<Event>`: `handleClick`, `handleSubmit`. Два разных имени для двух ролей.
- **Контролируемые и неконтролируемые компоненты.** Контролируемый — state живёт в родителе, через props. Неконтролируемый — state внутри, только при выходе сообщает наружу (`onSubmit`). Выбор зависит от того, нужен ли родителю доступ к промежуточным значениям.
- **Single source of truth.** Одно значение — в одном месте. Если ты хранишь его в state И синхронизируешь с props — рассинхронизируется. Или state, или производное от props — не оба.
- **Композиция vs наследование.** В React почти не используется наследование компонентов. Всё — композиция: обёртывание, вложение, передача JSX. Это сильно упрощает структуру.
- **Архитектурные слои.** UI-примитивы (Button, Input) — переиспользуемые, без бизнес-логики. Блоки (TodoList, UserCard) — с логикой, но без глобального state. Страницы (App, Dashboard) — оркестрация, state, данные.

**`## Пример кода`** — блок ```jsx```:
```jsx
import { useState } from "react";

// Lifted state: поле поиска + список фильтруются одним query
function SearchList({ items }) {
  const [query, setQuery] = useState("");

  const filtered = items.filter(i =>
    i.toLowerCase().includes(query.toLowerCase())
  );

  return (
    <>
      <SearchInput value={query} onChange={setQuery} />
      <List items={filtered} />
    </>
  );
}

function SearchInput({ value, onChange }) {
  return (
    <input
      value={value}
      onChange={e => onChange(e.target.value)}
      placeholder="Поиск..."
    />
  );
}

function List({ items }) {
  if (items.length === 0) return <p>Ничего не найдено</p>;
  return (
    <ul>
      {items.map(i => <li key={i}>{i}</li>)}
    </ul>
  );
}

// Композиция через children и slot-props
function Layout({ header, sidebar, children }) {
  return (
    <div className="layout">
      <header>{header}</header>
      <aside>{sidebar}</aside>
      <main>{children}</main>
    </div>
  );
}

function App() {
  return (
    <Layout
      header={<h1>Моё приложение</h1>}
      sidebar={<Nav />}
    >
      <SearchList items={["Яблоко", "Груша", "Слива"]} />
    </Layout>
  );
}

function Nav() {
  return <ul><li>Главная</li><li>О нас</li></ul>;
}
```

**`## Частые ошибки`** — 4 bullet-а:
- Хранить одно значение в state И в props одновременно → рассинхрон. Выбирай один источник правды.
- Держать state глубоко, потом тянуть его через 5 уровней props. Подними, либо используй Context (в M10).
- Наследование компонентов через HOC/inheritance — устарело. Сегодня — children и hooks.
- Писать callback-props без префикса `on`: `click`, `select`. Соглашение `onClick`, `onSelect` — важно для читаемости.

**`## Задания`:**
- [ ] Два поля ввода и компонент, показывающий сумму — state поднять в общего родителя.
- [ ] Компонент `Tabs` с props `tabs` (массив) и children (контент активной вкладки) — через lifting state.
- [ ] `Layout` с `header`/`footer` как JSX-props и `children` для main. Собери из него 2 разных страницы.
- [ ] Отрефактори вчерашний проект: выдели хотя бы один UI-примитив (Button/Input/Card) без бизнес-логики.

**`## Что почитать`:**
- [React docs — Sharing State Between Components](https://react.dev/learn/sharing-state-between-components)
- [React docs — Passing Data Deeply with Context](https://react.dev/learn/passing-data-deeply-with-context)
- [React docs — Choosing the State Structure](https://react.dev/learn/choosing-the-state-structure)
- [React docs — Extracting State Logic into a Reducer](https://react.dev/learn/extracting-state-logic-into-a-reducer)

Блок — `jsx`.

---

## Task 9: Мини-проект M09 — Todo на React

**Create:** `FrontendCourse/Проекты/Мини/M09-Todo-на-React.md`

**Exact content:**

```markdown
---
тип: мини-проект
модуль: 09-React-база
статус: not-started
---

# M09 — Todo на React

Мини-проект после модуля 09. Переписываешь свой M05 ToDo-лист с vanilla JS на React + Vite. Смысл — почувствовать разницу: вместо ручного `appendChild` и `querySelector` — декларативный UI, состояние в `useState`, автоматический ре-рендер.

## Задача

Функциональная копия твоего M05 ToDo, но:
- React + Vite (без TypeScript — он в модуле 11).
- Без прямой работы с DOM (`document.*`, `querySelector`, `innerHTML` запрещены).
- Состояние — только через `useState`.
- Компоненты разделены.

## Требования

### Функциональность
1. **Добавление задачи** — форма с `<input>` и кнопкой «Add» (или submit по Enter). Пустой ввод — не добавляется.
2. **Toggle done** — клик на задаче (или checkbox) — переключает `done`.
3. **Удаление** — кнопка ✕ у каждой задачи.
4. **Фильтр** — три вкладки: All / Active / Completed.
5. **Счётчик** — «X of Y active» в подвале.
6. **Пустое состояние** — когда задач нет в текущем фильтре: «Задач нет».
7. **Очистить завершённые** — кнопка «Clear completed».
8. **Персист в localStorage** — через `useEffect`, при F5 всё остаётся.
9. **Деплой** — Vercel / Netlify, прод-URL.

### Технические правила
- `npm create vite@latest ... -- --template react`, без TypeScript.
- Минимум 4 компонента: `App`, `TodoForm`, `TodoList`, `TodoItem` (можно добавить `FilterBar`, `Footer`).
- Состояние живёт в `App`, передаётся вниз через props. Обработчики тоже через props.
- `useState` для `todos` и `filter`.
- `useEffect` для синхронизации с localStorage (чтение при инициализации через lazy init, запись при изменении).
- `key` — уникальный id задачи (не index!). Генерируй через `crypto.randomUUID()` или `Date.now()`.
- Нет `document.querySelector`, нет `innerHTML`, нет `appendChild` — всё через JSX.
- `.gitignore` (node_modules, dist, .env).

## Чего НЕ должно быть

- Прямой работы с DOM (кроме единственного места — `createRoot` в `main.jsx`).
- `class` вместо `className`.
- `key={index}` в динамическом списке.
- Мутаций массива (`push`, `splice`) — только иммутабельные `[...arr, x]`, `filter`, `map`.
- Fetch и API — это следующий этап (модуль 10).
- Сторонних библиотек UI (MUI, Chakra) — пиши свои компоненты.
- TypeScript — будет в модуле 11.

## Этапы

1. Vite + React проект: `npm create vite@latest todo-react -- --template react`.
2. Продумать разделение: `App` → `TodoForm` + `FilterBar` + `TodoList` (`TodoList` → `TodoItem`).
3. В `App` — `useState` для `todos` и `filter`, обработчики `addTodo`/`toggleTodo`/`deleteTodo`/`clearCompleted`.
4. `TodoForm` — controlled input + onSubmit. Передаёт текст наверх через `onAdd`.
5. `TodoList` — получает `todos` и callback-props, `.map` → `TodoItem`.
6. `TodoItem` — получает todo и `onToggle`/`onDelete`.
7. `FilterBar` — получает `filter` и `onFilterChange`.
8. `useEffect` для localStorage — lazy init в `useState`, сохранение в effect.
9. Стили — любые (CSS-модули, чистый CSS, CSS-in-JS).
10. Деплой → Vercel.

## Сдача

1. Публичный GitHub-репозиторий.
2. Прод-URL.
3. README: как запускать, ссылка на деплой, 1-2 скриншота, краткое «что сделал сложного».
4. На созвоне — смотрим структуру компонентов и data flow.

## Критерии приёмки ревью

- [ ] Все 8 функциональных пунктов работают.
- [ ] Минимум 4 компонента, state живёт в `App`.
- [ ] Нет `document.*`, `innerHTML`, `querySelector`.
- [ ] `key={todo.id}`, не `index`.
- [ ] Обновления state — иммутабельные (map/filter/spread, не push/splice).
- [ ] `useEffect` для localStorage работает, F5 восстанавливает список.
- [ ] `TodoForm` — controlled input с onSubmit + `e.preventDefault()`.
- [ ] Фильтр All/Active/Completed переключается, пустое состояние показывается.
- [ ] Прод-URL работает по HTTPS.
- [ ] В Network нет 404-ок на ассеты.

## Что дальше
Дальше — **модуль 10 React-экосистема**: роутинг (React Router), Context, useReducer, TanStack Query для API. Откроется дорога к настоящим SPA.
```

---

## Task 10: Заполнить MOC-React

**Modify:** `FrontendCourse/MOC/MOC-React.md`

Заменить содержимое файла полностью, добавив раздел «База (модуль 09)» со всеми 7 уроками и ссылку на M09 в раздел «Практика». Сохранить структуру с разделами под модули 10 и 13 (как placeholder).

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

## Экосистема (модуль 10 — скоро)
- _React Router, Context, useReducer, useMemo/useCallback, TanStack Query / SWR, UI-библиотеки_

## Next.js (модуль 13 — скоро)
- _App Router, Server Components, Server Actions, routing, layouts_

## Практика
- [[M09-Todo-на-React]] — первая переработка vanilla-проекта на React.
```

---

## Task 11: Обновить 00-Start-Here.md

**Modify:** `FrontendCourse/00-Start-Here.md`

- [ ] **Step 11.1:** Убрать «_(скоро)_» у модуля 09:
  `- [[09-React-база/00-Обзор-модуля|Модуль 09 — React база]] _(скоро)_` → `- [[09-React-база/00-Обзор-модуля|Модуль 09 — React база]]`.

---

## Task 12: Верификация

- [ ] **Step 12.1:** `find FrontendCourse/09-React-база -type f -name "*.md" | sort` → 8 файлов (обзор + 7 уроков).
- [ ] **Step 12.2:** `M09-Todo-на-React.md` существует в `Проекты/Мини/`.
- [ ] **Step 12.3:** `MOC-React.md` содержит 7 ссылок на уроки 09.1–09.7 и ссылку на `M09-Todo-на-React`.
- [ ] **Step 12.4:** В `00-Start-Here.md` у модуля 09 нет «_(скоро)_».
- [ ] **Step 12.5:** Отчитаться: модуль 09 готов.

---

## Self-Review

**1. Spec coverage:**
- JSX + компоненты, props, state, events+формы, списки+условия, useEffect, lifting+композиция → Tasks 2–8. ✓
- Мини-проект Todo на React → Task 9. ✓
- MOC-React → Task 10. ✓
- Start-Here → Task 11. ✓

**2. Placeholder scan:** TBD/TODO отсутствуют. «_(скоро)_» в MOC-React у модулей 10 и 13 — осознанный маркер. ✓

**3. Type consistency:** Имена уроков/мини-проекта согласованы. ✓

---

## Out of Scope

- `useReducer`, `useContext`, `useMemo`, `useCallback`, `useRef` — модуль 10.
- React Router — модуль 10.
- TypeScript с React — модуль 11.
- Тестирование React (Vitest, Testing Library) — модуль 12.
- Server Components, Next.js — модуль 13.
- Производительность React (React DevTools Profiler, React.memo) — модуль 12/14.
