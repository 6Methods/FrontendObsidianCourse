# Frontend Course — Module 14 (Деплой и финал) Implementation Plan

**Goal:** Финальный модуль: обзор + 7 уроков (Vercel, next/image+font, метрики/Lighthouse, кеш+edge, monitoring, безопасность, финал+резюме) + большой проект P3 (расширение M13) + правки MOC-Nextjs и MOC-Web + Start-Here.

**Architecture:** Паттерн как в 01-13. 6 секций. «Главное» 340-420 слов. Tone — ментор-практик, «ты». Фокус на Vercel (Fluid Compute 2026 default), Core Web Vitals (LCP/INP/CLS), финальная готовность к найму.

**Пути:**
- Vault: `FrontendCourse/`
- Модуль: `FrontendCourse/14-Деплой-и-финал/`

---

## File Structure

```
FrontendCourse/
├── 00-Start-Here.md                          (правка)
├── 14-Деплой-и-финал/
│   ├── 00-Обзор-модуля.md                    (новый)
│   ├── 14.1-Vercel-и-деплой.md               (новый)
│   ├── 14.2-Image-и-Font.md                  (новый)
│   ├── 14.3-Метрики-и-Lighthouse.md          (новый)
│   ├── 14.4-Кеш-и-edge.md                    (новый)
│   ├── 14.5-Monitoring-и-аналитика.md        (новый)
│   ├── 14.6-Безопасность-в-проде.md          (новый)
│   └── 14.7-Финал-резюме-и-дальше.md         (новый)
├── Проекты/
│   └── P3-Fullstack-Nextjs.md                (новый)
└── MOC/
    ├── MOC-Nextjs.md                         (правка)
    └── MOC-Web.md                            (правка)
```

9 новых файлов + 3 правки.

---

## Темы уроков

### 14.1 Vercel и деплой
- Что даёт Vercel: GitHub-интеграция, preview per PR, rollback, custom domains, HTTPS автоматом, Fluid Compute (2026 default).
- Import GitHub repo, автодетект framework, build settings.
- Env vars: Production / Preview / Development. `NEXT_PUBLIC_*` для клиента.
- Preview deployments на каждый push.
- `vercel dev`, `vercel env pull`.
- `vercel.ts` — typed конфиг (replaces vercel.json в 2026).
- Rollback в UI / через CLI.
- Cost: Hobby (free non-commercial), Pro.

### 14.2 next/image и next/font
- Почему картинки и шрифты — главные виновники медленного LCP и CLS.
- `next/image`: автолейз, `sizes`, `priority`, `quality`, `placeholder="blur"`.
- Local `/public` vs remote images (`remotePatterns` в конфиге).
- `next/font/google` — zero-runtime, self-host шрифтов.
- `next/font/local` + `display: "swap"`.
- CLS из-за font swap — `size-adjust`.
- Responsive `sizes` правила.
- `priority` для LCP-картинки.

### 14.3 Метрики и Lighthouse
- Core Web Vitals: **LCP** (≤2.5s), **INP** (≤200ms, заменил FID), **CLS** (≤0.1).
- Lighthouse в Chrome DevTools — lab-метрики.
- PageSpeed Insights — real user + lab.
- Vercel Speed Insights — real Core Web Vitals с прода.
- Как читать отчёт: Opportunities, Diagnostics.
- Типичные фиксы: LCP (priority image, preload), CLS (`aspect-ratio`, reserve space), INP (less JS, Server Components).
- Lighthouse CI — блокировать PR по порогам.

### 14.4 Кеш и edge
- Browser cache: `Cache-Control`, `ETag`.
- Next.js **Data Cache** (кеш `fetch`), **Full Route Cache** (статик-страницы), **Router Cache** (client navigation).
- ISR: `revalidate: 60` — перегенерация на сервере.
- On-demand: `revalidatePath("/blog")` после публикации.
- Vercel CDN — раздаёт по 100+ точкам мира.
- Fluid Compute (2026 default) vs классический serverless — переиспользование инстансов, меньше cold starts.
- Когда edge не нужен: Fluid покрывает 90% кейсов.

### 14.5 Monitoring и аналитика
- **Vercel Analytics** — количество посетителей, страницы, страны. Privacy-friendly (без cookies).
- **Vercel Speed Insights** — реальные Web Vitals пользователей (field data).
- Vercel Logs: Runtime, Function, Build — где искать ошибки прода.
- **Sentry** — ошибки frontend + server, source maps, stack traces, alerts.
- Notifications: Slack / Discord webhook на deploy и error.
- Альтернативы Analytics: PostHog (продуктовая аналитика), Plausible.

### 14.6 Безопасность в проде
- Env secrets: всё, что не `NEXT_PUBLIC_`, видно только на сервере.
- **Content-Security-Policy** — защита от XSS, `Strict-Transport-Security`, `X-Frame-Options`.
- CORS на Route Handlers: разрешать только свои домены.
- **Rate limiting**: Vercel WAF (Pro), Upstash Ratelimit (free tier).
- **Vercel BotID** — защита от ботов.
- RLS в Supabase — никогда не выключай в проде.
- OAuth redirect URLs — список прод-доменов в провайдере (Google Cloud Console).
- `npm audit` и Dependabot для зависимостей.

### 14.7 Финал: резюме и дальше
- Портфолио-сайт: кратко о себе + 3 проекта (P1, P2, P3).
- Pinned repos на GitHub: имя, README с live URL, скриншоты, stack.
- README каждого проекта: зачем, стек, как запустить, env-vars (имена, не значения).
- LinkedIn: заголовок, описание, проекты.
- Резюме: 1 страница, ключевые технологии, P-проекты со ссылками.
- Собеседование: LeetCode — не главное. Показывай код, обсуждай решения, знай свой стек.
- Что дальше: backend (Node, Postgres), DevOps (Docker basics), system design, open-source.
- Ресурсы: roadmap.sh (закрой узлы), Josh Comeau, Theo (t3.gg), Lee Robinson (Vercel), web.dev.

---

## P3-Fullstack-Nextjs (большой проект)

Расширение M13 «Заметки» до полноценного продукта:
- **Комментарии** под публичными заметками (Server Action + RLS).
- **Теги**: many-to-many, фильтр ленты по тегу.
- **Поиск**: full-text через Postgres `ts_vector` или Supabase FTS.
- **Профили**: `/u/[username]` — публичные заметки юзера, аватарка.
- **Оптимизация**: `next/image` на аватарках, `priority` на LCP, Speed Insights, Lighthouse ≥ 90.
- **CI/CD**: preview deployments, Lighthouse CI в GitHub Actions.
- **Monitoring**: Sentry для error tracking.
- **Production-ready**: CSP headers, rate limit, dependency audit.
- Деплой на прод-домен, README с архитектурой, скриншотами, Lighthouse-скорами.

---

## MOC-Nextjs — заполнить раздел «Прод (модуль 14)»
## MOC-Web — заполнить модуль 10 и 13 разделы
## Start-Here — убрать «_(скоро)_» у модуля 14 и P3.

---

## Out of Scope
- Docker / Kubernetes — Vercel не требует.
- Другие хостинги (Netlify, Cloudflare Pages) — фокус на Vercel.
- SRE / infra-as-code — для фронтендера избыточно.
- Advanced observability (Datadog, Prometheus) — упомянуть, не углубляться.
