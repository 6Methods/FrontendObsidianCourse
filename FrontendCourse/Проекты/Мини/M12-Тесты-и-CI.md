---
тип: мини-проект
модуль: 12-Build-tools-и-тестирование
статус: not-started
---

# M12 — Тесты и CI

Мини-проект после модуля 12. Берёшь свой M11a (SPA-магазин на TS) и обкладываешь тестами: юнит (Vitest), компонентные (Testing Library), E2E (Playwright). Поднимаешь CI на GitHub Actions: без зелёной галочки PR не мёржится. Это то, что делает код «боевым», а не «домашним».

## Задача

На базе уже работающего M11a добавить тест-слой и CI-пайплайн. Никаких новых фич, только инфраструктура качества. После этого модуль 13 Next.js ты встречаешь с проектом, на который можно смотреть без стеснения.

## Требования

### Тесты
1. **Vitest (unit):** минимум 3 теста на утилиты и хуки. Кандидаты: `useDebounce`, `useCart` (редьюсер корзины), форматтер цены.
2. **Testing Library (component):** минимум 4 теста.
   - `ProductCard`: рендер, клик «В корзину» вызывает callback.
   - `CartPage`: отображение пустой и непустой корзины.
   - `CheckoutForm`: happy-path (валидные поля → submit), ошибка валидации (например, email).
   - `Nav`: счётчик товаров меняется при изменении Context.
3. **Playwright (E2E):** минимум 2 сценария.
   - Каталог → товар → «В корзину» → счётчик в навбаре вырос.
   - Checkout happy path: заполнить форму, submit, редирект на `/success`.
4. **Покрытие** (unit и component): `--coverage` в Vitest, минимум 50% по изменённым файлам.

### Lint и форматирование
- ESLint 9 flat config, `eslint-plugin-react-hooks`, `typescript-eslint`, `eslint-plugin-jsx-a11y`.
- Prettier: `.prettierrc` плюс `eslint-config-prettier` (отключить конфликтующие правила).
- Скрипты `lint`, `lint:fix`, `format` в `package.json`.

### CI
- `.github/workflows/ci.yml` на `push` и `pull_request` для `main`.
- Jobs: `install` → `lint` → `typecheck` → `test` → `build`.
- Playwright-job (опционально отдельно): `npx playwright install --with-deps chromium` плюс прогон E2E.
- Кэш npm через `actions/setup-node`.
- Артефакты: Playwright `playwright-report/` и `test-results/` при падении (`if: always()`).
- Required status check в настройках ветки `main`.
- Badge статуса в README.

### Прочее
- README обновлён: раздел «Как запускать тесты», «Как работает CI».
- Все локальные команды работают: `npm run lint`, `typecheck`, `test`, `test:e2e`.

## Чего НЕ должно быть
- Snapshot-тестов «для галочки»: только по реальному контракту UI.
- Тестов на стили или классы (`toHaveClass("btn-primary")`): тестируй поведение, не верстку.
- `xit` или `skip` без `TODO`-комментария.
- Моков, маскирующих баги. Моки только для сети и таймеров.

## Этапы

1. **Vitest:** `npm i -D vitest @vitest/coverage-v8`. Добавь `test` в `vite.config.ts` (через `defineConfig` и `test: { environment: "jsdom" }`).
2. **jsdom:** `npm i -D jsdom`. `tsconfig`: типы для vitest/globals.
3. **Testing Library:** `npm i -D @testing-library/react @testing-library/user-event @testing-library/jest-dom`. Файл `src/test/setup.ts` с `@testing-library/jest-dom`, подключи в `vite.config.ts` (`setupFiles`).
4. **Пишем 3 unit и 4 component теста.** Покрытие в Vitest `--coverage`.
5. **Playwright:** `npm init playwright@latest`. `webServer` в конфиге → `npm run dev`. 2 сценария.
6. **ESLint 9 flat:** `npm i -D eslint @eslint/js typescript-eslint eslint-plugin-react eslint-plugin-react-hooks eslint-plugin-jsx-a11y eslint-config-prettier`. `eslint.config.js`: React + TS preset.
7. **Prettier:** `.prettierrc`, `.prettierignore`, `npm i -D prettier`.
8. **Скрипты:** `lint`, `lint:fix`, `format`, `typecheck`, `test`, `test:e2e`, `test:coverage`.
9. **CI:** `.github/workflows/ci.yml`, тот самый пайплайн.
10. **Badge** статуса в README плюс раздел «Тесты и CI».

## Структура (что появится)
```
.github/
└── workflows/
    └── ci.yml
src/
├── test/
│   └── setup.ts
├── hooks/
│   └── useDebounce.test.ts
├── components/
│   ├── ProductCard.test.tsx
│   ├── Nav.test.tsx
│   └── CheckoutForm.test.tsx
└── pages/
    └── CartPage.test.tsx
tests/e2e/
├── catalog.spec.ts
└── checkout.spec.ts
eslint.config.js
.prettierrc
playwright.config.ts
```

## Сдача
1. Репозиторий M11a с добавленным слоем тестов и CI.
2. Зелёный последний прогон CI на ветке `main` (badge в README).
3. README: ссылка на прод, ссылка на отчёт Playwright (опционально), таблица «что покрыто».

## Критерии приёмки ревью
- [ ] `npm run lint` без варнингов (`--max-warnings 0`).
- [ ] `npm run typecheck` без ошибок.
- [ ] `npm run test`: все проходят, coverage ≥ 50% по изменённым файлам.
- [ ] `npm run test:e2e` проходит локально.
- [ ] `.github/workflows/ci.yml` существует, последний прогон зелёный.
- [ ] Badge статуса CI в README.
- [ ] В тестах нет проверки классов или стилей: только поведение.
- [ ] Prettier не конфликтует с ESLint.

## Что дальше
Дальше идёт модуль 13 «Next.js и backend»: App Router, Server Components, Server Actions, API routes. Будешь писать fullstack, не переключаясь между проектами.
