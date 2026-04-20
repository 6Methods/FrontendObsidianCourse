---
тип: MOC
тема: Архитектура и масштаб
---

# MOC — Architecture

Карта знаний Track 3: как писать код, который переживёт 10+ разработчиков, 3 года и два пивота. Шесть модулей — FSD для смысла, monorepo для инструмента, micro-frontends для крайнего случая, legacy для реальности, testing для уверенности, accessibility как hygiene factor.

Используй эту карту как навигатор: ссылки из «Что почитать» соседних уроков часто ведут сюда.

## A3.1 — Feature-Sliced Design

Архитектурная методология, которая делит код по бизнес-смыслу, а не по техническим слоям. Главное — понять, когда она оправдана, а когда добавляет шум.

- [[../A3-Архитектура-и-масштаб/A3.1-Feature-Sliced-Design/A3.1.1-Слои-FSD-и-их-назначение|A3.1.1 — Слои FSD и их назначение]]
- [[../A3-Архитектура-и-масштаб/A3.1-Feature-Sliced-Design/A3.1.2-Public-API-и-правила-импортов|A3.1.2 — Public API и правила импортов]]
- [[../A3-Архитектура-и-масштаб/A3.1-Feature-Sliced-Design/A3.1.3-Feature-как-единица-продукта|A3.1.3 — Feature как единица продукта]]
- [[../A3-Архитектура-и-масштаб/A3.1-Feature-Sliced-Design/A3.1.4-Entities-и-модель-домена|A3.1.4 — Entities и модель домена]]
- [[../A3-Архитектура-и-масштаб/A3.1-Feature-Sliced-Design/A3.1.5-Рефакторинг-из-legacy-в-FSD|A3.1.5 — Рефакторинг из legacy в FSD]]
- [[../A3-Архитектура-и-масштаб/A3.1-Feature-Sliced-Design/A3.1.6-FSD-в-Next-js-App-Router|A3.1.6 — FSD в Next.js App Router]]

## A3.2 — Monorepo на Turborepo

Один репозиторий для нескольких пакетов — когда это экономит время команды, а когда добавляет боли. Turborepo + pnpm + changesets как рабочий стек 2026.

- [[../A3-Архитектура-и-масштаб/A3.2-Monorepo-на-Turborepo/A3.2.1-Зачем-monorepo-и-когда-нет|A3.2.1 — Зачем monorepo и когда нет]]
- [[../A3-Архитектура-и-масштаб/A3.2-Monorepo-на-Turborepo/A3.2.2-Turborepo-pipeline-и-cache|A3.2.2 — Turborepo pipeline и cache]]
- [[../A3-Архитектура-и-масштаб/A3.2-Monorepo-на-Turborepo/A3.2.3-pnpm-workspaces-и-catalog|A3.2.3 — pnpm workspaces и catalog]]
- [[../A3-Архитектура-и-масштаб/A3.2-Monorepo-на-Turborepo/A3.2.4-Shared-packages|A3.2.4 — Shared packages]]
- [[../A3-Архитектура-и-масштаб/A3.2-Monorepo-на-Turborepo/A3.2.5-Changesets-и-версионирование|A3.2.5 — Changesets и версионирование]]
- [[../A3-Архитектура-и-масштаб/A3.2-Monorepo-на-Turborepo/A3.2.6-CI-на-monorepo|A3.2.6 — CI на monorepo]]

## A3.3 — Micro-frontends

Крайний случай архитектуры. В большинстве команд MF не нужны — и этот модуль объясняет почему честно, а не продаёт идею.

- [[../A3-Архитектура-и-масштаб/A3.3-Micro-frontends/A3.3.1-Когда-MF-оправданы|A3.3.1 — Когда MF оправданы]]
- [[../A3-Архитектура-и-масштаб/A3.3-Micro-frontends/A3.3.2-Module-Federation-механика|A3.3.2 — Module Federation: механика]]
- [[../A3-Архитектура-и-масштаб/A3.3-Micro-frontends/A3.3.3-Independent-deployment-и-shared-state|A3.3.3 — Independent deployment и shared state]]
- [[../A3-Архитектура-и-масштаб/A3.3-Micro-frontends/A3.3.4-Routing-между-MF|A3.3.4 — Routing между MF]]
- [[../A3-Архитектура-и-масштаб/A3.3-Micro-frontends/A3.3.5-MF-vs-monorepo-гибрид|A3.3.5 — MF vs monorepo — гибрид]]

## A3.4 — Legacy и рефакторинг

Как жить с унаследованным кодом. Когда переписывать, когда страдать и терпеть, как измерить прогресс и как защитить решение перед бизнесом.

- [[../A3-Архитектура-и-масштаб/A3.4-Legacy-и-рефакторинг/A3.4.1-Стратегии-рефакторинга|A3.4.1 — Стратегии рефакторинга]]
- [[../A3-Архитектура-и-масштаб/A3.4-Legacy-и-рефакторинг/A3.4.2-Inventory-и-метрики-legacy|A3.4.2 — Inventory и метрики legacy]]
- [[../A3-Архитектура-и-масштаб/A3.4-Legacy-и-рефакторинг/A3.4.3-Incremental-migration-React|A3.4.3 — Incremental migration React 16 → 19]]
- [[../A3-Архитектура-и-масштаб/A3.4-Legacy-и-рефакторинг/A3.4.4-Классы-в-hooks-без-остановки|A3.4.4 — Классы в hooks без остановки разработки]]
- [[../A3-Архитектура-и-масштаб/A3.4-Legacy-и-рефакторинг/A3.4.5-Когда-не-рефакторить|A3.4.5 — Когда не рефакторить]]

## A3.5 — Testing strategy

Стратегия тестирования для фронта: пирамида vs трофей, правильный баланс unit/integration/e2e, инструменты 2026.

- [[../A3-Архитектура-и-масштаб/A3.5-Testing-strategy/A3.5.1-Пирамида-vs-трофей-тестирования|A3.5.1 — Пирамида vs трофей тестирования]]
- [[../A3-Архитектура-и-масштаб/A3.5-Testing-strategy/A3.5.2-Vitest-и-React-Testing-Library|A3.5.2 — Vitest и React Testing Library]]
- [[../A3-Архитектура-и-масштаб/A3.5-Testing-strategy/A3.5.3-e2e-на-Playwright|A3.5.3 — e2e на Playwright]]
- [[../A3-Архитектура-и-масштаб/A3.5-Testing-strategy/A3.5.4-Contract-тесты-и-MSW|A3.5.4 — Contract тесты и MSW]]
- [[../A3-Архитектура-и-масштаб/A3.5-Testing-strategy/A3.5.5-Visual-regression-и-snapshots|A3.5.5 — Visual regression и snapshots]]

## A3.6 — Accessibility

A11y как hygiene factor 2026, а не nice-to-have. Семантика, focus management, тестирование.

- [[../A3-Архитектура-и-масштаб/A3.6-Accessibility/A3.6.1-Семантика-HTML-и-ARIA|A3.6.1 — Семантика HTML и ARIA]]
- [[../A3-Архитектура-и-масштаб/A3.6-Accessibility/A3.6.2-Focus-management-и-keyboard|A3.6.2 — Focus management и keyboard]]
- [[../A3-Архитектура-и-масштаб/A3.6-Accessibility/A3.6.3-Тестирование-a11y|A3.6.3 — Тестирование a11y]]

## Практика

- **A-P2 Monorepo Platform** _(скоро)_ — после этого трека. Turborepo + pnpm + changesets, 2 приложения + shared packages, Vercel remote cache.
- **A-P1 Performance Rescue** — можно рассматривать как легаси-пример из A3.4 (страница уже живёт, и её нужно чинить, а не переписывать).

## Связанные темы в других MOC

- [[MOC-Types]] — shared packages часто хранят типы; `declaration merging` и tsconfig paths пересекаются с A3.2.4.
- [[MOC-Internals]] — при миграции React 16 → 19 (A3.4.3) важны Compiler и new root API из Track 1.
