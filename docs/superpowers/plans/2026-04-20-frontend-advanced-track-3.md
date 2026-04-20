# Frontend Advanced — Track 3 (Архитектура и масштаб) Implementation Plan

> **For agentic workers:** execute task-by-task через параллельные dispatch-и sub-агентов по модулю. Итоговые уроки проходят грепо-проверку на 6 секций + канонический frontmatter + пояснения англицизмов.

**Goal:** Track 3 «Архитектура и масштаб» — 4 модуля (FSD, Monorepo на Turborepo, Micro-frontends, Legacy и рефакторинг), 22 урока, 4 обзора, обновление `00-Start-Here` и новый `MOC-Architecture`. После прохождения middle-разработчик умеет объяснить, когда FSD лишний, когда monorepo оправдан, когда MF это дорого, и как переводить legacy без остановки бизнеса.

**Architecture:** Тот же формат, что Track 1/2. Vault `FrontendAdvanced/`, 6-секционный шаблон урока (Зачем → Главное → Пример кода → Частые ошибки → Задания → Что почитать), «Главное» 500–1000 слов, тон — ментор-практик, «ты». Все англицизмы поясняются в скобках при первом появлении в файле.

**Tech Stack:** FSD 2.1 spec (feature-sliced.github.io state 2026), Turborepo 2.x, pnpm 9+ с workspaces и catalog, Module Federation (Webpack 5 / Vite plugin), Next.js 15 App Router, React 19. Примеры — из реальных команд 5–30 человек, не игрушечные.

**Пути:**
- Track 3: `FrontendAdvanced/A3-Архитектура-и-масштаб/`
- MOC: `FrontendAdvanced/MOC/MOC-Architecture.md`

**Каноничный frontmatter:**
```yaml
---
тип: урок
трек: A3-Архитектура-и-масштаб
модуль: A3.X-<имя>
урок: A3.X.Y
статус: to-read
---
```

---

## File Structure

```
FrontendAdvanced/
├── 00-Start-Here.md                # обновить: Track 3 теперь «готов»
├── A3-Архитектура-и-масштаб/
│   ├── A3.1-Feature-Sliced-Design/
│   │   ├── 00-Обзор-модуля.md
│   │   ├── A3.1.1-Слои-FSD-и-их-назначение.md
│   │   ├── A3.1.2-Public-API-и-правила-импортов.md
│   │   ├── A3.1.3-Feature-как-единица-продукта.md
│   │   ├── A3.1.4-Entities-и-модель-домена.md
│   │   ├── A3.1.5-Рефакторинг-из-legacy-в-FSD.md
│   │   └── A3.1.6-FSD-в-Next-js-App-Router.md
│   ├── A3.2-Monorepo-на-Turborepo/
│   │   ├── 00-Обзор-модуля.md
│   │   ├── A3.2.1-Зачем-monorepo-и-когда-нет.md
│   │   ├── A3.2.2-Turborepo-pipeline-и-cache.md
│   │   ├── A3.2.3-pnpm-workspaces-и-catalog.md
│   │   ├── A3.2.4-Shared-packages.md
│   │   ├── A3.2.5-Changesets-и-версионирование.md
│   │   └── A3.2.6-CI-на-monorepo.md
│   ├── A3.3-Micro-frontends/
│   │   ├── 00-Обзор-модуля.md
│   │   ├── A3.3.1-Когда-MF-оправданы.md
│   │   ├── A3.3.2-Module-Federation-механика.md
│   │   ├── A3.3.3-Independent-deployment-и-shared-state.md
│   │   ├── A3.3.4-Routing-между-MF.md
│   │   └── A3.3.5-MF-vs-monorepo-гибрид.md
│   └── A3.4-Legacy-и-рефакторинг/
│       ├── 00-Обзор-модуля.md
│       ├── A3.4.1-Стратегии-рефакторинга.md
│       ├── A3.4.2-Inventory-и-метрики-legacy.md
│       ├── A3.4.3-Incremental-migration-React.md
│       ├── A3.4.4-Классы-в-hooks-без-остановки.md
│       └── A3.4.5-Когда-не-рефакторить.md
└── MOC/
    └── MOC-Architecture.md
```

**Итого новых/обновлённых файлов:** 1 обновление + 4 обзора + 22 урока + 1 MOC = **28 файлов**.

---

## Темы уроков — ключевые концепты (для субагентов)

### Module A3.1 — Feature-Sliced Design

**Цель модуля:** перестать делить код по техническим слоям (`components/hooks/utils`) и начать думать слоями по бизнес-смыслу. После модуля студент может объяснить тимлиду, зачем этот оверхед, и где он не оправдан.

| Урок | Ключевые концепты «Главное» (500–1000 слов) |
|---|---|
| A3.1.1 Слои FSD и их назначение | 7 слоёв FSD 2.1: app / processes (deprecated) / pages / widgets / features / entities / shared, как поток зависимостей идёт сверху вниз, разница «слой» vs «слайс» vs «сегмент», практический пример — как реальная страница раскладывается на layers, что такое «верхний» и «нижний» слои |
| A3.1.2 Public API и правила импортов | `index.ts` как public API слайса, правило «impory only from public API», eslint-plugin-boundaries / `@feature-sliced/steiger` для enforce-а, как ловить cross-imports между features на одном уровне, паттерн re-export, как Vite/Webpack treeshake работает с barrel-файлами |
| A3.1.3 Feature как единица продукта | feature = минимальный кусок user value (не папка с компонентами), как распознать настоящую feature vs псевдо-feature, правило «каждая feature — отдельный PR и отдельный флаг», связка feature ↔ analytics event, антипаттерн «features/ui/Button» |
| A3.1.4 Entities и модель домена | entity как бизнес-сущность (User, Order, Product), что входит в entity (types + api-calls + базовый UI + model-slice), разница entity vs features, когда entity не нужна (CRUD-админка), как избежать «entity-god» с логикой всего приложения |
| A3.1.5 Рефакторинг из legacy в FSD | пошаговая миграция: сначала `app`+`shared`, потом `pages`, потом `entities` выявляются из duplicate types, потом `features` из PR-диффов, почему нельзя «переписать всё на FSD за спринт», метрики прогресса (% файлов вне legacy-папок), roll-forward vs big-bang |
| A3.1.6 FSD в Next.js App Router | как App Router `app/` ≠ FSD `app/`, паттерн: `app/` Next-а содержит только route-стабы, импортирующие `pages/*` FSD, `'use client'` границы и как они попадают на features, server components в entities для data fetching, серверные actions как часть features.api |

### Module A3.2 — Monorepo на Turborepo

**Цель модуля:** перестать бояться monorepo и перестать тащить его туда, где он не нужен. Уметь посчитать cache hit rate и объяснить, почему CI ускорился с 22 до 4 минут.

| Урок | Ключевые концепты |
|---|---|
| A3.2.1 Зачем monorepo и когда нет | outputs monorepo: atomic refactoring, shared tooling, discoverability, trade-off: `git clone` 2GB, CI-сложность, coupling команд; правило «monorepo имеет смысл от 3 пакетов с shared-зависимостями», nx/turbo/bazel — когда какой, антипаттерн monorepo для 1 приложения |
| A3.2.2 Turborepo pipeline и cache | `turbo.json` pipeline: `dependsOn`, `outputs`, `inputs`, `cache: false`, как turbo вычисляет hash (содержимое файлов + env + config), local cache в `.turbo/`, remote cache через Vercel или self-hosted (`turbo-cache`), метрика FULL_TURBO |
| A3.2.3 pnpm workspaces и catalog | `pnpm-workspace.yaml`, `workspace:*` протокол, версионирование в catalog (pnpm 9.5+ catalog:default), почему pnpm выигрывает у npm/yarn для монорепо (hard links, disk space), hoisting и как его не допускать через `.npmrc` |
| A3.2.4 Shared packages | устройство shared package: `package.json` с `main`/`module`/`exports`/`types`/`files`, tsconfig-base, eslint-config, ui-kit, shared хуки, правило «shared packages не содержат бизнес-логики», антипаттерн «shared/utils» как свалка |
| A3.2.5 Changesets и версионирование | `changesets` package: как engineer пишет changelog в PR, снепшот-релизы для preview, `changeset version` + `changeset publish` в CI, semver discipline, разница между `fixed` и `independent` стратегиями, как настроить auto-PR для changesets |
| A3.2.6 CI на monorepo | affected-стратегия через `turbo run test --filter=...[HEAD^]`, правило «тестируй только то, что реально изменилось», matrix по shard-ам, почему GitHub Actions cache недостаточно без remote cache, замер времени CI до/после remote cache, разумные limits на concurrency |

### Module A3.3 — Micro-frontends

**Цель модуля:** научить отличать случаи, когда MF это решение, от случаев, когда это cargo cult. В большинстве случаев ответ будет «не нужно» — и это главный вывод модуля.

| Урок | Ключевые концепты |
|---|---|
| A3.3.1 Когда MF оправданы | реальные кейсы: независимые команды >15 человек, разные релизные циклы (B2B vs B2C внутри одного домена), legacy-приложения на разных стеках, когда НЕ нужно: единая команда, единый продукт, «модульность ради модульности»; цена MF — дублирование runtime, shared state пазл, routing-ад |
| A3.3.2 Module Federation: механика | Webpack 5 ModuleFederationPlugin: `exposes` / `remotes` / `shared`, как работает runtime-загрузка chunk-а с удалённого хоста, singletons для React и React Router, Vite Module Federation plugin (`@originjs/vite-plugin-federation`), Native Federation как альтернатива |
| A3.3.3 Independent deployment и shared state | проблема: каждый MF деплоится независимо, но state нужно шарить, подходы: custom events, global event bus (RxJS Subject), URL-state, shared context через `shared: { singleton: true }`, почему Redux в MF — почти всегда ошибка, pattern «MF owns its state, host orchestrates» |
| A3.3.4 Routing между MF | проблема: роутинг принадлежит host или каждому MF?, pattern «host владеет root-роутером, MF регистрирует суб-роуты», как работать с React Router v7 singleton в MF, deep-linking в nested MF, что делает `basename` в shell vs child, ошибки «двойной BrowserRouter» |
| A3.3.5 MF vs monorepo — гибрид | matrix выбора: один продукт + одна команда → SPA, один продукт + много команд → monorepo, много продуктов + много команд → MF или monorepo с отдельными deployable-ами, гибрид «monorepo для кода + MF для deployment», реальный пример из Spotify/IKEA, что выбирают в 2026 |

### Module A3.4 — Legacy и рефакторинг

**Цель модуля:** научить жить с унаследованным кодом, а не бороться с ним. После модуля студент может предложить технически обоснованный план миграции с метриками и датами, а не «давайте перепишем на Vue».

| Урок | Ключевые концепты |
|---|---|
| A3.4.1 Стратегии рефакторинга | Martin Fowler: strangler fig (обрастание легаси новым кодом и постепенное удаление старого), branch by abstraction (введение интерфейса-прослойки для замены реализации), big bang (переписать целиком — почти всегда плохая идея), parallel run, когда каждая стратегия уместна, анти-паттерн «новый код и старый код параллельно навсегда» |
| A3.4.2 Inventory и метрики legacy | что инвентаризировать: LOC по папкам, cyclomatic complexity через `complexity-report`, test coverage, churn (git-метрика «как часто менялось»), bus factor, зависимости в `package.json` на устаревшие версии, как составить «тепловую карту» legacy-риска, KPI миграции (не «строки кода», а «MTTR (Mean Time To Recover) сократился») |
| A3.4.3 Incremental migration React 16 → 19 | пошаговая стратегия: 16 → 17 (LegacyRoot coexists), 17 → 18 (createRoot on routes by flag), 18 → 19 (useTransition, Actions, ref как prop), feature flag per page, обработка StrictMode double-invoke, совместимость legacy-библиотек (Enzyme → Testing Library), React codemod'ы |
| A3.4.4 Классы в hooks без остановки | правило «один компонент = один PR», паттерн «новый компонент hooks оборачивает старый class через compose», миграция HOC → custom hook, `componentDidMount` → `useEffect` с правильным cleanup, обработка `componentDidCatch` → `react-error-boundary` package, особые случаи: Redux connect → useSelector+useDispatch |
| A3.4.5 Когда не рефакторить | принцип «Chesterton's fence» (не снимай забор, пока не понимаешь, зачем он), метрики «этот legacy стоит рефакторить»: частота изменений, количество багов, onboarding-время; когда лучше feature flag вокруг и забыть, как продавать «не рефакторим» бизнесу и команде, ROI-оценка рефакторинга |

---

## Task 1: Scaffold Track 3 + обновить Start-Here

**Files:**
- Update: `FrontendAdvanced/00-Start-Here.md` — Track 3 из «скоро» в «готов», добавить ссылки на обзоры модулей A3.1–A3.4, добавить `MOC-Architecture.md` в секцию MOC.
- Create: `FrontendAdvanced/MOC/MOC-Architecture.md` — полный индекс 22 уроков Track 3 по тому же шаблону, что `MOC-Types.md`.

**Steps:**

- [ ] **Step 1:** Обновить `00-Start-Here.md`: пометить Track 3 как готовый, заменить блок Track 3 со ссылками на A3.1/A3.2/A3.3/A3.4 обзоры, добавить `MOC-Architecture.md` в секцию MOC.

- [ ] **Step 2:** Написать `MOC-Architecture.md` по образцу `MOC-Types.md` — оглавление с четырьмя модулями и полным списком уроков, каждый урок — одна строка `[[A3.X.Y-...|A3.X.Y ...]] — ...`.

- [ ] **Step 3:** Проверить, что ссылки резолвятся в Obsidian-стиле (wikilinks с относительными путями через `../A3-...`).

## Task 2: Module A3.1 — Feature-Sliced Design (7 файлов)

**Dispatch:** один subagent на весь модуль. Он создаёт `00-Обзор-модуля.md` + 6 уроков по темам из таблицы выше. Обзор — краткий: «Зачем», карта уроков, что студент будет уметь, указатель на следующий модуль A3.2.

**Steps:**

- [ ] **Step 1:** Dispatch subagent с задачей — создать 7 файлов в `FrontendAdvanced/A3-Архитектура-и-масштаб/A3.1-Feature-Sliced-Design/`. Передать на вход: описание каждого урока из таблицы, шаблон 6-секций, канонический frontmatter, правило про англицизмы, список запретов.

- [ ] **Step 2:** Post-dispatch greep-проверка:
  - все 7 файлов существуют
  - каждый урок содержит секции `## Зачем`, `## Главное`, `## Пример кода`, `## Частые ошибки`, `## Задания`, `## Что почитать`
  - frontmatter канонический (5 полей: тип/трек/модуль/урок/статус)
  - «Главное» — 500–1000 слов (грубо через wc -w на соответствующем участке)
  - англицизмы поясняются при первом появлении

- [ ] **Step 3:** Если что-то не так — fix-subagent с точечным списком нарушений.

## Task 3: Module A3.2 — Monorepo на Turborepo (7 файлов)

То же, что Task 2, но для A3.2 — 6 уроков + обзор.

- [ ] **Step 1:** Dispatch subagent на `A3.2-Monorepo-на-Turborepo/`.
- [ ] **Step 2:** Greep-проверка.
- [ ] **Step 3:** Fix-subagent по необходимости.

## Task 4: Module A3.3 — Micro-frontends (6 файлов)

То же для A3.3 — 5 уроков + обзор.

- [ ] **Step 1:** Dispatch subagent на `A3.3-Micro-frontends/`.
- [ ] **Step 2:** Greep-проверка.
- [ ] **Step 3:** Fix-subagent по необходимости.

## Task 5: Module A3.4 — Legacy и рефакторинг (6 файлов)

То же для A3.4 — 5 уроков + обзор.

- [ ] **Step 1:** Dispatch subagent на `A3.4-Legacy-и-рефакторинг/`.
- [ ] **Step 2:** Greep-проверка.
- [ ] **Step 3:** Fix-subagent по необходимости.

## Task 6: Retro + переход

- [ ] **Step 1:** Финальная проверка: все 28 файлов на месте, frontmatter унифицирован, секции есть, англицизмы пояснены.
- [ ] **Step 2:** Убедиться, что `MOC-Architecture` и `00-Start-Here` отражают реальный статус.
- [ ] **Step 3:** Сохранить в памяти retro — что получилось, где проблемные места, поправки для Track 4.

---

## Конвенции для всех subagent-ов

**При создании файла каждый subagent обязан:**

1. Frontmatter — строго 5 полей (тип/трек/модуль/урок/статус), без уровня/длительности/аудитории.
2. Заголовок — `# A3.X.Y — <Тема>` (тире длинное — em dash, не минус).
3. 6 секций в порядке: `## Зачем` → `## Главное` → `## Пример кода` → `## Частые ошибки` → `## Задания` → `## Что почитать`.
4. «Главное» — 500–1000 слов. Подразделы `### …` допустимы и приветствуются.
5. Тон — «ты», ментор-практик, без снисходительности и без академического языка.
6. **Англицизмы — с пояснениями в скобках при первом появлении в файле.**
   - Хорошо: «Strangler fig (паттерн «удушающий плющ» — старая система постепенно обрастает новой и заменяется по кускам) — это…»
   - Плохо: вываливать три термина в ряд без пояснений.
   - Не пояснять: общеизвестные (TS, JS, React, props, state, CI, PR, commit).
7. Код в примерах — реальный, на TS/React 19, с импортами и осмысленными именами. Не «foo/bar». Где уместно — конфиги (`turbo.json`, `pnpm-workspace.yaml`, `package.json`).
8. «Частые ошибки» — 3–5 конкретных кейсов с кодом-«как не надо» + «как правильно».
9. «Задания» — 2–4 задачи разного уровня (recall, понимание, приложение, hard).
10. «Что почитать» — 2–4 ссылки: спека FSD, docs Turborepo, книга Sam Newman «Building Microservices», Martin Fowler «Refactoring», статьи Kent C. Dodds / Theo / Addy Osmani, по месту.

**Запрещено:**
- Emoji в тексте уроков.
- Английские термины без пояснений при первом появлении (кроме общеизвестных).
- Заимствование фраз из предыдущих уроков.
- «Любезности» типа «Отличный вопрос!» — стиль мануальный.
- Утверждения вроде «FSD это лучшая архитектура» — тон должен быть trade-off'ный: когда да, когда нет.

## Критерии готовности Track 3

- 28 файлов на местах.
- Все уроки проходят 6-секционный grep.
- `MOC-Architecture` + `00-Start-Here` обновлены.
- Англицизмы поясняются.
- Студент, прочитавший Track 3 целиком, умеет: объяснить, когда FSD нужен и когда нет; собрать monorepo на Turborepo + pnpm; оценить применимость MF честно; предложить incremental-миграцию React 16→19 с метриками.

## Self-Review (для controller-а)

- [ ] Каждая тема в таблице тянет на 500–1000 слов «Главное».
- [ ] Нет дублей между уроками (Module Federation живёт в A3.3.2, не всплывает в A3.2).
- [ ] Уроки упорядочены от простого к сложному внутри модуля.
- [ ] Модули упорядочены: A3.1 учит мыслить архитектурой, A3.2 даёт инструмент, A3.3 показывает крайний случай, A3.4 закрывает тему «как жить с тем, что уже есть».
- [ ] Не навязывается «одна правильная архитектура» — каждый модуль честно обсуждает trade-off-ы.
