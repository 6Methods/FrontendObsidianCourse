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
