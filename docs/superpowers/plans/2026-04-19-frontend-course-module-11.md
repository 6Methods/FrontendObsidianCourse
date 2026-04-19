# Frontend Course — Module 11 (TypeScript) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: superpowers:subagent-driven-development. Контентный проект.

**Goal:** Наполнить модуль 11 «TypeScript»: обзор + 7 уроков + 2 мини-проекта (рефакторинг M10 на TS + Pokédex на TS) + заполнить MOC-TS + обновить Start-Here.

**Architecture:** Структура модулей 01–10. Шаблон урока (6 секций), средняя глубина. Фокус — прикладной TS для React-разработчика: типы, generics, utility types, строгая интеграция с React, схемы через zod. Цель — чтобы к концу модуля ты переписывал с JS на TS без боли и делал новые проекты сразу типизированными.

**Базовые пути:**
- Vault: `/Users/luckyme/Desktop/maloyfront/FrontendCourse/`
- Модуль: `FrontendCourse/11-TypeScript/`

---

## File Structure

```
FrontendCourse/
├── 00-Start-Here.md                           (правка: убрать «_(скоро)_»)
├── 11-TypeScript/
│   ├── 00-Обзор-модуля.md                     (новый)
│   ├── 11.1-Зачем-TS-и-setup.md               (новый)
│   ├── 11.2-Базовые-типы.md                   (новый)
│   ├── 11.3-Aliases-interfaces-unions.md      (новый)
│   ├── 11.4-Generics.md                       (новый)
│   ├── 11.5-Utility-types.md                  (новый)
│   ├── 11.6-TS-и-React.md                     (новый)
│   └── 11.7-Zod-inference-и-API.md            (новый)
├── Проекты/Мини/
│   ├── M11a-Рефакторинг-M10-на-TS.md          (новый)
│   └── M11b-Pokedex-на-TS.md                  (новый)
└── MOC/
    └── MOC-TS.md                              (правка: заполнить)
```

Итого: **11 новых файлов**, 2 правки.

---

## Task 1: Обзор модуля 11

**Create:** `FrontendCourse/11-TypeScript/00-Обзор-модуля.md`

```markdown
---
тип: обзор-модуля
модуль: 11-TypeScript
статус: not-started
roadmap: https://roadmap.sh/typescript
---

# Модуль 11 — TypeScript

**roadmap.sh:** [TypeScript roadmap](https://roadmap.sh/typescript)

На JS ты уже написал два React-проекта. Проблема в том, что половину багов ты ловишь только в рантайме: опечатка в ключе объекта, `undefined` вместо объекта, строка вместо числа. TypeScript — надстройка над JS, которая добавляет статическую типизацию: ошибки видишь в редакторе до запуска. Для фронтенда это больше не опция — почти все вакансии и open-source-проекты ждут TS по умолчанию.

## Что изучаем
- Зачем TS и как поставить: `tsc`, `tsconfig.json`, Vite + TS.
- Базовые типы: примитивы, массивы, объекты, функции, `any` vs `unknown`.
- Type aliases, interfaces, union, intersection, narrowing.
- Generics — переиспользуемые типизированные функции и компоненты.
- Utility types: `Partial`, `Pick`, `Omit`, `Record`, `ReturnType` и другие.
- TS + React: props, state, events, refs, типы детей.
- Zod — рантайм-валидация + `z.infer` для типов из схем.

## Уроки
- [ ] [[11.1-Зачем-TS-и-setup]]
- [ ] [[11.2-Базовые-типы]]
- [ ] [[11.3-Aliases-interfaces-unions]]
- [ ] [[11.4-Generics]]
- [ ] [[11.5-Utility-types]]
- [ ] [[11.6-TS-и-React]]
- [ ] [[11.7-Zod-inference-и-API]]

## Итоговая практика
- [ ] Мини-проект A: [[M11a-Рефакторинг-M10-на-TS]] — переписать SPA-магазин из модуля 10 на TypeScript. Прямое сравнение «JS → TS» на своём коде.
- [ ] Мини-проект B: [[M11b-Pokedex-на-TS]] — новый проект с нуля на TS: Pokédex с PokéAPI, типизация ответов, generic-хуки.

## Связанные MOC
- [[MOC-TS]] — карта TypeScript.

## Чек-лист завершения
- [ ] все 7 уроков прочитаны
- [ ] M10 переписан на TS, `strict: true`, без `any` (за редкими оправданными исключениями)
- [ ] Pokédex на TS задеплоен
- [ ] понимаешь разницу между `type` и `interface`, `any` и `unknown`
- [ ] умеешь писать generic-функцию и generic-компонент
- [ ] умеешь вывести тип из zod-схемы через `z.infer`
- [ ] узлы TypeScript в roadmap.sh закрыты
```

---

## Task 2: Урок 11.1 — Зачем TS и setup

**Create:** `FrontendCourse/11-TypeScript/11.1-Зачем-TS-и-setup.md`

**Frontmatter:**
```yaml
---
модуль: 11-TypeScript
тема: Зачем TS и setup
статус: to-read
roadmap: https://roadmap.sh/typescript
связано: [[11.2-Базовые-типы]]
---
```

**Заголовок:** `# Зачем TS и setup`

**`## Зачем это нужно`:** JS динамический — ошибки типа «передал строку вместо числа» ловятся только в рантайме. TS добавляет статическую проверку: IDE подсказывает типы, рефакторинг без страха, документация встроена в код. В 2026 году это базовый язык фронтенда — без него смотрят на резюме хуже.

**`## Главное` (~320-400 слов):** подразделы `###`:
- **TS — надстройка над JS.** Валидный JS — это валидный TS. Компилятор `tsc` проверяет типы и снимает аннотации — на выходе обычный JS. В браузере TS не выполняется.
- **Статическая vs динамическая типизация.** В JS `"1" + 1` = `"11"` — интерпретатор ничего не подскажет. В TS — ошибка компиляции с указанием файла и строки. Ошибки ловишь до запуска.
- **Установка в проект.** Свежий: `npm create vite@latest my-app -- --template react-ts`. Существующий: `npm install -D typescript && npx tsc --init`. Все Vite-шаблоны из реальных проектов — с TS по умолчанию.
- **Файлы.** `.ts` — обычный код, `.tsx` — JSX внутри TS. Компоненты с JSX всегда в `.tsx`. Хуки и утилиты — чаще `.ts`.
- **tsconfig.json.** Главный файл настройки: что компилировать, какие правила. Ключевые опции: `strict: true` (все проверки), `jsx: "react-jsx"` (новый JSX-трансформер), `target: "ES2022"`, `moduleResolution: "bundler"` (для Vite/Webpack).
- **Типовая аннотация.** `let x: number = 10; function greet(name: string): string { return ... }`. Двоеточие `:` + тип. Для переменных часто не нужна — TS сам выведет.
- **Инференция типов.** `const x = 10` — TS сам понимает, что `x: number`. Пиши типы, только когда они нужны: на границах (параметры функций, возвращаемые значения, структура данных с API).
- **Режим strict.** `strict: true` включает пачку флагов: `noImplicitAny`, `strictNullChecks` и другие. Всегда включай — без него TS слишком лёгкий и пропускает баги.
- **VS Code + TS.** TS встроен: подсказки типов, автоимпорт, переименование переменных по всему проекту. Горячее — `F12` (перейти к определению), `Shift+F12` (найти все использования), `F2` (переименовать).
- **tsc --noEmit.** Для проверки типов без генерации JS. В `package.json`: `"typecheck": "tsc --noEmit"` — прогоняешь в CI и локально.

**`## Пример кода`** — блок ```ts:
```ts
// tsconfig.json (основное)
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "moduleResolution": "bundler",
    "jsx": "react-jsx",
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "skipLibCheck": true
  },
  "include": ["src"]
}

// src/greet.ts
export function greet(name: string): string {
  return `Привет, ${name}!`;
}

// ошибка на этапе компиляции:
greet(42); // Argument of type 'number' is not assignable to parameter of type 'string'.

// инференция: тип возвращаемого — выведется автоматически
export function add(a: number, b: number) {
  return a + b; // number
}

// валидный JS — валидный TS
export const config = { retries: 3, timeout: 1000 }; // TS сам выведет структуру
```

**`## Частые ошибки`** — 4 буллета:
- Учить TS как «язык типов» — TS это JS + типы. Сначала нужен уверенный JS.
- Писать `: any` везде, где TS ругается. `any` выключает проверку — смысл теряется. Используй `unknown` или напиши честный тип.
- Не включать `strict: true` — без него `null`/`undefined` проходят мимо, появляются NPE в рантайме.
- Бороться с типами вместо чтения ошибки. TS-ошибки длинные, но всегда по делу — читай снизу вверх.

**`## Задания`:**
- [ ] Создай проект `npm create vite@latest ts-sandbox -- --template react-ts`. Запусти.
- [ ] Поломай типы специально: передай число туда, где ждут строку. Посмотри ошибку в IDE и `tsc`.
- [ ] Открой `tsconfig.json` в своём проекте — прочитай все опции, пойми зачем они.
- [ ] Добавь скрипт `"typecheck": "tsc --noEmit"` и прогоняй перед каждым коммитом.

**`## Что почитать`:**
- [TypeScript Handbook — The Basics](https://www.typescriptlang.org/docs/handbook/2/basic-types.html)
- [TypeScript — tsconfig Reference](https://www.typescriptlang.org/tsconfig)
- [Vite — TypeScript](https://vite.dev/guide/features.html#typescript)
- [TS Playground](https://www.typescriptlang.org/play) — учебная песочница онлайн

Блок — `ts`.

---

## Task 3: Урок 11.2 — Базовые типы

**Create:** `FrontendCourse/11-TypeScript/11.2-Базовые-типы.md`

**Frontmatter:**
```yaml
---
модуль: 11-TypeScript
тема: Базовые типы
статус: to-read
roadmap: https://roadmap.sh/typescript
связано: [[11.1-Зачем-TS-и-setup]], [[11.3-Aliases-interfaces-unions]]
---
```

**Заголовок:** `# Базовые типы`

**`## Зачем это нужно`:** TS даёт словарь типов для описания почти любой структуры данных. Без уверенного знания примитивов и базовых коллекций остальное (generics, utility types) бесполезно. Это — фундамент, на котором строится всё остальное.

**`## Главное` (~340-420 слов):** подразделы `###`:
- **Примитивы.** `string`, `number`, `boolean`, `null`, `undefined`, `bigint`, `symbol`. Пишутся с маленькой буквы. `String`, `Number` (с большой) — это обёртки, не используй.
- **Литеральные типы.** `let x: "small" | "large"` — только эти две строки. Часто для вариантов: `type Status = "idle" | "loading" | "success" | "error"`.
- **Массивы.** Два синтаксиса: `number[]` или `Array<number>`. Смешанные массивы: `(string | number)[]`. Tuple — массив фиксированной длины с разными типами: `[string, number]`.
- **Объекты.** Inline: `{ name: string; age: number }`. Опциональное поле: `age?: number`. Readonly: `readonly id: number`. Index signature: `{ [key: string]: string }` — словарь.
- **Функции.** `function sum(a: number, b: number): number`. Тип возвращаемого можно не писать — TS выведет. Параметр с дефолтом: `function f(x = 0)` — тип `number`.
- **any vs unknown.** `any` — «выключаю типы». Можно всё — но теряешь смысл TS. `unknown` — «не знаю тип, но буду сужать». Безопасно: обязательно проверять, прежде чем использовать.
- **void и never.** `void` — функция ничего не возвращает (`logger(): void`). `never` — никогда не возвращается: бесконечный цикл, `throw Error()`. Используются в редких случаях, но знать надо.
- **Type assertion.** `const el = document.getElementById("x") as HTMLInputElement`. Говоришь TS «я знаю лучше». Осторожно: это НЕ проверка в рантайме, а обещание программисту самому себе.
- **Narrowing.** TS сужает типы внутри `if`: `if (typeof x === "string") { ... }`. Внутри блока `x: string`. Используется постоянно — см. 11.3.
- **null и undefined.** При `strictNullChecks: true` (включён strict) — это отдельные типы. Значение может быть `null` только если в типе есть `| null`. `string` — не допускает `null`.
- **Optional chaining и nullish coalescing.** Уже знакомо из JS (`?.`, `??`), в TS — важный инструмент работы с nullable типами: `user?.name ?? "Гость"`.

**`## Пример кода`** — блок ```ts:
```ts
// Примитивы
const name: string = "Иван";
const age: number = 25;
const isAdmin: boolean = true;

// Литералы
type Theme = "light" | "dark";
let theme: Theme = "light";
// theme = "blue"; // ошибка

// Массивы и tuple
const ids: number[] = [1, 2, 3];
const row: [string, number] = ["count", 42];

// Объект
type User = {
  readonly id: number;
  name: string;
  email?: string;       // опционально
};

const u: User = { id: 1, name: "Иван" };

// Функции
function sum(a: number, b: number): number {
  return a + b;
}

const multiply = (a: number, b: number) => a * b; // тип выведется

// any vs unknown
let a: any = 10;
a.foo.bar; // TS разрешит — и в рантайме упадёт

let u1: unknown = 10;
// u1.toFixed(2); // ошибка — TS не даст
if (typeof u1 === "number") {
  u1.toFixed(2); // ok, TS сузил тип
}

// null
function formatName(name: string | null): string {
  return name ?? "Гость";
}

// Type assertion (осторожно)
const input = document.getElementById("email") as HTMLInputElement;
input.value = "test";
```

**`## Частые ошибки`** — 4 буллета:
- Писать `String` вместо `string` — большая буква это обёртка `new String(...)`, почти никогда не нужна.
- Использовать `any`, когда не знаешь тип. Используй `unknown` и сужай через проверки.
- Забывать про `| undefined` для опциональных полей: `age?: number` на самом деле `number | undefined`.
- Злоупотреблять `as` — это не проверка, а обещание. Если ошибёшься — падение в рантайме.

**`## Задания`:**
- [ ] Опиши тип `User` с полями: `id`, `name`, `email?`, `role: "admin" | "user"`. Создай массив `User[]`.
- [ ] Напиши функцию `parseAge(raw: unknown): number` — на `unknown` через narrowing привести к числу (или бросить ошибку).
- [ ] Сделай tuple `[string, number, boolean]` — описание записи лог-файла `[level, code, isError]`.
- [ ] Возьми `any` в одной переменной — посмотри, как TS молчит. Замени на `unknown` — сравни.

**`## Что почитать`:**
- [TS Handbook — Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)
- [TS Handbook — Narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)
- [Matt Pocock — any vs unknown](https://www.totaltypescript.com/concepts/the-difference-between-any-and-unknown)
- [Type-challenges](https://github.com/type-challenges/type-challenges) — задачки на типы

Блок — `ts`.

---

## Task 4: Урок 11.3 — Aliases, interfaces, unions, narrowing

**Create:** `FrontendCourse/11-TypeScript/11.3-Aliases-interfaces-unions.md`

**Frontmatter:**
```yaml
---
модуль: 11-TypeScript
тема: Type aliases, interfaces, unions, narrowing
статус: to-read
roadmap: https://roadmap.sh/typescript
связано: [[11.2-Базовые-типы]], [[11.4-Generics]]
---
```

**Заголовок:** `# Type aliases, interfaces, unions, narrowing`

**`## Зачем это нужно`:** Примитивы — это только начало. Реальные структуры описываются через `type`/`interface`, варианты состояний — через union, безопасная работа с union — через narrowing. Без этих инструментов не получится типизировать реальное приложение.

**`## Главное` (~340-420 слов):** подразделы `###`:
- **Type alias.** `type User = { id: number; name: string }`. Даёт имя типу — можно переиспользовать. Работает с чем угодно: объекты, unions, tuples, примитивы.
- **Interface.** `interface User { id: number; name: string }`. Очень похоже на `type`, но с отличиями. Интерфейсы можно расширять и сливать (declaration merging), `type` — нет.
- **type vs interface — практика.** Для объектов и React-props — в большинстве проектов `type`. Для расширяемых API-контрактов и classes — `interface`. Команды редко строго фиксируют выбор, главное — согласованность.
- **Расширение.** `interface Admin extends User { role: string }`. Для `type` — через intersection: `type Admin = User & { role: string }`.
- **Union.** `type Id = string | number` — одно из двух. Работать с union-ом напрямую можно только через общие поля. Для доступа к специфичным — нужен narrowing.
- **Intersection.** `type A = User & { isActive: boolean }` — объединение полей. Получаешь объект с обоими наборами.
- **Discriminated union.** Самый важный паттерн: union объектов с общим полем-тегом. `type State = { kind: "loading" } | { kind: "success"; data: T } | { kind: "error"; error: Error }`. Switch по `kind` — TS сам сужает тип.
- **Narrowing: typeof.** `if (typeof x === "string") { ... }` — сужает до `string`. Работает с примитивами.
- **Narrowing: in.** `if ("admin" in user) { ... }` — внутри `user` имеет нужный подтип. Полезно для union объектов.
- **Narrowing: instanceof.** `if (err instanceof Error) { ... }` — для классов. Особенно в `catch (err: unknown)`.
- **Type guards.** Функция с return-типом `is T`: `function isUser(x: unknown): x is User { ... }`. В условии TS сужает до `User`.
- **Exhaustiveness check.** В switch по discriminated union добавь `default: const _: never = value` — если появится новый вариант, TS заругается на этой строке. Защита от забытых case-ов.

**`## Пример кода`** — блок ```ts:
```ts
// Type alias
type User = {
  id: number;
  name: string;
  email?: string;
};

// Interface
interface Admin extends User {
  role: "admin" | "moderator";
}

// Union
type Id = string | number;

function printId(id: Id) {
  if (typeof id === "string") {
    console.log(id.toUpperCase()); // TS знает: string
  } else {
    console.log(id.toFixed(0));    // TS знает: number
  }
}

// Discriminated union — состояние загрузки
type FetchState<T> =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; data: T }
  | { status: "error"; error: Error };

function render(state: FetchState<User>) {
  switch (state.status) {
    case "idle":    return "ждём";
    case "loading": return "грузим…";
    case "success": return state.data.name;  // TS знает: есть data
    case "error":   return state.error.message;
    default:
      const _exhaustive: never = state; // защита
      return _exhaustive;
  }
}

// Type guard
function isError(x: unknown): x is Error {
  return x instanceof Error;
}

try {
  throw new Error("oops");
} catch (err: unknown) {
  if (isError(err)) {
    console.log(err.message); // TS знает: Error
  }
}

// in-оператор
type Cat = { purr(): void };
type Dog = { bark(): void };

function sound(pet: Cat | Dog) {
  if ("purr" in pet) pet.purr();
  else pet.bark();
}
```

**`## Частые ошибки`** — 4 буллета:
- Использовать union без narrowing: `id.toUpperCase()` на `string | number` — TS заругается. Сначала проверка.
- Писать плоский тип `{ status: string; data?: T; error?: Error }` вместо discriminated union — плодит `if (data)` везде.
- Забывать exhaustiveness check в switch — добавил новый `kind`, забыл обработать, получил `undefined` в рантайме.
- Спор «type vs interface» на два часа. Выбери одно и используй в проекте последовательно.

**`## Задания`:**
- [ ] Опиши `Shape` = круг | квадрат | треугольник (discriminated union). Функция `area(s: Shape): number` — switch с exhaustiveness.
- [ ] Напиши type guard `isString(x: unknown): x is string`. Используй в функции.
- [ ] Возьми интерфейс `User` и расширь его до `Admin` — сравни с intersection через `type`.
- [ ] Обработай `catch (err: unknown)` — через `instanceof Error` извлеки `err.message`.

**`## Что почитать`:**
- [TS Handbook — Object Types](https://www.typescriptlang.org/docs/handbook/2/objects.html)
- [TS Handbook — Unions and Intersections](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types)
- [TS Handbook — Narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)
- [Matt Pocock — Discriminated Unions](https://www.totaltypescript.com/discriminated-unions-are-a-devs-best-friend)

Блок — `ts`.

---

## Task 5: Урок 11.4 — Generics

**Create:** `FrontendCourse/11-TypeScript/11.4-Generics.md`

**Frontmatter:**
```yaml
---
модуль: 11-TypeScript
тема: Generics
статус: to-read
roadmap: https://roadmap.sh/typescript
связано: [[11.3-Aliases-interfaces-unions]], [[11.5-Utility-types]]
---
```

**Заголовок:** `# Generics`

**`## Зачем это нужно`:** Generics — способ написать функцию или тип, которые работают с разными типами, сохраняя точность. Без generics ты либо теряешь типы (`any`), либо копируешь функцию под каждый случай. С ними — одна функция типизирует всё.

**`## Главное` (~320-400 слов):** подразделы `###`:
- **Проблема, которую решают generics.** `function first(arr: any[]): any` — взял первый элемент, тип потерял. `function first<T>(arr: T[]): T` — TS сохранит тип: `first([1,2,3])` вернёт `number`.
- **Синтаксис.** Угловые скобки с именем: `<T>`. Обычно одна буква: `T` (type), `K` (key), `V` (value), `U`/`S` — дополнительные. Длинные имена тоже можно: `<Item>`.
- **Generic-функция.** `function identity<T>(x: T): T { return x }`. TS выводит `T` из аргумента — при `identity(42)` `T = number` автоматически. Явно указать: `identity<string>("x")`.
- **Ограничения (constraints).** `<T extends { id: number }>` — работает с любым типом, где есть `id: number`. Без ограничений нельзя использовать свойства внутри функции: TS не знает, что доступно.
- **Несколько параметров.** `function map<T, U>(arr: T[], fn: (x: T) => U): U[]`. Каждый параметр — своя буква, свои ограничения.
- **Generic в type/interface.** `type Box<T> = { value: T }`. Используешь: `Box<string>`, `Box<User>`. Многие утилиты React используют generics: `useState<string>("")`.
- **Generic в React-компоненте.** Компонент-список: `function List<T>({ items, render }: { items: T[]; render: (item: T) => ReactNode }) { ... }`. При использовании — TS подставит тип автоматически.
- **Инференция в generic.** TS почти всегда выводит тип сам из аргументов. Явно указывать нужно, когда аргументов нет или чтобы сузить. `useState<User | null>(null)` — без явного типа TS выведет `null`.
- **Default type parameters.** `<T = string>` — если не передано, возьмётся по умолчанию. Полезно в универсальных хелперах.
- **Когда НЕ использовать generics.** Если параметр один и тип всегда известен — не лепите `<T>`. Generics нужны, когда функция действительно универсальна. Преждевременная универсализация = читать сложнее.

**`## Пример кода`** — блок ```ts:
```ts
// Простой generic
function identity<T>(x: T): T {
  return x;
}
identity(42);        // T = number
identity("hello");   // T = string
identity<boolean>(true); // явно

// Два параметра + ограничение
function pick<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}
const user = { id: 1, name: "Иван", age: 25 };
const name = pick(user, "name"); // string
// pick(user, "foo");            // ошибка: нет такого ключа

// Generic с constraint
interface HasId {
  id: number;
}
function findById<T extends HasId>(list: T[], id: number): T | undefined {
  return list.find(item => item.id === id);
}

// Generic в type
type Box<T> = { value: T };
const numBox: Box<number> = { value: 10 };
const strBox: Box<string> = { value: "hello" };

// Generic в React-компоненте
import { ReactNode } from "react";

function List<T>({ items, render }: {
  items: T[];
  render: (item: T) => ReactNode;
}) {
  return <ul>{items.map((item, i) => <li key={i}>{render(item)}</li>)}</ul>;
}

// Использование
<List
  items={[{ id: 1, name: "Иван" }]}
  render={(u) => u.name}  // u: { id: number; name: string }
/>

// Default generic
async function fetchJSON<T = unknown>(url: string): Promise<T> {
  const r = await fetch(url);
  return r.json();
}

const data = await fetchJSON<User[]>("/api/users"); // User[]
```

**`## Частые ошибки`** — 4 буллета:
- Пытаться использовать поля `T` без constraint: `function f<T>(x: T) { x.id }` — TS не знает, что `id` есть. Нужно `<T extends { id: ... }>`.
- Явно писать generic-параметр, когда TS выводит сам: `identity<number>(42)` — лишнее. Пусть выводит.
- Использовать `any` вместо generic: «ну типы сложные» — начни с одной буквы, TS поможет.
- Generics ради generics: если функция всегда принимает один конкретный тип — пиши этот тип, не `<T>`.

**`## Задания`:**
- [ ] Напиши `first<T>(arr: T[]): T | undefined` — TS должен вывести правильный тип.
- [ ] Generic-компонент `<Select<T>>` с props `options: T[]`, `value: T`, `onChange: (v: T) => void`.
- [ ] `fetchJSON<T>(url): Promise<T>` — используй в проекте с явным типом ответа.
- [ ] Напиши `pick<T, K extends keyof T>(obj, key)` — ограничение через `keyof`.

**`## Что почитать`:**
- [TS Handbook — Generics](https://www.typescriptlang.org/docs/handbook/2/generics.html)
- [TS Handbook — Keyof Type Operator](https://www.typescriptlang.org/docs/handbook/2/keyof-types.html)
- [Matt Pocock — Generics Tutorial](https://www.totaltypescript.com/tutorials/typescript-generics)
- [React + Generics](https://react-typescript-cheatsheet.netlify.app/docs/advanced/patterns_by_usecase/#generic-components)

Блок — `ts`.

---

## Task 6: Урок 11.5 — Utility types

**Create:** `FrontendCourse/11-TypeScript/11.5-Utility-types.md`

**Frontmatter:**
```yaml
---
модуль: 11-TypeScript
тема: Utility types
статус: to-read
roadmap: https://roadmap.sh/typescript
связано: [[11.4-Generics]], [[11.6-TS-и-React]]
---
```

**Заголовок:** `# Utility types`

**`## Зачем это нужно`:** У тебя есть тип `User` — а нужен такой же, но со всеми полями опциональными (для формы редактирования), или только 2 поля (для превью), или без пароля (для ответа API). Вручную переписывать — копипаста. Utility types — готовые генераторы типов из других типов.

**`## Главное` (~320-400 слов):** подразделы `###`:
- **Partial<T>.** Делает все поля опциональными. `Partial<User>` = `{ id?: number; name?: string }`. Для форм редактирования, patch-запросов.
- **Required<T>.** Противоположность Partial — все опциональные становятся обязательными.
- **Readonly<T>.** Все поля readonly. Защита от случайного изменения. Используется в `Object.freeze`-подобных паттернах.
- **Pick<T, K>.** Выбирает подмножество полей. `Pick<User, "id" | "name">` = `{ id: number; name: string }`. Для API-ответов, где возвращают только часть.
- **Omit<T, K>.** Убирает поля. `Omit<User, "password">` — всё, кроме `password`. Типичный паттерн для Response-типов.
- **Record<K, V>.** Объект-словарь. `Record<string, number>` = `{ [key: string]: number }`. `Record<"en" | "ru", string>` — гарантированные ключи.
- **ReturnType<F>.** Тип возвращаемого функцией. `type Result = ReturnType<typeof fetchUser>`. Полезно, когда не хочешь дублировать тип.
- **Parameters<F>.** Кортеж типов параметров функции. `Parameters<typeof fetchUser>` — массив типов аргументов.
- **Awaited<T>.** Разворачивает Promise: `Awaited<Promise<User>>` = `User`. Для `ReturnType<typeof asyncFn>` нужен `Awaited`, иначе получишь `Promise<User>`.
- **Exclude<U, E> и Extract<U, E>.** Работа с union: `Exclude<"a" | "b" | "c", "a">` = `"b" | "c"`. `Extract` — оставить только указанные.
- **NonNullable<T>.** Убирает `null` и `undefined`: `NonNullable<string | null>` = `string`. Часто после narrowing или в утилитах.
- **typeof и keyof.** `keyof User` = `"id" | "name" | "email"` — все ключи как union строк. `typeof user` — взять тип реального значения. Часто комбинируется с utility types: `Pick<User, keyof Partial<User>>`.

**`## Пример кода`** — блок ```ts:
```ts
type User = {
  id: number;
  name: string;
  email: string;
  password: string;
  role: "admin" | "user";
};

// Partial — для формы редактирования
type UserEdit = Partial<User>;
// { id?: number; name?: string; email?: string; password?: string; role?: ... }

// Pick — для превью
type UserPreview = Pick<User, "id" | "name">;

// Omit — для ответа API (без пароля)
type UserResponse = Omit<User, "password">;

// Readonly — защита от мутации
type FrozenUser = Readonly<User>;

// Record — словарь переводов
type Lang = "en" | "ru";
type Translations = Record<Lang, string>;
const t: Translations = { en: "Hello", ru: "Привет" };

// ReturnType и Awaited
async function fetchUser(id: number): Promise<User> {
  const r = await fetch(`/api/users/${id}`);
  return r.json();
}
type User2 = Awaited<ReturnType<typeof fetchUser>>; // User

// keyof
type UserKey = keyof User; // "id" | "name" | "email" | "password" | "role"

function getField<K extends UserKey>(user: User, key: K): User[K] {
  return user[key];
}

// Exclude
type PublicKey = Exclude<UserKey, "password">; // всё кроме password

// NonNullable
type Name = NonNullable<string | null>; // string

// Комбинация: «тип User без пароля, где все поля опциональные»
type EditForm = Partial<Omit<User, "id" | "password">>;
```

**`## Частые ошибки`** — 4 буллета:
- Дублировать тип вручную вместо `Partial`/`Omit` — при изменении базового типа забудешь обновить копию.
- `ReturnType<asyncFn>` без `Awaited` — получишь `Promise<User>` вместо `User`.
- `Pick<User, "some_string">` — ключ должен совпадать с полем. TS заругается, читай ошибку.
- Utility types не работают в рантайме — это только типы. Для получения полей объекта в коде — `Object.keys()`.

**`## Задания`:**
- [ ] Опиши `User` с 6 полями. Получи: `UserPreview` (2 поля), `UserResponse` (без пароля), `UserEdit` (все опциональные, без id).
- [ ] Напиши `Record<"primary" | "secondary" | "danger", string>` — карта цветов кнопок.
- [ ] Выведи тип ответа через `Awaited<ReturnType<typeof fetchUsers>>`. Используй в компоненте.
- [ ] Сделай `type KeysOf<T> = keyof T` — и generic-функцию `pick<T, K extends keyof T>(obj: T, ...keys: K[])`.

**`## Что почитать`:**
- [TS Handbook — Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html)
- [TS Handbook — Typeof Type Operator](https://www.typescriptlang.org/docs/handbook/2/typeof-types.html)
- [TS Handbook — Keyof Type Operator](https://www.typescriptlang.org/docs/handbook/2/keyof-types.html)
- [Matt Pocock — Utility Types](https://www.totaltypescript.com/category/utility-types)

Блок — `ts`.

---

## Task 7: Урок 11.6 — TS и React

**Create:** `FrontendCourse/11-TypeScript/11.6-TS-и-React.md`

**Frontmatter:**
```yaml
---
модуль: 11-TypeScript
тема: TS и React
статус: to-read
roadmap: https://roadmap.sh/typescript
связано: [[11.5-Utility-types]], [[11.7-Zod-inference-и-API]]
---
```

**Заголовок:** `# TS и React`

**`## Зачем это нужно`:** React + TS — индустриальный стандарт. Props типизированы — нельзя забыть обязательное поле. Events типизированы — сразу видно, что `e.target.value` — это строка. State-хуки типизированы — `useState<User | null>(null)` и TS сам знает, где проверять.

**`## Главное` (~340-420 слов):** подразделы `###`:
- **Типизация props.** `type Props = { title: string; onClick: () => void }`. В компоненте: `function Button({ title, onClick }: Props) { ... }`. Type или interface — см. 11.3.
- **Опциональные props.** `type Props = { label: string; variant?: "primary" | "secondary" }`. Внутри — `variant ?? "primary"` для дефолта.
- **children.** `children: ReactNode` — любой валидный JSX. `import { ReactNode } from "react"`. Иногда строже: `children: string` или `children: ReactElement`.
- **Props для HTML-элементов.** `ComponentPropsWithoutRef<"button">` — все стандартные props `<button>`. Удобно при обёртке нативных элементов: `type Props = ComponentPropsWithoutRef<"button"> & { variant: string }`.
- **useState.** `useState<User | null>(null)` — явный тип. Без него TS выведет тип из initial: `useState("")` = `string`. Уточняй, когда initial — `null` или пустой массив.
- **useEffect.** Без типов — хук сам типизирован. Главное — cleanup возвращает `void` или функцию (TS проверит).
- **useRef.** `useRef<HTMLInputElement>(null)`. Для DOM `ref.current: HTMLInputElement | null` — всегда проверяй на null.
- **useReducer.** `useReducer<Reducer<State, Action>>(reducer, initial)` или тип выводится из reducer. Типизируй `State` и `Action` (часто discriminated union — см. 11.3).
- **События.** `onChange: (e: ChangeEvent<HTMLInputElement>) => void`. Важные: `ChangeEvent`, `FormEvent`, `MouseEvent`, `KeyboardEvent`. Импорт из `react`.
- **useContext.** Типизируй через дефолт или generic: `const Ctx = createContext<Theme | null>(null)`. В `useTheme` — narrow + throw, чтобы возвращать строго `Theme`.
- **Generic-компоненты.** `function List<T>({ items, render }: { items: T[]; render: (t: T) => ReactNode })`. При использовании TS сам подставит `T`.
- **Типы от библиотек.** React Router, TanStack Query, RHF — все ship с типами. Например, `useQuery<User[]>(...)`, `UseFormReturn<FormData>`. Импортируй из пакетов, не пиши сам.

**`## Пример кода`** — блок ```tsx:
```tsx
import {
  useState, useRef, useEffect, ChangeEvent, FormEvent,
  ReactNode, ComponentPropsWithoutRef
} from "react";

// Простой компонент с props
type ButtonProps = {
  label: string;
  variant?: "primary" | "secondary";
  onClick: () => void;
};

function Button({ label, variant = "primary", onClick }: ButtonProps) {
  return (
    <button className={variant} onClick={onClick}>
      {label}
    </button>
  );
}

// Обёртка нативного <input>
type InputProps = ComponentPropsWithoutRef<"input"> & {
  label: string;
};

function Field({ label, ...rest }: InputProps) {
  return (
    <label>
      {label}
      <input {...rest} />
    </label>
  );
}

// useState + events
type User = { id: number; name: string };

function UserForm() {
  const [user, setUser] = useState<User | null>(null);
  const [name, setName] = useState("");
  const inputRef = useRef<HTMLInputElement>(null);

  useEffect(() => {
    inputRef.current?.focus();
  }, []);

  function handleChange(e: ChangeEvent<HTMLInputElement>) {
    setName(e.target.value);
  }

  function handleSubmit(e: FormEvent<HTMLFormElement>) {
    e.preventDefault();
    setUser({ id: Date.now(), name });
  }

  return (
    <form onSubmit={handleSubmit}>
      <input ref={inputRef} value={name} onChange={handleChange} />
      <Button label="OK" onClick={() => {}} />
      {user && <p>Добавлен: {user.name}</p>}
    </form>
  );
}

// children
function Card({ title, children }: { title: string; children: ReactNode }) {
  return (
    <div className="card">
      <h3>{title}</h3>
      {children}
    </div>
  );
}

// Generic-компонент
function List<T>({
  items,
  renderItem,
}: {
  items: T[];
  renderItem: (item: T) => ReactNode;
}) {
  return <ul>{items.map((item, i) => <li key={i}>{renderItem(item)}</li>)}</ul>;
}
```

**`## Частые ошибки`** — 4 буллета:
- `React.FC<Props>` — устаревший паттерн, неявно добавляет `children`. Современный React: просто `function X(props: Props)`.
- `useState([])` без generic — TS выведет `never[]`. Нужен `useState<User[]>([])`.
- `e: any` в обработчике — привет, весь смысл TS пропал. Используй правильный `ChangeEvent<...>`.
- `useRef(null)` без generic — `ref.current: null`. Укажи тип элемента: `useRef<HTMLInputElement>(null)`.

**`## Задания`:**
- [ ] Напиши типизированный `Button` с `variant`, `size`, `disabled`. Ошибка в IDE, если забыл обязательное поле.
- [ ] Форма с `useState<User | null>(null)`. При submit типизированный `FormEvent`.
- [ ] Generic-компонент `<List<T>>` с `renderItem`. Проверь, что TS подставляет тип автоматически.
- [ ] Обёртка `<Input label="..." type="text" placeholder="..." />` через `ComponentPropsWithoutRef<"input">`.

**`## Что почитать`:**
- [React + TypeScript Cheatsheet](https://react-typescript-cheatsheet.netlify.app/)
- [React docs — TypeScript](https://react.dev/learn/typescript)
- [TS + React — Matt Pocock](https://www.totaltypescript.com/tutorials/react-with-typescript)
- [Kent C. Dodds — How to write a React Component in TypeScript](https://kentcdodds.com/blog/how-to-write-a-react-component-in-typescript)

Блок — `tsx`.

---

## Task 8: Урок 11.7 — Zod inference и API

**Create:** `FrontendCourse/11-TypeScript/11.7-Zod-inference-и-API.md`

**Frontmatter:**
```yaml
---
модуль: 11-TypeScript
тема: Zod inference и типизация API
статус: to-read
roadmap: https://roadmap.sh/typescript
связано: [[11.6-TS-и-React]]
---
```

**Заголовок:** `# Zod inference и типизация API`

**`## Зачем это нужно`:** TS типы существуют только в коде — в рантайме их нет. Когда приходит ответ с API, TS безоружен: сервер может прислать что угодно, а ты считаешь, что там `User`. Zod — библиотека, которая валидирует данные в рантайме и выводит TS-тип из схемы. Одна схема = один источник правды для типа и для валидации.

**`## Главное` (~340-420 слов):** подразделы `###'`:
- **Проблема.** `const user = await fetch("/api/user").then(r => r.json())` — `user: any`. Ты типизируешь `as User`, но если сервер прислал мусор — падение где-то глубоко внутри.
- **Zod-схема.** `const UserSchema = z.object({ id: z.number(), name: z.string() })`. Описание не только структуры, но и правил: min, max, regex.
- **parse vs safeParse.** `UserSchema.parse(data)` — вернёт `User` или бросит исключение. `safeParse` вернёт `{ success, data | error }` — для обработки без try/catch.
- **z.infer<typeof Schema>.** Генерирует TS-тип из схемы. `type User = z.infer<typeof UserSchema>`. Одна правка в схеме — тип обновился везде.
- **Вложенные структуры.** `z.object({ user: UserSchema, posts: z.array(PostSchema) })`. Схемы композятся как LEGO.
- **Опциональные и nullable.** `z.string().optional()` = `string | undefined`. `z.string().nullable()` = `string | null`. `.nullish()` = `string | null | undefined`.
- **Enums и literals.** `z.enum(["light", "dark"])` или `z.literal("admin")`. Для union — `z.union([z.string(), z.number()])`.
- **Transform.** `z.string().transform(s => s.trim())` — нормализовать после валидации. Например, строка даты → `Date`.
- **Refine.** `z.string().refine(s => s.length > 0, "Пусто")` — кастомная проверка. Для более сложного: `z.object(...).refine(data => data.password === data.confirmPassword)`.
- **Типизация API.** В `fetchUser` — `UserSchema.parse(await r.json())`. Получаешь гарантированно валидный `User`. Если бэк сломал контракт — ошибка в своей ровной строке, а не в глубине UI.
- **Zod + TanStack Query.** `queryFn: async () => UserSchema.parse(await fetch(...).then(r => r.json()))`. Query.data автоматически типизирован как `User` через inference.
- **Zod + RHF.** Уже знаешь из 10.7: `zodResolver(schema)`. Типы формы выводятся из схемы через `z.infer`.

**`## Пример кода`** — блок ```ts:
```ts
import { z } from "zod";

// Схема
const UserSchema = z.object({
  id: z.number(),
  name: z.string().min(1),
  email: z.string().email(),
  role: z.enum(["admin", "user"]),
  createdAt: z.string().transform(s => new Date(s)),
});

// Тип — выводится автоматически
type User = z.infer<typeof UserSchema>;
// { id: number; name: string; email: string; role: "admin" | "user"; createdAt: Date }

// Массив
const UsersSchema = z.array(UserSchema);
type Users = z.infer<typeof UsersSchema>;

// Валидация API
async function fetchUser(id: number): Promise<User> {
  const res = await fetch(`/api/users/${id}`);
  const raw: unknown = await res.json();
  return UserSchema.parse(raw); // бросит ZodError, если не совпало
}

// safeParse — без исключений
function parseSafely(raw: unknown) {
  const result = UserSchema.safeParse(raw);
  if (!result.success) {
    console.error(result.error.issues);
    return null;
  }
  return result.data;
}

// Refine (кастомная проверка)
const SignupSchema = z.object({
  password: z.string().min(8),
  confirmPassword: z.string(),
}).refine(data => data.password === data.confirmPassword, {
  message: "Пароли не совпадают",
  path: ["confirmPassword"],
});
type Signup = z.infer<typeof SignupSchema>;

// Zod + TanStack Query
import { useQuery } from "@tanstack/react-query";

function useUser(id: number) {
  return useQuery({
    queryKey: ["user", id],
    queryFn: async () => {
      const raw: unknown = await fetch(`/api/users/${id}`).then(r => r.json());
      return UserSchema.parse(raw);
    },
  });
}
// useUser(1).data: User | undefined — типы работают
```

**`## Частые ошибки`** — 4 буллета:
- `UserSchema.parse(data) as User` — приведение лишнее, `parse` уже возвращает `User`. Просто `UserSchema.parse(data)`.
- Дублировать `type User` и `UserSchema` — забудешь обновить. Всегда `z.infer<typeof UserSchema>`.
- Использовать `parse` в React-компоненте прямо в рендере — бросит исключение, уронит UI. Вызывай в `queryFn` или loader-е.
- `z.any()` в схеме — теряешь смысл валидации. Опиши структуру точно.

**`## Задания`:**
- [ ] Опиши схему `Product` (id, title, price, category, description). Выведи тип через `z.infer`.
- [ ] Напиши `fetchProduct(id)` с `ProductSchema.parse`. Протестируй на сломанном JSON.
- [ ] Интегрируй Zod в `useQuery` из TanStack Query. Данные типизированы автоматически.
- [ ] Напиши схему регистрации с `refine` (password == confirmPassword). Используй в RHF.

**`## Что почитать`:**
- [Zod docs](https://zod.dev/)
- [Zod — Inference](https://zod.dev/?id=type-inference)
- [TkDodo — Validating API responses](https://tkdodo.eu/blog/zod-and-react-query)
- [Total TypeScript — Zod](https://www.totaltypescript.com/workshops/zod)

Блок — `ts`.

---

## Task 9: Мини-проект M11a — Рефакторинг M10 на TS

**Create:** `FrontendCourse/Проекты/Мини/M11a-Рефакторинг-M10-на-TS.md`

**Exact content:**

```markdown
---
тип: мини-проект
модуль: 11-TypeScript
статус: not-started
---

# M11a — Рефакторинг M10 на TypeScript

Первый мини-проект после модуля 11. Берёшь свой M10 SPA-магазин (JS) и переписываешь его на TypeScript. Цель — прочувствовать ценность TS на уже знакомом коде: сколько багов TS ловит, что упрощается, что ломается.

## Задача

Переписать все файлы проекта M10 из `.jsx` в `.tsx` (и `.js` → `.ts`), добавить типы для props, state, API, форм. Без `any`. Проект должен работать после рефакторинга точно так же, как раньше.

## Требования

### Функциональность
- Весь функционал M10 работает: роуты, каталог, корзина, checkout, персист.
- Деплой на Vercel (можно старый проект переключить на новую ветку/новый деплой).

### TypeScript-правила
1. **`strict: true` в tsconfig** — `noImplicitAny`, `strictNullChecks` и всё остальное из `strict`.
2. **Ноль `any`.** Если реально не можешь — `unknown` + narrowing. Комментарий с причиной, если оставляешь.
3. **Props типизированы** для каждого компонента через `type Props = { ... }` или `interface`.
4. **Типизирован Context.** `CartContext` — generic или явный тип, хук `useCart` выбрасывает при отсутствии Provider.
5. **API-ответы через zod.** Минимум `ProductSchema` для dummyjson. Тип продукта — через `z.infer`.
6. **TanStack Query с типами.** `useQuery<Product[]>` или автовывод через zod-parse в queryFn.
7. **Форма checkout — zod-схема + RHF с `zodResolver`.** Тип формы — `z.infer<typeof CheckoutSchema>`.
8. **useState с generic**, где initial не даёт однозначного вывода: `useState<User | null>(null)`, `useState<Product[]>([])`.
9. **События типизированы.** `ChangeEvent`, `FormEvent`, `MouseEvent` — вместо `any`.
10. **useRef с типом элемента.** `useRef<HTMLInputElement>(null)`.

### Технические правила
- `npm install -D typescript @types/node` (если не было).
- Обнови Vite-проект: `vite.config.ts`, переименуй `main.jsx` → `main.tsx`, `App.jsx` → `App.tsx`.
- Переноси по одному файлу: `.jsx` → `.tsx`, исправляй ошибки TS, продолжай.
- Добавь `"typecheck": "tsc --noEmit"` в `package.json`. Скрипт должен проходить без ошибок.
- README обнови: секция «TypeScript — что поменялось».

## Чего НЕ должно быть
- `any` (кроме явно обоснованных мест — с комментарием).
- Типа-мусора (`type Props = any`).
- `@ts-ignore` без обоснования.
- Импортов типов ради импортов — убирай неиспользуемое.

## Этапы

1. В копии M10 (`git checkout -b ts-refactor`) — `npm install -D typescript @types/node`.
2. Создай `tsconfig.json` (на базе Vite react-ts шаблона).
3. Переименуй `main.jsx` → `main.tsx`, `App.jsx` → `App.tsx`.
4. Один за другим — компоненты из `pages/` и `components/`. Типизируй props, state, events.
5. Context (`CartContext`) — типизируй generic-ом, переведи в `.tsx`.
6. API-слой: создай `schemas/product.ts` с zod-схемой. Переведи `useProducts` на zod-parse.
7. Форма checkout: вынеси `CheckoutSchema` + `type CheckoutForm = z.infer<...>`.
8. Прогони `npm run typecheck` — исправь все ошибки.
9. Убедись, что приложение работает: `npm run dev`, пройдись по всему flow.
10. Деплой. Обнови README: что было, что стало.

## Сдача
1. Публичный GitHub-репозиторий (новый или ветка в старом).
2. Прод-URL (HTTPS).
3. README: секция «TS-рефакторинг: что улучшилось». Минимум 3 конкретных бага, которые TS помог найти, или места, где типы сделали код понятнее.
4. `package.json`: скрипт `typecheck`.

## Критерии приёмки ревью
- [ ] `tsconfig.json` с `strict: true`.
- [ ] `npm run typecheck` проходит без ошибок.
- [ ] Нет `any` без комментария.
- [ ] Props всех компонентов типизированы.
- [ ] Context типизирован + хук с защитой от отсутствия Provider.
- [ ] Zod-схема для API-ответа (минимум Product).
- [ ] Форма checkout: `zodResolver` + `z.infer` для типа формы.
- [ ] `useState<T>` с явным типом там, где TS не выводит.
- [ ] Функциональность M10 не сломана.
- [ ] Прод работает.

## Что дальше
После этого — **M11b Pokédex на TS** с нуля. Там TS сразу проектируется, а не ретроспективно.
```

---

## Task 10: Мини-проект M11b — Pokédex на TS

**Create:** `FrontendCourse/Проекты/Мини/M11b-Pokedex-на-TS.md`

**Exact content:**

```markdown
---
тип: мини-проект
модуль: 11-TypeScript
статус: not-started
---

# M11b — Pokédex на TS

Второй мини-проект после модуля 11. Новый проект с нуля на TypeScript — без шаблона «переписать на TS». Здесь ты проектируешь типы сразу. Данные — с [PokéAPI](https://pokeapi.co/).

## Задача

Web-приложение Pokédex: список покемонов, страница покемона, избранное в localStorage. Полноценный TS-стек: strict, zod для схем API, типизированные хуки, generic-компоненты.

## Требования

### Функциональность
1. **Список покемонов** — первые 151 (или пагинация по 20). Карточка: имя, картинка, типы, номер.
2. **Страница покемона** — `/pokemon/:name` — полная инфа: stats (HP, Attack, Defense…), abilities, sprite.
3. **Поиск** — по имени, debounce 300мс.
4. **Фильтр по типу** — water/fire/grass/… — через `useSearchParams`.
5. **Избранное** — сердечко на карточке, отдельная страница `/favorites`. Persist в localStorage.
6. **Роуты:** `/` (список), `/pokemon/:name`, `/favorites`, `*` (404).
7. **Деплой** — Vercel.

### TypeScript/архитектура
- `strict: true`, ноль `any`.
- Zod-схемы для ответов PokéAPI: `PokemonListSchema`, `PokemonSchema`, `PokemonTypeSchema`.
- Типы — через `z.infer`, не дублируй.
- Generic-хук: свой `useLocalStorage<T>(key, initial)` с типизацией.
- Generic-компонент: `List<T>` или `Grid<T>` с `renderItem`.
- TanStack Query с автовыводом типа через zod-parse в queryFn.
- React Router: типизированные `useParams<{ name: string }>()` (или с обёрткой).
- Context для избранного (или zustand — тоже ок, но Context достаточно) — типизирован.

### Технические правила
- `npm create vite@latest pokedex-ts -- --template react-ts`.
- `@tanstack/react-query`, `react-router-dom`, `zod`.
- `"typecheck": "tsc --noEmit"` в `package.json`.
- Адаптивный layout (mobile + desktop).

## Чего НЕ должно быть
- `any` без комментария-обоснования.
- `as` для приведения API-ответа — используй zod-parse.
- Дублирования типов: если есть zod-схема — тип выводится через `z.infer`.
- Прямого fetch в компоненте — всё через хуки (useQuery или кастомный).
- UI-библиотек (MUI, Chakra) — свои компоненты + CSS.

## Этапы

1. `npm create vite@latest pokedex-ts -- --template react-ts` + установи: `react-router-dom`, `@tanstack/react-query`, `@tanstack/react-query-devtools`, `zod`.
2. Проверь `tsconfig.json` — `strict: true`.
3. Спроектируй папки: `pages/`, `components/`, `hooks/`, `schemas/`, `context/`.
4. `schemas/pokemon.ts` — `PokemonListItemSchema`, `PokemonSchema` под PokéAPI. `z.infer` для типов.
5. `hooks/usePokemons.ts` — TanStack Query, zod-parse. `usePokemon(name: string)` — тоже.
6. `hooks/useLocalStorage.ts` — generic `<T>(key: string, initial: T): [T, (v: T) => void]`.
7. `context/FavoritesContext.tsx` — типизированный провайдер + хук `useFavorites`.
8. Роуты: `/`, `/pokemon/:name`, `/favorites`, 404.
9. `components/PokemonCard.tsx`, `components/Grid.tsx` (generic), `components/TypeBadge.tsx`, `components/SearchBar.tsx`.
10. Страницы: `PokemonsPage`, `PokemonPage`, `FavoritesPage`, `NotFoundPage`.
11. Стили — CSS-модули или просто CSS.
12. `npm run typecheck` → ноль ошибок. Деплой.

## Структура проекта (ориентир)
```
src/
├── main.tsx
├── App.tsx
├── pages/
│   ├── PokemonsPage.tsx
│   ├── PokemonPage.tsx
│   ├── FavoritesPage.tsx
│   └── NotFoundPage.tsx
├── components/
│   ├── PokemonCard.tsx
│   ├── Grid.tsx           # generic
│   ├── TypeBadge.tsx
│   └── SearchBar.tsx
├── hooks/
│   ├── usePokemons.ts
│   ├── usePokemon.ts
│   ├── useLocalStorage.ts # generic
│   └── useDebounce.ts
├── context/
│   └── FavoritesContext.tsx
└── schemas/
    └── pokemon.ts
```

## Сдача
1. Публичный GitHub-репозиторий.
2. Прод-URL (HTTPS).
3. README: стек, структура, ссылки, 2-3 скриншота, «сложные места».
4. На созвоне — проходим типы по схемам и generic-хукам.

## Критерии приёмки ревью
- [ ] `strict: true`, `typecheck` проходит.
- [ ] Zod-схемы для PokéAPI, типы через `z.infer`.
- [ ] Generic-хук `useLocalStorage<T>`.
- [ ] Generic-компонент (Grid/List с `renderItem`).
- [ ] TanStack Query с типизированным data (через zod-parse).
- [ ] Context с type-guarded хуком.
- [ ] Поиск + фильтр через `useSearchParams`.
- [ ] Избранное persist в localStorage.
- [ ] Ноль `any` без обоснования.
- [ ] Прод работает, 151 покемон есть (или работает пагинация).

## Что дальше
Дальше — **модуль 12 Build tools и тестирование**: Vite в деталях, ESLint/Prettier, Vitest, Testing Library, Playwright. Добавим зелёную планку «тесты проходят» к twoim проектам.
```

---

## Task 11: Заполнить MOC-TS

**Modify:** `FrontendCourse/MOC/MOC-TS.md`

Заменить содержимое полностью.

**Exact content:**

```markdown
---
тип: MOC
тема: TypeScript
---

# MOC — TypeScript

Карта знаний по TypeScript. Заполняется в модуле 11.

## Основы (модуль 11)
- [[11.1-Зачем-TS-и-setup]]
- [[11.2-Базовые-типы]]
- [[11.3-Aliases-interfaces-unions]]
- [[11.4-Generics]]
- [[11.5-Utility-types]]

## TS в React и API (модуль 11)
- [[11.6-TS-и-React]]
- [[11.7-Zod-inference-и-API]]

## Практика
- [[M11a-Рефакторинг-M10-на-TS]] — прикладной рефакторинг знакомого проекта на TS.
- [[M11b-Pokedex-на-TS]] — новый TS-проект с нуля.
```

---

## Task 12: Обновить 00-Start-Here.md

**Modify:** `FrontendCourse/00-Start-Here.md`

Убрать «_(скоро)_» у модуля 11:
`- [[11-TypeScript/00-Обзор-модуля|Модуль 11 — TypeScript]] _(скоро)_` → `- [[11-TypeScript/00-Обзор-модуля|Модуль 11 — TypeScript]]`.

---

## Task 13: Верификация

- [ ] `FrontendCourse/11-TypeScript/` содержит 8 `.md` файлов.
- [ ] `M11a-Рефакторинг-M10-на-TS.md` и `M11b-Pokedex-на-TS.md` существуют в `Проекты/Мини/`.
- [ ] `MOC-TS.md` содержит 7 ссылок на уроки + 2 ссылки на M11a/M11b.
- [ ] В `00-Start-Here.md` у модуля 11 нет «_(скоро)_».
- [ ] Отчитаться: модуль 11 готов.

---

## Out of Scope

- Продвинутые типы (conditional types, mapped types, template literal types) — обзорно в М14, если успеем.
- Тесты и Vitest + TS — модуль 12.
- Серверный TS (Next.js API routes, Node) — модуль 13.
- Декораторы, классы (TS классами) — не нужно для фронтенда.
