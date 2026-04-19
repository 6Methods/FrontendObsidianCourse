# Frontend Course — Module 07 (Веб-архитектура) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: superpowers:subagent-driven-development. Контентный проект.

**Goal:** Наполнить модуль 07 «Веб-архитектура»: обзор + 6 уроков + мини-проект (Mock auth) + создать MOC-Web + обновить Start-Here.

**Architecture:** Структура модулей 01–06. Шаблон урока (6 секций), средняя глубина. Практический уклон: что делает браузер, что делает сервер, что значат статусы, где ходят куки и где токены. Без глубокого backend-а (это модуль 13).

**Базовые пути:**
- Vault: `/Users/luckyme/Desktop/maloyfront/FrontendCourse/`
- Модуль: `FrontendCourse/07-Веб-архитектура/`

---

## File Structure

```
FrontendCourse/
├── 00-Start-Here.md                               (правка: убрать «_(скоро)_», добавить MOC-Web)
├── 07-Веб-архитектура/
│   ├── 00-Обзор-модуля.md                         (новый)
│   ├── 07.1-Как-работает-веб.md                   (новый)
│   ├── 07.2-HTTP-методы-статусы-заголовки.md      (новый)
│   ├── 07.3-REST-API-и-JSON.md                    (новый)
│   ├── 07.4-CORS-и-безопасность.md                (новый)
│   ├── 07.5-Cookies-sessions-JWT.md               (новый)
│   └── 07.6-Хранилища-в-браузере.md               (новый)
├── Проекты/Мини/
│   └── M07-Mock-auth.md                           (новый)
└── MOC/
    └── MOC-Web.md                                 (новый)
```

Итого: **9 новых файлов**, 1 правка.

---

## Task 1: Обзор модуля 07

**Create:** `FrontendCourse/07-Веб-архитектура/00-Обзор-модуля.md`

**Exact content:**

```markdown
---
тип: обзор-модуля
модуль: 07-Веб-архитектура
статус: not-started
roadmap: https://roadmap.sh/frontend#internet
---

# Модуль 07 — Веб-архитектура

**roadmap.sh:** [раздел Internet / How the web works](https://roadmap.sh/frontend#internet)

К этому моменту ты умеешь ходить в API через `fetch`. Но пока это «чёрный ящик» — куда уходит запрос, что с ним делает браузер, почему в одном случае приходит 200, в другом 401, а в третьем ничего и CORS-ошибка в консоли. Этот модуль — про то, что реально происходит между твоим кодом и сервером.

## Что изучаем
- Как работает веб: клиент, сервер, DNS, URL, HTTPS.
- HTTP: методы (GET/POST/PUT/PATCH/DELETE), статус-коды, заголовки, query/body.
- REST-стиль API и формат JSON.
- Same-origin policy, CORS, XSS, CSRF, HTTPS — модель угроз и типичная защита.
- Cookies, sessions, JWT — как сайт «помнит», кто ты.
- Браузерные хранилища: `localStorage`, `sessionStorage`, cookies, IndexedDB.

## Уроки
- [ ] [[07.1-Как-работает-веб]]
- [ ] [[07.2-HTTP-методы-статусы-заголовки]]
- [ ] [[07.3-REST-API-и-JSON]]
- [ ] [[07.4-CORS-и-безопасность]]
- [ ] [[07.5-Cookies-sessions-JWT]]
- [ ] [[07.6-Хранилища-в-браузере]]

## Итоговая практика
- [ ] Мини-проект: [[M07-Mock-auth]] — клиент с логином, токеном в localStorage, приватной страницей и logout-ом, на mock-API (`dummyjson.com/auth`).

## Связанные MOC
- [[MOC-Web]] — карта по вебу, HTTP, auth и безопасности. Дополняется в модулях 10 (экосистема) и 13 (Next.js + backend).

## Чек-лист завершения
- [ ] все 6 уроков прочитаны
- [ ] мини-проект с логином работает, токен сохраняется, logout чистит
- [ ] DevTools → Network открыт и ты умеешь читать request/response в реальных запросах
- [ ] DevTools → Application → Storage просмотрен: видны cookies, localStorage, sessionStorage
- [ ] узлы Internet / HTTP в roadmap.sh закрыты
```

---

## Task 2: Урок 07.1 — Как работает веб

**Create:** `FrontendCourse/07-Веб-архитектура/07.1-Как-работает-веб.md`

**Frontmatter:**
```yaml
---
модуль: 07-Веб-архитектура
тема: Как работает веб
статус: to-read
roadmap: https://roadmap.sh/frontend#internet
связано: [[07.2-HTTP-методы-статусы-заголовки]]
---
```

**Заголовок:** `# Как работает веб`

**`## Зачем это нужно`:** Интуиция «есть браузер, есть сервер» — слишком грубая. Надо понимать цепочку «пользователь ввёл URL → браузер нашёл IP → открыл соединение → отправил HTTP-запрос → получил ответ → распарсил HTML → пошёл за CSS/JS/изображениями». Без этого все дальнейшие темы (HTTP-статусы, CORS, кэширование) — набор магии.

**`## Главное` (~320–400 слов):** подразделы `### ...`:
- **Клиент и сервер.** Клиент — тот, кто инициирует запрос (чаще всего браузер, но также мобильное приложение или другой сервер). Сервер — программа, которая слушает на каком-то порту и отвечает на запросы. HTTP — язык, на котором они разговаривают.
- **URL — адрес ресурса.** `https://example.com:443/users/42?sort=asc#section`. Схема (https), домен, порт, путь, query, фрагмент. Фрагмент (`#...`) на сервер не отправляется — он только для браузера.
- **DNS.** Люди запоминают имена, сеть работает с IP. DNS — глобальная телефонная книга: превращает `example.com` в `93.184.216.34`. Результат кэшируется в ОС и браузере.
- **TCP и TLS.** Браузер открывает TCP-соединение с сервером (нужно, чтобы данные доходили в правильном порядке без потерь). Если `https://` — сверху шифруется TLS: никто по дороге не прочитает и не подменит.
- **HTTP-запрос.** Строка типа `GET /users/42 HTTP/1.1`, список заголовков (`Host`, `User-Agent`, `Accept`, `Cookie`), иногда тело. Всё — обычный текст (поверх TLS, но семантически — текст).
- **HTTP-ответ.** Статус (`200 OK`, `404 Not Found`), заголовки (`Content-Type: text/html`), тело — HTML/JSON/картинка.
- **Каскад загрузки страницы.** Браузер получил HTML → распарсил → нашёл `<link rel=stylesheet>`, `<script>`, `<img>` → **каждый из них — отдельный HTTP-запрос**. Поэтому одна страница — это десятки сетевых запросов. В DevTools → Network видно всё.
- **Статические сайты vs динамические.** Статика — сервер просто отдаёт готовые файлы. Динамика — сервер генерирует HTML на каждый запрос или API возвращает JSON, а фронт рендерит. SPA (React) — экстремум динамики: HTML почти пустой, всё собирается на клиенте.
- **HTTP/1.1 vs HTTP/2 vs HTTP/3.** 1.1 — одно соединение на запрос (медленно). 2 — мультиплексирование, много запросов в одном соединении. 3 — поверх QUIC (UDP), ещё быстрее на плохой сети. Для прикладной работы разницу почти не заметишь — но знай, что нового кода не требуется, всё работает прозрачно.

**`## Пример кода`** — блок ```http``` с примером сырого запроса-ответа:
```http
GET /users/42 HTTP/1.1
Host: api.example.com
Accept: application/json
User-Agent: Mozilla/5.0

HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 57

{"id": 42, "name": "Иван", "email": "ivan@example.com"}
```

И мини-блок ```js``` с тем же через `fetch`:
```js
const res = await fetch("https://api.example.com/users/42", {
  headers: { Accept: "application/json" },
});
const data = await res.json();
console.log(data);
```

**`## Частые ошибки`** — 4 bullet-а:
- Думать, что браузер «сам всё знает»: на самом деле каждый `<img>`, `<script>`, шрифт — отдельный HTTP-запрос. Это видно в Network.
- Путать домен и IP. `localhost` и `127.0.0.1` — одно и то же, но браузер может считать их разными origin (разные правила same-origin). В продакшене используется только домен.
- Считать, что HTTPS защищает от любого взлома. HTTPS защищает канал «от A до B»; XSS и SQL-инъекции он не лечит.
- Ставить `#` в URL и удивляться, что сервер не получает его. Фрагмент — локальное дело браузера.

**`## Задания`:**
- [ ] Открой DevTools → Network, обнови страницу — посмотри, сколько запросов, какие типы файлов, какие статусы.
- [ ] В Network → один из запросов → Headers — прочитай request и response. Найди `Host`, `Content-Type`, `Set-Cookie`, `Cache-Control`.
- [ ] `ping google.com` в терминале — посмотри, какой IP возвращается. Это DNS-резолв.
- [ ] Сравни объём загрузки первого визита и F5 — многое закэшируется. Изучи колонку Size в Network.

**`## Что почитать`:**
- [MDN — How the web works](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Web_mechanics/How_does_the_Internet_work)
- [MDN — What is HTTP?](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
- [Cloudflare — What is DNS?](https://www.cloudflare.com/learning/dns/what-is-dns/)
- [web.dev — How the browser renders a page](https://web.dev/articles/howbrowserswork)

Блоки — `http` и `js`.

---

## Task 3: Урок 07.2 — HTTP: методы, статусы, заголовки

**Create:** `FrontendCourse/07-Веб-архитектура/07.2-HTTP-методы-статусы-заголовки.md`

**Frontmatter:**
```yaml
---
модуль: 07-Веб-архитектура
тема: HTTP — методы, статусы, заголовки
статус: to-read
roadmap: https://roadmap.sh/frontend#internet
связано: [[07.1-Как-работает-веб]], [[07.3-REST-API-и-JSON]]
---
```

**Заголовок:** `# HTTP — методы, статусы, заголовки`

**`## Зачем это нужно`:** Когда ты пишешь `fetch`, ты неявно указываешь метод, смотришь статус ответа, передаёшь заголовки. Разбираться в них — это уметь читать чужие API (документацию), понимать ошибки в Network, не делать POST там, где нужен PUT, и не слать JSON без `Content-Type`.

**`## Главное` (~340–420 слов):** подразделы `### ...`:
- **HTTP-методы.** GET — прочитать (без тела, идемпотентно, кешируется). POST — создать/выполнить действие (с телом). PUT — заменить ресурс целиком. PATCH — изменить часть. DELETE — удалить. Ещё есть OPTIONS (преflight CORS), HEAD (как GET, но без тела).
- **Идемпотентность.** GET, PUT, DELETE — вызов 1 раз и 100 раз даёт один итог на сервере. POST — каждый вызов создаёт новое. Важно для ретраев и кеша.
- **Семантика против реальности.** REST говорит, «что должен делать каждый метод». Но API в жизни разные — некоторые используют POST для всего. В чужом API смотри документацию, в своём — следуй правилам.
- **Статус-коды: 5 классов.**
    - **1xx** — информационные (редко).
    - **2xx — успех.** `200 OK` — всё ок. `201 Created` — создано, в `Location` ссылка. `204 No Content` — ок, но тела нет (часто после DELETE).
    - **3xx — редиректы.** `301 Moved Permanently` (навсегда), `302 Found` (временно), `304 Not Modified` (кэш свежий).
    - **4xx — ошибка клиента.** `400 Bad Request` (кривой запрос), `401 Unauthorized` (не залогинен), `403 Forbidden` (залогинен, нельзя), `404 Not Found`, `409 Conflict`, `422 Unprocessable Entity` (данные не прошли валидацию), `429 Too Many Requests`.
    - **5xx — ошибка сервера.** `500 Internal Server Error`, `502 Bad Gateway`, `503 Service Unavailable`.
- **Важное различие 401 vs 403.** 401 — «покажи кто ты». 403 — «знаю, кто ты, но сюда нельзя».
- **Заголовки запроса.** `Content-Type` — формат тела (`application/json`, `multipart/form-data`). `Accept` — какой формат хочешь в ответ. `Authorization` — токен/логин. `Cookie` — автоматически браузером.
- **Заголовки ответа.** `Content-Type`, `Content-Length`, `Set-Cookie`, `Cache-Control`, `Location` (для редиректов), `Access-Control-Allow-Origin` (CORS).
- **Query vs body.** Параметры в URL (`?q=abc`) — для фильтрации/пагинации в GET. Тело — для данных в POST/PUT/PATCH. Параметры в URL видны в логах — не передавай там пароли.
- **Идемпотентные POST? Идемпотентные ключи.** Платёжные API часто просят `Idempotency-Key` в заголовке — чтобы при ретрае не списать дважды.

**`## Пример кода`** — блок ```js```:
```js
// GET с query и заголовком
const url = new URL("https://api.example.com/posts");
url.searchParams.set("limit", "10");
const res = await fetch(url, {
  headers: { Accept: "application/json" },
});

// POST с JSON-телом
await fetch("https://api.example.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Authorization": "Bearer abc123",
  },
  body: JSON.stringify({ title: "Привет", body: "мир" }),
});

// PATCH — частичное обновление
await fetch("https://api.example.com/posts/42", {
  method: "PATCH",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ title: "Новый заголовок" }),
});

// DELETE
await fetch("https://api.example.com/posts/42", {
  method: "DELETE",
  headers: { Authorization: "Bearer abc123" },
});

// обработка статусов
const r = await fetch("https://api.example.com/profile");
if (r.status === 401) redirectToLogin();
else if (r.status === 404) showNotFound();
else if (!r.ok) throw new Error(`Ошибка: ${r.status}`);
else console.log(await r.json());
```

**`## Частые ошибки`** — 4 bullet-а:
- POST там, где должен быть PUT/PATCH/DELETE — по REST-соглашению; но в чужом API смотри документацию.
- Игнорировать 401 vs 403 — приложение показывает «ошибка» вместо «войдите заново».
- Отправлять JSON без `Content-Type: application/json` → сервер не распарсит тело.
- Передавать пароли/токены в query (`?token=...`) → попадают в логи, историю браузера. Используй `Authorization` header.

**`## Задания`:**
- [ ] В Network найди запрос и прочитай все его заголовки — request и response.
- [ ] Через `fetch` отправь POST и PATCH на `https://jsonplaceholder.typicode.com/posts/1`, сравни ответ.
- [ ] Заспуфь 401: обратись к API, которое требует auth, без заголовка — смотри статус.
- [ ] Прочитай `Cache-Control` и `ETag` на разных сайтах, пойми, что такое 304.

**`## Что почитать`:**
- [MDN — HTTP methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- [MDN — HTTP response status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [MDN — HTTP headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
- [httpstatuses.com](https://httpstatuses.com/)

Блок — `js`.

---

## Task 4: Урок 07.3 — REST API и JSON

**Create:** `FrontendCourse/07-Веб-архитектура/07.3-REST-API-и-JSON.md`

**Frontmatter:**
```yaml
---
модуль: 07-Веб-архитектура
тема: REST API и JSON
статус: to-read
roadmap: https://roadmap.sh/frontend#internet
связано: [[07.2-HTTP-методы-статусы-заголовки]], [[07.4-CORS-и-безопасность]]
---
```

**Заголовок:** `# REST API и JSON`

**`## Зачем это нужно`:** REST — самый распространённый стиль бэкенда, с которым ты столкнёшься в 90% проектов. JSON — язык обмена данными между фронтом и бэком. Научишься читать чужие API за 5 минут, а не за час.

**`## Главное` (~320–400 слов):** подразделы `### ...`:
- **REST — не стандарт, а стиль.** Ресурсы (существительные!), операции над ресурсами через HTTP-методы. Никаких `/getUserList` — это было в SOAP. В REST — `GET /users`.
- **Ресурсы и эндпоинты.**
    - `GET /users` — список.
    - `GET /users/42` — один.
    - `POST /users` — создать.
    - `PUT /users/42` — заменить целиком.
    - `PATCH /users/42` — частично.
    - `DELETE /users/42` — удалить.
- **Вложенные ресурсы.** `GET /users/42/posts` — посты пользователя 42. `POST /users/42/posts` — новый пост от него.
- **Фильтрация и пагинация через query.** `GET /posts?userId=5&page=2&limit=20`. Стандартных соглашений нет — каждый API решает сам. Читай доку.
- **Статусы как сигналы.** 201 при создании (с `Location: /users/42`), 204 при удалении, 409 при конфликте (дубликат), 422 при ошибке валидации.
- **Версионирование.** `/api/v1/users`. Когда ломающее изменение — `/api/v2/...`. Клиенты на v1 продолжают работать, новые — на v2.
- **JSON — формат данных.** Обычный текст. Поддерживает: строки, числа, boolean, `null`, массивы, объекты. НЕ поддерживает: `undefined`, `Date` (только как строка ISO), функции, комментарии.
- **Сериализация и парсинг в JS.** `JSON.stringify(obj)` — в строку. `JSON.parse(str)` — обратно. `fetch` делает это за тебя через `res.json()` и `body: JSON.stringify(...)`.
- **Ошибки в REST.** Частый паттерн: тело JSON-ответа с `{ "error": "...", "code": "VALIDATION_ERROR", "details": {...} }`. Читай `!res.ok` + `res.json()` чтобы показать понятное сообщение.
- **GraphQL и другие.** Альтернатива REST — GraphQL, tRPC, gRPC. Знать, что они есть, достаточно — в основном ты будешь встречать REST.
- **HATEOAS и «чистый» REST.** По Филдингу настоящий REST включает ссылки на связанные ресурсы в ответе. Почти никто так не делает — «REST-like» API достаточно для индустрии.

**`## Пример кода`** — блок ```http``` + блок ```js```.

HTTP-пример:
```http
GET /api/users/42 HTTP/1.1
Host: example.com

HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 42,
  "name": "Иван",
  "email": "ivan@example.com",
  "createdAt": "2024-01-15T10:30:00Z"
}
```

JS:
```js
// GET список с пагинацией
async function getUsers(page = 1, limit = 20) {
  const url = new URL("https://api.example.com/users");
  url.searchParams.set("page", String(page));
  url.searchParams.set("limit", String(limit));
  const res = await fetch(url);
  if (!res.ok) throw new Error("Не удалось загрузить");
  return res.json();
}

// POST — создание
async function createUser(data) {
  const res = await fetch("https://api.example.com/users", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(data),
  });

  if (res.status === 422) {
    const err = await res.json();
    throw new Error(`Валидация: ${err.error}`);
  }
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  return res.json();
}

// DELETE
async function deleteUser(id) {
  const res = await fetch(`https://api.example.com/users/${id}`, {
    method: "DELETE",
  });
  if (res.status === 204) return; // успех без тела
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
}
```

**`## Частые ошибки`** — 4 bullet-а:
- Делать эндпоинты вроде `POST /getUser` — это не REST. Ресурсы — существительные, действие задаётся методом.
- Забывать проверять `!res.ok` — `fetch` не падает на 404/500, ошибка проглатывается.
- Парсить JSON до проверки статуса — на 500 сервер может вернуть HTML-страницу, `res.json()` упадёт.
- Не читать документацию API — разные бэкенды по-разному называют пагинацию, сортировку, ошибки.

**`## Задания`:**
- [ ] На `https://jsonplaceholder.typicode.com/` сделай GET `/posts`, GET `/posts/1`, POST `/posts`, PATCH `/posts/1`, DELETE `/posts/1`. Посмотри статусы.
- [ ] Разбери структуру JSON-ответа — выведи `title` у первых 5 постов.
- [ ] Добавь обработку 404 — обратись к `/posts/99999`, вырази это в UI сообщением «Не найдено».
- [ ] Изучи публичную документацию какого-нибудь API (например, `https://api.github.com`) — найди пагинацию, поиск, rate limit.

**`## Что почитать`:**
- [MDN — An overview of HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
- [MDN — Working with JSON](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON)
- [restfulapi.net — REST API Tutorial](https://restfulapi.net/)
- [json.org](https://www.json.org/json-en.html)

Блоки — `http` и `js`.

---

## Task 5: Урок 07.4 — CORS и безопасность

**Create:** `FrontendCourse/07-Веб-архитектура/07.4-CORS-и-безопасность.md`

**Frontmatter:**
```yaml
---
модуль: 07-Веб-архитектура
тема: CORS и безопасность
статус: to-read
roadmap: https://roadmap.sh/frontend#internet
связано: [[07.3-REST-API-и-JSON]], [[07.5-Cookies-sessions-JWT]]
---
```

**Заголовок:** `# CORS и безопасность`

**`## Зачем это нужно`:** 90% «странных» ошибок в консоли начинающего — CORS. И 90% дыр в приложениях — XSS/CSRF. Тут не про то, чтобы стать security-инженером, а про то, чтобы не делать типовых глупостей и понимать, что пишет браузер в ошибке.

**`## Главное` (~340–420 слов):** подразделы `### ...`:
- **Same-origin policy.** Браузер запрещает JS одной страницы читать ответы от другого origin. Origin = схема + домен + порт: `https://example.com:443` и `http://example.com:80` — разные origin-ы.
- **Зачем.** Если бы policy не было, на вредоносном сайте `evil.com` скрипт мог бы делать запросы к `mybank.com` в контексте твоих куков и увидеть твой баланс. Same-origin — базовая стена между сайтами.
- **CORS.** Способ сервера разрешить легитимным чужим origin-ам читать свои ответы. Сервер отвечает заголовком `Access-Control-Allow-Origin: https://myapp.com` — браузер видит, разрешает. Нет заголовка или он не совпал — браузер блокирует доступ к ответу (запрос ушёл и сервер обработал, но JS не увидит результат).
- **Preflight OPTIONS.** Для «сложных» запросов (нестандартные заголовки, методы кроме GET/POST/HEAD, `Content-Type: application/json` часто даёт преflight) браузер сначала шлёт `OPTIONS` с вопросом «можно?». Сервер отвечает `Access-Control-Allow-Methods`, `Access-Control-Allow-Headers`, `Access-Control-Max-Age`. Только после этого идёт реальный запрос.
- **Куки и CORS.** По умолчанию кросс-доменные запросы НЕ шлют куки. Чтобы слали — `fetch(url, { credentials: "include" })` + сервер должен ответить `Access-Control-Allow-Credentials: true` и НЕ-`*` в `Allow-Origin`.
- **HTTPS.** Шифрует канал, предотвращает подмену MITM, обязателен для куки с флагом `Secure`, для `geolocation`, `camera`, Service Workers. Для продакшена — всегда HTTPS.
- **XSS — Cross-Site Scripting.** Атакующий умудряется вставить свой JS на твой сайт через поле ввода, URL, комментарий — и его скрипт получает полный доступ к твоему DOM и токенам. Главная защита: **не вставляй пользовательские данные через `innerHTML`**. Используй `textContent` или шаблонизатор (React/Vue делают это по умолчанию).
- **CSRF — Cross-Site Request Forgery.** Другой сайт заставляет браузер отправить запрос к твоему API в контексте твоих куков (например, форма с `POST /transfer` на вредоносной странице). Защита: токен в отдельном заголовке (браузер не умеет его подделать кросс-доменно) или `SameSite` куки.
- **CSP — Content Security Policy.** Заголовок сервера, говорящий браузеру «JS можно грузить только с этих доменов, inline-скрипты запрещены». Сильно снижает поверхность XSS.
- **Минимальные привычки.** Не используй `innerHTML` с userInput; экранируй; проверяй на бэкенде; не храни токены в самом URL; используй HTTPS везде; читай ошибки CORS до конца, а не просто гугли «fetch cors fix».

**`## Пример кода`** — блок ```js```:
```js
// Типичный CORS-сценарий — запрос с куками
await fetch("https://api.example.com/me", {
  credentials: "include",  // без этого куки не поедут
});

// Типичная CORS-ошибка в консоли:
// "Access to fetch at 'https://api.example.com/me' from origin
//  'https://myapp.com' has been blocked by CORS policy: No
//  'Access-Control-Allow-Origin' header is present..."

// XSS — как НЕ делать
const userInput = "<img src=x onerror=alert('XSS')>";
const target = document.querySelector("#bio");
target.innerHTML = userInput;  // 💣 исполнится

// XSS — как правильно
target.textContent = userInput; // безопасно, текст
```

**`## Частые ошибки`** — 4 bullet-а:
- Пытаться обойти CORS фронтендом (заголовки `Origin` руками не меняются — браузер не даст). Исправляется **на сервере**, не на клиенте.
- `innerHTML` с пользовательским вводом без санитизации → XSS. Используй `textContent` / React / `DOMPurify`.
- Хранить токены в `localStorage` и думать, что это безопасно. Это удобно, но при XSS злодей получит токен. Альтернатива — HttpOnly-куки.
- Забыть `credentials: "include"` при кросс-доменных запросах с куками → auth не работает; при этом сервер должен разрешить `Allow-Credentials: true`.

**`## Задания`:**
- [ ] Сделай локальный `index.html` и открой его через `file://` — попробуй `fetch` к публичному API. Увидишь CORS-ошибки. Подними через `python -m http.server` или Vite, сравни.
- [ ] Отправь запрос к API, который не разрешает твой origin (например, серверу без CORS) — прочитай ошибку, разбери её.
- [ ] Сделай `innerHTML = "<img src=x onerror=alert(1)>"` — увидишь XSS-демо. Замени на `textContent` — убедись, что безопасно.
- [ ] Прочитай `Cookie` и `Set-Cookie` в Network — найди атрибуты `HttpOnly`, `Secure`, `SameSite`.

**`## Что почитать`:**
- [MDN — CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
- [MDN — Same-origin policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)
- [MDN — Cross-site scripting (XSS)](https://developer.mozilla.org/en-US/docs/Glossary/Cross-site_scripting)
- [OWASP — Top Ten](https://owasp.org/www-project-top-ten/)

Блок — `js`.

---

## Task 6: Урок 07.5 — Cookies, sessions, JWT

**Create:** `FrontendCourse/07-Веб-архитектура/07.5-Cookies-sessions-JWT.md`

**Frontmatter:**
```yaml
---
модуль: 07-Веб-архитектура
тема: Cookies, sessions, JWT
статус: to-read
roadmap: https://roadmap.sh/frontend#internet
связано: [[07.4-CORS-и-безопасность]], [[07.6-Хранилища-в-браузере]]
---
```

**Заголовок:** `# Cookies, sessions, JWT`

**`## Зачем это нужно`:** HTTP — stateless: сервер не помнит, что ты заходил секунду назад. Как же сайт «помнит» логин? Через специальные механизмы: cookies, server sessions или JWT-токены. Понимание нужно, чтобы писать клиент к auth-API, работать с ролями, правильно разлогинивать.

**`## Главное` (~340–420 слов):** подразделы `### ...`:
- **Cookies — как это работает.** Маленькие строки, которые сервер просит браузер «запомнить и прикладывать к каждому запросу на мой домен». Сервер отправляет `Set-Cookie: token=abc; HttpOnly; Secure`. Браузер автоматически шлёт `Cookie: token=abc` во всех следующих запросах.
- **Атрибуты cookies.**
    - `HttpOnly` — JS через `document.cookie` НЕ прочитает. Защита от XSS, но всё равно шлётся сервером автоматически.
    - `Secure` — шлётся только по HTTPS.
    - `SameSite=Strict/Lax/None` — не шлётся с чужих сайтов (защита от CSRF). `Lax` по умолчанию в современных браузерах.
    - `Domain`, `Path`, `Max-Age`, `Expires` — область и срок жизни.
- **Server-side sessions.** Классическая схема. Логин → сервер создаёт запись в БД `{sessionId, userId, expires}` и ставит куку `sessionId`. Каждый запрос — браузер присылает `sessionId` в куке, сервер идёт в БД, находит `userId`. Плюсы: легко инвалидировать (удалил строку — сессия мертва). Минусы: БД на каждый запрос, плохо масштабируется на множество серверов.
- **JWT — JSON Web Token.** Токен, в который зашита информация о пользователе и подпись сервера. Три части через точку: `header.payload.signature`. Payload — base64-JSON типа `{ "userId": 42, "role": "user", "exp": ... }`. Подпись гарантирует, что никто не подделал содержимое.
- **Stateless auth на JWT.** Сервер не хранит сессии. На каждый запрос — проверяет подпись, читает `userId` прямо из токена. Плюсы: масштабируется (любой сервер проверит). Минусы: **нельзя отозвать до истечения `exp`** — токен «живёт» пока не протухнет.
- **Где хранить JWT на клиенте.**
    - `localStorage` — удобно, но XSS-чувствительно (скрипт злодея прочитает).
    - `HttpOnly`-cookie — безопаснее от XSS, но требует CSRF-защиты.
    - В памяти приложения — ещё безопаснее, но слетит при F5.
- **Authorization header.** При JWT токен обычно передают в заголовке: `Authorization: Bearer <JWT>`. Это **не** куки — ты сам ставишь заголовок в `fetch`. Не страдает от CSRF, но ты должен добавлять в каждый запрос.
- **Access + refresh токены.** Access-токен живёт 10–15 мин (короткий = менее опасен при утечке). Refresh — 30 дней, хранится в HttpOnly-куке, используется только на `/refresh` чтобы получить новый access. Баланс удобства и безопасности.
- **Logout.** При сессиях — удалить запись на сервере и стереть куку. При JWT без серверного хранения — просто удалить токен у клиента (старый токен всё ещё валиден до `exp`, но без клиента им некому пользоваться). Настоящий «отзыв» JWT требует blacklist или короткой жизни.

**`## Пример кода`** — блок ```js```:
```js
// Логин: получить токен от сервера, сохранить
async function login(username, password) {
  const res = await fetch("https://dummyjson.com/auth/login", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ username, password }),
  });
  if (!res.ok) throw new Error("Неверный логин или пароль");
  const data = await res.json();
  // data.accessToken — JWT
  localStorage.setItem("token", data.accessToken);
  return data;
}

// Приватный запрос — кладём JWT в Authorization
async function getProfile() {
  const token = localStorage.getItem("token");
  if (!token) throw new Error("Не авторизован");

  const res = await fetch("https://dummyjson.com/auth/me", {
    headers: { Authorization: `Bearer ${token}` },
  });
  if (res.status === 401) {
    localStorage.removeItem("token");
    throw new Error("Сессия истекла");
  }
  if (!res.ok) throw new Error("Ошибка");
  return res.json();
}

// Logout
function logout() {
  localStorage.removeItem("token");
  location.href = "/login";
}

// Авто-refresh (упрощённо)
async function refreshToken(refreshToken) {
  const res = await fetch("https://dummyjson.com/auth/refresh", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ refreshToken }),
  });
  if (!res.ok) throw new Error("Refresh failed");
  return res.json();
}
```

**`## Частые ошибки`** — 4 bullet-а:
- Хранить access-токен с долгим сроком в `localStorage` — при XSS утечёт. Либо короткий срок + refresh в HttpOnly, либо принимай риск осознанно.
- Присылать куки кросс-доменно без `credentials: "include"` и удивляться, что auth не работает.
- Думать, что удаление JWT на клиенте = logout. До `exp` токен всё ещё валиден на сервере.
- Класть в payload JWT секреты — payload читается **любым**, base64 не шифрование. Там можно хранить только то, что нестрашно показать.

**`## Задания`:**
- [ ] На https://dummyjson.com/docs/auth сделай логин (`emilys` / `emilyspass`), залогируй ответ.
- [ ] Расшифруй JWT на https://jwt.io — увидишь payload.
- [ ] Сделай приватный запрос `/auth/me` с `Authorization: Bearer ...` — получи профиль.
- [ ] Исчезни токен из storage, повтори запрос — получишь 401.

**`## Что почитать`:**
- [MDN — HTTP cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)
- [jwt.io — Introduction to JSON Web Tokens](https://jwt.io/introduction)
- [MDN — Authentication](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication)
- [OWASP — Session management](https://owasp.org/www-project-cheat-sheets/cheatsheets/Session_Management_Cheat_Sheet.html)

Блок — `js`.

---

## Task 7: Урок 07.6 — Хранилища в браузере

**Create:** `FrontendCourse/07-Веб-архитектура/07.6-Хранилища-в-браузере.md`

**Frontmatter:**
```yaml
---
модуль: 07-Веб-архитектура
тема: Хранилища в браузере
статус: to-read
roadmap: https://roadmap.sh/frontend#internet
связано: [[07.5-Cookies-sessions-JWT]]
---
```

**Заголовок:** `# Хранилища в браузере`

**`## Зачем это нужно`:** Часто нужно что-то сохранить на клиенте: токен, настройки темы, корзину, кэш ответа. Браузер даёт несколько инструментов с разным сроком жизни, объёмом и уровнем защиты. Выбирать правильный — часть работы.

**`## Главное` (~320–400 слов):** подразделы `### ...`:
- **`localStorage`.** Синхронное key-value хранилище. Только строки (массив/объект — через `JSON.stringify`). Объём ~5–10 МБ на origin. Живёт **без ограничения по времени** до ручного удаления. Не шлётся на сервер автоматически.
- **`sessionStorage`.** Такой же API, что `localStorage`, но **живёт только пока открыта вкладка**. Закрыл вкладку — стёрлось. Хорошо для «временного» состояния (шаг мастера, временного поиска).
- **Cookies.** Маленькие строки (~4 КБ). Автоматически шлются на сервер. Для auth, CSRF-защиты через `SameSite`, и старых сценариев. В JS — `document.cookie` (медленно и неудобно), или `HttpOnly` — тогда JS вообще не видит.
- **IndexedDB.** Асинхронная NoSQL-база в браузере, индексы, большие объёмы (сотни МБ). Для офлайн-первых приложений, кэширования больших данных. Нативный API неудобный — на практике используют обёртки (`idb`, `Dexie`).
- **Cache API.** Используется с Service Workers для офлайн-работы. Хранит Response-объекты. Не путать с HTTP-кешем браузера.
- **Как выбрать.**
    - Токен, настройки, состояние UI, небольшие данные → `localStorage`.
    - Временное, только на одну вкладку → `sessionStorage`.
    - Auth с HttpOnly/SameSite → cookie.
    - Большие офлайн-данные → IndexedDB + Cache API.
- **Типичные ошибки с `localStorage`.** Синхронный API — не делай тяжёлых операций в нём в обработчике скролла. Данные — строки; забудешь `JSON.parse` — получишь строку вместо объекта. Исключения: режим инкогнито может отключить хранилище или ограничить объём.
- **`JSON.parse(... ?? "[]")`.** Частый паттерн: `const items = JSON.parse(localStorage.getItem("items") ?? "[]")`. Без `??` и `try/catch` на битых данных можно словить ошибку.
- **Проверка поддержки.** В старых браузерах и инкогнито может быть ограничен. Делать try/catch на `setItem`.
- **Версионирование формата.** Если ты изменил схему сохраняемых данных — старые клиенты прочитают чужое. Паттерн: ключ `"todos.v2"` и миграция на загрузке.
- **DevTools.** `Application → Storage` — LocalStorage, SessionStorage, Cookies, IndexedDB, Cache. Кнопка Clear site data — полная очистка, полезно при странных багах «у меня что-то закэшировалось».

**`## Пример кода`** — блок ```js```:
```js
// localStorage — объекты через JSON
const theme = { mode: "dark", accent: "blue" };
localStorage.setItem("theme", JSON.stringify(theme));

const saved = JSON.parse(localStorage.getItem("theme") ?? "null");
console.log(saved?.mode); // "dark"

localStorage.removeItem("theme");

// sessionStorage
sessionStorage.setItem("wizard-step", "2");

// cookie (через document.cookie, неудобно)
document.cookie = "theme=dark; path=/; max-age=604800; SameSite=Lax";
console.log(document.cookie); // "theme=dark"

// безопасная обёртка
function readStore(key, fallback = null) {
  try {
    const raw = localStorage.getItem(key);
    return raw ? JSON.parse(raw) : fallback;
  } catch {
    return fallback;
  }
}

// IndexedDB — пример на нативном API (упрощённо)
const request = indexedDB.open("my-db", 1);
request.onupgradeneeded = (e) => {
  const db = e.target.result;
  db.createObjectStore("items", { keyPath: "id" });
};
request.onsuccess = (e) => {
  const db = e.target.result;
  const tx = db.transaction("items", "readwrite");
  tx.objectStore("items").put({ id: 1, title: "Привет" });
};
```

**`## Частые ошибки`** — 4 bullet-а:
- Класть объекты/массивы в `localStorage` без `JSON.stringify` → увидишь `[object Object]`.
- Читать без `JSON.parse` и сравнивать как объект → `"dark" === {mode:"dark"}` никогда не true.
- Использовать `localStorage` для auth-токенов «потому что удобно» — при XSS всё утечёт. Подумай про HttpOnly-cookie.
- Хранить огромные JSON-ы (сотни МБ) в `localStorage` — он для мелочи; большие данные → IndexedDB.

**`## Задания`:**
- [ ] Сохрани в `localStorage` объект `{ theme: "dark", count: 3 }`, прочти обратно и выведи.
- [ ] Сделай функцию `persistState(key)` — синхронизирует состояние UI (например, тему) с `localStorage`.
- [ ] Проверь `Application → Storage` в DevTools — увидь свои данные.
- [ ] Нажми Clear site data — убедись, что всё стёрлось и приложение вернулось в дефолт.

**`## Что почитать`:**
- [MDN — Web Storage API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API)
- [MDN — IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API)
- [web.dev — Storage for the web](https://web.dev/articles/storage-for-the-web)
- [MDN — Using cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)

Блок — `js`.

---

## Task 8: Мини-проект M07 — Mock auth

**Create:** `FrontendCourse/Проекты/Мини/M07-Mock-auth.md`

**Exact content:**

```markdown
---
тип: мини-проект
модуль: 07-Веб-архитектура
статус: not-started
---

# M07 — Mock auth

Мини-проект после модуля 07. Первый клиент с логином — без настоящего бэкенда. Цель — прочувствовать полный цикл: форма → запрос → токен → приватный раздел → logout. Всё на публичном mock-API (`dummyjson.com/auth`), без поднятия сервера.

## Задача

Одностраничное приложение на vanilla JS: логин → защищённый экран профиля → logout. Три view-состояния, переключаются без перезагрузки страницы.

## Требования

### Функциональность
1. **Форма логина** — `username` + `password`. На submit — POST на `https://dummyjson.com/auth/login`.
2. **Валидные данные для теста:** `emilys` / `emilyspass` (смотри https://dummyjson.com/docs/auth).
3. **Loading** — пока ждём ответ, кнопка заблокирована, показываем «Вход…».
4. **Ошибка** — если 400/401 — показываем в UI «Неверный логин или пароль», не `alert`.
5. **Успех** — токен (`accessToken`) сохраняется в `localStorage`. UI переключается на экран профиля (без перезагрузки).
6. **Профиль** — на экране профиля делаем GET `https://dummyjson.com/auth/me` с `Authorization: Bearer <token>`, показываем имя, email, аватар.
7. **401 на `/auth/me`** — токен удаляется, редирект на экран логина, сообщение «Сессия истекла».
8. **Logout** — кнопка, чистит `localStorage`, возвращает на экран логина.
9. **Запоминать состояние** — на F5 если токен есть, сразу показываем профиль (и пробуем его загрузить).
10. **Деплой** — Vercel или Netlify, рабочий прод-URL.

### Технические правила
- Vanilla JS: HTML + CSS + JS. Без фреймворков.
- Стили любые (чистый CSS или Tailwind через CLI/Vite).
- `fetch` + `async/await` + `try/catch/finally`.
- Три render-функции для трёх состояний: `renderLogin()`, `renderProfile(user)`, `renderLoading()`.
- Отдельный модуль/секция `auth.js` с функциями `login`, `getProfile`, `logout`, `getToken` — не раскидывай логику по всему коду.
- Токен — только в `localStorage`. В **следующем** проекте (с настоящим бэкендом) сравним с куками.
- `.gitignore` (node_modules, .env, .DS_Store).

## Чего НЕ должно быть

- Библиотек для UI (React, Vue, Svelte — потом).
- Библиотек для запросов (axios, ky) — только встроенный `fetch`.
- Захардкоженных credentials в коде вне формы (типа `const password = "emilyspass"`).
- `alert` для ошибок.
- `innerHTML` с данными из API без экранирования (даже если там безопасные данные — привычка).
- Утечки токена в URL или логах.

## Этапы

1. **Документация API.** Прочитай https://dummyjson.com/docs/auth. Запусти ручной запрос из DevTools Console или Postman — убедись, что логин возвращает `accessToken`.
2. **Разметка.** Два блока в HTML: `#login-view` и `#profile-view`, скрытие через `hidden` или класс.
3. **Стили.** Разный look у loading/error/success.
4. **auth-модуль.** Функции `login`, `getProfile`, `logout`, `getToken`, `isAuthenticated`.
5. **Submit-обработчик.** `try`→ login → success → `finally` убрать loader.
6. **Boot.** На загрузку страницы: если токен есть → попытаться загрузить профиль. Если 401 → очистить, показать логин.
7. **Logout.** Кнопка, `localStorage.removeItem`, render login.
8. **Деплой.** Vercel / Netlify, README со скриншотами и ссылкой.

## Сдача

1. Публичный GitHub-репозиторий.
2. Прод-URL.
3. README: как запускать, какие credentials для теста, ссылка на деплой, 2 скриншота (login + profile).
4. На созвоне — смотрим Network-вкладку на реальном логине, сверяемся с критериями.

## Критерии приёмки ревью

- [ ] Все 10 функциональных пунктов работают.
- [ ] Токен приходит в ответе и попадает в `localStorage`.
- [ ] `/auth/me` вызывается с корректным `Authorization: Bearer`.
- [ ] 401 корректно обрабатывается: токен удаляется, пользователь возвращается на логин.
- [ ] Logout действительно чистит `localStorage`.
- [ ] После F5 с валидным токеном — сразу показывается профиль.
- [ ] Ошибки показываются в UI, не в alert и не только в console.
- [ ] Loader виден во время запроса, исчезает в `finally`.
- [ ] Нет `innerHTML` с сырыми данными.
- [ ] В Network видно: POST `/auth/login` → 200, GET `/auth/me` → 200 с `Authorization`.
- [ ] Прод-URL работает по HTTPS.

## Что дальше
Дальше — **модуль 08 Git и DevTools**: уметь коммитить, ветвиться, делать PR, читать blame, пользоваться Network/Performance/Sources. После него откроется дорога в React (модуль 09).
```

---

## Task 9: Создать MOC-Web

**Create:** `FrontendCourse/MOC/MOC-Web.md`

**Exact content:**

```markdown
---
тип: MOC
тема: Веб и HTTP
---

# MOC — Веб и HTTP

Карта по веб-архитектуре, HTTP, auth и браузерной безопасности. Заполняется в модулях 07 (база), 10 (экосистема React — fetching-библиотеки) и 13 (Next.js + backend — auth, server actions).

## Основы (модуль 07)
- [[07.1-Как-работает-веб]]
- [[07.2-HTTP-методы-статусы-заголовки]]
- [[07.3-REST-API-и-JSON]]
- [[07.4-CORS-и-безопасность]]
- [[07.5-Cookies-sessions-JWT]]
- [[07.6-Хранилища-в-браузере]]

## Дополнения (модуль 10 — скоро)
- _TanStack Query / SWR, оптимистичные апдейты, кеширование, retry_

## Бэкенд и auth (модуль 13 — скоро)
- _Next.js API routes, Server Actions, middleware, auth-провайдеры_

## Практика
- [[M06-Fetch-приложение]] — здесь только `fetch` + публичный API.
- [[M07-Mock-auth]] — первый клиент с логином, токен в `localStorage`.
```

---

## Task 10: Обновить 00-Start-Here.md

**Modify:** `FrontendCourse/00-Start-Here.md`

- [ ] **Step 10.1:** Убрать «_(скоро)_» у модуля 07:
  `- [[07-Веб-архитектура/00-Обзор-модуля|Модуль 07 — Веб-архитектура]] _(скоро)_` → `- [[07-Веб-архитектура/00-Обзор-модуля|Модуль 07 — Веб-архитектура]]`.
- [ ] **Step 10.2:** В разделе «Карты знаний (MOC)» добавить строку `- [[MOC-Web]]` после `- [[MOC-CSS]]` или сохранить разумный порядок (CSS, JS, Web, React, TS, Nextjs).

---

## Task 11: Верификация

- [ ] **Step 11.1:** `find FrontendCourse/07-Веб-архитектура -type f -name "*.md" | sort` → 7 файлов.
- [ ] **Step 11.2:** `M07-Mock-auth.md` существует в `Проекты/Мини/`.
- [ ] **Step 11.3:** `MOC-Web.md` существует и содержит 6 ссылок на уроки 07.1–07.6.
- [ ] **Step 11.4:** В `00-Start-Here.md` у модуля 07 нет «_(скоро)_», и добавлена ссылка `[[MOC-Web]]`.
- [ ] **Step 11.5:** Отчитаться: модуль 07 готов.

---

## Self-Review

**1. Spec coverage:**
- Веб-основы, HTTP, REST+JSON, CORS+безопасность, cookies/JWT, хранилища → Tasks 2–7. ✓
- Мини-проект Mock auth → Task 8. ✓
- MOC-Web → Task 9. ✓
- Start-Here → Task 10. ✓

**2. Placeholder scan:** TBD/TODO отсутствуют. «_(скоро)_» в MOC-Web у модулей 10 и 13 — осознанный контент-маркер. ✓

**3. Type consistency:** Имена уроков/мини-проекта согласованы: обзор, frontmatter уроков, MOC, верификация. ✓

---

## Out of Scope

- HTTP-кеширование в деталях (`Cache-Control`, `ETag`, `Vary`) — задевается в 07.1/07.2, подробно → модуль 14 (деплой).
- Websockets, SSE, WebRTC → отдельные темы, не в этом модуле.
- Глубокая криптография (HMAC, RSA, TLS handshake) → не цель курса.
- Конкретные auth-провайдеры (Auth0, Clerk, NextAuth) → модуль 13.
