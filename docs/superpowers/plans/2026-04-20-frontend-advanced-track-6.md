# Track 6 — Команда и культура — Implementation Plan

**Goal:** Написать 4 модуля (~20 уроков) трека «Команда и культура» для FrontendAdvanced. Soft + документальная сторона senior-работы.

**Architecture:** Каталог `A6-Команда-и-культура/` с 4 подпапками. По `00-Обзор-модуля.md` + 5 уроков. Та же структура, что в Track 3/4/5.

**Tech stack:** Markdown, GitHub (PR, review), ADR-tools, RFC templates, semver.

---

## File Structure

```
A6-Команда-и-культура/
├── A6.1-Tech-writing/
│   ├── 00-Обзор-модуля.md
│   ├── A6.1.1-ADR-Architectural-Decision-Record.md
│   ├── A6.1.2-RFC-Request-for-Comments.md
│   ├── A6.1.3-Postmortem-blameless.md
│   ├── A6.1.4-README-и-docs-для-пакета.md
│   └── A6.1.5-Changelog-и-release-notes.md
├── A6.2-Senior-code-review/
│   ├── 00-Обзор-модуля.md
│   ├── A6.2.1-Цели-code-review.md
│   ├── A6.2.2-Уровни-комментариев-nits-vs-blockers.md
│   ├── A6.2.3-Как-писать-комментарий.md
│   ├── A6.2.4-Как-принимать-ревью.md
│   └── A6.2.5-Антипаттерны-ревью.md
├── A6.3-Open-source/
│   ├── 00-Обзор-модуля.md
│   ├── A6.3.1-Зачем-контрибьютить.md
│   ├── A6.3.2-Как-выбрать-проект.md
│   ├── A6.3.3-Первый-PR-процесс.md
│   ├── A6.3.4-Поддержание-и-maintainer-mode.md
│   └── A6.3.5-Лицензии-и-DCO-CLA.md
└── A6.4-Команда-и-менторинг/
    ├── 00-Обзор-модуля.md
    ├── A6.4.1-1-1-и-обратная-связь.md
    ├── A6.4.2-Онбординг-джуна.md
    ├── A6.4.3-Tech-lead-vs-staff.md
    ├── A6.4.4-Конфликты-и-эскалация.md
    └── A6.4.5-Личный-рост-senior-plus.md
```

## Lesson content themes

**A6.1 Tech writing** — ADR (формат Michael Nygard, status/context/decision/consequences, когда писать), RFC (от идеи до решения, public draft, stakeholders), postmortem (blameless, timeline, contributing factors, action items), README (TL;DR, quickstart, API, contributing), changelog (Keep a Changelog, semver, автогенерация).

**A6.2 Senior code review** — цели (knowledge sharing, bugs, стандарты), уровни nit/suggestion/question/blocker, как формулировать (вопрос vs команда, приоритет, пример), принимать ревью (не защищаться, объяснять why, push back с аргументами), антипаттерны (bike-shedding, rubber-stamp, toxic nitpicking, ревью по стилю вместо автоформаттера).

**A6.3 Open source** — мотивация (опыт/резюме/вклад), выбор (активность, good-first-issue, maintainer-вежливость), процесс первого PR (issue → discussion → PR → review-цикл), поддержание своего проекта (release cadence, issue triage, burnout), лицензии (MIT/Apache/GPL/ISC), DCO/CLA.

**A6.4 Команда и менторинг** — 1:1 с менеджером/джуном (cadence, структура, feedback), онбординг (первая неделя/месяц, buddy, первые таски), tech lead vs staff (scope, ответственность, IC path), конфликты (disagree and commit, эскалация), рост senior+ (T-shape → M-shape, публичность, доклады).

## Subagent dispatch

4 параллельных субагента — по одному на модуль. Те же правила (em-dash, пояснения англицизмов, 6 секций).

Референс: `A4.1.1` или любой A3/A4-урок.

## Follow-up

- Обновить `00-Start-Here.md`: Track 6 в готовый.
- Создать `MOC/MOC-Senior.md`.
- Добавить `MOC-Senior` в список MOC в Start-Here.
