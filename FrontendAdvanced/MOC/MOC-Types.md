---
тип: MOC
тема: TypeScript Mastery
---

# MOC — Types

Карта знаний Track 2: TypeScript не как «аннотации к JS», а как инструмент дизайна. Три модуля — type-level программирование, precision-типы для ловли багов, DX библиотечных типов.

Используй эту карту как навигатор: ссылки из «Что почитать» соседних уроков часто ведут сюда.

## A2.1 — Type-level Programming

Типы как отдельный язык. Условная логика, мапинги ключей, строковые шаблоны, рекурсии.

- [[../A2-TypeScript-Mastery/A2.1-Type-level-Programming/A2.1.1-Conditional-types-и-distributivity|A2.1.1 — Conditional types и distributivity]]
- [[../A2-TypeScript-Mastery/A2.1-Type-level-Programming/A2.1.2-Mapped-types-и-key-remapping|A2.1.2 — Mapped types и key remapping]]
- [[../A2-TypeScript-Mastery/A2.1-Type-level-Programming/A2.1.3-Template-literal-types|A2.1.3 — Template literal types]]
- [[../A2-TypeScript-Mastery/A2.1-Type-level-Programming/A2.1.4-Recursive-types|A2.1.4 — Recursive types]]
- [[../A2-TypeScript-Mastery/A2.1-Type-level-Programming/A2.1.5-infer-в-глубине|A2.1.5 — infer в глубине]]
- [[../A2-TypeScript-Mastery/A2.1-Type-level-Programming/A2.1.6-Variance-и-модификаторы|A2.1.6 — Variance и модификаторы]]
- [[../A2-TypeScript-Mastery/A2.1-Type-level-Programming/A2.1.7-Свои-type-level-утилиты|A2.1.7 — Свои type-level утилиты]]

## A2.2 — Precision Types

Типы, которые ловят баги, а не «просто лучше, чем `any`». Как сделать так, чтобы компилятор работал на тебя.

- [[../A2-TypeScript-Mastery/A2.2-Precision-Types/A2.2.1-Branded-types|A2.2.1 — Branded types]]
- [[../A2-TypeScript-Mastery/A2.2-Precision-Types/A2.2.2-const-assertions|A2.2.2 — const assertions и literal widening]]
- [[../A2-TypeScript-Mastery/A2.2-Precision-Types/A2.2.3-Discriminated-Unions|A2.2.3 — Discriminated Unions и exhaustiveness]]
- [[../A2-TypeScript-Mastery/A2.2-Precision-Types/A2.2.4-satisfies-operator|A2.2.4 — satisfies operator]]
- [[../A2-TypeScript-Mastery/A2.2-Precision-Types/A2.2.5-unknown-vs-any-vs-never|A2.2.5 — unknown vs any vs never]]
- [[../A2-TypeScript-Mastery/A2.2-Precision-Types/A2.2.6-Type-guards-и-assertion-functions|A2.2.6 — Type guards и assertion functions]]

## A2.3 — Библиотечный DX

Пишем типы так, чтобы IDE выдавала хорошие подсказки пользователям твоей библиотеки. Именно это отличает library-автора от consumer-а.

- [[../A2-TypeScript-Mastery/A2.3-Библиотечный-DX/A2.3.1-Overloads-vs-union|A2.3.1 — Overloads vs union]]
- [[../A2-TypeScript-Mastery/A2.3-Библиотечный-DX/A2.3.2-Generic-constraints-и-defaults|A2.3.2 — Generic constraints и defaults]]
- [[../A2-TypeScript-Mastery/A2.3-Библиотечный-DX/A2.3.3-Declaration-merging-и-augmentation|A2.3.3 — Declaration merging и augmentation]]
- [[../A2-TypeScript-Mastery/A2.3-Библиотечный-DX/A2.3.4-NoInfer-и-управление-выводом|A2.3.4 — NoInfer и управление выводом]]
- [[../A2-TypeScript-Mastery/A2.3-Библиотечный-DX/A2.3.5-TSDoc-и-tooltips|A2.3.5 — TSDoc и tooltips]]

## Практика

- **A-P1 Performance Rescue** ссылается сюда через типы точных API-границ (если проект с TS).
- **A-P2 Monorepo Platform** _(скоро)_ — типы поверх shared packages, augmentation в tsconfig paths.

## Связанные темы в других MOC

- [[MOC-Internals]] — V8 runtime работает с теми самыми значениями, которые ты описываешь типами.
