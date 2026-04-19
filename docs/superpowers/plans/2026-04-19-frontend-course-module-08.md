# Frontend Course — Module 08 (Git и DevTools) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: superpowers:subagent-driven-development. Контентный проект.

**Goal:** Наполнить модуль 08 «Git и DevTools»: обзор + 6 уроков + мини-проект (Git-workflow с DevTools debug) + создать MOC-Tools + обновить Start-Here.

**Architecture:** Структура модулей 01–07. Шаблон урока (6 секций), средняя глубина. Практика: каждую команду Git и каждый DevTools-таб — нажать руками. Цель модуля — рутинные рабочие инструменты (Git + браузерные DevTools), без которых дальше React/Next.js невозможен.

**Базовые пути:**
- Vault: `/Users/luckyme/Desktop/maloyfront/FrontendCourse/`
- Модуль: `FrontendCourse/08-Git-и-DevTools/`

---

## File Structure

```
FrontendCourse/
├── 00-Start-Here.md                               (правка: убрать «_(скоро)_», добавить MOC-Tools)
├── 08-Git-и-DevTools/
│   ├── 00-Обзор-модуля.md                         (новый)
│   ├── 08.1-Git-основы.md                         (новый)
│   ├── 08.2-Ветки-и-merge.md                      (новый)
│   ├── 08.3-GitHub-и-PR.md                        (новый)
│   ├── 08.4-DevTools-Elements-и-Console.md        (новый)
│   ├── 08.5-DevTools-Network-и-Sources.md         (новый)
│   └── 08.6-DevTools-Application-и-Performance.md (новый)
├── Проекты/Мини/
│   └── M08-Git-workflow-и-debug.md                (новый)
└── MOC/
    └── MOC-Tools.md                               (новый)
```

Итого: **9 новых файлов**, 1 правка.

---

## Task 1: Обзор модуля 08

**Create:** `FrontendCourse/08-Git-и-DevTools/00-Обзор-модуля.md`

**Exact content:**

```markdown
---
тип: обзор-модуля
модуль: 08-Git-и-DevTools
статус: not-started
roadmap: https://roadmap.sh/frontend#version-control-systems
---

# Модуль 08 — Git и DevTools

**roadmap.sh:** [Version Control Systems](https://roadmap.sh/frontend#version-control-systems)

Ты уже коммитишь и пушишь — но скорее «по памяти команд», чем понимая, что реально происходит. И браузерные DevTools ты открываешь только чтобы посмотреть консоль. Этот модуль — про два рутинных инструмента фронтендера, которые используются каждый день: Git и DevTools браузера. Без них дальше (React, Next.js, реальные проекты) — никак.

## Что изучаем
- Git: что такое коммит, staging, HEAD, как Git хранит историю.
- Ветки, merge vs rebase, разрешение конфликтов.
- GitHub: remote, push/pull, PR, code review.
- DevTools: Elements + Console — правка DOM/CSS, консольные трюки.
- DevTools: Network + Sources — наблюдение запросов, точки остановки, отладка в браузере.
- DevTools: Application (storage, service workers), Performance, Lighthouse.

## Уроки
- [ ] [[08.1-Git-основы]]
- [ ] [[08.2-Ветки-и-merge]]
- [ ] [[08.3-GitHub-и-PR]]
- [ ] [[08.4-DevTools-Elements-и-Console]]
- [ ] [[08.5-DevTools-Network-и-Sources]]
- [ ] [[08.6-DevTools-Application-и-Performance]]

## Итоговая практика
- [ ] Мини-проект: [[M08-Git-workflow-и-debug]] — feature-branch → PR → merge с разрешением конфликта + отладка 3-4 подсунутых багов через DevTools.

## Связанные MOC
- [[MOC-Tools]] — карта по инструментам: Git, DevTools, build-tools (дополняется в модуле 12).

## Чек-лист завершения
- [ ] все 6 уроков прочитаны
- [ ] мини-проект: PR создан, merge с конфликтом прошёл, баги пофикшены с помощью DevTools
- [ ] в DevTools умеешь: поставить breakpoint, прочитать Network, отредактировать CSS в Elements, очистить storage
- [ ] в терминале уверенно делаешь: commit, branch, checkout, merge, rebase, push, pull, fetch
- [ ] узлы Git / VCS в roadmap.sh закрыты
```

---

## Task 2: Урок 08.1 — Git-основы

**Create:** `FrontendCourse/08-Git-и-DevTools/08.1-Git-основы.md`

**Frontmatter:**
```yaml
---
модуль: 08-Git-и-DevTools
тема: Git — основы, коммиты, staging
статус: to-read
roadmap: https://roadmap.sh/frontend#version-control-systems
связано: [[08.2-Ветки-и-merge]]
---
```

**Заголовок:** `# Git — основы, коммиты, staging`

**`## Зачем это нужно`:** Git — машина времени для кода. Без него невозможно откатить ошибку, работать в команде, держать историю и понимать, что ты вообще менял неделю назад. Даже соло-разработчик без Git работает вслепую.

**`## Главное` (~330–400 слов):** подразделы `### ...`:
- **Что такое Git.** Распределённая система контроля версий. У тебя локально — полная копия истории (не только текущее состояние, а ВСЕ коммиты, когда-либо сделанные в проекте). В GitHub — удалённая копия. Git ≠ GitHub.
- **Репозиторий и `.git`.** `git init` создаёт папку `.git/` в корне проекта — это и есть репозиторий. Там хранится вся история. Удалишь `.git/` — история пропадёт, код останется.
- **Три состояния файла.** Working directory (то, что ты сейчас видишь и правишь) → Staging area (index, что готово к коммиту) → Repository (история коммитов). `git add` двигает из working в staging, `git commit` — из staging в repo.
- **Что такое коммит.** Снимок состояния (snapshot), не diff. У коммита есть: хэш (SHA-1), автор, дата, сообщение, ссылка на родительский коммит. Один коммит = одно логическое изменение.
- **`git status` и `git diff`.** `status` — что изменилось, что в staging, что untracked. `diff` — что конкретно изменилось в строках (working vs staging по умолчанию). `diff --staged` — что сейчас в staging vs repo.
- **Атомарные коммиты.** Один коммит — одна мысль. Не смешивай «добавил фичу + поправил типос + отформатировал всё». Разные мысли = разные коммиты.
- **Сообщения коммитов.** Короткая строка (~50 симв) в императиве: «Add login form», «Fix typo in footer». Без точки. Хорошее сообщение отвечает на вопрос «что изменится, если я это применю?».
- **`git log` и HEAD.** `log` — история. `HEAD` — указатель на последний коммит текущей ветки. `HEAD~1` — предыдущий коммит, `HEAD~5` — пять назад.
- **`git restore` и `git reset`.** `restore <файл>` — откатить изменения в working directory (до последнего коммита). `restore --staged <файл>` — вынуть из staging обратно. `reset HEAD~1` — «забыть» последний коммит, но сохранить его изменения как untracked.
- **`.gitignore`.** Список того, что НЕ коммитится: `node_modules/`, `.env`, `.DS_Store`, `dist/`. Создавай СРАЗУ, иначе потом чистить.

**`## Пример кода`** — блок ```bash```:
```bash
# создание репо
git init
git status                 # посмотреть состояние

# первый коммит
echo "# My project" > README.md
git add README.md          # в staging
git status                 # теперь: Changes to be committed
git commit -m "Add README"

# проверка истории
git log --oneline

# typical workflow
echo "new line" >> README.md
git status                 # modified: README.md
git diff                   # что изменилось
git add README.md
git commit -m "Expand README"

# откат изменений до коммита
echo "oops" >> README.md
git restore README.md      # вернули как было

# вытащить из staging
git add README.md
git restore --staged README.md
```

**`## Частые ошибки`** — 4 bullet-а:
- Коммитить без `.gitignore` → в репо попадают `node_modules`, `.DS_Store`, `.env` с секретами. Добавляй `.gitignore` первым коммитом.
- Писать сообщения вроде «wip», «fix», «changes» — через месяц непонятно, что было. Пиши по-человечески.
- Делать один коммит на целый день работы — невозможно откатить часть. Коммить каждую логическую единицу.
- Путать `git reset` и `git revert`. `reset` — переписывает историю (опасно на пушнутом). `revert` — добавляет новый коммит, который «отменяет» старый (безопасно).

**`## Задания`:**
- [ ] Создай пустой репо, сделай 5 коммитов, посмотри `git log --oneline --graph`.
- [ ] Добавь `.gitignore` (например, node_modules, .DS_Store), сделай файл `node_modules/foo.js`, проверь `git status` — он не должен быть показан.
- [ ] Сделай правку в файл, выполни `git diff`, затем `git add`, затем `git diff --staged` — сравни.
- [ ] Сделай коммит, потом `git restore` прежней версии — убедись, что работает.

**`## Что почитать`:**
- [Pro Git book — Chapter 2](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)
- [GitHub — gitignore templates](https://github.com/github/gitignore)
- [MDN — Git](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/GitHub/Git)
- [Oh Shit, Git!?!](https://ohshitgit.com/)

Блок — `bash`.

---

## Task 3: Урок 08.2 — Ветки и merge

**Create:** `FrontendCourse/08-Git-и-DevTools/08.2-Ветки-и-merge.md`

**Frontmatter:**
```yaml
---
модуль: 08-Git-и-DevTools
тема: Ветки, merge, rebase, конфликты
статус: to-read
roadmap: https://roadmap.sh/frontend#version-control-systems
связано: [[08.1-Git-основы]], [[08.3-GitHub-и-PR]]
---
```

**Заголовок:** `# Ветки, merge, rebase, конфликты`

**`## Зачем это нужно`:** Ветка — это параллельная линия разработки. Ты начинаешь фичу или эксперимент, не ломая main. В командах это основа процесса — каждая задача живёт в своей ветке до мерджа. Ветки в Git дешёвые, короткие и должны использоваться постоянно.

**`## Главное` (~340–420 слов):** подразделы `### ...`:
- **Что такое ветка.** Указатель на коммит. Всего лишь. `main` — ветка, `feature/login` — ветка. Они обе указывают на какой-то коммит в истории. Когда ты коммитишь в `feature/login`, указатель двигается вперёд, а `main` остаётся на своём.
- **`git branch` и `git checkout/switch`.** `branch` — список веток. `branch new-feature` — создать. `checkout new-feature` или `switch new-feature` — переключиться. `checkout -b new-feature` или `switch -c new-feature` — создать и сразу перейти.
- **HEAD и detached HEAD.** `HEAD` обычно указывает на ветку. Если ты сделал `checkout <хэш-коммита>` — HEAD указывает напрямую на коммит, не на ветку. Новые коммиты не попадут ни в одну ветку. Звучит страшно, но лечится `checkout main`.
- **Merge.** `git checkout main && git merge feature/login` — соединить ветку с main. Если ветки не пересекались — fast-forward (main просто «догоняет»). Если пересекались — Git создаёт merge-коммит с двумя родителями.
- **Rebase.** `git rebase main` (стоя на feature) — перенести коммиты feature так, будто они были сделаны ПОСЛЕ последнего коммита main. История получается линейная, без merge-коммитов. Плата — переписывается история ветки.
- **Merge vs rebase — когда что.** Merge — сохраняет точную историю, безопасен всегда. Rebase — красивая история, но **не делай rebase на публичных (пушнутых) ветках** — другие люди могут иметь копию.
- **Конфликты.** Возникают, когда Git не может автоматически соединить два разных изменения одной и той же строки. В файле появляются маркеры `<<<<<<< HEAD`, `=======`, `>>>>>>> branch`. Нужно руками оставить правильный код, убрать маркеры, `git add`, `git commit` (или `git rebase --continue`).
- **`git log --graph --oneline --all`.** Твой лучший друг — наглядное дерево всех веток и коммитов. Разок настрой алиас в `~/.gitconfig`, потом не живи без него.
- **Удаление веток.** `git branch -d feature/login` — удалить локально (после мерджа). `-D` — принудительно. Ветку нужно удалять после мерджа, иначе репо превращается в свалку.
- **`git stash`.** Нужно переключиться, но изменения не готовы к коммиту. `stash` — отложить. `stash pop` — вернуть. Спасает, когда срочно просят посмотреть другой баг.

**`## Пример кода`** — блок ```bash```:
```bash
# создать ветку и переключиться
git switch -c feature/login

# пара коммитов
echo "login" > login.js
git add login.js
git commit -m "Add login stub"

# вернуться на main и смерджить
git switch main
git merge feature/login         # fast-forward если main не двигалась

# если был конфликт
git merge feature/login
# Auto-merging login.js
# CONFLICT (content): Merge conflict in login.js
# Automatic merge failed; fix conflicts and then commit the result.

# правим файл, убираем маркеры <<<<<<< ======= >>>>>>>
git add login.js
git commit                       # создаёт merge-коммит

# rebase (линейная история)
git switch feature/login
git rebase main                  # переносим коммиты поверх main

# конфликты при rebase
git rebase --continue            # после фикса
git rebase --abort               # если передумал

# удалить ветку после мерджа
git branch -d feature/login

# stash
git stash                        # отложить незакоммиченное
git switch main
# посмотреть что-то
git switch feature/login
git stash pop
```

**`## Частые ошибки`** — 4 bullet-а:
- Работать прямо в `main` вместо ветки. Даже один — заведи привычку: задача = ветка.
- Делать `rebase` на пушнутой ветке, которую тянут другие → перепишешь чужую историю. `rebase` — только в локальных ветках до пуша.
- Игнорировать конфликты, коммитить файл с `<<<<<<<` маркерами внутри — в проекте сломается сборка.
- Накапливать десятки мёртвых веток. После мерджа — сразу `branch -d`.

**`## Задания`:**
- [ ] Создай ветку, сделай 2 коммита, вернись на main, сделай merge, посмотри `git log --graph`.
- [ ] Специально создай конфликт: правка одной строки в двух ветках, сделай merge, разреши руками.
- [ ] Тот же сценарий, но через `rebase`. Сравни вид `git log --graph`.
- [ ] Настрой алиас: `git config --global alias.lg "log --oneline --graph --all"` и пользуйся `git lg`.

**`## Что почитать`:**
- [Pro Git — Branching](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)
- [Atlassian — merge vs rebase](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Learn Git Branching (интерактив)](https://learngitbranching.js.org/)
- [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow)

Блок — `bash`.

---

## Task 4: Урок 08.3 — GitHub и PR

**Create:** `FrontendCourse/08-Git-и-DevTools/08.3-GitHub-и-PR.md`

**Frontmatter:**
```yaml
---
модуль: 08-Git-и-DevTools
тема: GitHub — remote, push/pull, PR
статус: to-read
roadmap: https://roadmap.sh/frontend#version-control-systems
связано: [[08.2-Ветки-и-merge]], [[08.4-DevTools-Elements-и-Console]]
---
```

**Заголовок:** `# GitHub — remote, push/pull, PR`

**`## Зачем это нужно`:** Без GitHub твой Git — дневник в шкафу. С GitHub — публичное портфолио, место совместной работы, стандартный workflow индустрии (PR → review → merge). Любой заказчик или работодатель смотрит твой GitHub в первую очередь.

**`## Главное` (~330–400 слов):** подразделы `### ...`:
- **Remote.** Ссылка на удалённый репозиторий (на GitHub, GitLab и т.п.). `git remote -v` — покажет origin (обычно единственный remote). `git remote add origin <url>` — привязать.
- **`git push` и `git pull`.** `push` — отправить локальные коммиты в remote. `pull` — забрать чужие. `pull` = `fetch` + `merge`. `fetch` — просто скачать (увидишь коммиты, но не сольёшь); `merge` — соединить.
- **SSH vs HTTPS.** GitHub принимает оба. SSH требует ключа (`ssh-keygen` → добавить публичный на GitHub) — потом push/pull без пароля. HTTPS требует PAT (personal access token) вместо пароля с 2021 г. SSH удобнее для ежедневной работы.
- **Upstream и `-u`.** При первом push нужно связать локальную ветку с удалённой: `git push -u origin feature/login`. Один раз — дальше просто `git push`.
- **Pull Request (PR).** Предложение «смерджить мою ветку в main». Создаётся на GitHub через кнопку «Compare & pull request». В PR — diff, обсуждение, review. PR — основная единица работы в команде.
- **PR-workflow.**
    1. `switch -c feature/x`.
    2. Коммиты, `push -u`.
    3. На GitHub — Create PR с main как база.
    4. Review / обсуждение / правки → новые коммиты → `git push` → PR обновляется.
    5. Merge (через UI). Обычно: Squash, Merge, или Rebase — команда выбирает.
    6. Удалить ветку локально и на GitHub.
- **Squash merge.** Все коммиты ветки сжимаются в один перед мерджем. Чистая история main, но теряется детальная история ветки. Самый популярный вариант в командах.
- **Конфликты в PR.** Если main ушла вперёд и пересеклась с твоей веткой — GitHub покажет «Can't merge». Лечится: `git switch feature/x && git pull origin main && <разрешить конфликт> && git push`.
- **Code review.** Комментарии, реквесты изменений, approval. Даже для pet-проектов — привычка писать аккуратный PR с описанием «что поменял и зачем» окупится в команде.
- **GitHub CLI (`gh`).** Опционально, но удобно: `gh pr create`, `gh pr status`, `gh issue list` — всё из терминала, не открывая браузер.

**`## Пример кода`** — блок ```bash```:
```bash
# привязать к GitHub
git remote add origin git@github.com:user/repo.git
git push -u origin main             # первый push

# типичный PR-flow
git switch -c feature/navbar
# ... правки ...
git add .
git commit -m "Add navbar component"
git push -u origin feature/navbar

# на GitHub: Create Pull Request → review → merge

# после мерджа — почистить
git switch main
git pull                            # подтянуть мёрдженый код
git branch -d feature/navbar        # удалить локально
git push origin --delete feature/navbar   # удалить на GitHub (или через UI)

# конфликт в PR
git switch feature/navbar
git pull origin main                # подтянуть свежий main
# разрешить конфликт, git add, git commit
git push                            # PR обновится

# GitHub CLI
gh pr create --title "Add navbar" --body "Closes #12"
gh pr status
```

**`## Частые ошибки`** — 4 bullet-а:
- Пушить прямо в main без PR — нарушает процесс, ничего не ревьюится. Пиши PR даже для своих проектов.
- Не делать `pull` перед началом работы и упираться в конфликты при push. Начинай день с `git pull` на main.
- Пушить секреты (`.env`, ключи API). Если запушил — старое лечение `git filter-branch` опасно; используй `BFG` или токен-ротацию.
- Игнорировать описание PR — «fix stuff». В командах PR без внятного описания разворачивают на ревью.

**`## Задания`:**
- [ ] Создай пустой GitHub-репо, подключи локальный проект, запушь.
- [ ] Сделай ветку, коммит, `push -u`, открой PR на GitHub, смерджи.
- [ ] Спровоцируй конфликт: с GitHub UI поправь README, локально — тоже, пуш → merge-конфликт, разреши.
- [ ] Настрой SSH-ключ, сравни удобство с HTTPS.

**`## Что почитать`:**
- [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow)
- [GitHub — Connecting with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- [GitHub CLI](https://cli.github.com/)
- [Atlassian — Pull requests](https://www.atlassian.com/git/tutorials/making-a-pull-request)

Блок — `bash`.

---

## Task 5: Урок 08.4 — DevTools Elements и Console

**Create:** `FrontendCourse/08-Git-и-DevTools/08.4-DevTools-Elements-и-Console.md`

**Frontmatter:**
```yaml
---
модуль: 08-Git-и-DevTools
тема: DevTools — Elements и Console
статус: to-read
roadmap: https://roadmap.sh/frontend#version-control-systems
связано: [[08.3-GitHub-и-PR]], [[08.5-DevTools-Network-и-Sources]]
---
```

**Заголовок:** `# DevTools — Elements и Console`

**`## Зачем это нужно`:** DevTools — главный рентген фронтендера. Открыл страницу — можешь прочитать её DOM, исправить CSS в реалтайме, выполнить произвольный JS, посмотреть, что сломалось. Два первых таба (Elements и Console) — 80% ежедневного использования.

**`## Главное` (~330–400 слов):** подразделы `### ...`:
- **Как открыть.** Cmd+Opt+I (Mac) / F12 (Windows). Правая кнопка → Inspect. DevTools стыкуется справа, снизу, слева, отдельным окном.
- **Elements — DOM в реальном времени.** Показывает текущий DOM (не исходный HTML!). React/Vue вставляют элементы динамически — здесь ты видишь результат. Слева — дерево, справа — стили и Computed. Можно редактировать прямо тут: удвоить клик по тегу/атрибуту — изменить.
- **Styles + Computed.** Styles — CSS-правила как в коде, с селекторами и файлами. Зачёркнутое = перебито более специфичным. Computed — финальные значения всех свойств, как их применил браузер.
- **Force state (:hover, :focus).** В Styles → `.hov` — принудительно включить состояние. Удобно для тестирования ховер-эффектов без зажатия мыши.
- **Box model.** В Computed — квадрат с margin/border/padding/content. Видно, чего не хватает и почему разметка «съезжает».
- **Console — твой REPL.** Выполняет любой JS в контексте страницы. `document.querySelectorAll('a').length` — сколько ссылок на странице. Можно обращаться ко всем переменным, объявленным в глобале или доступных из текущего контекста.
- **Полезные console-методы.** `console.log`, `.warn`, `.error` — разные уровни. `console.table(arr)` — массив объектов как таблица. `console.group` / `.groupEnd` — вложенные блоки. `console.time('x')` / `.timeEnd('x')` — замер времени.
- **Shortcut $.** `$('.selector')` = `querySelector`, `$$('.selector')` = `querySelectorAll`. `$0` — последний выбранный элемент в Elements (очень удобно: выбрал элемент → `$0` в консоли).
- **Ошибки и источник.** Красные ошибки в консоли → кликни по файлу справа → откроется Sources с точным местом. Читай трассировку снизу вверх (сверху — где упало, ниже — кто вызвал).
- **Live expression.** «Глаз» в консоли — висячая переменная, значение обновляется в реальном времени (удобно следить за `document.scrollY`, например).
- **Preserve log и Clear.** По умолчанию консоль чистится при перезагрузке. Чекбокс Preserve log — не чистить. Кнопка-запрет (⊘) — очистить сейчас.

**`## Пример кода`** — блок ```js``` с «командами в консоли»:
```js
// быстрый DOM-аудит
$$('a').length                        // сколько ссылок
$$('img:not([alt])')                  // картинки без alt (a11y)

// потыкать элемент
$0.style.outline = '2px solid red'    // подсветить выбранный элемент
$0.click()                            // программный клик

// массив объектов — как таблица
const users = [{id:1,name:"Иван"},{id:2,name:"Анна"}];
console.table(users);

// замер времени
console.time('calc');
for (let i = 0; i < 1e6; i++) Math.sqrt(i);
console.timeEnd('calc');              // "calc: 12.3ms"

// условный breakpoint через консоль
// выбрал кнопку в Elements → правой кнопкой → Break on → subtree modifications
```

**`## Частые ошибки`** — 4 bullet-а:
- Думать, что в Elements — исходный HTML. Это актуальный DOM, который мог быть изменён JS-ом после загрузки. Исходник — в Sources или View Source.
- Пытаться отредактировать `node_modules/...` или компилированный JS в Sources вместо исходника. Ищи setup source maps (следующий урок).
- Не использовать `$0` — каждый раз копировать селектор. `$0` экономит кучу времени.
- Оставить `console.log`-и в проде. Убирай перед коммитом или отключай через линтер/плагин.

**`## Задания`:**
- [ ] На любом сайте: открой DevTools, выдели заголовок, в Styles поменяй `color: red` — посмотри, как меняется.
- [ ] В Computed найди реальный `padding` и `margin` выбранного элемента.
- [ ] В Console выполни `$$('img').forEach(img => console.log(img.src))` — получи список всех картинок.
- [ ] В Styles включи `:hover` принудительно, проверь hover-эффект кнопки.

**`## Что почитать`:**
- [Chrome DevTools — Overview](https://developer.chrome.com/docs/devtools/overview)
- [Chrome DevTools — CSS features reference](https://developer.chrome.com/docs/devtools/css)
- [Chrome DevTools — Console features reference](https://developer.chrome.com/docs/devtools/console/reference)
- [MDN — Browser DevTools](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Tools_and_setup/What_are_browser_developer_tools)

Блок — `js`.

---

## Task 6: Урок 08.5 — DevTools Network и Sources

**Create:** `FrontendCourse/08-Git-и-DevTools/08.5-DevTools-Network-и-Sources.md`

**Frontmatter:**
```yaml
---
модуль: 08-Git-и-DevTools
тема: DevTools — Network и Sources
статус: to-read
roadmap: https://roadmap.sh/frontend#version-control-systems
связано: [[08.4-DevTools-Elements-и-Console]], [[08.6-DevTools-Application-и-Performance]]
---
```

**Заголовок:** `# DevTools — Network и Sources`

**`## Зачем это нужно`:** Network — где живут все запросы твоей страницы: API, картинки, шрифты, скрипты. Sources — где ты пошагово отлаживаешь JS-код с breakpoint-ами, не вставляя `console.log`-и. Вместе — самый мощный дебаг-инструмент фронта.

**`## Главное` (~340–420 слов):** подразделы `### ...`:
- **Таб Network.** Слева колонки: Name, Status, Type (xhr/fetch/document/script/img), Size, Time, Waterfall. Клик по запросу → справа панели Headers, Payload, Response, Preview, Timing.
- **Фильтры Network.** Наверху: All / Fetch-XHR / JS / CSS / Img / Media / Font / Doc / WS. Клик на «Fetch/XHR» — только API-запросы, не медиа.
- **Preserve log и Disable cache.** `Preserve log` — не чистить при переходе по страницам. `Disable cache` — работает пока DevTools открыт; удобно для отладки, но не забывай выключить, иначе разработка медленная.
- **Throttling.** Пресеты Fast 3G / Slow 3G / Offline — эмулируют плохую сеть. Обязательно тестируй loader-ы на Slow 3G, иначе на реальных мобильных они пролетают незаметно.
- **Headers / Payload / Response / Preview.** Headers — request и response заголовки + статус + remote address. Payload — тело запроса (для POST/PUT). Response — сырое тело ответа. Preview — отрендеренный ответ (JSON-дерево, HTML-превью). Timing — когда началось/DNS/TCP/TLS/waiting/download.
- **Copy as fetch / cURL.** Правой кнопкой по запросу → Copy → Copy as fetch (готовый JS) или Copy as cURL (для терминала/Postman). Экономит часы.
- **Таб Sources.** Дерево файлов слева (Page — по origin), редактор в центре, панели справа (Breakpoints, Scope, Call stack, Watch). Видишь все JS/CSS-файлы, которые подгрузила страница.
- **Breakpoints.** Клик по номеру строки — поставить breakpoint. Перезапуск действия (например, клик по кнопке) → выполнение останавливается на этой строке. Справа — Scope (все переменные), Call stack (кто вызвал). Кнопки сверху: Resume (▶), Step over (↷), Step into (↓), Step out (↑).
- **Conditional и logpoint breakpoints.** Правой кнопкой по номеру строки → Add conditional breakpoint (`i === 42`) — остановится только если условие истинно. Logpoint — печатает выражение в консоль без остановки (замена `console.log` без правки кода).
- **debugger statement.** Добавь `debugger;` в код — срабатывает как breakpoint, если DevTools открыт. Удобно для ловли случая, который трудно воспроизвести вручную.
- **Source maps.** Минифицированный или TypeScript-код в проде выглядит как каша. Source maps — карта соответствия между минификацией и исходником. В Sources ты видишь оригинал. Включены по умолчанию в Chrome; если не работают — проверь `.js.map` в Network.
- **Snippets.** Вкладка Sources → Snippets — сохранённые JS-скрипты, которые запускаются в контексте любой страницы. Удобно для собственной библиотечки отладочных хелперов.

**`## Пример кода`** — блок ```js``` + короткий текст:
```js
// Как пользоваться debugger programmatically
function calculatePrice(items) {
  debugger;                             // DevTools остановятся здесь
  return items.reduce((sum, i) => sum + i.price, 0);
}

// Logpoint — аналог console.log, но без правки кода
// ПКМ по строке в Sources → Add logpoint → "sum is", sum
// теперь при каждом прохождении печатает, но файл не меняется

// Запрос из Network → Copy as fetch (пример того, что скопируется)
await fetch("https://api.example.com/users/42", {
  "headers": {
    "accept": "application/json",
    "authorization": "Bearer abc123"
  },
  "method": "GET"
});
```

**`## Частые ошибки`** — 4 bullet-а:
- Отлаживаться только через `console.log` — медленнее, чем breakpoint со Scope-панелью, где видны все переменные разом.
- Забыть `Disable cache` → обновляешь страницу, а в консоли старая версия кода. Или наоборот — оставить навсегда и страдать от медленной разработки.
- Думать, что 401/500 в Network — это «fetch упал». `fetch` не бросает на HTTP-ошибку; проверяй `res.ok`.
- Игнорировать Preserve log — ушёл на другую страницу, логи потеряны, ошибки не видно. На багах, связанных с переходами, включай сразу.

**`## Задания`:**
- [ ] В Network сымитируй Slow 3G на любом сайте — посмотри, как загружается, видны ли loader-ы.
- [ ] На одном из своих проектов (M06 Fetch-приложение) — Copy as fetch запроса к API, запусти в консоли.
- [ ] Поставь breakpoint в JS-коде, в Scope посмотри локальные переменные. Step over / Step into несколько шагов.
- [ ] Добавь logpoint в цикл — увидишь значения без `console.log` в коде.

**`## Что почитать`:**
- [Chrome DevTools — Network](https://developer.chrome.com/docs/devtools/network)
- [Chrome DevTools — Sources](https://developer.chrome.com/docs/devtools/sources)
- [Chrome DevTools — JavaScript debugger](https://developer.chrome.com/docs/devtools/javascript)
- [MDN — The JavaScript Debugger](https://firefox-source-docs.mozilla.org/devtools-user/debugger/)

Блок — `js`.

---

## Task 7: Урок 08.6 — DevTools Application и Performance

**Create:** `FrontendCourse/08-Git-и-DevTools/08.6-DevTools-Application-и-Performance.md`

**Frontmatter:**
```yaml
---
модуль: 08-Git-и-DevTools
тема: DevTools — Application, Performance, Lighthouse
статус: to-read
roadmap: https://roadmap.sh/frontend#version-control-systems
связано: [[08.5-DevTools-Network-и-Sources]]
---
```

**Заголовок:** `# DevTools — Application, Performance, Lighthouse`

**`## Зачем это нужно`:** Когда «что-то закэшировалось», «не могу разлогиниться», «страница тормозит» — это три таба: Application (хранилища), Performance (профилировщик), Lighthouse (общий аудит). Без них ты гадаешь, с ними — видишь факты.

**`## Главное` (~330–400 слов):** подразделы `### ...`:
- **Application → Storage.** Слева: Local Storage, Session Storage, Cookies, IndexedDB, Cache Storage. По каждому — список ключей и значений; можно править и удалять прямо в UI.
- **Application → Cookies.** Для каждого куки видно: Name, Value, Domain, Path, Expires, Size, HttpOnly, Secure, SameSite. Удаление — правой кнопкой → Delete. Удобно при отладке auth.
- **Application → Clear storage.** Кнопка «Clear site data» стирает всё: localStorage, cookies, IndexedDB, Cache, Service Workers. Спасает от загадочных багов «у меня что-то закэшировалось».
- **Service Workers.** Worker-ы между страницей и сетью — основа offline-приложений. В Application → Service Workers: статус, Unregister (для отладки), Update on reload (обязательно при разработке SW).
- **Таб Performance.** Профилировщик. Запись (Record) → действие на странице → Stop → толстый timeline: FPS, CPU, Network, Main thread, Screenshots. Видно, на что уходит время: скрипты, рендер, layout.
- **Как читать flame chart.** Вертикаль — stack вызовов. Горизонталь — время. Длинная жёлтая/фиолетовая полоса в Main — долгие вызовы JS / layout. Ищи `Task` дольше 50 мс — это lag на пользовательском вводе.
- **FPS и long tasks.** 60 FPS = 16.6 мс на кадр. Если frame занимает 50+ мс — видимый дерганый анимации. Performance помечает такие задачи красным.
- **Lighthouse.** Автоматический аудит: Performance / Accessibility / Best Practices / SEO / PWA. Оценки 0-100. Каждая метрика с объяснением «что это, почему плохо, как починить».
- **Core Web Vitals.** Три главные метрики Google: LCP (Largest Contentful Paint — когда появляется основной контент), INP (Interaction to Next Paint — отзывчивость на ввод), CLS (Cumulative Layout Shift — прыжки разметки). Lighthouse показывает их.
- **Coverage.** DevTools → … → More tools → Coverage. Показывает, сколько % JS и CSS на странице реально использовалось. Неиспользуемый — кандидат на code splitting или удаление.
- **Memory.** Таб Memory — heap snapshots, allocation timeline. Нужно, когда приложение «течёт» (растёт потребление памяти при работе). На пет-проектах редко; знай, что существует.
- **Rendering.** … → More tools → Rendering. Чекбоксы: Paint flashing, Layer borders, Layout Shift Regions. Визуализация того, что реально перерисовывается — помогает поймать лишние re-render-ы.

**`## Пример кода`** — маленький блок ```js``` (нет больших примеров, это UI-таб):
```js
// Проверка размеров localStorage — вручную через DevTools удобнее
const size = Object.keys(localStorage)
  .reduce((s, k) => s + (k.length + localStorage.getItem(k).length), 0);
console.log(`localStorage: ${(size / 1024).toFixed(2)} КБ`);

// Хак: выполнить Lighthouse из CLI (когда UI недоступен)
// npx lighthouse https://your-site.com --view
```

**`## Частые ошибки`** — 4 bullet-а:
- «Почему не обновляется?» — забыл про Service Worker, который отдаёт старую версию. Смотри Application → Service Workers, жми Update / Unregister.
- Гадать, что тормозит, вместо записи Performance-профиля. 30 секунд записи — точный ответ.
- Читать Lighthouse как «оценку сайта» — это набор подсказок, а не итог. Делай 2-3 замера в incognito без расширений.
- Чистить localStorage руками через консоль вместо Application → Clear storage. Последнее — один клик, чистит всё.

**`## Задания`:**
- [ ] В Application посмотри localStorage своего проекта M07 Mock auth — найди токен, удали его, перезагрузи — увидишь разлогин.
- [ ] Запусти Performance recording на любом сайте, сделай пару кликов, посмотри flame chart.
- [ ] Запусти Lighthouse в incognito на одном из своих задеплоенных проектов — прочитай отчёт, попробуй 1-2 рекомендации исправить.
- [ ] Открой Coverage — посмотри, сколько неиспользуемого JS на большом сайте (twitter.com, vk.com).

**`## Что почитать`:**
- [Chrome DevTools — Application](https://developer.chrome.com/docs/devtools/application)
- [Chrome DevTools — Performance](https://developer.chrome.com/docs/devtools/performance)
- [Lighthouse documentation](https://developer.chrome.com/docs/lighthouse)
- [web.dev — Core Web Vitals](https://web.dev/articles/vitals)

Блок — `js`.

---

## Task 8: Мини-проект M08 — Git-workflow и debug

**Create:** `FrontendCourse/Проекты/Мини/M08-Git-workflow-и-debug.md`

**Exact content:**

```markdown
---
тип: мини-проект
модуль: 08-Git-и-DevTools
статус: not-started
---

# M08 — Git-workflow и debug

Мини-проект после модуля 08. Две цели в одной задаче: отработать feature-branch → PR → merge с конфликтом + отладить 3-4 «подсунутых» бага через DevTools. Практика максимально приближена к реальной работе.

## Задача

Возьми **свой** предыдущий проект — M06 Fetch-приложение (или M07 Mock auth, если удобнее). Не с нуля — именно свой уже написанный. Сделай в нём:
1. Небольшое улучшение через feature-branch → PR → merge.
2. Прогони код через 4 подсунутых бага (список ниже), найди и почини каждый — используя DevTools, без `console.log`-ов в коде.

## Часть A — Git-workflow

### Требования
1. **Создай feature-ветку** `feature/<что-делаешь>`, например `feature/loading-skeleton` или `feature/retry-button`.
2. **Сделай небольшое улучшение** в ней — 1-2 коммита. Что именно — на твой вкус. Примеры: скелетон вместо текста «Загрузка», кнопка Retry, debounce поиска, пустое состояние, улучшение доступности (alt, aria-label, клавиатура).
3. **На main** (параллельно) — отредактируй README (например, добавь секцию «Как запускать»). 1 коммит.
4. **Push обеих веток.** В GitHub UI открой PR из feature в main. Дай ему осмысленное название и описание («что, зачем, как тестировать»).
5. **Merge конфликт.** Синхронизируй feature с main (`git pull origin main` в feature) — если не конфликт, специально создай: отредактируй README и в feature-ветке (та же строка, что правил в main). Разреши конфликт, запушь.
6. **Смерджи PR** на GitHub. Выбери Squash merge или Merge commit — любой, главное осознанно.
7. **Удали ветку** локально и на GitHub.
8. **Посмотри `git log --oneline --graph --all`** — сохрани скриншот, приложи к README.

## Часть B — Debug через DevTools

В своём проекте внеси **4 искусственных бага** в отдельной ветке `bugs/debug-session` (не мерджи её). Потом найди и опиши каждый. Цель — не починить, а доказать, что ты нашёл и понял через DevTools.

### Список багов (выбери минимум 4, можно все)

1. **Console-баг.** Где-то напиши вызов несуществующей функции (`dolmStuff()` вместо `doStuff()`). Ошибка в консоли → открой файл → найди место.
2. **Network-баг.** Измени URL запроса на неверный (`/auht` вместо `/auth`). Fetch вернёт 404. Увидеть в Network, прочитать статус и path.
3. **Breakpoint-баг.** В обработчике submit пропусти `e.preventDefault()` — форма будет перезагружать страницу. Поставь breakpoint в обработчике, заметь, что `preventDefault` не вызывается.
4. **Storage-баг.** Сохрани токен не в `"token"`, а в `"tokem"`. Логин проходит, но на F5 приложение считает, что не залогинен. Найди через Application → Local Storage.
5. **Layout-shift-баг** (опционально). Картинка без фиксированной высоты вызывает layout shift при загрузке. Видно в Performance или Rendering → Layout Shift Regions.

### Отчёт по каждому багу
Для каждого опиши в README (отдельный файл `DEBUG.md` или секция в README):
- Какой баг.
- Каким инструментом DevTools нашёл (какой таб, что сделал).
- Что увидел на экране (можно скриншотом).
- Как бы починил (1-2 строки кода).

## Технические правила
- Никаких `console.log` в коде багов (кроме самих ошибок). Находи через DevTools, не через правку.
- Коммиты атомарные. Ветка фичи = одна фича. Ветка багов = только баги.
- README обновлён: ссылка на прод-URL (предыдущий проект уже задеплоен), секция «Debug-session».
- `.gitignore` в порядке (node_modules, .DS_Store, .env если есть).

## Чего НЕ должно быть
- Работы в `main` без PR.
- `git push --force` в main (и вообще на этом этапе — не нужно).
- Файла `.env` с секретами в истории.
- Мёртвых веток после мерджа.

## Этапы
1. Выбери базовый проект (M06 или M07) — клонируй/открой.
2. Создай feature-ветку, сделай улучшение (2 коммита).
3. В main — правка README (1 коммит).
4. Push обеих веток, открой PR.
5. Спровоцируй конфликт, разреши, запушь, merge PR.
6. Почисти ветки.
7. В отдельной ветке `bugs/debug-session` внеси 4 бага.
8. Найди каждый через DevTools, опиши в `DEBUG.md`.
9. README: ссылка на PR, скриншот `git log --graph`, ссылка на DEBUG.md.

## Сдача
1. Публичный GitHub-репозиторий.
2. Прод-URL (базового проекта) работает.
3. Ссылка на смёрдженый PR.
4. `DEBUG.md` с разбором 4 багов и скриншотами.
5. На созвоне — покажи `git log --graph`, вместе пройдёмся по одному из багов.

## Критерии приёмки ревью
- [ ] Feature-ветка создана, сделан осмысленный PR с описанием.
- [ ] В PR был merge-конфликт, разрешён руками.
- [ ] PR смёржен, ветка удалена локально и на GitHub.
- [ ] `git log --graph` показывает историю с двумя ветками и их слиянием.
- [ ] Ветка `bugs/debug-session` существует и НЕ смёржена.
- [ ] В `DEBUG.md` разобрано минимум 4 бага с указанием инструмента DevTools.
- [ ] По каждому багу понятно: таб, шаги, что увидел.
- [ ] Нет `console.log` в коде багов.
- [ ] `.gitignore` на месте, `node_modules` не в истории.

## Что дальше
Дальше — **модуль 09 React база**: компоненты, props, state, events. С Git и DevTools ты теперь готов работать с серьёзным инструментом, а не просто читать туториалы.
```

---

## Task 9: Создать MOC-Tools

**Create:** `FrontendCourse/MOC/MOC-Tools.md`

**Exact content:**

```markdown
---
тип: MOC
тема: Инструменты
---

# MOC — Инструменты

Карта по инструментам разработчика: Git, DevTools браузера, build-tools и тестирование. Заполняется в модулях 08 (Git + DevTools) и 12 (Vite / тесты).

## Git (модуль 08)
- [[08.1-Git-основы]]
- [[08.2-Ветки-и-merge]]
- [[08.3-GitHub-и-PR]]

## DevTools (модуль 08)
- [[08.4-DevTools-Elements-и-Console]]
- [[08.5-DevTools-Network-и-Sources]]
- [[08.6-DevTools-Application-и-Performance]]

## Build-tools и тесты (модуль 12 — скоро)
- _Vite, bundling, ESLint, Prettier, Vitest, Playwright_

## Практика
- [[M08-Git-workflow-и-debug]] — PR-workflow + отладка через DevTools.
```

---

## Task 10: Обновить 00-Start-Here.md

**Modify:** `FrontendCourse/00-Start-Here.md`

- [ ] **Step 10.1:** Убрать «_(скоро)_» у модуля 08:
  `- [[08-Git-и-DevTools/00-Обзор-модуля|Модуль 08 — Git и DevTools]] _(скоро)_` → `- [[08-Git-и-DevTools/00-Обзор-модуля|Модуль 08 — Git и DevTools]]`.
- [ ] **Step 10.2:** В разделе «Карты знаний (MOC)» добавить строку `- [[MOC-Tools]]` (в конце списка, после `- [[MOC-Nextjs]]`).

---

## Task 11: Верификация

- [ ] **Step 11.1:** `find FrontendCourse/08-Git-и-DevTools -type f -name "*.md" | sort` → 7 файлов.
- [ ] **Step 11.2:** `M08-Git-workflow-и-debug.md` существует в `Проекты/Мини/`.
- [ ] **Step 11.3:** `MOC-Tools.md` существует и содержит 6 ссылок на уроки 08.1–08.6.
- [ ] **Step 11.4:** В `00-Start-Here.md` у модуля 08 нет «_(скоро)_», и добавлена ссылка `[[MOC-Tools]]`.
- [ ] **Step 11.5:** Отчитаться: модуль 08 готов.

---

## Self-Review

**1. Spec coverage:**
- Git (основы, ветки, GitHub) → Tasks 2–4. ✓
- DevTools (Elements/Console, Network/Sources, Application/Performance) → Tasks 5–7. ✓
- Мини-проект (PR + debug) → Task 8. ✓
- MOC-Tools → Task 9. ✓
- Start-Here → Task 10. ✓

**2. Placeholder scan:** TBD/TODO отсутствуют. «_(скоро)_» в MOC-Tools — осознанный маркер. ✓

**3. Type consistency:** Имена уроков/мини-проекта согласованы между всеми файлами. ✓

---

## Out of Scope

- `git bisect`, `git cherry-pick`, `git reflog` — продвинутый Git, не первый заход.
- Git-hooks, submodules, worktrees — уходит в модули 12/14 при необходимости.
- Build tools (Vite, webpack) → модуль 12.
- React DevTools → отдельная тема в модуле 09/10.
- Монорепозитории, CI/CD → модуль 14.
