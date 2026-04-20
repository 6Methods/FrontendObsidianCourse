---
тип: MOC
тема: Инфра, DevOps, SQL
---

# MOC — Infra

Карта знаний Track 4: как поднять свой стек без Vercel, написать CI, который не занимает полчаса, читать EXPLAIN и ставить OTel в прод. Шесть модулей — Docker, self-hosting, CI/CD глубже, SQL, observability, web security.

## A4.1 — Docker для фронтендера

Контейнеры — не «бэкендерская» вещь. Это воспроизводимый env, детерминированный build и локальная Postgres одной командой.

- [[../A4-Инфра-DevOps-SQL/A4.1-Docker-для-фронтендера/A4.1.1-Контейнеризация-и-зачем-фронту|A4.1.1 — Контейнеризация и зачем фронту]]
- [[../A4-Инфра-DevOps-SQL/A4.1-Docker-для-фронтендера/A4.1.2-Dockerfile-для-Next-js|A4.1.2 — Dockerfile для Next.js]]
- [[../A4-Инфра-DevOps-SQL/A4.1-Docker-для-фронтендера/A4.1.3-docker-compose-локальная-разработка|A4.1.3 — docker-compose для локальной разработки]]
- [[../A4-Инфра-DevOps-SQL/A4.1-Docker-для-фронтендера/A4.1.4-Health-checks-и-graceful-shutdown|A4.1.4 — Health checks и graceful shutdown]]
- [[../A4-Инфра-DevOps-SQL/A4.1-Docker-для-фронтендера/A4.1.5-Docker-в-CI|A4.1.5 — Docker в CI]]

## A4.2 — Self-hosting без Vercel

Что происходит, когда ты сам деплоишь. VPS, reverse proxy, zero-downtime, secrets без Vercel-магии.

- [[../A4-Инфра-DevOps-SQL/A4.2-Self-hosting-без-Vercel/A4.2.1-Выбор-VPS-и-первичная-настройка|A4.2.1 — Выбор VPS и первичная настройка]]
- [[../A4-Инфра-DevOps-SQL/A4.2-Self-hosting-без-Vercel/A4.2.2-Next-js-на-VPS-systemd-Docker-pm2|A4.2.2 — Next.js на VPS: systemd vs Docker vs pm2]]
- [[../A4-Инфра-DevOps-SQL/A4.2-Self-hosting-без-Vercel/A4.2.3-Caddy-Nginx-reverse-proxy-HTTPS|A4.2.3 — Caddy/Nginx reverse proxy и HTTPS]]
- [[../A4-Инфра-DevOps-SQL/A4.2-Self-hosting-без-Vercel/A4.2.4-Rolling-deployments-zero-downtime|A4.2.4 — Rolling deployments и zero downtime]]
- [[../A4-Инфра-DevOps-SQL/A4.2-Self-hosting-без-Vercel/A4.2.5-Secrets-и-env-vars-без-Vercel|A4.2.5 — Secrets и env vars без Vercel]]

## A4.3 — CI/CD глубже

GitHub Actions — устройство, кэширование, preview deployments, secrets, release automation.

- [[../A4-Инфра-DevOps-SQL/A4.3-CI-CD-глубже/A4.3.1-GitHub-Actions-устройство|A4.3.1 — GitHub Actions: устройство]]
- [[../A4-Инфра-DevOps-SQL/A4.3-CI-CD-глубже/A4.3.2-Build-matrix-и-caching|A4.3.2 — Build matrix и caching]]
- [[../A4-Инфра-DevOps-SQL/A4.3-CI-CD-глубже/A4.3.3-Preview-deployments-на-self-hosted|A4.3.3 — Preview deployments на self-hosted]]
- [[../A4-Инфра-DevOps-SQL/A4.3-CI-CD-глубже/A4.3.4-Secrets-management-в-CI|A4.3.4 — Secrets management в CI]]
- [[../A4-Инфра-DevOps-SQL/A4.3-CI-CD-глубже/A4.3.5-Release-automation|A4.3.5 — Release automation]]

## A4.4 — SQL для фронтендера

PostgreSQL от синтаксиса до EXPLAIN. Когда ORM помогает, когда мешает.

- [[../A4-Инфра-DevOps-SQL/A4.4-SQL-для-фронтендера/A4.4.1-PostgreSQL-базовый-синтаксис|A4.4.1 — PostgreSQL базовый синтаксис]]
- [[../A4-Инфра-DevOps-SQL/A4.4-SQL-для-фронтендера/A4.4.2-JOIN-subquery-CTE|A4.4.2 — JOIN, subquery, CTE]]
- [[../A4-Инфра-DevOps-SQL/A4.4-SQL-для-фронтендера/A4.4.3-Индексы-и-EXPLAIN|A4.4.3 — Индексы и EXPLAIN]]
- [[../A4-Инфра-DevOps-SQL/A4.4-SQL-для-фронтендера/A4.4.4-Транзакции-и-isolation-levels|A4.4.4 — Транзакции и isolation levels]]
- [[../A4-Инфра-DevOps-SQL/A4.4-SQL-для-фронтендера/A4.4.5-Prisma-Drizzle-когда-ORM-мешает|A4.4.5 — Prisma/Drizzle: когда ORM мешает]]

## A4.5 — Observability

Три столпа (metrics/logs/traces). OpenTelemetry, pino, Sentry/GlitchTip, dashboards.

- [[../A4-Инфра-DevOps-SQL/A4.5-Observability/A4.5.1-Что-такое-observability|A4.5.1 — Что такое observability]]
- [[../A4-Инфра-DevOps-SQL/A4.5-Observability/A4.5.2-OpenTelemetry-в-Next-js|A4.5.2 — OpenTelemetry в Next.js]]
- [[../A4-Инфра-DevOps-SQL/A4.5-Observability/A4.5.3-Structured-logging-pino|A4.5.3 — Structured logging с pino]]
- [[../A4-Инфра-DevOps-SQL/A4.5-Observability/A4.5.4-Error-tracking-Sentry-GlitchTip|A4.5.4 — Error tracking: Sentry vs GlitchTip]]
- [[../A4-Инфра-DevOps-SQL/A4.5-Observability/A4.5.5-Dashboards-и-alerts|A4.5.5 — Dashboards и alerts]]

## A4.6 — Web Security

Что нужно знать фронтендеру про безопасность. XSS/CSP с Trusted Types, CSRF/CORS/SameSite, OAuth 2.1 + PKCE + OIDC, security headers и аудит.

- [[../A4-Инфра-DevOps-SQL/A4.6-Web-Security/A4.6.1-XSS-и-CSP|A4.6.1 — XSS и CSP]]
- [[../A4-Инфра-DevOps-SQL/A4.6-Web-Security/A4.6.2-CSRF-CORS-SameSite-cookies|A4.6.2 — CSRF, CORS, SameSite cookies]]
- [[../A4-Инфра-DevOps-SQL/A4.6-Web-Security/A4.6.3-OAuth-OIDC-JWT|A4.6.3 — OAuth, OIDC, JWT]]
- [[../A4-Инфра-DevOps-SQL/A4.6-Web-Security/A4.6.4-Security-headers-и-audit|A4.6.4 — Security headers и audit]]

## Практика

- **A-P3 Self-hosted Production** _(скоро)_ — после этого трека. Next.js без Vercel: Docker + VPS + Caddy + Postgres + OTel.

## Связанные темы в других MOC

- [[MOC-Architecture]] — changesets и CI на monorepo (A3.2) пересекаются с A4.3; self-hosted deployment — продолжение A3.2/A3.3.
- [[MOC-Internals]] — Core Web Vitals из A1 продолжаются в A4.5 как мониторинг в проде.
