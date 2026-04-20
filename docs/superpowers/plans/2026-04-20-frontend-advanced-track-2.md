# Frontend Advanced — Track 2 (TypeScript Mastery) Implementation Plan

> **For agentic workers:** execute task-by-task через параллельные dispatch-и sub-агентов по модулю. Итоговые уроки проходят грепо-проверку на 6 секций + канонический frontmatter + пояснения англицизмов.

**Goal:** Track 2 «TypeScript Mastery» — три модуля (Type-level Programming, Precision Types, Библиотечный DX), 18 уроков, 3 обзора, обновление `00-Start-Here` и новый `MOC-Types`. После прохождения middle-разработчик умеет думать типами, а не «ставить типы».

**Architecture:** Тот же формат, что Track 1. Vault `FrontendAdvanced/`, 6-секционный шаблон урока (Зачем → Главное → Пример кода → Частые ошибки → Задания → Что почитать), «Главное» 500–1000 слов, тон — ментор-практик, «ты». Все англицизмы поясняются в скобках при первом появлении в файле (feedback-правило).

**Tech Stack:** TypeScript 5.6+ (стабильные фичи 2025–2026: `NoInfer`, typed `await`, `satisfies` в выражениях, tail-recursive conditional types). Примеры — React/TS-прикладные, а не абстрактные. Где уместно — ссылки на `type-fest`, Zod, Effect, tRPC как ориентиры на реальный library DX.

**Пути:**
- Track 2: `FrontendAdvanced/A2-TypeScript-Mastery/`
- MOC: `FrontendAdvanced/MOC/MOC-Types.md`

**Каноничный frontmatter:**
```yaml
---
тип: урок
трек: A2-TypeScript-Mastery
модуль: A2.X-<имя>
урок: A2.X.Y
статус: to-read
---
```

---

## File Structure

```
FrontendAdvanced/
├── 00-Start-Here.md            # обновить: Track 2 теперь «готов»
├── A2-TypeScript-Mastery/
│   ├── A2.1-Type-level-Programming/
│   │   ├── 00-Обзор-модуля.md
│   │   ├── A2.1.1-Conditional-types-и-distributivity.md
│   │   ├── A2.1.2-Mapped-types-и-key-remapping.md
│   │   ├── A2.1.3-Template-literal-types.md
│   │   ├── A2.1.4-Recursive-types.md
│   │   ├── A2.1.5-infer-в-глубине.md
│   │   ├── A2.1.6-Variance-и-модификаторы.md
│   │   └── A2.1.7-Свои-type-level-утилиты.md
│   ├── A2.2-Precision-Types/
│   │   ├── 00-Обзор-модуля.md
│   │   ├── A2.2.1-Branded-types.md
│   │   ├── A2.2.2-const-assertions.md
│   │   ├── A2.2.3-Discriminated-Unions.md
│   │   ├── A2.2.4-satisfies-operator.md
│   │   ├── A2.2.5-unknown-vs-any-vs-never.md
│   │   └── A2.2.6-Type-guards-и-assertion-functions.md
│   └── A2.3-Библиотечный-DX/
│       ├── 00-Обзор-модуля.md
│       ├── A2.3.1-Overloads-vs-union.md
│       ├── A2.3.2-Generic-constraints-и-defaults.md
│       ├── A2.3.3-Declaration-merging-и-augmentation.md
│       ├── A2.3.4-NoInfer-и-управление-выводом.md
│       └── A2.3.5-TSDoc-и-tooltips.md
└── MOC/
    └── MOC-Types.md
```

**Итого новых/обновлённых файлов:** 1 обновление + 3 × (1 обзор + 5–7 уроков) + 1 MOC = **24 файла**.

---

## Темы уроков — ключевые концепты (для субагентов)

### Module A2.1 — Type-level Programming

**Цель модуля:** научить мыслить про тип как про программу. В конце модуля студент читает `type-fest` без паники и пишет свои утилиты.

| Урок | Ключевые концепты «Главное» (500–1000 слов) |
|---|---|
| A2.1.1 Conditional types и distributivity | `T extends U ? X : Y`, naked type parameter, distributive conditional types над union-ами, трюк `[T] extends [U]` для отключения дистрибутивности, `Exclude/Extract` как встроенные примеры, практический пример — фильтрация ключей |
| A2.1.2 Mapped types и key remapping | `{ [K in keyof T]: ... }`, `as` clause (TS 4.1+), `readonly`/`?` модификаторы и их снятие через `-readonly`/`-?`, homomorphic vs non-homomorphic mapped types, реальные утилиты — `PickBy`, `MutableOnly` |
| A2.1.3 Template literal types | `` `${A}-${B}` `` типы, distribution при union-ах внутри, `infer` внутри TL, `Uppercase/Lowercase/Capitalize/Uncapitalize`, парсинг роутов (`/users/:id` → `{ id: string }`), ограничения (quadratic blow-up, TS 5.0 улучшения) |
| A2.1.4 Recursive types | Рекурсия в conditional types, `instantiation depth limit` и ошибка «Type instantiation is excessively deep», tail-recursive conditional types (TS 4.5+), `TupleToUnion`, `Length`, `Reverse`, `Join` — работа с кортежами, trade-off «глубокая рекурсия vs читаемость» |
| A2.1.5 infer в глубине | `infer` в conditional types, вытаскивание: `ReturnType`, `Parameters`, `Awaited`, `ConstructorParameters`, `infer` с constraint (TS 4.7 `infer X extends Y`), множественные `infer` в одном шаблоне, infer в template literals |
| A2.1.6 Variance и модификаторы | Что такое co-/contra-/bi-/invariant, почему методы bivariant по умолчанию (`strictFunctionTypes`), `in`/`out`/`in out` модификаторы generic-параметров (TS 4.7+), практический пример — как это ломает типизацию «общих» колбеков |
| A2.1.7 Свои type-level утилиты | Написать с нуля: `IsEqual<A, B>`, `IsNever`, `UnionToIntersection`, `UnionToTuple` (через intersection + infer), `Prettify<T>` (для красивых hover-тултипов), `DeepPartial/DeepReadonly`, `Merge<A, B>` с правильной семантикой override, `Simplify` |

### Module A2.2 — Precision Types

**Цель модуля:** перестать писать `string` там, где на самом деле `UserId`. Использовать TS как инструмент дисциплины, а не «шумовой фильтр».

| Урок | Ключевые концепты |
|---|---|
| A2.2.1 Branded types | Nominal typing в структурной системе TS, `type UserId = string & { readonly __brand: unique symbol }`, нулевой runtime-cost, pattern «валидация → brand → типобезопасный результат», `Brand<T, 'Name'>` helper, когда это overkill |
| A2.2.2 const assertions | `as const` и literal widening, разница `let x = 'a'` (widening) vs `x as const` (narrow), `as const satisfies`, deep readonly через `as const`, практика: конфиги, enum-замена, discriminated union literal-тэги |
| A2.2.3 Discriminated Unions | Дискриминатор-поле, `switch` exhaustiveness + `assertNever(x: never)` для compile-time гарантии, почему `if/else` хуже `switch` для проверки, factory-функции, паттерн Result<T, E>, Zod и автоматический discriminator |
| A2.2.4 satisfies operator | Зачем satisfies (TS 4.9+): проверка соответствия типу без widening, разница с annotation `:`, с `as`, с `as const`, pattern «объявил контракт — сохранил точный тип для consumers», сочетание `as const satisfies X` |
| A2.2.5 unknown vs any vs never | `any` отключает проверки, `unknown` требует narrow-а перед использованием, `never` — пустой тип (отсутствие значений), практические правила: `unknown` для API-границ, `never` для exhaustiveness, `any` почти никогда |
| A2.2.6 Type guards и assertion functions | User-defined type guard `x is Type`, assertion function `asserts x is Type`, разница с `as` cast, интеграция с control flow analysis, Zod `.parse` как assertion, кастомные guards для discriminated union-ов |

### Module A2.3 — Библиотечный DX

**Цель модуля:** писать библиотеки, которые приятно использовать — хорошие hover-тултипы, точные автокомплиты, ошибки по делу. Именно это отличает library-автора от consumer-а.

| Урок | Ключевые концепты |
|---|---|
| A2.3.1 Overloads vs union | Function overloads (`function f(x: A): R1; function f(x: B): R2;`), когда они реально нужны (return-тип зависит от argument-типа без conditional), когда лучше union-тип, когда conditional return type, сравнение DX для consumer-а |
| A2.3.2 Generic constraints и defaults | `T extends X`, `T extends X = Default`, почему дефолты работают на границе — когда ты хочешь, чтобы `f()` работало без явных generics, `const` type parameters (TS 5.0), inference hints через `NoInfer<>` (см. след. урок) |
| A2.3.3 Declaration merging и augmentation | Module augmentation: `declare module 'x' { ... }`, глобальные расширения `declare global`, реальные случаи — расширить `React.HTMLAttributes`, `Window`, `ProcessEnv`, интеграция с TypeScript plugin-ами библиотек (styled-components `DefaultTheme`, CSS Modules) |
| A2.3.4 NoInfer и управление выводом | `NoInfer<T>` (TS 5.4+), как исключить параметр из inference site, классический пример `function addKeys<T>(obj: T, keys: NoInfer<keyof T>[])`, const type parameters, `InferIn`/`InferOut` паттерны из Zod/Effect, когда инженеру нужно ручное управление вывода |
| A2.3.5 TSDoc и tooltips | `@param`, `@returns`, `@example`, `@deprecated`, `@see`, как VS Code рендерит markdown в hover, `@remarks`, `@default`, `@internal` (с api-extractor), релиз-заметки к публичному API, TSDoc vs JSDoc различия, `declarationMap`/`declaration` в tsconfig |

---

## Task 1: Scaffold Track 2 + обновить Start-Here

**Files:**
- Update: `FrontendAdvanced/00-Start-Here.md` — Track 2 из «скоро» в «готов», добавить ссылки на обзоры модулей A2.1–A2.3.
- Create: `FrontendAdvanced/MOC/MOC-Types.md` — полный индекс 18 уроков Track 2 с описанием каждого.

**Steps:**

- [ ] **Step 1:** Обновить `00-Start-Here.md`: пометить Track 2 как готовый, добавить блок с прямыми ссылками на A2.1/A2.2/A2.3 обзоры, добавить `MOC-Types.md` в секцию MOC.

- [ ] **Step 2:** Написать `MOC-Types.md` по образцу `MOC-Internals.md` — оглавление с тремя модулями и полным списком уроков, где каждый урок — одна строка вида `[[A2.1.1-Conditional-types-и-distributivity|A2.1.1 Conditional types]] — зачем и когда`. Длина — до 150 строк.

- [ ] **Step 3:** Проверить, что ссылки резолвятся в Obsidian-стиле (wikilinks без абсолютных путей).

## Task 2: Module A2.1 — Type-level Programming (8 файлов)

**Dispatch:** один subagent на весь модуль. Он создаёт `00-Обзор-модуля.md` + 7 уроков по темам из таблицы выше. Обзор — краткий: «Зачем», карта уроков, что студент будет уметь в конце, указатель на следующий модуль A2.2.

**Steps:**

- [ ] **Step 1:** Dispatch subagent с задачей — создать 8 файлов в `FrontendAdvanced/A2-TypeScript-Mastery/A2.1-Type-level-Programming/`. На входе у субагента: описание темы каждого урока (из таблицы), шаблон 6-секций, канонический frontmatter, правило про англицизмы.

- [ ] **Step 2:** Post-dispatch greep-проверка:
  - все 8 файлов существуют
  - каждый урок содержит секции `## Зачем`, `## Главное`, `## Пример кода`, `## Частые ошибки`, `## Задания`, `## Что почитать`
  - frontmatter canonical (5 полей: тип/трек/модуль/урок/статус)
  - «Главное» — 500–1000 слов (грубо через `wc -w` на соответствующем участке)
  - англицизмы с пояснениями: точечная выборочная проверка

- [ ] **Step 3:** Если что-то не так — fix-subagent с точечным списком нарушений.

## Task 3: Module A2.2 — Precision Types (7 файлов)

То же, что Task 2, но для A2.2 — 6 уроков + обзор.

- [ ] **Step 1:** Dispatch subagent на `A2.2-Precision-Types/`.
- [ ] **Step 2:** Greep-проверка.
- [ ] **Step 3:** Fix-subagent по необходимости.

## Task 4: Module A2.3 — Библиотечный DX (6 файлов)

То же для A2.3 — 5 уроков + обзор.

- [ ] **Step 1:** Dispatch subagent на `A2.3-Библиотечный-DX/`.
- [ ] **Step 2:** Greep-проверка.
- [ ] **Step 3:** Fix-subagent по необходимости.

## Task 5: Retro + переход

- [ ] **Step 1:** Финальная проверка: все 24 файла на месте, frontmatter унифицирован, секции есть, англицизмы пояснены. Автоматизировать через bash + `head -N` / `grep`.
- [ ] **Step 2:** Обновить MOC-Types и 00-Start-Here с реальным статусом.
- [ ] **Step 3:** Сохранить краткий retro-документ (в памяти, не в файл) — что получилось, что пошло не так, поправки для Track 3.

---

## Конвенции для всех subagent-ов

**При создании файла каждый subagent обязан:**

1. Frontmatter — строго 5 полей (тип/трек/модуль/урок/статус), без уровня/длительности/аудитории.
2. Заголовок — `# A2.X.Y — <Тема>` (тире длинное — em dash, не минус).
3. 6 секций в порядке: `## Зачем` → `## Главное` → `## Пример кода` → `## Частые ошибки` → `## Задания` → `## Что почитать`.
4. «Главное» — 500–1000 слов. Подразделы `### …` допустимы и приветствуются (облегчают навигацию).
5. Тон — «ты», ментор-практик, без снисходительности и без академического языка.
6. **Англицизмы — с пояснениями в скобках при первом появлении в файле.**
   - Хорошо: «Covariance (ковариантность — подтип в одной позиции приводит к подтипу и в результате) — это…»
   - Плохо: вываливать три термина в ряд без пояснений.
   - Не пояснять: общеизвестные (TS, JS, React, props, state, type, interface, generic).
7. Код в примерах — реальный, на TS 5.6+, с импортами и осмысленными именами. Не «foo/bar».
8. «Частые ошибки» — 3–5 конкретных кейсов с кодом-«как не надо» + «как правильно».
9. «Задания» — 2–3 задачи разного уровня (recall, понимание, приложение).
10. «Что почитать» — 2–4 ссылки: TS Handbook, тикеты PR в microsoft/TypeScript, статьи от Matt Pocock / Tanner Linsley / type-fest / Effect, по месту.

**Запрещено:**
- Emoji в тексте уроков.
- Английские термины без пояснений при первом появлении (кроме общеизвестных).
- Заимствование фраз из предыдущих уроков (каждый файл пишется с нуля по теме).
- Встраивание «любезностей» типа «Отличный вопрос!» — стиль мануальный, не разговорный.

## Критерии готовности Track 2

- 24 файла на местах.
- Все уроки проходят 6-секционный grep.
- MOC-Types + Start-Here обновлены.
- Англицизмы пояснены (выборочная проверка).
- Студент, прочитавший Track 2 целиком, умеет: написать branded type, читать `type-fest`, построить свой generic с defaults + NoInfer, понимать когда satisfies лучше annotation, различать unknown/any/never по правилам.

## Self-Review (для controller-а)

- [ ] Каждая тема в таблице даёт достаточно материала на 500–1000 слов «Главное».
- [ ] Нет дублей между уроками (например, `satisfies` живёт в A2.2.4, но не упоминается как «главная фича» в A2.2.2).
- [ ] Уроки упорядочены от простого к сложному внутри модуля.
- [ ] Модули упорядочены по зависимости: A2.1 даёт базу, A2.2 применяет, A2.3 использует обе.
