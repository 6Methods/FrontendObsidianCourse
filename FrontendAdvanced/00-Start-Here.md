---
тип: точка-входа
---

# Frontend Advanced — старт

Привет. Это продвинутая версия курса. **Не для новичков.** Это слой поверх базового `FrontendObsidianCourse`: то, что отличает middle от middle+/senior, и то, что вытягивает на собеседованиях в сильные продуктовые команды.

## Для кого этот vault

- Ты прошёл базовый `FrontendObsidianCourse` (14 модулей, P1/P2/P3), **или**
- У тебя 1+ год реального опыта с React+TypeScript в команде.
- Ты свободно пишешь на JS/TS, читаешь чужой код, умеешь в Git, PR, code review, терминал, npm/pnpm.
- Ты хочешь расти в глубину: понимать, что происходит под капотом, уметь строить архитектуру на команду 10+ человек, проектировать типы как инструмент дизайна, деплоить не только на Vercel.

Если чего-то из этого нет — **вернись в базовый курс**. Этот vault предполагает, что база уже есть.

## Что здесь и чего нет

**Есть:** Browser/V8 internals, event loop глубже, memory и GC, React 2026 (Compiler, Suspense streaming, selective hydration), TypeScript type-level, Feature-Sliced Design, monorepo на Turborepo, micro-frontends, testing strategy, accessibility, Docker и self-hosting, SQL для фронтовика, web security, observability (OTel), алгоритмы с применением, tech writing, senior code review, open source.

**Нет:** базовый HTML/CSS/JS/React (это в базовом курсе), Vue/Svelte, React Native, GoF-паттерны ради паттернов, LeetCode Hard, ИИ-инструменты (отдельный трек).

## Как проходить

1. **Основной путь — по порядку Track 1 → Track 2 → Track 3 → Track 4.** Каждый опирается на предыдущий.
2. **Параллельные дорожки:** Track 5 (Алгоритмы) и Track 6 (Команда и культура) лучше читать не в конце, а параллельно — 1–2 урока в неделю с середины Track 3. Алгоритмы не требуют Docker/SQL, а A6.1/A6.2 (tech writing, code review) полезны уже когда ты начинаешь проектировать и ревьюить.
3. В каждом модуле сначала открой `00-Обзор-модуля.md` — чек-лист и карта уроков.
4. Формат урока — те же 6 секций, что в базовом курсе: **Зачем → Главное → Пример кода → Частые ошибки → Задания → Что почитать**. Объём «Главное» — 500–1000 слов, код-примеры реалистичные.
5. Задания делать **всегда**. Курс без практики — потеря времени. В продвинутом — особенно.
6. Между треками — большие проекты (A-P1 … A-P4), они в отдельном каталоге.
7. Темп — 10–15 часов в неделю, 9–12 месяцев.
8. **Advanced/optional** — некоторые уроки помечены как advanced. Их можно пропустить на первом проходе: `A2.1.7` (свои type-level утилиты), `A3.3` целиком (micro-frontends — нужны 1 команде из 20), `A5.5` (Dynamic Programming).

## Карта треков

### Track 1 — Deep Frontend
Что происходит под капотом. Browser rendering, event loop, memory/GC, React performance 2026.

- [[A1-Deep-Frontend/A1.1-Browser-Rendering/00-Обзор-модуля|A1.1 — Browser Rendering Pipeline]]
- [[A1-Deep-Frontend/A1.2-Event-Loop-и-Concurrency/00-Обзор-модуля|A1.2 — Event Loop и Concurrency]]
- [[A1-Deep-Frontend/A1.3-Memory-и-GC/00-Обзор-модуля|A1.3 — Memory и GC]]
- [[A1-Deep-Frontend/A1.4-React-Performance-2026/00-Обзор-модуля|A1.4 — React Performance 2026]]

### Track 2 — TypeScript Mastery
Типы как инструмент дизайна, не декорация. Type-level programming, precision types, библиотечный DX.

- [[A2-TypeScript-Mastery/A2.1-Type-level-Programming/00-Обзор-модуля|A2.1 — Type-level Programming]]
- [[A2-TypeScript-Mastery/A2.2-Precision-Types/00-Обзор-модуля|A2.2 — Precision Types]]
- [[A2-TypeScript-Mastery/A2.3-Библиотечный-DX/00-Обзор-модуля|A2.3 — Библиотечный DX]]

### Track 3 — Архитектура и масштаб
Feature-Sliced Design, monorepo на Turborepo, micro-frontends, legacy и рефакторинг, testing strategy, accessibility.

- [[A3-Архитектура-и-масштаб/A3.1-Feature-Sliced-Design/00-Обзор-модуля|A3.1 — Feature-Sliced Design]]
- [[A3-Архитектура-и-масштаб/A3.2-Monorepo-на-Turborepo/00-Обзор-модуля|A3.2 — Monorepo на Turborepo]]
- [[A3-Архитектура-и-масштаб/A3.3-Micro-frontends/00-Обзор-модуля|A3.3 — Micro-frontends]] _(advanced, optional)_
- [[A3-Архитектура-и-масштаб/A3.4-Legacy-и-рефакторинг/00-Обзор-модуля|A3.4 — Legacy и рефакторинг]]
- [[A3-Архитектура-и-масштаб/A3.5-Testing-strategy/00-Обзор-модуля|A3.5 — Testing strategy]]
- [[A3-Архитектура-и-масштаб/A3.6-Accessibility/00-Обзор-модуля|A3.6 — Accessibility]]

### Track 4 — Инфра, DevOps, SQL
Docker, self-hosting без Vercel, CI/CD глубже, SQL для фронтендера, observability, web security.

- [[A4-Инфра-DevOps-SQL/A4.1-Docker-для-фронтендера/00-Обзор-модуля|A4.1 — Docker для фронтендера]]
- [[A4-Инфра-DevOps-SQL/A4.2-Self-hosting-без-Vercel/00-Обзор-модуля|A4.2 — Self-hosting без Vercel]]
- [[A4-Инфра-DevOps-SQL/A4.3-CI-CD-глубже/00-Обзор-модуля|A4.3 — CI/CD глубже]]
- [[A4-Инфра-DevOps-SQL/A4.4-SQL-для-фронтендера/00-Обзор-модуля|A4.4 — SQL для фронтендера]]
- [[A4-Инфра-DevOps-SQL/A4.5-Observability/00-Обзор-модуля|A4.5 — Observability]]
- [[A4-Инфра-DevOps-SQL/A4.6-Web-Security/00-Обзор-модуля|A4.6 — Web Security]]

### Track 5 — Алгоритмы и структуры данных
Не LeetCode-гринд, а применимо: структуры данных с фронтовыми кейсами, деревья, графы, DP.

- [[A5-Алгоритмы-и-структуры-данных/A5.1-Сложность-и-измерения/00-Обзор-модуля|A5.1 — Сложность и измерения]]
- [[A5-Алгоритмы-и-структуры-данных/A5.2-Структуры-данных-для-фронтенда/00-Обзор-модуля|A5.2 — Структуры данных для фронтенда]]
- [[A5-Алгоритмы-и-структуры-данных/A5.3-Деревья/00-Обзор-модуля|A5.3 — Деревья]]
- [[A5-Алгоритмы-и-структуры-данных/A5.4-Графы/00-Обзор-модуля|A5.4 — Графы]]
- [[A5-Алгоритмы-и-структуры-данных/A5.5-Dynamic-Programming/00-Обзор-модуля|A5.5 — Dynamic Programming]] _(advanced, optional)_

### Track 6 — Команда и культура
Tech writing (ADR/RFC/postmortem), senior code review, open source, менторинг и командные практики.

- [[A6-Команда-и-культура/A6.1-Tech-writing/00-Обзор-модуля|A6.1 — Tech writing]]
- [[A6-Команда-и-культура/A6.2-Senior-code-review/00-Обзор-модуля|A6.2 — Senior code review]]
- [[A6-Команда-и-культура/A6.3-Open-source/00-Обзор-модуля|A6.3 — Open source contribution]]
- [[A6-Команда-и-культура/A6.4-Команда-и-менторинг/00-Обзор-модуля|A6.4 — Команда и менторинг]]

## Проекты

- **A-P1 Performance Rescue** — после Track 1. Взять медленный репозиторий, вытащить Lighthouse 60 → 95+.
- **A-P2 Monorepo Platform** — после Track 3. Turborepo, 2 приложения + shared packages, changesets, Vercel.
- **A-P3 Self-hosted Production** — после Track 4. Next.js без Vercel: Docker + VPS + Caddy + Postgres + OTel.
- **A-P4 OSS Contribution** — после Track 6. Реальный merged PR в популярный OSS-проект.

## Карты знаний (MOC)

- [[MOC-Internals]] — Browser и JS internals (Track 1)
- [[MOC-Types]] — TypeScript Mastery (Track 2)
- [[MOC-Architecture]] — Архитектура и масштаб (Track 3)
- [[MOC-Infra]] — Инфра, DevOps, SQL (Track 4)
- [[MOC-Algorithms]] — Алгоритмы и структуры данных (Track 5)
- [[MOC-Senior]] — Команда и культура (Track 6)

## Приложения _(скоро)_

- **Алгоритмы-advanced.md** — 50 задач medium+ (расширение базового с 30 easy).
- **Чтение-чужого-кода.md** — методология входа в legacy за 2 дня.
- **Senior-собес.md** — system design light, trade-off вопросы, scenario questions.

## Ресурсы

Книги и статьи собираются внутри уроков, в секции «Что почитать».

---

**Старт — [[A1-Deep-Frontend/A1.1-Browser-Rendering/00-Обзор-модуля|A1.1 Browser Rendering Pipeline]].**
