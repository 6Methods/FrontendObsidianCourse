# Frontend Course — Module 12 (Build tools и тестирование) Implementation Plan

**Goal:** Модуль 12: обзор + 7 уроков (Vite, ESLint+Prettier, TS+React-линт, Vitest, Testing Library, Playwright, CI на GHA) + мини-проект (обложить M11a тестами и CI) + MOC-Tools + Start-Here.

**Architecture:** Шаблон уроков из модулей 01-11. 6 секций. «Главное» 340-420 слов. Tone — ментор-практик, «ты». Фокус на быстрый старт и релевантные команды.

**Пути:**
- Vault: `FrontendCourse/`
- Модуль: `FrontendCourse/12-Build-tools-и-тестирование/`

---

## File Structure

```
FrontendCourse/
├── 00-Start-Here.md                                (правка)
├── 12-Build-tools-и-тестирование/
│   ├── 00-Обзор-модуля.md                          (новый)
│   ├── 12.1-Vite-в-деталях.md                      (новый)
│   ├── 12.2-ESLint-и-Prettier.md                   (новый)
│   ├── 12.3-Линтер-для-TS-React.md                 (новый)
│   ├── 12.4-Vitest.md                              (новый)
│   ├── 12.5-Testing-Library.md                     (новый)
│   ├── 12.6-Playwright.md                          (новый)
│   └── 12.7-CI-на-GitHub-Actions.md                (новый)
├── Проекты/Мини/
│   └── M12-Тесты-и-CI.md                           (новый)
└── MOC/
    └── MOC-Tools.md                                (правка)
```

9 новых файлов + 2 правки.

---

## Темы уроков (по подразделам «Главное»)

### 12.1 Vite в деталях
- Зачем сборщик: модули, dev-сервер, HMR.
- Vite = ESM dev + Rollup prod.
- Dev vs build: команды `vite`, `vite build`, `vite preview`.
- HMR и React Fast Refresh.
- Env-переменные: `.env`, `.env.local`, префикс `VITE_`, `import.meta.env`.
- Aliases через `resolve.alias` (`@` → `src`).
- Proxy к бэку: `server.proxy` в `vite.config`.
- Ассеты: `src/assets` (обрабатываются) vs `public/` (копируются как есть).
- Output: `dist/`, source maps, chunking.
- Плагины: `@vitejs/plugin-react`, `vite-tsconfig-paths`.

### 12.2 ESLint и Prettier
- Зачем: ESLint ловит баги, Prettier форматирует.
- Разделение ролей: не заставляй ESLint форматировать.
- Установка в Vite+React+TS проект.
- Базовый flat config (ESLint 9): `eslint.config.js`.
- Prettier: `.prettierrc`, `.prettierignore`.
- Конфликты: `eslint-config-prettier`.
- Скрипты: `lint`, `lint:fix`, `format`.
- VS Code: `editor.formatOnSave`, расширения.
- Правила-хуки: `eslint-plugin-react-hooks`.
- pre-commit через husky + lint-staged.

### 12.3 Линтер для TS+React
- `typescript-eslint` — парсер и правила.
- `eslint-plugin-react` + `eslint-plugin-jsx-a11y`.
- Ключевые правила: `no-explicit-any`, `no-unused-vars`, `react-hooks/exhaustive-deps`.
- Как читать ошибку: файл:строка:правило → ссылка.
- Отключение: `// eslint-disable-next-line` с комментарием «почему».
- Flat config пример под React+TS.
- Preset от Vite (`eslint-config-vite`?): использовать готовый.
- CI: `eslint . --max-warnings 0`.

### 12.4 Vitest
- Что такое юнит-тест. TDD-интуиция.
- Vitest vs Jest: Vitest быстрее, конфиг общий с Vite.
- Установка, `vitest run`, `vitest` (watch).
- describe/it/expect, матчеры.
- Моки: `vi.fn()`, `vi.mock()`, `vi.spyOn`.
- Асинхронные тесты.
- Тесты чистых функций и хуков (через `renderHook`).
- Покрытие: `--coverage` (v8/istanbul).

### 12.5 Testing Library
- Философия: тестируй поведение, не имплементацию.
- `@testing-library/react` + `@testing-library/user-event`.
- `render`, `screen`, семантические queries (`getByRole`, `getByLabelText`).
- getBy vs queryBy vs findBy — когда какой.
- События через `user.click`, `user.type`.
- Тесты форм, списков, условного рендеринга.
- Обёртка для провайдеров (QueryClient, Router, Context).
- Что НЕ тестировать: внутренние классы, стили, snapshots без смысла.

### 12.6 Playwright
- Зачем E2E поверх юнитов.
- Playwright vs Cypress — короткий выбор.
- Установка, `npx playwright install`.
- `test`, `expect`, `page`, локаторы (`getByRole`, `getByText`).
- Запись теста (`codegen`).
- Конфиг `playwright.config.ts`: `webServer` (автозапуск dev), браузеры, retries.
- Скриншоты, traces, видео — при падении.
- Когда E2E окупается, а когда нет.

### 12.7 CI на GitHub Actions
- Зачем CI: зелёная планка на PR.
- Анатомия workflow: triggers, jobs, steps.
- `.github/workflows/ci.yml` — пример (lint + typecheck + test + build).
- `actions/setup-node` + кэш npm.
- Матрица по Node (18/20/22) — опционально.
- Статус-чеки и required-checks в ветке main.
- Интеграция с Vercel: Preview Deployments автоматически.
- Playwright в CI: `actions/upload-artifact` для traces.

---

## Мини-проект M12 — Тесты и CI

Обложить M11a (или Pokédex M11b) тестами + поднять CI.

Требования:
1. Vitest: unit на 3+ утилиты/хука (включая `useCart`/`useDebounce` или `useLocalStorage`).
2. Testing Library: 4+ компонентных теста (карточка товара, корзина, форма checkout happy path + ошибка валидации).
3. Playwright: 2+ E2E (каталог → товар → добавить в корзину; checkout happy path).
4. ESLint + Prettier настроены, конфликты разрешены, `lint` зелёный.
5. `package.json` скрипты: `lint`, `typecheck`, `test`, `test:e2e`.
6. GitHub Actions: workflow `ci.yml` — `install → lint → typecheck → test → build`. Отдельный job `e2e` (опционально).
7. Покрытие unit+component >= 50% на files changed.
8. Badge с CI-статусом в README.

---

## MOC-Tools (заменить)

```markdown
---
тип: MOC
тема: Инструменты
---

# MOC — Инструменты

Карта по инструментам разработки: пакетный менеджер, сборщик, линт, тесты, CI.

## Пакетный менеджер и Git
- [[08.1-Git-базовые-команды]]
- [[08.2-Ветки-и-PR]]

## Сборщик и dev-окружение
- [[12.1-Vite-в-деталях]]

## Линт и форматирование
- [[12.2-ESLint-и-Prettier]]
- [[12.3-Линтер-для-TS-React]]

## Тестирование
- [[12.4-Vitest]]
- [[12.5-Testing-Library]]
- [[12.6-Playwright]]

## CI/CD
- [[12.7-CI-на-GitHub-Actions]]

## Практика
- [[M12-Тесты-и-CI]]
```

---

## Start-Here — убрать «_(скоро)_» у модуля 12.

---

## Out of Scope
- Webpack, Rollup напрямую — не нужно после Vite.
- Storybook — можно в M14, если успеем.
- Stress/load-тесты — не фронтенд.
- Docker/прод-сервер — модули 13-14.
