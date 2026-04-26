# Frontend Course — Module 06 (JS продвинутый) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: superpowers:subagent-driven-development. Контентный проект.

**Goal:** Наполнить модуль 06 «JS продвинутый»: обзор + 5 уроков + мини-проект (fetch-приложение на выбор: погода или GitHub) + обновить MOC-JS + снять пометку «скоро» в Start-Here.

**Architecture:** Структура модулей 01–05. Шаблон урока (6 секций), средняя глубина. Современный JS: `async/await`, `fetch`, `Promise`, классы, `try/catch`.

**Базовые пути:**
- Vault: `/Users/luckyme/Desktop/maloyfront/FrontendCourse/`
- Модуль: `FrontendCourse/06-JS-продвинутый/`

---

## File Structure

```
FrontendCourse/
├── 00-Start-Here.md                              (правка)
├── 06-JS-продвинутый/
│   ├── 00-Обзор-модуля.md                        (новый)
│   ├── 06.1-Замыкания-и-this.md                  (новый)
│   ├── 06.2-Прототипы-и-классы.md                (новый)
│   ├── 06.3-Промисы-и-async-await.md             (новый)
│   ├── 06.4-Fetch-и-работа-с-API.md              (новый)
│   └── 06.5-Event-loop-и-обработка-ошибок.md     (новый)
├── Проекты/Мини/
│   └── M06-Fetch-приложение.md                   (новый)
└── MOC/
    └── MOC-JS.md                                 (правка — заполнить «Продвинутое» и практику)
```

Итого: **7 новых файлов**, 2 правки.

---

## Task 1: Обзор модуля 06

**Create:** `FrontendCourse/06-JS-продвинутый/00-Обзор-модуля.md`

**Exact content:**

```markdown
---
тип: обзор-модуля
модуль: 06-JS-продвинутый
статус: not-started
roadmap: https://roadmap.sh/frontend#javascript
---

# Модуль 06 — JS продвинутый

**roadmap.sh:** [раздел JavaScript во frontend-roadmap](https://roadmap.sh/frontend#javascript)

В модуле 05 ты научился писать логику, которая решает задачу на странице. Теперь нужно понять, как JS устроен «под капотом» — чтобы не ломаться на `this`, не бояться асинхронности и уметь работать с API. Это мост между «сделал ToDo на localStorage» и «сделал приложение, которое ходит в сервер».

## Что изучаем
- Замыкания поглубже и `this` (правила вызова, стрелочные vs обычные).
- Прототипы и классы (ES2015+): наследование, методы, `instanceof`.
- Промисы: состояния, `.then`/`.catch`/`.finally`, `async`/`await`.
- `fetch` и работа с REST API: GET/POST, заголовки, JSON, CORS.
- Event loop, микро- и макрозадачи, обработка ошибок (`try/catch`, rejection handlers).

## Уроки
- [ ] [[06.1-Замыкания-и-this]]
- [ ] [[06.2-Прототипы-и-классы]]
- [ ] [[06.3-Промисы-и-async-await]]
- [ ] [[06.4-Fetch-и-работа-с-API]]
- [ ] [[06.5-Event-loop-и-обработка-ошибок]]

## Итоговая практика
- [ ] Мини-проект: [[M06-Fetch-приложение]] — приложение погоды или поиск GitHub-профилей (на выбор) через `fetch` + `async/await` + обработка ошибок.

## Связанные MOC
- [[MOC-JS]] — карта по JavaScript (теперь заполнена полностью).

## Чек-лист завершения
- [ ] все 5 уроков прочитаны
- [ ] мини-проект работает: запрос, loading/error состояния, рабочий деплой
- [ ] DevTools → Network просмотрен на реальных запросах, понятны коды статусов
- [ ] узлы JavaScript в roadmap.sh закрыты
```

---

## Task 2: Урок 06.1 — Замыкания и this

**Create:** `FrontendCourse/06-JS-продвинутый/06.1-Замыкания-и-this.md`

**Frontmatter:**
```yaml
---
модуль: 06-JS-продвинутый
тема: Замыкания и this
статус: to-read
roadmap: https://roadmap.sh/frontend#javascript
связано: "[[05.3-Функции]], [[06.2-Прототипы-и-классы]]"
---
```

**Заголовок:** `# Замыкания и this`

**`## Зачем это нужно`:** Два самых «магических» места в JS, на которых спотыкаются. Замыкания — основа модулей, приватных переменных, стейта в React-хуках. `this` — то, почему в одном коде метод работает, а скопированный в коллбек «теряется». Без них не понять ни одну нормальную библиотеку.

**`## Главное` (~340–420 слов):** подразделы `### ...`:
- **Что такое замыкание.** Функция «помнит» переменные того scope-а, где она была создана, даже когда этот scope уже отработал. Классика: функция возвращает функцию, внутренняя помнит переменную внешней.
- **Зачем.** Приватные переменные (инкапсуляция), фабрики функций, счётчики, мемоизация, currying. В React — основа `useState` и `useEffect`.
- **Частый подвох с циклом.** Раньше на `var` в `for` все коллбеки видели одно и то же значение. С `let` и `const` — каждая итерация создаёт свой scope, замыкание ловит актуальное значение. Это один из главных аргументов против `var`.
- **`this` — контекст вызова.** `this` не определяется местом объявления функции; он определяется тем, **как** функция вызвана.
- **Четыре правила `this` в обычной функции.**
    - Как метод объекта: `obj.method()` → `this === obj`.
    - Просто вызов: `fn()` → `this === undefined` (в strict mode) или `globalThis`.
    - Через `call`/`apply`/`bind` → `this` задан явно: `fn.call(ctx)`.
    - В конструкторе `new Fn()` → `this === новый объект`.
- **Стрелочные функции и `this`.** У стрелочной функции `this` **не свой** — он наследуется от внешнего scope. Идеально для коллбеков внутри методов, где `this` должен остаться тем же. Поэтому в классах `onClick = () => this.doStuff()` «просто работает», а `onClick() { ... }` — отвалится без `bind`.
- **`bind`.** Возвращает новую функцию с «зашитым» `this`. Полезно, когда метод передают как коллбек: `button.addEventListener("click", obj.handle.bind(obj))`.
- **Главная практическая подсказка.** В 2026 году в 90% случаев ответ — «используй стрелочную функцию». Обычные `function` нужны для конструкторов, методов классов и редких случаев, когда `this` должен меняться динамически.

**`## Пример кода`** — блок ```js```:
```js
// замыкание: приватный счётчик
function createCounter() {
  let count = 0;
  return {
    inc: () => ++count,
    get: () => count,
  };
}
const counter = createCounter();
counter.inc(); counter.inc();
console.log(counter.get()); // 2
// count снаружи недоступен — инкапсуляция

// this как метод объекта
const user = {
  name: "Иван",
  greet() {
    return `Привет, я ${this.name}`;
  },
};
console.log(user.greet()); // "Привет, я Иван"

// потеря this в коллбеке
const greet = user.greet;
// greet(); // this === undefined, ошибка

// фикс через bind
const bound = user.greet.bind(user);
console.log(bound()); // "Привет, я Иван"

// стрелочная функция наследует this
const obj = {
  name: "Пётр",
  delayed() {
    setTimeout(() => console.log(this.name), 10);
    // стрелка — this === obj → "Пётр"
  },
};
obj.delayed();

// цикл с let — каждая итерация своё замыкание
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0); // 0, 1, 2
}
```

**`## Частые ошибки`** — 4 bullet-а:
- Передавать метод как коллбек «в голом виде» (`btn.addEventListener("click", user.greet)`) → `this` теряется. Нужен `bind` или стрелочная обёртка.
- Использовать стрелочную там, где `this` должен меняться — например, как метод объекта. Стрелка возьмёт `this` из внешнего scope.
- Думать, что `var` в цикле «просто работает» — в старых туториалах с `setTimeout` вываливают одно и то же значение. Используй `let`.
- Перегружать замыкания состоянием, когда просится класс или `useState`. Замыкания — инструмент, а не архитектура.

**`## Задания`:**
- [ ] Напиши `createCounter()`, возвращающую объект с `inc`, `dec`, `get`.
- [ ] Напиши `once(fn)` — возвращает функцию, которая вызовет `fn` только при первом вызове, дальше возвращает прошлый результат. Это замыкание + флаг.
- [ ] Метод объекта: вызови его напрямую и через `setTimeout(obj.method, 0)` — сравни поведение `this`. Почини `bind`-ом.
- [ ] Перепиши тот же `setTimeout` через стрелочную функцию — убедись, что `this` сохраняется.

**`## Что почитать`:**
- [MDN — Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
- [MDN — `this`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- [learn.javascript.ru — Замыкания](https://learn.javascript.ru/closure)
- [learn.javascript.ru — Привязка контекста](https://learn.javascript.ru/bind)

Блок — `js`.

---

## Task 3: Урок 06.2 — Прототипы и классы

**Create:** `FrontendCourse/06-JS-продвинутый/06.2-Прототипы-и-классы.md`

**Frontmatter:**
```yaml
---
модуль: 06-JS-продвинутый
тема: Прототипы и классы
статус: to-read
roadmap: https://roadmap.sh/frontend#javascript
связано: "[[06.1-Замыкания-и-this]], [[06.3-Промисы-и-async-await]]"
---
```

**Заголовок:** `# Прототипы и классы`

**`## Зачем это нужно`:** В JS нет «классического» ООП как в Java. Всё наследование — через прототипы. В 99% нового кода ты пишешь `class`, но понимать, что это синтаксический сахар над прототипами, — обязательно. Это нужно, чтобы читать код React (классовые компоненты старые, но встречаются), `instanceof`, ошибки типа `... is not a function`.

**`## Главное` (~340–420 слов):** подразделы `### ...`:
- **Прототип.** У каждого объекта есть скрытая ссылка на «родителя» — прототип. Если свойство не найдено в самом объекте — JS идёт в прототип, потом в прототип прототипа, и так до `null`. Это цепочка прототипов.
- **Зачем это нужно.** Один прототип шарится между многими объектами. Методы — на прототипе, данные — на экземпляре. Экономия памяти, общие правила поведения.
- **`class` — современный синтаксис.** `class User { constructor(name) { this.name = name; } greet() { return ... } }`. Методы автоматически попадают на прототип, `constructor` — функция создания экземпляра.
- **Поля экземпляра и класса.** `class { count = 0; static total = 0; }`. Поля без `static` — на каждом экземпляре, со `static` — на самом классе. Приватные: `#count`.
- **Наследование `extends`.** `class Admin extends User { ... }`. `super(...)` в конструкторе — вызов родительского. `super.method()` — вызов метода родителя.
- **Методы — обычные или arrow-поля.** `greet() {}` — на прототипе, теряет `this` при передаче как коллбек. `greet = () => {}` — поле экземпляра, `this` «зашит», но хранится на каждом объекте отдельно (дороже по памяти). Выбор зависит от ситуации.
- **`instanceof` и `typeof`.** `obj instanceof User` — проверка по цепочке прототипов. `typeof` — для примитивов, для объектов почти бесполезен (всегда `"object"` или `"function"`).
- **Статические методы.** `static create(name) { return new User(name); }` — вызывается на классе, не на экземпляре: `User.create("Иван")`.
- **Геттеры/сеттеры.** `get fullName() { ... }` — доступ как к свойству: `user.fullName`, но под капотом вызов функции.
- **Когда использовать классы.** Сложные состояния с методами (игровые сущности, сервисы, модели). Для простых данных — просто объект. В React функциональные компоненты давно обгоняют классовые.

**`## Пример кода`** — блок ```js```:
```js
class User {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    return `Привет, я ${this.name}`;
  }

  get isAdult() {
    return this.age >= 18;
  }

  static createGuest() {
    return new User("Гость", 0);
  }
}

const ivan = new User("Иван", 28);
console.log(ivan.greet());      // "Привет, я Иван"
console.log(ivan.isAdult);       // true
console.log(ivan instanceof User); // true

const guest = User.createGuest();

// наследование
class Admin extends User {
  constructor(name, age, permissions) {
    super(name, age);
    this.permissions = permissions;
  }

  greet() {
    return `${super.greet()} (админ)`;
  }
}

const root = new Admin("Root", 40, ["all"]);
console.log(root.greet()); // "Привет, я Root (админ)"

// arrow-поле — this не теряется
class Button {
  label = "Нажми";
  handleClick = () => console.log(this.label);
}
const b = new Button();
setTimeout(b.handleClick, 10); // "Нажми" — ок
```

**`## Частые ошибки`** — 4 bullet-а:
- Забыть `new` — `User(...)` без `new` в strict mode выбросит ошибку; без strict — `this === undefined`.
- Не вызвать `super(...)` первым в конструкторе наследника — `this` нельзя использовать до `super`.
- Обычный метод (`greet()`) передать как коллбек → потеря `this`. Либо `.bind(this)`, либо сделай arrow-полем.
- Пытаться имитировать приватность подчёркиванием (`_count`) — сейчас есть `#private`-поля, реально приватные.

**`## Задания`:**
- [ ] Напиши класс `Counter` с методами `inc`, `dec`, `reset`, геттером `value`.
- [ ] Класс `Rectangle` (`width`, `height`), геттеры `area` и `perimeter`, метод `scale(factor)`.
- [ ] Отнаследуй `Square extends Rectangle` — конструктор берёт одну сторону.
- [ ] Сделай статический метод `Rectangle.fromObject({width, height})`.

**`## Что почитать`:**
- [MDN — Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
- [MDN — Inheritance and the prototype chain](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
- [learn.javascript.ru — Классы](https://learn.javascript.ru/classes)
- [learn.javascript.ru — Прототипы](https://learn.javascript.ru/prototypes)

Блок — `js`.

---

## Task 4: Урок 06.3 — Промисы и async/await

**Create:** `FrontendCourse/06-JS-продвинутый/06.3-Промисы-и-async-await.md`

**Frontmatter:**
```yaml
---
модуль: 06-JS-продвинутый
тема: Промисы и async/await
статус: to-read
roadmap: https://roadmap.sh/frontend#javascript
связано: "[[06.2-Прототипы-и-классы]], [[06.4-Fetch-и-работа-с-API]]"
---
```

**Заголовок:** `# Промисы и async/await`

**`## Зачем это нужно`:** Всё, что занимает время (запрос к серверу, чтение файла, `setTimeout`), в JS асинхронно. Промисы — стандартный способ представить «значение, которое будет позже». `async/await` — синтаксис, который делает асинхронный код читаемым. Без этого нет `fetch`, нет загрузки данных, нет работы с API.

**`## Главное` (~340–420 слов):** подразделы `### ...`:
- **Что такое Promise.** Объект-обёртка над будущим значением. Имеет три состояния: `pending` (в процессе), `fulfilled` (успех), `rejected` (ошибка). Переход между состояниями — один раз и навсегда.
- **Создание.** `new Promise((resolve, reject) => { ... resolve(value); ... reject(error); })`. На практике ты создаёшь промисы редко — обычно их возвращают API (`fetch`, `setTimeout`-обёртка).
- **`.then` / `.catch` / `.finally`.** `p.then(value => ...)` — обработать успех. `.catch(err => ...)` — обработать ошибку. `.finally(() => ...)` — выполнится в любом случае (чистка, скрытие loader-а).
- **Цепочки.** `fetch(...).then(res => res.json()).then(data => ...)`. Каждый `then` возвращает новый промис; можно цеплять.
- **`async/await` — сахар над промисами.** `async function f() { const data = await fetch(...); }`. `await` «ждёт» промис и возвращает его значение. Код читается как синхронный, но под капотом — те же промисы. Любая `async`-функция всегда возвращает промис.
- **Обработка ошибок через `try/catch`.** Вместо `.catch` — обычный `try/catch`. Чище для нескольких `await` подряд.
- **Параллельный запуск — `Promise.all`.** Ждёт массив промисов, возвращает массив результатов. Если хоть один упал — весь `Promise.all` упадёт. Полезно, когда независимые запросы.
- **`Promise.allSettled`.** То же, но не падает на ошибке одного — возвращает массив объектов со статусами. Используй, когда один запрос не должен обрушить остальные.
- **`Promise.race`.** Возвращает первый завершившийся промис (успех или ошибка). Используется для таймаутов.
- **Последовательный vs параллельный.** `await a(); await b();` — последовательно (медленно, если независимы). `await Promise.all([a(), b()]);` — параллельно. Запоминай разницу, чтобы не тормозить приложение.

**`## Пример кода`** — блок ```js```:
```js
// промис из воздуха
const wait = (ms) => new Promise(resolve => setTimeout(resolve, ms));

// .then-цепочка
fetch("https://api.github.com/users/octocat")
  .then(res => res.json())
  .then(data => console.log(data.name))
  .catch(err => console.error("Ошибка:", err));

// тот же код через async/await
async function loadUser(login) {
  try {
    const res = await fetch(`https://api.github.com/users/${login}`);
    if (!res.ok) throw new Error(`HTTP ${res.status}`);
    const data = await res.json();
    return data;
  } catch (err) {
    console.error("Ошибка:", err);
    return null;
  }
}

loadUser("octocat").then(user => console.log(user?.name));

// параллельно — Promise.all
async function loadMany() {
  const [a, b] = await Promise.all([
    loadUser("octocat"),
    loadUser("torvalds"),
  ]);
  return [a, b];
}

// последовательно — медленнее, если независимы
async function loadSlow() {
  const a = await loadUser("octocat");
  const b = await loadUser("torvalds");
  return [a, b];
}
```

**`## Частые ошибки`** — 4 bullet-а:
- Забыть `await` — `const data = fetch(...)` — переменная станет промисом, а не данными. Логируется как `Promise { <pending> }`.
- Не обрабатывать ошибки (`fetch` без `.catch` и без `try/catch`) → unhandled rejection в консоли, тихие падения.
- Последовательные `await` там, где можно `Promise.all` → приложение ждёт лишние секунды.
- Бросить `throw` в коллбеке обычного `.then` без второго аргумента/`.catch` — ошибка «съедается». В `async/await` с `try/catch` — проще не промахнуться.

**`## Задания`:**
- [ ] Напиши `wait(ms)` — промис, который резолвится через `ms` миллисекунд.
- [ ] Через `async`+`fetch` загрузи https://api.github.com/users/octocat, выведи имя.
- [ ] Добавь `try/catch` + обработку `!res.ok`.
- [ ] Загрузи параллельно двух пользователей (`Promise.all`), сравни время с последовательной версией (`console.time`).

**`## Что почитать`:**
- [MDN — Using promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
- [MDN — `async function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
- [learn.javascript.ru — Промисы](https://learn.javascript.ru/promise-basics)
- [learn.javascript.ru — async/await](https://learn.javascript.ru/async-await)

Блок — `js`.

---

## Task 5: Урок 06.4 — Fetch и работа с API

**Create:** `FrontendCourse/06-JS-продвинутый/06.4-Fetch-и-работа-с-API.md`

**Frontmatter:**
```yaml
---
модуль: 06-JS-продвинутый
тема: Fetch и работа с API
статус: to-read
roadmap: https://roadmap.sh/frontend#javascript
связано: "[[06.3-Промисы-и-async-await]], [[06.5-Event-loop-и-обработка-ошибок]]"
---
```

**Заголовок:** `# Fetch и работа с API`

**`## Зачем это нужно`:** Это граница между «статическим сайтом» и «приложением». `fetch` — встроенный способ отправить HTTP-запрос из браузера: загрузить данные, отправить форму, авторизоваться. Почти вся работа фронтендера — разные способы ходить в API.

**`## Главное` (~340–420 слов):** подразделы `### ...`:
- **`fetch(url, options)`.** Возвращает промис, резолвится объектом `Response`. Важно: `fetch` **не падает** при HTTP-ошибках (404, 500) — только при сетевой проблеме. Поэтому проверяй `res.ok` вручную.
- **GET (по умолчанию).** `fetch(url)` — простой GET. Передача параметров: `new URL(url)` + `url.searchParams.set("q", value)` — чтобы правильно экранировать.
- **POST / PUT / DELETE.** `fetch(url, { method: "POST", headers: {...}, body: JSON.stringify(data) })`. Тело — строка. Для JSON — обязательно `Content-Type: application/json`.
- **Чтение ответа.** `res.json()` — JSON. `res.text()` — строка. `res.blob()` — бинарный (файлы). Все возвращают промис, каждый ответ можно прочитать **только один раз**.
- **Статусы.** `res.status` — 200, 404, 500, etc. `res.ok` — true если 200–299. Дальше `throw new Error` — уходим в `catch`.
- **Заголовки.** `res.headers.get("Content-Type")`. Отправить свои — `{ headers: { Authorization: "Bearer ..." } }`.
- **CORS в двух словах.** Браузер блокирует запросы к чужому домену, если сервер не разрешил явно заголовком `Access-Control-Allow-Origin`. В публичных API (GitHub, open-meteo) CORS настроен, можно ходить с `localhost`. В свой бэкенд — настраивай CORS на сервере.
- **AbortController — отменить запрос.** `const ctrl = new AbortController(); fetch(url, { signal: ctrl.signal }); ... ctrl.abort();`. Пригодится, если пользователь быстро печатает в поиске и старые запросы уже не нужны.
- **Типичный паттерн «загрузить и отобразить».** 1) показать loader, 2) `await fetch`, 3) `if (!res.ok) throw`, 4) `await res.json()`, 5) обновить UI, 6) `catch` → показать ошибку, 7) `finally` → убрать loader.
- **Таймауты.** Нативного таймаута у `fetch` нет — делай сам через `AbortController` + `setTimeout`. Или `AbortSignal.timeout(5000)` (современный).

**`## Пример кода`** — блок ```js```:
```js
// GET с параметрами
async function searchUser(login) {
  const url = new URL("https://api.github.com/search/users");
  url.searchParams.set("q", login);

  const res = await fetch(url, {
    headers: { Accept: "application/vnd.github+json" },
  });

  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  return res.json();
}

// POST с JSON-телом
async function createPost(title, body) {
  const res = await fetch("https://jsonplaceholder.typicode.com/posts", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ title, body, userId: 1 }),
  });

  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  return res.json();
}

// Loader + ошибка — типичный паттерн
async function renderUser(login) {
  const loader = document.querySelector("#loader");
  const error  = document.querySelector("#error");
  const view   = document.querySelector("#view");

  loader.hidden = false;
  error.hidden = true;

  try {
    const res = await fetch(`https://api.github.com/users/${login}`);
    if (!res.ok) throw new Error(`Не найден: ${res.status}`);
    const data = await res.json();
    view.textContent = data.name || data.login;
  } catch (err) {
    error.textContent = err.message;
    error.hidden = false;
  } finally {
    loader.hidden = true;
  }
}

// Отмена — AbortController
const ctrl = new AbortController();
fetch("https://api.github.com/users/octocat", { signal: ctrl.signal });
ctrl.abort(); // прервать
```

**`## Частые ошибки`** — 4 bullet-а:
- Считать, что `fetch` кинет исключение на 404. Нет: нужно проверять `res.ok` вручную.
- Забыть `Content-Type: application/json` при POST с JSON-телом → сервер не распарсит.
- Читать `res` дважды: `await res.json()`, потом `await res.text()` → `TypeError: body used already`.
- Не чистить loader в `finally` → при ошибке крутилка висит вечно.

**`## Задания`:**
- [ ] Загрузи 5 постов: `https://jsonplaceholder.typicode.com/posts?_limit=5`, выведи в консоль заголовки.
- [ ] Отправь POST-запрос туда же: `{title, body, userId:1}`, логируй ответ.
- [ ] Напиши функцию `getUser(login)` с loader, ошибкой и `finally`.
- [ ] Добавь отмену запроса через `AbortController` — вызвал `abort()` до завершения, в `catch` обработай `err.name === "AbortError"`.

**`## Что почитать`:**
- [MDN — Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
- [MDN — Response](https://developer.mozilla.org/en-US/docs/Web/API/Response)
- [learn.javascript.ru — Fetch](https://learn.javascript.ru/fetch)
- [MDN — CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

Блок — `js`.

---

## Task 6: Урок 06.5 — Event loop и обработка ошибок

**Create:** `FrontendCourse/06-JS-продвинутый/06.5-Event-loop-и-обработка-ошибок.md`

**Frontmatter:**
```yaml
---
модуль: 06-JS-продвинутый
тема: Event loop и обработка ошибок
статус: to-read
roadmap: https://roadmap.sh/frontend#javascript
связано: "[[06.4-Fetch-и-работа-с-API]]"
---
```

**Заголовок:** `# Event loop и обработка ошибок`

**`## Зачем это нужно`:** JS — однопоточный. Но работает с асинхронными задачами: таймерами, кликами, запросами. Как это сочетается — объясняет event loop. Понимание нужно, чтобы не делать странных предположений о порядке `console.log` и правильно обрабатывать ошибки, которые теперь могут прилетать «из будущего».

**`## Главное` (~320–400 слов):** подразделы `### ...`:
- **Однопоточность и call stack.** В каждый момент JS выполняет одну инструкцию. Все вызовы попадают в стек. Пустой стек = движок готов брать следующую задачу.
- **Web APIs (браузер).** `setTimeout`, `fetch`, DOM-события — это не JS, это **браузерные API**. Они умеют работать параллельно движку и по готовности кладут callback в очередь.
- **Очередь задач (macrotask).** Коллбеки `setTimeout`, DOM-события, `setInterval`. Event loop забирает одну задачу, когда стек пуст.
- **Очередь микрозадач.** Резолв промисов, `queueMicrotask`. **Микрозадачи выполняются все подряд после текущей задачи**, до следующей macrotask. Поэтому `Promise.resolve().then(...)` всегда выполнится раньше `setTimeout(..., 0)`.
- **Порядок.** Сценарий: `console.log("A"); setTimeout(() => log("B")); Promise.resolve().then(() => log("C")); log("D");` → A, D, C, B. Потому что микрозадача (`C`) идёт до macrotask (`B`).
- **Блокировка.** Длинный синхронный код (тяжёлый цикл, огромный JSON) **блокирует event loop** — вкладка фризится, UI не реагирует. Рецепт: разбить на куски, использовать воркеры (модуль 07+), не грузить 50 МБ данных в один `for`.
- **Ошибки в синхронном коде.** `try { ... } catch (err) { ... }` — классика. Некритичные — логируй, критичные — пробрось выше.
- **Ошибки в промисах.** `async function` бросает `throw` → промис уходит в rejected. Ловим через `.catch` или `try/catch` вокруг `await`. Глобально — `window.addEventListener("unhandledrejection", ...)`.
- **Ошибки в `setTimeout`/обработчиках событий.** Не ловятся внешним `try/catch` — коллбек вызывается позже и вне текущего контекста. Оборачивай внутри коллбека: `setTimeout(() => { try { ... } catch {} });`.
- **Error-объект.** Создавай свои: `throw new Error("сообщение")`. Даёт стек вызовов, поля `message`/`name`/`stack`. Бросать строки — плохо, теряешь контекст.

**`## Пример кода`** — блок ```js```:
```js
// порядок выполнения
console.log("1 — синхронно");

setTimeout(() => console.log("4 — macrotask"), 0);

Promise.resolve().then(() => console.log("3 — microtask"));

console.log("2 — синхронно");
// порядок: 1, 2, 3, 4

// try/catch и async
async function load(url) {
  try {
    const res = await fetch(url);
    if (!res.ok) throw new Error(`HTTP ${res.status}`);
    return await res.json();
  } catch (err) {
    console.error("Не удалось загрузить:", err.message);
    throw err; // пробрасываем выше, если нужно
  }
}

// ошибки не лечатся внешним try/catch вокруг setTimeout
try {
  setTimeout(() => {
    throw new Error("бум");
  }, 0);
} catch (e) {
  // сюда НЕ попадёт — коллбек выполняется позже
}

// корректно — try/catch внутри коллбека
setTimeout(() => {
  try {
    throw new Error("бум");
  } catch (e) {
    console.warn("поймал:", e.message);
  }
}, 0);

// глобальный перехват unhandled promise rejection
window.addEventListener("unhandledrejection", (event) => {
  console.error("Unhandled:", event.reason);
  event.preventDefault();
});
```

**`## Частые ошибки`** — 4 bullet-а:
- Оборачивать `setTimeout(() => throw ...)` внешним `try/catch` и удивляться, что не ловится. Лови внутри коллбека.
- Забывать `await` перед функцией, которая возвращает промис → `try/catch` пропускает ошибку.
- Делать тяжёлый синхронный цикл в обработчике клика → заморозка UI. Разбивай или переноси в воркер.
- Бросать строку (`throw "ошибка"`) вместо `new Error(...)` → в `catch` нет стека, сложнее дебажить.

**`## Задания`:**
- [ ] Напиши программу, печатающую «1, 2, 3, 4» в правильном порядке через `setTimeout(..., 0)` и `Promise.resolve().then(...)`. Разберись, почему так.
- [ ] Создай функцию `safe(fn)`, которая пытается вызвать `fn()` в `try/catch` и возвращает `null` при ошибке.
- [ ] Сделай fetch-запрос к заведомо несуществующему URL, обработай ошибку и выведи сообщение.
- [ ] Подпишись на `unhandledrejection` и протестируй, что срабатывает на необработанный rejected-промис.

**`## Что почитать`:**
- [MDN — The event loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)
- [MDN — `try/catch`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch)
- [learn.javascript.ru — Event loop](https://learn.javascript.ru/event-loop)
- [learn.javascript.ru — Обработка ошибок](https://learn.javascript.ru/try-catch)

Блок — `js`.

---

## Task 7: Мини-проект M06 — Fetch-приложение

**Create:** `FrontendCourse/Проекты/Мини/M06-Fetch-приложение.md`

**Exact content:**

```markdown
---
тип: мини-проект
модуль: 06-JS-продвинутый
статус: not-started
---

# M06 — Fetch-приложение

Мини-проект после модуля 06. Первое приложение, которое реально ходит в интернет. Задача — не «покрасиво», а прочувствовать цикл: запрос → loading → ответ (данные или ошибка) → обновление UI.

## Задача — на выбор

Выбираешь один из двух вариантов (оба подходят, оба без API-ключа):

### Вариант A — Погода по городу
- API: [open-meteo.com](https://open-meteo.com/) — бесплатно, без ключа, CORS открыт.
- Поле ввода для города (сначала resolve в координаты через Geocoding API open-meteo, потом прогноз).
- Показать текущую температуру, ощущение, ветер, 3–5-дневный прогноз.
- Иконка/эмодзи по коду погоды.

### Вариант B — Поиск GitHub-профилей
- API: `https://api.github.com/users/:login` — без ключа (60 запросов/час с IP).
- Поле ввода логина, по submit — загрузка.
- Показать: аватар, имя, bio, кол-во репов, подписчиков.
- Бонус: список последних 5 репов `/users/:login/repos?sort=updated&per_page=5`.

## Требования (общие для обоих)

### Функциональность
1. **Ввод + submit** — форма с `<input>` и кнопкой. На пустой ввод — не запрашивать.
2. **Loading-состояние** — пока ждём ответ, виден loader (спиннер / текст «Загрузка…»). Кнопка блокируется.
3. **Успех** — DOM обновляется данными из API.
4. **Ошибка** — если `!res.ok` или сеть упала — показать понятное сообщение («Город не найден», «Пользователь не найден», «Проверьте интернет»). НЕ alert-ом.
5. **Повторный запрос работает** — можно искать снова без перезагрузки.
6. **В `finally` — убирать loader и разблокировать кнопку**, в любой ситуации.
7. **Деплой** — Vercel или Netlify, рабочий прод-URL.

### Технические правила
- Только `fetch` + `async/await` + `try/catch/finally`. Никаких axios/jQuery.
- Без фреймворков — vanilla JS (HTML + CSS + JS).
- Стили любые (чистый CSS или Tailwind через CLI/Vite).
- Типичная структура: `renderLoading()`, `renderSuccess(data)`, `renderError(message)` — три состояния UI, чистое разделение.
- `AbortController` — опционально, но круто иметь для быстрого переввода в поле.
- Никаких ключей в клиентском коде (тут API и так открытые — просто запомни правило).
- В DevTools → Network видны реальные запросы, и ты можешь их прочитать.

## Чего НЕ должно быть

- Библиотек (axios, lodash, React — ничего).
- `alert` для ошибок — делай текстовый блок в разметке.
- `innerHTML` с сырым ответом API (XSS-риск на экзотических данных).
- «Голого» `fetch` без проверки `res.ok`.
- Скрытия ошибок под коврик (`catch(() => {})`).

## Этапы

1. **Выбрать API**, прочитать его документацию. Проверить пару запросов в DevTools или Postman.
2. **Разметка**: форма, блоки loader/error/result.
3. **Стили**: три состояния должны различаться визуально.
4. **Логика запроса**: `fetchData(query)` — асинхронная функция, возвращает данные или бросает `Error`.
5. **Обработчик submit**: состояние → try/catch/finally → три render-функции.
6. **Деплой**: Vercel / Netlify, README со скриншотами.

## Сдача

1. Публичный GitHub-репозиторий.
2. Прод-URL.
3. README: какой вариант выбрал, какой API, ссылка на деплой, скриншот.
4. На созвоне — вместе смотрим код и Network-вкладку.

## Критерии приёмки ревью

- [ ] Все 7 функциональных пунктов работают.
- [ ] Используется `async/await` + `try/catch/finally`.
- [ ] Ошибка (404 / сеть / некорректный ввод) показывается в UI, не в alert и не только в консоли.
- [ ] Loader действительно появляется и исчезает (в том числе при ошибке).
- [ ] Проверяется `res.ok` перед `res.json()`.
- [ ] Нет `innerHTML` с сырыми строками из ответа.
- [ ] Network во время запроса показывает корректный метод и URL.
- [ ] Прод-URL работает по HTTPS.

## Что дальше
После этого проекта заканчивается серия «просто JS» и начинаются **модули 07–08** — веб-архитектура (HTTP, клиент-сервер, авторизация) и Git с DevTools. После них откроется дорога в React.
```

---

## Task 8: Обновить MOC-JS

**Modify:** `FrontendCourse/MOC/MOC-JS.md`

- [ ] **Step 8.1:** Полностью заменить содержимое на:

```markdown
---
тип: MOC
тема: JavaScript
---

# MOC — JavaScript

Карта знаний по JavaScript. Заполняется в модулях 05 и 06.

## База (модуль 05)
- [[05.1-Переменные-типы-операторы]]
- [[05.2-Ветвления-и-циклы]]
- [[05.3-Функции]]
- [[05.4-Массивы]]
- [[05.5-Объекты]]
- [[05.6-DOM-и-события]]

## Продвинутое (модуль 06)
- [[06.1-Замыкания-и-this]]
- [[06.2-Прототипы-и-классы]]
- [[06.3-Промисы-и-async-await]]
- [[06.4-Fetch-и-работа-с-API]]
- [[06.5-Event-loop-и-обработка-ошибок]]

## Практика
- [[M05-ToDo-лист]]
- [[M06-Fetch-приложение]]
```

---

## Task 9: Обновить 00-Start-Here.md

**Modify:** `FrontendCourse/00-Start-Here.md`

- [ ] **Step 9.1:** Заменить строку `- [[06-JS-продвинутый/00-Обзор-модуля|Модуль 06 — JS продвинутый]] _(скоро)_` на `- [[06-JS-продвинутый/00-Обзор-модуля|Модуль 06 — JS продвинутый]]`.

---

## Task 10: Верификация

- [ ] **Step 10.1:** `find FrontendCourse/06-JS-продвинутый -type f -name "*.md" | sort` → 6 файлов.
- [ ] **Step 10.2:** `M06-Fetch-приложение.md` существует в `Проекты/Мини/`.
- [ ] **Step 10.3:** MOC-JS содержит 5 ссылок на уроки 06.1–06.5.
- [ ] **Step 10.4:** В `00-Start-Here.md` у модуля 06 нет «_(скоро)_».
- [ ] **Step 10.5:** Отчитаться: модуль 06 готов.

---

## Self-Review

**1. Spec coverage:**
- Замыкания глубже + `this` → Task 2. ✓
- Прототипы + классы → Task 3. ✓
- Промисы + async/await → Task 4. ✓
- fetch + API → Task 5. ✓
- Event loop + обработка ошибок → Task 6. ✓
- Мини-проект с выбором двух API → Task 7. ✓

**2. Placeholder scan:** TBD/TODO нет. ✓

**3. Type consistency:** Имена уроков и мини-проекта согласованы во всех местах (обзор, frontmatter, MOC, верификация). ✓

---

## Out of Scope

- Модули ES (`import/export`), пакетные менеджеры, сборка → модули 07, 08, 12.
- TypeScript → модуль 11.
- Глубокое HTTP / cookies / auth / JWT → модуль 07.
- React, JSX, хуки → модуль 09.
