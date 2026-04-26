# Frontend Course — Module 04 (CSS продвинутый) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: superpowers:subagent-driven-development. Контентный проект.

**Goal:** Наполнить модуль 04 «CSS продвинутый»: обзор + 4 урока + мини-проект «Tailwind-редизайн резюме» + обновить MOC-CSS + снять пометку «скоро» в Start-Here.

**Architecture:** Структура как в модулях 01–03. Шаблон урока (6 секций), средняя глубина.

**Базовые пути:**
- Vault: `/Users/luckyme/Desktop/maloyfront/FrontendCourse/`
- Модуль: `FrontendCourse/04-CSS-продвинутый/`

---

## File Structure

```
FrontendCourse/
├── 00-Start-Here.md                             (правка)
├── 04-CSS-продвинутый/
│   ├── 00-Обзор-модуля.md                       (новый)
│   ├── 04.1-CSS-переменные.md                   (новый)
│   ├── 04.2-Transitions-и-анимации.md           (новый)
│   ├── 04.3-Препроцессоры-и-современный-CSS.md  (новый)
│   └── 04.4-Tailwind-CSS.md                     (новый)
├── Проекты/Мини/
│   └── M04-Tailwind-редизайн-резюме.md          (новый)
└── MOC/
    └── MOC-CSS.md                               (правка — заполнить «Продвинутое»)
```

Итого: **6 новых файлов**, 2 правки.

---

## Task 1: Обзор модуля 04

**Create:** `FrontendCourse/04-CSS-продвинутый/00-Обзор-модуля.md`

**Exact content:**

```markdown
---
тип: обзор-модуля
модуль: 04-CSS-продвинутый
статус: not-started
roadmap: https://roadmap.sh/frontend#css
---

# Модуль 04 — CSS продвинутый

**roadmap.sh:** [раздел CSS во frontend-roadmap](https://roadmap.sh/frontend#css)

База CSS уже есть. Этот модуль — про инструменты, которые ускоряют работу и делают интерфейс «живым»: CSS-переменные для тематизации, анимации для отклика, обзор препроцессоров (чтобы прочитать чужой код) и Tailwind — главный utility-фреймворк современного фронта.

## Что изучаем
- CSS custom properties (переменные) — дизайн-токены, тема, динамика из JS.
- Transitions и `@keyframes` — плавные состояния и анимации.
- Препроцессоры (Sass, PostCSS) и современный CSS (nesting) — обзорно, чтобы читать и понимать.
- Tailwind CSS — utility-first подход, config, responsive/state-варианты.

## Уроки
- [ ] [[04.1-CSS-переменные]]
- [ ] [[04.2-Transitions-и-анимации]]
- [ ] [[04.3-Препроцессоры-и-современный-CSS]]
- [ ] [[04.4-Tailwind-CSS]]

## Итоговая практика
- [ ] Мини-проект: [[M04-Tailwind-редизайн-резюме]] — переписать резюме из [[M03-Стилизованное-резюме]] на Tailwind + добавить CSS-переменные и анимации.

## Связанные MOC
- [[MOC-CSS]] — обновляется по итогам модуля.

## Чек-лист завершения
- [ ] все 4 урока прочитаны
- [ ] мини-проект с Tailwind запушен на GitHub
- [ ] Lighthouse Accessibility ≥ 95, Performance ≥ 90
- [ ] узлы CSS в roadmap.sh отмечены как done

## Milestone
После этого модуля идёт **первый крупный проект [[P1-Лендинг-по-Figma]]** — по макету сверстать полноценный лендинг.
```

---

## Task 2: Урок 04.1 — CSS-переменные

**Create:** `FrontendCourse/04-CSS-продвинутый/04.1-CSS-переменные.md`

**Frontmatter:**
```yaml
---
модуль: 04-CSS-продвинутый
тема: CSS-переменные (custom properties)
статус: to-read
roadmap: https://roadmap.sh/frontend#css
связано: "[[04.4-Tailwind-CSS]]"
---
```

**Заголовок:** `# CSS-переменные (custom properties)`

**`## Зачем это нужно`:** Проект вырос — и ты заметил, что фирменный синий цвет прописан в 30 местах CSS. Поменять его теперь — ад. CSS-переменные решают это: одно значение в одном месте, используется везде. Плюс открывают темизацию и динамику из JS.

**`## Главное` (~280–360 слов):**
- **Синтаксис.** Объявление: `--имя: значение;` внутри любого селектора (обычно `:root`). Чтение: `color: var(--имя);`. Имя — любое, с двумя дефисами в начале.
- **`:root` и scope.** `:root` = корень документа (`<html>`), переменные оттуда доступны везде. Но переменные можно объявлять и в любом другом селекторе — тогда они доступны только внутри этого элемента и его потомков (наследуются).
- **Fallback.** `var(--primary, #2d6cdf)` — если переменная не задана, используется вторая часть. Полезно при постепенной миграции.
- **Тематизация (light/dark).** Классика: переменные в `:root`, переопределение в `[data-theme="dark"] { --bg: #111; --text: #eee; }`. Переключение — одним атрибутом на `<html>` из JS, стили применяются сами благодаря наследованию.
- **Динамика из JS.** `element.style.setProperty('--x', '200px')` — меняет переменную прямо во время работы страницы. Так делают слайдеры, drag-n-drop, эффекты с координатами курсора.
- **Отличие от препроцессорных переменных.** Sass-переменные существуют только на этапе компиляции. CSS custom properties живут в рантайме — их видят браузер, DevTools и JS. Это принципиально другой инструмент.
- **Дизайн-токены.** В реальных проектах переменные группируют по смыслу: цвета (`--color-primary`), отступы (`--space-sm`, `--space-lg`), шрифты (`--font-body`). Это становится основой дизайн-системы.

**`## Пример кода`** — блок css:
```css
:root {
  --color-primary: #2d6cdf;
  --color-text: #222;
  --color-bg: #ffffff;
  --space-md: 16px;
  --radius: 8px;
}

[data-theme="dark"] {
  --color-text: #eee;
  --color-bg: #111;
}

body {
  color: var(--color-text);
  background: var(--color-bg);
  font-family: system-ui, sans-serif;
}

.btn {
  background: var(--color-primary);
  padding: var(--space-md);
  border-radius: var(--radius);
  color: white;
}

/* локальный scope — переменная только внутри .card */
.card {
  --card-padding: 24px;
  padding: var(--card-padding);
}
```

**`## Частые ошибки`** — 4 пункта:
- Забыть два дефиса при объявлении (`-primary` вместо `--primary`) → переменная не работает, ошибок в консоли нет.
- Пытаться использовать Sass-переменную (`$primary`) там, где нужна рантайм-переменная → не сработает в `calc()` с JS-значениями, в медиа-запросах, не видит браузер.
- Объявлять всё внутри `:root` подряд, без группировки → через полгода палитра станет кашей.
- Переопределять переменные на каждом селекторе «на всякий случай» → ломает наследование и темы.

**`## Задания`:**
- [ ] В `style.css` резюме вынеси палитру (минимум 4 цвета) и отступы в переменные на `:root`.
- [ ] Добавь переключение `data-theme="dark"` на `<html>` — через кнопку или devtools. Проверь, что все цвета переключаются одним свойством.
- [ ] Через DevTools → Elements → Styles → `:root` отредактируй переменную вживую и посмотри, как обновляется страница.
- [ ] Проверь `element.style.setProperty('--color-primary', 'crimson')` в консоли — убедись, что работает.

**`## Что почитать`:**
- [MDN — Using CSS custom properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
- [web.dev — A complete guide to CSS custom properties](https://web.dev/learn/css/custom-properties/)
- [CSS-Tricks — A Complete Guide to Custom Properties](https://css-tricks.com/a-complete-guide-to-custom-properties/)

Блок — `css`.

---

## Task 3: Урок 04.2 — Transitions и анимации

**Create:** `FrontendCourse/04-CSS-продвинутый/04.2-Transitions-и-анимации.md`

**Frontmatter:**
```yaml
---
модуль: 04-CSS-продвинутый
тема: Transitions и анимации
статус: to-read
roadmap: https://roadmap.sh/frontend#css
связано: "[[04.1-CSS-переменные]]"
---
```

**Заголовок:** `# Transitions и анимации`

**`## Зачем это нужно`:** Кнопки, которые мгновенно меняют цвет при hover, выглядят дёшево. Плавный переход в 150мс — и интерфейс ощущается качественным. Анимации (`@keyframes`) позволяют создавать спиннеры, появление модалок, скролл-эффекты — всё без JS-библиотек.

**`## Главное` (~320–400 слов):**
- **Transition — переход между состояниями.** `transition: свойство длительность easing задержка;`. Пример: `transition: background 200ms ease;`. Применяется автоматически, когда значение свойства меняется (hover, focus, класс через JS).
- **Easing (функция кривой).** `ease` (по умолчанию), `linear`, `ease-in`, `ease-out`, `ease-in-out`. Тонкая настройка — `cubic-bezier(...)` из онлайн-редактора. `ease-out` приятнее всего для UI: быстро на старте, мягко в конце.
- **Что анимировать дёшево.** `transform` (translate, rotate, scale) и `opacity` — браузер считает их на GPU, 60 fps даже на слабом ноуте. Это главное правило: для движения используй `transform`, не `top`/`left`/`margin`.
- **Что анимировать дорого.** `width`, `height`, `margin`, `top`/`left` — заставляют браузер пересчитывать раскладку всей страницы (reflow). На мобиле фризы гарантированы.
- **`@keyframes` — многошаговые анимации.** Описываешь кадры по процентам: `0%`, `50%`, `100%` (или `from`/`to`). Запускаешь через `animation: имя длительность easing iteration direction fill-mode;`.
- **`animation-iteration-count`, `animation-fill-mode`.** `iteration-count: infinite` — крутится вечно (спиннер). `fill-mode: forwards` — после окончания остаётся в конечном состоянии, иначе скакнёт обратно.
- **`prefers-reduced-motion`.** Пользователи могут отключить анимации в ОС. Уважай это: `@media (prefers-reduced-motion: reduce) { * { animation: none !important; transition: none !important; } }`.
- **`will-change`.** Подсказка браузеру: «этот элемент будет анимироваться, готовься». Используй точечно на сложных анимациях, не навешивай на всё подряд — расход памяти.

**`## Пример кода`** — блок css:
```css
/* плавная кнопка */
.btn {
  background: #2d6cdf;
  color: white;
  padding: 12px 20px;
  border: none;
  border-radius: 8px;
  transition: background 150ms ease-out, transform 150ms ease-out;
}

.btn:hover {
  background: #1e4fa0;
  transform: translateY(-2px);
}

.btn:active {
  transform: translateY(0);
}

/* спиннер */
@keyframes spin {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}

.spinner {
  width: 32px;
  height: 32px;
  border: 3px solid #eee;
  border-top-color: #2d6cdf;
  border-radius: 50%;
  animation: spin 800ms linear infinite;
}

/* появление модалки */
@keyframes fade-in {
  from { opacity: 0; transform: translateY(-10px); }
  to   { opacity: 1; transform: translateY(0); }
}

.modal {
  animation: fade-in 200ms ease-out forwards;
}

@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

**`## Частые ошибки`** — 4 пункта:
- Анимировать `width`/`height` вместо `transform: scale(...)` → фризы на мобиле.
- Transition длиннее 300мс для простых UI-переходов → интерфейс ощущается заторможенным. 100–200мс — норма для hover и смен состояний.
- Не учитывать `prefers-reduced-motion` → для людей с вестибулярными нарушениями это реальная боль.
- Навешивать `will-change: transform` на все элементы профилактически → браузер выделяет память под каждое, общий тормоз.

**`## Задания`:**
- [ ] Сделай плавный hover для всех кнопок и ссылок в резюме (`transition: ... 150ms ease-out`).
- [ ] Добавь `@keyframes fade-in` и прогони им появление основных секций при загрузке страницы.
- [ ] Сделай простой спиннер (`@keyframes spin`, `animation-iteration-count: infinite`).
- [ ] Добавь `@media (prefers-reduced-motion: reduce)` c отключением анимаций.
- [ ] Открой DevTools → Performance → нажми запись, сделай hover/скролл. Посмотри, проседает ли FPS.

**`## Что почитать`:**
- [MDN — Using CSS transitions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_transitions/Using_CSS_transitions)
- [MDN — Using CSS animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animations/Using_CSS_animations)
- [web.dev — Animations and performance](https://web.dev/articles/animations-guide)
- [cubic-bezier.com](https://cubic-bezier.com/) — редактор easing-кривых.

Блок — `css`.

---

## Task 4: Урок 04.3 — Препроцессоры и современный CSS

**Create:** `FrontendCourse/04-CSS-продвинутый/04.3-Препроцессоры-и-современный-CSS.md`

**Frontmatter:**
```yaml
---
модуль: 04-CSS-продвинутый
тема: Препроцессоры и современный CSS
статус: to-read
roadmap: https://roadmap.sh/frontend#css
связано: "[[04.1-CSS-переменные]]"
---
```

**Заголовок:** `# Препроцессоры и современный CSS`

**`## Зачем это нужно`:** Исторически CSS был беден — не было переменных, вложенности, функций. Появились препроцессоры (Sass, Less) — они компилируют свой синтаксис в обычный CSS. Сегодня многое из этого уже есть в нативном CSS, и роль препроцессоров убывает — но они всё ещё живут в легаси и крупных дизайн-системах. Этот урок — обзорный: чтобы не пугаться `.scss`-файлов в чужом проекте и понимать, когда это действительно нужно.

**`## Главное` (~300–380 слов):**
- **Что такое препроцессор.** Инструмент, который пишет «расширенный CSS» (свой синтаксис), а потом билдит его в обычный `.css`, который понимает браузер. Самый популярный — **Sass** (расширение `.scss`).
- **Что даёт Sass.** Переменные (`$primary: blue;`), вложенность (nesting), миксины (функции), наследование стилей (`@extend`), разбиение на файлы (`partials`, `@use`), математика (`width: 100% / 3`).
- **Синтаксис SCSS — быстрый обзор.** Выглядит как обычный CSS, но с фичами:
    - Nesting: `.card { h2 { color: blue; } &:hover { ... } }` — `&` означает «родитель».
    - Mixin: `@mixin button($color) { background: $color; ... }` → `@include button(red);`.
    - Partial: файл `_variables.scss` импортируется через `@use "variables";`.
- **CSS Nesting нативный.** С 2023 браузеры (Chrome 112+, Safari 16.5+) поддерживают вложенность без препроцессора:
    ```css
    .card {
      & h2 { color: blue; }
      &:hover { background: #eee; }
    }
    ```
    Синтаксис почти идентичен Sass. Это серьёзно снижает необходимость в препроцессоре.
- **PostCSS и autoprefixer.** Другая категория инструментов: берут обычный CSS и прогоняют через плагины. Autoprefixer сам дорисует вендорные префиксы (`-webkit-`, `-moz-`), куда нужно. Почти во всех сборках (Vite, Next.js) это встроено по умолчанию.
- **Когда реально нужен Sass.** Легаси-проект (готовая кодобаза уже на Sass). Дизайн-система с большим количеством mixin-логики. Команда привыкла и не хочет мигрировать. Для новых pet-проектов — CSS custom properties + nesting + Tailwind закрывают 99% задач.
- **Не путай с CSS-in-JS.** `styled-components`, `Emotion`, CSS Modules — это уже React-территория, рассмотрим в модуле 10.

**`## Пример кода`** — блок scss:
```scss
// variables.scss
$primary: #2d6cdf;
$space-md: 16px;

@mixin card {
  padding: $space-md;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.article {
  @include card;
  color: $primary;

  h2 {
    margin-top: 0;

    &:hover {
      color: darken($primary, 10%);
    }
  }

  .badge {
    background: $primary;
    color: white;
  }
}
```

И тот же смысл на нативном современном CSS:
```css
:root {
  --primary: #2d6cdf;
  --space-md: 16px;
}

.article {
  padding: var(--space-md);
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  color: var(--primary);

  & h2 {
    margin-top: 0;

    &:hover {
      color: color-mix(in srgb, var(--primary) 80%, black);
    }
  }

  & .badge {
    background: var(--primary);
    color: white;
  }
}
```

**`## Частые ошибки`** — 3 пункта:
- Начинать новый pet-проект в 2026 с Sass «по привычке» → потеряешь время на билд, а выгоды почти нет, если не работаешь с большой дизайн-системой.
- Путать Sass-переменные и CSS custom properties → Sass-переменные не работают в рантайме, их не видно в DevTools, нельзя менять из JS.
- Вкладывать селекторы на 5 уровней вглубь («потому что Sass позволяет») → специфичность выстреливает в ногу, код становится нечитаемым.

**`## Задания`:**
- [ ] Открой любой заметный open-source React-проект на GitHub (например, [MUI](https://github.com/mui/material-ui)) и найди `.scss` или `.css` файлы — посмотри на структуру.
- [ ] Попробуй один раз: создай маленький проект, поставь `sass` (`npm i -D sass`), напиши `style.scss` с переменной и mixin, скомпилируй в `style.css`. Прочувствуй workflow.
- [ ] На своём резюме — перепиши пару секций с CSS Nesting (без препроцессора). Проверь в современном Chrome.
- [ ] Прочитай [одну статью про современный CSS](https://moderncss.dev/) — там классный обзор фич, которые пришли за последние годы.

**`## Что почитать`:**
- [Sass official docs](https://sass-lang.com/guide) — быстрый старт на 30 минут.
- [MDN — CSS Nesting](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_nesting)
- [Modern CSS Solutions](https://moderncss.dev/) — серия статей «как раньше делали через костыли, а теперь нативно».
- [PostCSS](https://postcss.org/) — официальный сайт.

Блоки — `scss` и `css`.

---

## Task 5: Урок 04.4 — Tailwind CSS

**Create:** `FrontendCourse/04-CSS-продвинутый/04.4-Tailwind-CSS.md`

**Frontmatter:**
```yaml
---
модуль: 04-CSS-продвинутый
тема: Tailwind CSS
статус: to-read
roadmap: https://roadmap.sh/frontend#css
связано: "[[04.1-CSS-переменные]], [[04.3-Препроцессоры-и-современный-CSS]]"
---
```

**Заголовок:** `# Tailwind CSS`

**`## Зачем это нужно`:** Писать CSS по-старому — придумывать классы, держать файл стилей рядом с HTML, следить за именованием. Tailwind переворачивает подход: вместо `.card { padding: 16px; }` ты пишешь `<div class="p-4">` прямо в разметке. Звучит странно, но это самый популярный CSS-инструмент последних 3 лет — за счёт скорости разработки и консистентности. Для pet-проектов, MVP и React-приложений — стандарт де-факто.

**`## Главное` (~340–420 слов):**
- **Utility-first идея.** Каждый класс — это одно свойство. `p-4` = `padding: 16px;`. `flex` = `display: flex;`. `text-lg` = `font-size: 18px;`. Ты комбинируешь утилиты прямо в HTML, не придумывая имён классов.
- **Почему это не плохо, хотя выглядит ужасно.** (1) Не надо придумывать классы — огромная экономия когнитивной нагрузки. (2) Стили не «утекают» — ничего случайно не стилизуется. (3) Удалил компонент — удалил его стили вместе с ним. (4) Консистентность: `p-4`, `p-6`, `p-8` — только из согласованной шкалы, а не «вчера 14px, сегодня 15px».
- **Установка.** Для проекта с Vite/Next.js: `npm i -D tailwindcss`, дальше `npx tailwindcss init`. Подключить директивы в главный CSS: `@tailwind base; @tailwind components; @tailwind utilities;`. Классы сразу работают.
- **`tailwind.config.js` — твоя дизайн-система.** Здесь переопределяется палитра, брейкпоинты, шрифты, радиусы. `theme.extend.colors.primary = "#2d6cdf"` — и теперь работает `bg-primary`, `text-primary`. Это и есть дизайн-токены.
- **Responsive префиксы.** `md:flex` = применяется от брейкпоинта `md` (768px) и выше. Mobile-first: по умолчанию стиль для узкого экрана, потом `md:` дорисовывает. Пример: `<div class="flex-col md:flex-row">` — колонка на мобилке, ряд на десктопе.
- **State-префиксы.** `hover:bg-blue-600`, `focus:ring-2`, `disabled:opacity-50`, `dark:bg-slate-900`. Всё, что было псевдо-классами в CSS, здесь становится префиксом.
- **`@apply` — когда очень хочется именованный класс.** Внутри CSS: `.btn-primary { @apply px-4 py-2 bg-blue-500 text-white rounded; }`. Используй редко, только для реально повторяющихся сложных комбинаций. Если всегда `@apply` — это просто старый CSS в обёртке.
- **Когда использовать.** Pet-проекты, MVP, React/Next.js, landing-страницы с жёстким дедлайном. В модулях 10 и 13 будем делать React-приложения с Tailwind.
- **Когда НЕ использовать.** Очень кастомный дизайн, где утилиты не ложатся на макет (скорее — настрой config). Корпоративные дизайн-системы с жёсткими токенами (но и там можно, через кастомизацию config).

**`## Пример кода`** — блоки html и js:
```html
<!-- карточка товара на Tailwind -->
<article class="max-w-sm rounded-lg bg-white p-6 shadow-md hover:shadow-lg transition-shadow dark:bg-slate-800">
  <h2 class="text-xl font-semibold text-slate-900 dark:text-white">
    Название товара
  </h2>
  <p class="mt-2 text-sm text-slate-600 dark:text-slate-300">
    Короткое описание в две строки.
  </p>
  <div class="mt-4 flex items-center justify-between">
    <span class="text-lg font-bold text-blue-600">1 990 ₽</span>
    <button class="rounded-md bg-blue-600 px-4 py-2 text-white hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-400">
      Купить
    </button>
  </div>
</article>

<!-- адаптивная сетка -->
<div class="grid gap-4 grid-cols-1 md:grid-cols-2 lg:grid-cols-3">
  <!-- карточки -->
</div>
```

```js
// tailwind.config.js — пример кастомизации
/** @type {import('tailwindcss').Config} */
export default {
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
  theme: {
    extend: {
      colors: {
        primary: "#2d6cdf",
        accent: "#ffb347",
      },
      fontFamily: {
        sans: ["Inter", "system-ui", "sans-serif"],
      },
    },
  },
  plugins: [],
};
```

**`## Частые ошибки`** — 4 пункта:
- Использовать `@apply` везде подряд → возвращаешься к старому CSS, теряешь преимущества Tailwind.
- Не настраивать `tailwind.config.js` под свой дизайн → используешь дефолтные цвета и получаешь «bootstrap-look».
- Забывать про `content: [...]` в config → Tailwind не сканирует твои файлы и в prod-билде классы выпиливаются как «неиспользуемые».
- Писать «магические» строки типа `class="w-[237px] text-[13.5px]"` всегда → arbitrary-значения норм для исключений, но если ты их ставишь постоянно, твоя шкала не настроена.

**`## Задания`:**
- [ ] Создай отдельную папку, поставь Tailwind по [официальному гайду](https://tailwindcss.com/docs/installation). Убедись, что `<h1 class="text-4xl font-bold text-blue-600">Hello</h1>` — работает.
- [ ] Свёрстай одну карточку (как в примере выше) и одну адаптивную сетку карточек (`grid-cols-1 md:grid-cols-2 lg:grid-cols-3`).
- [ ] В `tailwind.config.js` добавь кастомный цвет `primary` и используй `bg-primary text-primary` в разметке.
- [ ] Пройди официальный [Tailwind Play](https://play.tailwindcss.com/) — sandbox, можно без установки потренироваться.

**`## Что почитать`:**
- [Tailwind CSS — официальная документация](https://tailwindcss.com/docs) — лучшие доки в отрасли, читать как справочник.
- [Tailwind CSS — why utility-first](https://tailwindcss.com/docs/utility-first) — философия подхода.
- [Tailwind UI](https://tailwindui.com/) — платная библиотека компонентов, но бесплатные примеры дают вдохновение.
- [Heroicons](https://heroicons.com/) — бесплатные SVG-иконки от авторов Tailwind.

Блоки — `html` и `js`.

---

## Task 6: Мини-проект M04 — Tailwind-редизайн резюме

**Create:** `FrontendCourse/Проекты/Мини/M04-Tailwind-редизайн-резюме.md`

**Exact content:**

```markdown
---
тип: мини-проект
модуль: 04-CSS-продвинутый
статус: not-started
---

# M04 — Tailwind-редизайн резюме

Мини-проект после модуля 04. Берём результат [[M03-Стилизованное-резюме]] и переписываем стили на Tailwind + добавляем CSS-переменные и анимации. Цель — прочувствовать utility-first подход на реальной странице.

## Задача

Новая ветка `tailwind-redesign` в том же репозитории `resume-html` (или отдельный `resume-tailwind` — на твой выбор).

## Требования

1. **Установка:** Tailwind подключён через CLI или Vite. В билде работают только используемые классы (проверить через DevTools — чистый `style.css` без мусора).
2. **Typography:** шрифт через `tailwind.config.js` (Google Fonts или system-ui). Иерархия заголовков через `text-*` утилиты.
3. **Цвета:** минимум 2 кастомных цвета (`primary`, `accent`) в `tailwind.config.js`. НЕ использовать базовую палитру Tailwind как «как есть» — это должно выглядеть узнаваемо твоим.
4. **Layout:** Flex в шапке, Grid в основном контенте. Все адаптивные стили через `sm:`, `md:`, `lg:` префиксы. Mobile-first.
5. **CSS-переменные:** хотя бы одна `:root` переменная для чего-то, что не закрывается Tailwind-ом (например, `--scroll-padding` или `--header-height` для sticky-шапки). Интеграция через `theme.extend` или прямой `var()`.
6. **Анимации:** hover на кнопках/ссылках (`transition` + `hover:`), fade-in на главном заголовке или секциях (`@keyframes` в кастомном CSS). Уважать `prefers-reduced-motion`.
7. **Dark mode:** включить `darkMode: 'class'` в конфиге, проверить ключевые классы с `dark:` и переключатель темы (кнопка + `document.documentElement.classList.toggle('dark')`).
8. **Accessibility:** focus-ring видимый, `:focus-visible`, labels на инпутах.
9. **Lighthouse:** Accessibility ≥ 95, Performance ≥ 90.

## Чего НЕ должно быть

- `@apply`-классов на всё подряд — это антипаттерн.
- Захардкоженных цветов в HTML типа `style="color: #2d6cdf"`.
- Фикс-`px` в критичных местах (ширина основного контейнера должна тянуться через `max-w-*`).
- Самописного «сброса» стилей, который ломает `preflight` Tailwind.

## Сдача

1. Пуш в ветку `tailwind-redesign` (или отдельный репо).
2. README обновить: «Переписано на Tailwind в рамках модуля 04», короткий список фич (dark mode, анимации, адаптив).
3. Скриншоты в `/screenshots/` — light и dark, на 375/768/1440px.
4. Ревью на созвоне.

## Критерии приёмки ревью
- [ ] Tailwind настроен, prod-билд без лишних классов.
- [ ] В `tailwind.config.js` кастомные токены (минимум цвета и шрифт).
- [ ] Dark mode работает переключателем.
- [ ] Анимации корректно отключаются через `prefers-reduced-motion`.
- [ ] Lighthouse проходит пороги.
- [ ] Классы в разметке читаемы — нет «1000 классов подряд» от отчаяния, там где надо — компонентизация через `@apply` или React (в будущем).

## Что дальше
После этого модуля — **первый большой проект [[P1-Лендинг-по-Figma]]**. Все CSS-инструменты уже есть; нужно только научиться переводить макет в код.
```

---

## Task 7: Обновить MOC-CSS

**Modify:** `FrontendCourse/MOC/MOC-CSS.md`

- [ ] **Step 7.1:** Заменить секцию «## Продвинутое (модуль 04 — скоро)» на наполненную. Итоговый файл (полностью):

```markdown
---
тип: MOC
тема: CSS
---

# MOC — CSS

Карта знаний по CSS. Пополняется по мере прохождения модулей 03, 04 и возвратов из React/Tailwind.

## База (модуль 03)
- [[03.1-Подключение-CSS-и-синтаксис]]
- [[03.2-Селекторы]]
- [[03.3-Каскад-специфичность-наследование]]
- [[03.4-Box-model-и-позиционирование]]

## Layout (модуль 03)
- [[03.5-Flexbox]]
- [[03.6-Grid-и-адаптив]]

## Продвинутое (модуль 04)
- [[04.1-CSS-переменные]]
- [[04.2-Transitions-и-анимации]]
- [[04.3-Препроцессоры-и-современный-CSS]]
- [[04.4-Tailwind-CSS]]

## Практика
- [[M03-Стилизованное-резюме]]
- [[M04-Tailwind-редизайн-резюме]]
- [[P1-Лендинг-по-Figma]] _(скоро)_
```

---

## Task 8: Обновить 00-Start-Here.md

**Modify:** `FrontendCourse/00-Start-Here.md`

- [ ] **Step 8.1:** Заменить строку `- [[04-CSS-продвинутый/00-Обзор-модуля|Модуль 04 — CSS продвинутый]] _(скоро)_` на `- [[04-CSS-продвинутый/00-Обзор-модуля|Модуль 04 — CSS продвинутый]]`.

---

## Task 9: Верификация

- [ ] **Step 9.1:** `find FrontendCourse/04-CSS-продвинутый -type f -name "*.md" | sort` должен вернуть 5 файлов.

- [ ] **Step 9.2:** `M04-Tailwind-редизайн-резюме.md` существует в `Проекты/Мини/`.

- [ ] **Step 9.3:** MOC-CSS содержит 4 ссылки на уроки 04.1–04.4.

- [ ] **Step 9.4:** В 00-Start-Here.md у модуля 04 больше нет «_(скоро)_».

- [ ] **Step 9.5:** Отчитаться: модуль 04 готов, 4 урока + мини-проект + MOC обновлён.

---

## Self-Review

**1. Spec coverage:**
- CSS продвинутый по design: анимации, CSS-переменные, Tailwind, препроцессоры (обзор) → Tasks 2–5 покрывают всё. ✓
- Мини-проект после модуля → Task 6 (Tailwind-редизайн). ✓
- MOC-CSS обновлён → Task 7. ✓
- Start-Here обновлён → Task 8. ✓

**2. Placeholder scan:**
- TBD/TODO отсутствуют. ✓
- «_(скоро)_» в MOC-CSS рядом с `[[P1-Лендинг-по-Figma]]` — осознанный контент-маркер для ученика, не plan-плейсхолдер. ✓

**3. Type consistency:**
- Имена уроков и мини-проекта согласованы везде: обзор (Task 1), frontmatter уроков (Tasks 2–5), MOC (Task 7), верификация (Task 9). ✓

Self-review пройден.

---

## Out of Scope

- CSS-in-JS, CSS Modules, styled-components — модуль 10 (React экосистема).
- Сложные анимации с GSAP, Framer Motion — отдельно в React-стеке, если будет нужно.
- SVG-анимации, canvas — за пределами курса.
- Глубокая настройка PostCSS-пайплайна — по мере появления задач.
