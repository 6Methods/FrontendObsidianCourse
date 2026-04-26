---
тип: MOC
тема: Веб и HTTP
---

# MOC — Веб и HTTP

Карта по веб-архитектуре, HTTP, auth и браузерной безопасности. Заполняется в модулях 07 (база), 10 (экосистема React, fetching-библиотеки) и 13 (Next.js + backend: auth, server actions).

## Основы (модуль 07)
- [[07.1-Как-работает-веб]]
- [[07.2-HTTP-методы-статусы-заголовки]]
- [[07.3-REST-API-и-JSON]]
- [[07.4-CORS-и-безопасность]]
- [[07.5-Cookies-sessions-JWT]]
- [[07.6-Хранилища-в-браузере]]
- [[07.7-Как-браузер-рендерит-страницу]]: устройство браузера, DOM/CSSOM, layout/paint/composite, render-blocking.

## Дополнения (модуль 10)
- [[10.6-TanStack-Query]]: кеширование, retry, оптимистичные апдейты.

## Бэкенд и auth (модуль 13)
- [[13.5-Route-Handlers]]: API-эндпоинты в App Router.
- [[13.6-Server-Actions]]: мутации без API.
- [[13.7-База-данных-и-Auth]]: Supabase, Drizzle, auth.js, RLS.

## Прод: безопасность (модуль 14)
- [[14.6-Безопасность-в-проде]]: CSP, CORS, rate limit, BotID, secrets.

## Практика
- [[M06-Fetch-приложение]]: только `fetch` и публичный API.
- [[M07-Mock-auth]]: первый клиент с логином, токен в `localStorage`.
- [[M13-Fullstack-заметки]]: реальный auth через auth.js, RLS в БД.
- [[P3-Fullstack-Nextjs]]: прод-безопасность — CSP, rate limit, BotID.
