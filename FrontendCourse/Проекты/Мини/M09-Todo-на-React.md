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
