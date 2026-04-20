# Track 5 — Алгоритмы и структуры данных — Implementation Plan

**Goal:** Написать 5 модулей (~25 уроков) трека «Алгоритмы и структуры данных» для FrontendAdvanced. Не LeetCode-гринд — алгоритмы с применимыми фронтовыми кейсами.

**Architecture:** Один каталог `A5-Алгоритмы-и-структуры-данных/` с 5 подпапками `A5.1-…`/`A5.2-…`/`A5.3-…`/`A5.4-…`/`A5.5-…`. В каждой подпапке `00-Обзор-модуля.md` + 5 уроков. Канонический frontmatter (тип/трек/модуль/урок/статус). 6 секций в уроке (Зачем / Главное / Пример кода / Частые ошибки / Задания / Что почитать) + «Следующий урок» навигация. Em-dash `—` в заголовках. Англицизмы в скобках при первом употреблении.

**Tech stack:** JavaScript/TypeScript 5.x, Node 24, benchmark.js, DevTools Performance, V8 (для упоминаний про JIT-эффекты), Web APIs (WeakRef, WeakMap).

---

## File Structure

```
A5-Алгоритмы-и-структуры-данных/
├── A5.1-Сложность-и-измерения/
│   ├── 00-Обзор-модуля.md
│   ├── A5.1.1-Big-O-и-амортизация.md
│   ├── A5.1.2-Измерения-и-benchmark-js.md
│   ├── A5.1.3-Микро-vs-макро-оптимизации.md
│   ├── A5.1.4-Профайлинг-в-DevTools.md
│   └── A5.1.5-Asymptotic-vs-реальный-JIT.md
├── A5.2-Структуры-данных-для-фронтенда/
│   ├── 00-Обзор-модуля.md
│   ├── A5.2.1-Map-Set-WeakMap-WeakRef.md
│   ├── A5.2.2-Queue-Stack-Deque.md
│   ├── A5.2.3-LRU-cache.md
│   ├── A5.2.4-Trie-для-autocomplete.md
│   └── A5.2.5-Bloom-filter-и-HyperLogLog.md
├── A5.3-Деревья/
│   ├── 00-Обзор-модуля.md
│   ├── A5.3.1-Бинарные-деревья-и-BST.md
│   ├── A5.3.2-DOM-как-дерево-обходы.md
│   ├── A5.3.3-VDOM-diff-как-tree-matching.md
│   ├── A5.3.4-Heap-и-priority-queue.md
│   └── A5.3.5-LCA-и-иерархические-меню.md
├── A5.4-Графы/
│   ├── 00-Обзор-модуля.md
│   ├── A5.4.1-Представления-графов.md
│   ├── A5.4.2-BFS-DFS-и-когда-что.md
│   ├── A5.4.3-Topological-sort-для-build-order.md
│   ├── A5.4.4-Dijkstra-и-routing.md
│   └── A5.4.5-Cycle-detection-и-dependency-graphs.md
└── A5.5-Dynamic-Programming/
    ├── 00-Обзор-модуля.md
    ├── A5.5.1-Memo-vs-tabulation.md
    ├── A5.5.2-Edit-distance-для-fuzzy-search.md
    ├── A5.5.3-LCS-для-diff.md
    ├── A5.5.4-DAG-DP-и-зависимые-вычисления.md
    └── A5.5.5-Knapsack-подобные-кейсы.md
```

## Lesson content themes

**A5.1 Сложность и измерения** — Big-O (ворст-кейс, амортизация, O(1) push vs O(n) copy), benchmark.js + process.hrtime.bigint, подводные камни (warm-up, dead-code elimination, inline caching), разница между «микро» (инструкция) и «макро» (архитектура), DevTools Performance flame graph, JIT-эффекты (polymorphic IC, де-оптимизация при нестабильных типах).

**A5.2 Структуры для фронтенда** — Map/Set O(1) lookup, WeakMap для приватных данных/мемоизации, WeakRef для кешей, Queue для event loop (ArrayBuffer vs linked list), Deque для UNDO, LRU через Map+doubly-linked list, Trie для autocomplete, Bloom filter для client-side pre-check (e.g. "username taken"), HyperLogLog для cardinality.

**A5.3 Деревья** — бинарное, BST, balancing (AVL/RB — только упомянуть), DFS/BFS, DOM traversal (Node.childNodes, TreeWalker), VDOM diff (keys, unit of work), heap-based priority queue (mini-scheduler), LCA для breadcrumbs/menu highlight.

**A5.4 Графы** — adjacency list vs matrix, BFS (shortest unweighted path), DFS (компоненты, cycle), topological sort (Kahn для Turborepo pipeline order), Dijkstra для routing с весом, cycle detection в import graph.

**A5.5 DP** — memoization recurrence → tabulation, edit distance (Levenshtein) для fuzzy поиска команд, LCS для git diff / Myers, DAG-DP для dependency cost, knapsack на примере «лимит бандла».

## Subagent dispatch

5 параллельных субагентов — по одному на модуль. Каждый получает:
- Полный список файлов его модуля.
- Канонический frontmatter шаблон.
- Шаблон 6 секций + «Следующий урок».
- Правило про em-dash `—` (не `--`).
- Правило про пояснение англицизмов.
- Ссылку на пример: `A4.1.1-Контейнеризация-и-зачем-фронту.md`.
- 500–1000 слов в секции «Главное», реалистичные примеры кода.

После завершения всех 5 — bash-верификация (30 файлов, счётчик `## `, em-dash).

## Follow-up

- Обновить `00-Start-Here.md`: Track 5 из _(скоро)_ в готовый.
- Создать `MOC/MOC-Algorithms.md` (индекс 25 уроков).
- Добавить `MOC-Algorithms` в список MOC в Start-Here.
