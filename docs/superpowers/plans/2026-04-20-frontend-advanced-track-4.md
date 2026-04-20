# Frontend Advanced — Track 4 (Инфра, DevOps, SQL) Implementation Plan

> **For agentic workers:** execute task-by-task через параллельные dispatch-и sub-агентов по модулю. Итоговые уроки проходят грепо-проверку на 6 секций + канонический frontmatter + пояснения англицизмов.

**Goal:** Track 4 «Инфра, DevOps, SQL» — 5 модулей (Docker, Self-hosting, CI/CD, SQL, Observability), 25 уроков, 5 обзоров, обновление `00-Start-Here` и новый `MOC-Infra`. После прохождения middle-разработчик умеет задеплоить Next.js на свой VPS без Vercel, написать нормальный CI на GitHub Actions, читать EXPLAIN и ставить OTel в прод.

**Architecture:** Тот же формат, что Track 1–3. Vault `FrontendAdvanced/`, 6-секционный шаблон урока, «Главное» 500–1000 слов, тон — ментор-практик, «ты». Англицизмы поясняются в скобках при первом появлении в файле.

**Tech Stack:** Docker 27+, Docker Compose v2, Next.js 15, Node 22 LTS, Caddy 2.8 (и альтернатива Nginx), GitHub Actions 2026, PostgreSQL 16, Prisma 6 / Drizzle, OpenTelemetry JS SDK, pino 9, Sentry / GlitchTip.

**Пути:**
- Track 4: `FrontendAdvanced/A4-Инфра-DevOps-SQL/`
- MOC: `FrontendAdvanced/MOC/MOC-Infra.md`

**Frontmatter:**
```yaml
---
тип: урок
трек: A4-Инфра-DevOps-SQL
модуль: A4.X-<имя>
урок: A4.X.Y
статус: to-read
---
```

---

## File Structure

```
FrontendAdvanced/
├── 00-Start-Here.md                # обновить Track 4 → готов
├── A4-Инфра-DevOps-SQL/
│   ├── A4.1-Docker-для-фронтендера/
│   │   ├── 00-Обзор-модуля.md
│   │   ├── A4.1.1-Контейнеризация-и-зачем-фронту.md
│   │   ├── A4.1.2-Dockerfile-для-Next-js.md
│   │   ├── A4.1.3-docker-compose-локальная-разработка.md
│   │   ├── A4.1.4-Health-checks-и-graceful-shutdown.md
│   │   └── A4.1.5-Docker-в-CI.md
│   ├── A4.2-Self-hosting-без-Vercel/
│   │   ├── 00-Обзор-модуля.md
│   │   ├── A4.2.1-Выбор-VPS-и-первичная-настройка.md
│   │   ├── A4.2.2-Next-js-на-VPS-systemd-Docker-pm2.md
│   │   ├── A4.2.3-Caddy-Nginx-reverse-proxy-HTTPS.md
│   │   ├── A4.2.4-Rolling-deployments-zero-downtime.md
│   │   └── A4.2.5-Secrets-и-env-vars-без-Vercel.md
│   ├── A4.3-CI-CD-глубже/
│   │   ├── 00-Обзор-модуля.md
│   │   ├── A4.3.1-GitHub-Actions-устройство.md
│   │   ├── A4.3.2-Build-matrix-и-caching.md
│   │   ├── A4.3.3-Preview-deployments-на-self-hosted.md
│   │   ├── A4.3.4-Secrets-management-в-CI.md
│   │   └── A4.3.5-Release-automation.md
│   ├── A4.4-SQL-для-фронтендера/
│   │   ├── 00-Обзор-модуля.md
│   │   ├── A4.4.1-PostgreSQL-базовый-синтаксис.md
│   │   ├── A4.4.2-JOIN-subquery-CTE.md
│   │   ├── A4.4.3-Индексы-и-EXPLAIN.md
│   │   ├── A4.4.4-Транзакции-и-isolation-levels.md
│   │   └── A4.4.5-Prisma-Drizzle-когда-ORM-мешает.md
│   └── A4.5-Observability/
│       ├── 00-Обзор-модуля.md
│       ├── A4.5.1-Что-такое-observability.md
│       ├── A4.5.2-OpenTelemetry-в-Next-js.md
│       ├── A4.5.3-Structured-logging-pino.md
│       ├── A4.5.4-Error-tracking-Sentry-GlitchTip.md
│       └── A4.5.5-Dashboards-и-alerts.md
└── MOC/
    └── MOC-Infra.md
```

**Итого:** 1 update + 5 × (обзор + 5 уроков) + 1 MOC = **32 файла**.

---

## Темы уроков (для субагентов)

### Module A4.1 — Docker для фронтендера

**Цель:** перестать считать Docker «для бэкендеров», начать использовать его осознанно.

| Урок | Ключевые концепты |
|---|---|
| A4.1.1 Контейнеризация и зачем фронту | что такое контейнер (изолированный процесс + файловая система), отличие от VM, зачем фронтенду — воспроизводимость env, детерминированный билд, локальная Postgres одной командой; когда Docker не нужен (чистый SPA с Vercel) |
| A4.1.2 Dockerfile для Next.js | multi-stage build (deps → build → runtime), standalone output, использование distroless/alpine для runtime, `.dockerignore`, слоёвый кэш (сначала package.json, потом src), реальный рабочий Dockerfile для Next 15 |
| A4.1.3 docker-compose локальная разработка | `compose.yaml` с app + postgres + redis, depends_on с healthchecks, volumes для persistence, профили для опциональных сервисов, hot reload через bind mount (и его подводные камни на macOS) |
| A4.1.4 Health checks и graceful shutdown | HTTP healthcheck endpoint `/api/health`, разница liveness vs readiness, SIGTERM в Node.js, ожидание завершения inflight requests, таймауты, что делает Next.js 15 из коробки |
| A4.1.5 Docker в CI | GHA job: login to registry → build с `docker/build-push-action` → push с тегом `${{ github.sha }}`, кэш через `type=gha`, multi-arch build для ARM, публичные vs приватные registry (GHCR, DockerHub) |

### Module A4.2 — Self-hosting без Vercel

**Цель:** знать, что происходит, когда ты сам деплоишь, и не бояться этого.

| Урок | Ключевые концепты |
|---|---|
| A4.2.1 Выбор VPS и первичная настройка | сравнение Hetzner/DO/Scaleway/Contabo (цены 2026), базовый setup: non-root user, SSH keys only, ufw, fail2ban, unattended-upgrades, почему не стоит использовать root для деплоя |
| A4.2.2 Next.js на VPS: systemd vs Docker vs pm2 | три варианта, таблица trade-off, пример unit-файла systemd с правильным User/Group/Restart, почему pm2 в 2026 уже сомнительный выбор, когда Docker проще systemd |
| A4.2.3 Caddy/Nginx reverse proxy + HTTPS | Caddyfile для Next.js с автоматическим Let's Encrypt, эквивалент на Nginx + certbot, HTTP/3, WebSocket и streaming SSE прокси, security headers (CSP basics) |
| A4.2.4 Rolling deployments и zero downtime | blue-green через два systemd units + symlink, docker variant через compose + health wait, zero-downtime гарантии при миграциях БД (отдельная тема, здесь — обзор), откат на предыдущий release |
| A4.2.5 Secrets и env vars без Vercel | `.env` файлы не коммитятся, загрузка через systemd `EnvironmentFile=`, sealed secrets / sops для git-хранения зашифрованных, Doppler/Infisical как self-hosted альтернативы, разница build-time vs runtime env в Next.js |

### Module A4.3 — CI/CD глубже

**Цель:** понять устройство GitHub Actions и писать CI, который не занимает 30 минут на одно изменение.

| Урок | Ключевые концепты |
|---|---|
| A4.3.1 GitHub Actions: устройство | runners, jobs, steps, events, concurrency group (cancel stale runs), matrix, reusable workflows через `workflow_call`, composite actions vs docker actions, workflow vs action |
| A4.3.2 Build matrix и caching | matrix по Node версиям и shard-ам тестов, `actions/cache` для node_modules/turbo/next cache, правила cache key (branch + lockfile hash + OS), invalidation, ограничения размера cache (10 GB) |
| A4.3.3 Preview deployments на self-hosted | pattern «PR → сабдомен `pr-123.staging.example.com`», скрипт деплоя на VPS через SSH, очистка после закрытия PR, comment на PR с ссылкой, сравнение с Vercel preview |
| A4.3.4 Secrets management в CI | GitHub encrypted secrets, environment-scoped secrets, OIDC federation (без долгих секретов — push токена, доступ к AWS/GCP по short-lived token), проверка protected branches, approved reviewers |
| A4.3.5 Release automation | semantic-release vs changesets (у нас были в A3.2.5 — отличие), changelog generation, GitHub Releases, автогенерация release notes, signing tags, npm publish в CI |

### Module A4.4 — SQL для фронтендера

**Цель:** перестать бояться SQL, уметь читать EXPLAIN, объяснить бэкендеру, почему его endpoint медленный.

| Урок | Ключевые концепты |
|---|---|
| A4.4.1 PostgreSQL базовый синтаксис | DDL vs DML, CREATE TABLE с правильными типами (text vs varchar, uuid vs id, timestamptz), INSERT/UPDATE/DELETE, WHERE, ORDER BY, LIMIT; когда сырой SQL лучше ORM (массовые операции, сложные агрегаты) |
| A4.4.2 JOIN, subquery, CTE | inner/left/right/full join — когда какой, когда subquery, когда CTE (`WITH`) для читаемости, materialized vs plain CTE (PG 12+), рекурсивный CTE на примере дерева категорий |
| A4.4.3 Индексы и EXPLAIN | B-tree vs hash vs GIN, EXPLAIN vs EXPLAIN ANALYZE vs EXPLAIN (ANALYZE, BUFFERS), seq scan vs index scan, bitmap heap scan, covering indexes, partial indexes, как поймать N+1 запрос через pg_stat_statements |
| A4.4.4 Транзакции и isolation levels | ACID, 4 уровня изоляции (READ UNCOMMITTED / READ COMMITTED / REPEATABLE READ / SERIALIZABLE), phantom read, dirty read, lost update, когда нужно SERIALIZABLE, SELECT FOR UPDATE / FOR SHARE, advisory locks |
| A4.4.5 Prisma/Drizzle: когда ORM мешает | когда ORM помогает (типобезопасность, relations, миграции), когда мешает (сложные агрегаты, оконные функции, перформанс-критичные запросы), raw SQL в Prisma (`$queryRaw`), Drizzle как более близкий к SQL, когда стоит смотреть на Kysely |

### Module A4.5 — Observability

**Цель:** понимать, что происходит в проде без догадок. Три столпа (metrics/logs/traces) и как их поставить осмысленно.

| Урок | Ключевые концепты |
|---|---|
| A4.5.1 Что такое observability | три столпа (metrics, logs, traces) — что каждый отвечает на какой вопрос, monitoring vs observability (разница), SLI/SLO/SLA basics, почему для фронтовика это не «необязательная дисциплина» |
| A4.5.2 OpenTelemetry в Next.js | OTel concepts (trace, span, context propagation), `@vercel/otel` для Next.js, ручной инструментирование server actions / route handlers, экспорт в Jaeger/Tempo/Honeycomb, distributed tracing через trace-id header |
| A4.5.3 Structured logging с pino | почему pino, уровни логирования, структурированный vs текстовый лог, `pino.child` для контекста, redaction (скрытие токенов), интеграция с OTel (trace-id в логах), как не логировать PII |
| A4.5.4 Error tracking: Sentry vs GlitchTip | Sentry features (source maps, release tracking, performance), GlitchTip как self-hosted бесплатная альтернатива, sampling rate, user context, breadcrumbs, privacy-aware инициализация |
| A4.5.5 Dashboards и alerts | что действительно мониторить на фронте (LCP, INP, CLS, JS errors rate), Grafana для self-hosted, paging правила (alert fatigue), SLO-based алерты вместо «CPU > 80%», runbook на каждый alert |

---

## Task 1: Scaffold + MOC

- [ ] Step 1: Обновить `00-Start-Here.md` (Track 4 из «скоро» в «готов»), добавить ссылки на 5 обзоров, привязать `MOC-Infra.md` в секцию MOC.
- [ ] Step 2: Создать `MOC-Infra.md` по образцу `MOC-Architecture.md` — индекс 25 уроков с короткими пояснениями.

## Task 2–6: Модули

Для каждого модуля (A4.1–A4.5) — один субагент, который создаёт обзор + 5 уроков = 6 файлов.

- [ ] Task 2: A4.1 Docker (6 файлов)
- [ ] Task 3: A4.2 Self-hosting (6 файлов)
- [ ] Task 4: A4.3 CI/CD (6 файлов)
- [ ] Task 5: A4.4 SQL (6 файлов)
- [ ] Task 6: A4.5 Observability (6 файлов)

## Task 7: Greep-проверка

- [ ] Все 32 файла на месте.
- [ ] Каждый урок имеет 7 секций (6 основных + «Следующий урок»), обзор — 4.
- [ ] Frontmatter canonical (5 полей).
- [ ] Англицизмы пояснены на первом вводе.

---

## Конвенции (те же, что Track 2/3)

1. Frontmatter: тип/трек/модуль/урок/статус.
2. Заголовок: `# A4.X.Y — <Тема>` с длинным тире.
3. 6 секций: Зачем → Главное → Пример кода → Частые ошибки → Задания → Что почитать.
4. «Главное» 500–1000 слов.
5. Тон «ты», ментор-практик, trade-off'ный.
6. Англицизмы с пояснениями при первом появлении.
7. Код реалистичный: Dockerfile для Next 15, pg_stat_statements запросы, настоящие конфиги Caddy.
8. Частые ошибки — 3–5 конкретных кейсов с «как не надо» + «как правильно».
9. Задания — 2–4 уровня сложности.
10. «Что почитать» — 2–4 ссылки на docs / статьи / книги.

Запреты: emoji, ASCII-тире в заголовках, фразы вежливости, утверждения «всегда используй X».

## Критерии готовности Track 4

- 32 файла на местах.
- Все 7-секционный grep проходит на уроках.
- MOC-Infra + Start-Here обновлены.
- Студент умеет: написать Dockerfile для Next.js, поднять VPS с Caddy, настроить GHA с кэшем и preview, прочитать EXPLAIN, поставить OTel в Next.js.
