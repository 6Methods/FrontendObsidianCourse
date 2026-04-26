---
тип: мини-проект
модуль: 10-React-экосистема
статус: not-started
---

# M10 — SPA-магазин

Мини-проект после модуля 10. SPA-магазин на React + Vite, который интегрирует все темы модуля: React Router (роуты), Context (корзина), TanStack Query (каталог с API), React Hook Form + zod (оформление заказа). Это первый «серьёзный» проект, по структуре близкий к реальной работе.

## Задача

Маленький интернет-магазин с 4 роутами: каталог, страница товара, корзина, checkout. Данные с публичного API [dummyjson.com/products](https://dummyjson.com/products). Корзина в Context с персистом в localStorage. Checkout — форма с валидацией через RHF + zod, отправка — mock POST (консоль или dummyjson).

## Требования

### Функциональность
1. **Роуты:** `/` (редирект на /products), `/products` (каталог), `/products/:id` (деталь), `/cart` (корзина), `/checkout` (форма). 404 для всего остального.
2. **Каталог:** 20+ товаров из dummyjson, карточки с картинкой, названием и ценой, кнопкой «В корзину».
3. **Поиск и фильтр:** по названию (debounce 300 мс через `useDebounce`), по категории через `useSearchParams`.
4. **Страница товара:** полная информация, кнопка «В корзину», «Назад к каталогу».
5. **Корзина (Context):** добавление, удаление, изменение количества, подсчёт суммы, очистка. Персист в localStorage.
6. **Счётчик в навбаре:** сколько товаров в корзине, в реальном времени.
7. **Checkout:** форма с 5–6 полями (имя, email, телефон, город, адрес, комментарий), RHF + zod.
8. **Валидация формы:** email, телефон (regex), все обязательные поля, минимальные длины. Ошибки под полями.
9. **После успеха** редирект на `/success` с поздравлением, очистка корзины.
10. **Деплой:** Vercel, прод-URL.

### Технические правила
- `npm create vite@latest ... -- --template react`, без TypeScript.
- React Router v6 или v7, `BrowserRouter`.
- Состояние корзины только в Context (никаких Redux или Zustand).
- Данные только через TanStack Query (никаких голых `fetch` в `useEffect`).
- Форма только RHF + zod (никаких `useState` для полей).
- Минимум один кастомный хук (например, `useCart`, `useDebounce` или `useProducts`).
- `React Query DevTools` в dev-сборке.
- `.gitignore` (node_modules, dist, .env).
- README: ссылка на прод, скриншоты, краткое «архитектура».

### Структура проекта (ориентир)
```
src/
├── main.jsx              # BrowserRouter + QueryClientProvider + CartProvider
├── App.jsx               # Routes
├── pages/
│   ├── ProductsPage.jsx
│   ├── ProductPage.jsx
│   ├── CartPage.jsx
│   ├── CheckoutPage.jsx
│   └── SuccessPage.jsx
├── components/
│   ├── Nav.jsx           # с счётчиком корзины
│   ├── ProductCard.jsx
│   └── CheckoutForm.jsx  # RHF + zod
├── context/
│   └── CartContext.jsx   # useCart + провайдер
└── hooks/
    ├── useProducts.js    # TanStack Query
    └── useDebounce.js
```

## Чего НЕ должно быть

- Голых `fetch` в компонентах (всё через TanStack Query).
- Локальных `useState` для полей формы checkout (RHF + zod).
- Redux/Zustand: Context достаточно.
- UI-библиотек (MUI, Chakra). Пиши свои компоненты плюс чистый CSS.
- TypeScript будет в модуле 11.
- `key={index}` в списках (используй `product.id`).

## Этапы

1. Vite + React, поставить: `react-router-dom`, `@tanstack/react-query`, `@tanstack/react-query-devtools`, `react-hook-form`, `zod`, `@hookform/resolvers`.
2. Скелет роутов: 5 страниц плюс 404. `BrowserRouter` в main.
3. `CartProvider` и `useCart` хук. Persist в localStorage.
4. `useProducts` и `useProduct(id)` через TanStack Query плюс dummyjson.
5. Каталог: карточки, поиск с debounce, фильтр по категории через searchParams.
6. Страница товара плюс кнопка «В корзину».
7. Корзина: список, изменение qty, удаление, сумма.
8. Checkout-форма: 5–6 полей, zod-схема, обработка submit.
9. Success-страница, reset корзины.
10. Стили: CSS Modules или просто CSS. Адаптивный layout.
11. Деплой на Vercel.

## Сдача

1. Публичный GitHub-репозиторий.
2. Прод-URL (HTTPS, Vercel или Netlify).
3. README: ссылка на деплой, 2–3 скриншота, «стек», «структура папок», «что сложного».
4. На созвоне смотрим код по слоям: роуты → Context → TanStack Query → форма.

## Критерии приёмки ревью

- [ ] 5 рабочих роутов + 404.
- [ ] Каталог загружается через TanStack Query, есть loader и error-состояния.
- [ ] Поиск с debounce работает (проверяется в Network: нет запроса на каждый keystroke).
- [ ] Фильтр категории через `useSearchParams`: URL меняется, shareable.
- [ ] Context-корзина: add / remove / qty / clear, сумма корректная.
- [ ] Корзина сохраняется в localStorage (F5 не очищает).
- [ ] Счётчик в навбаре обновляется в реальном времени.
- [ ] Checkout на RHF + zod, валидация работает, ошибки отображаются.
- [ ] После submit редирект на /success, корзина очищена.
- [ ] Минимум один кастомный хук в `src/hooks/`.
- [ ] React Query DevTools установлен (виден overlay в dev).
- [ ] Нет `useState` для полей формы checkout.
- [ ] Нет голых `fetch` в компонентах.
- [ ] Прод-URL работает.

## Что дальше
Дальше идёт модуль 11 «TypeScript»: типизация props, state, API-ответов, generics. Перепишешь этот магазин на TS и увидишь, как ошибки ловятся до запуска.
