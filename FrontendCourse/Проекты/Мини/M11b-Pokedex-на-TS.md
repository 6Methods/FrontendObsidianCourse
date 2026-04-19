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
Дальше — **модуль 12 Build tools и тестирование**: Vite в деталях, ESLint/Prettier, Vitest, Testing Library, Playwright. Добавим зелёную планку «тесты проходят» к твоим проектам.
