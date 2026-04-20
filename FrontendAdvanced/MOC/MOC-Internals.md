---
тип: MOC
тема: Browser и JS internals
---

# MOC — Internals

Карта знаний Track 1: всё, что про «под капотом». Browser rendering, event loop, память, React performance 2026.

Используй эту карту как навигатор: когда что-то из reference-секций урока ссылается на смежную тему — быстро найдёшь.

## A1.1 — Browser Rendering Pipeline

Что делает браузер между «HTML пришёл» и «пиксели видны».

- [[../A1-Deep-Frontend/A1.1-Browser-Rendering/A1.1.1-Parse-и-DOM|A1.1.1 — Parse и DOM construction]]
- [[../A1-Deep-Frontend/A1.1-Browser-Rendering/A1.1.2-Style-и-CSSOM|A1.1.2 — Style и CSSOM, каскад глубже]]
- [[../A1-Deep-Frontend/A1.1-Browser-Rendering/A1.1.3-Layout-и-reflow|A1.1.3 — Layout (reflow) и box model]]
- [[../A1-Deep-Frontend/A1.1-Browser-Rendering/A1.1.4-Paint-и-composite|A1.1.4 — Paint и Composite слои]]
- [[../A1-Deep-Frontend/A1.1-Browser-Rendering/A1.1.5-Reflow-vs-Repaint-vs-Composite|A1.1.5 — Reflow vs Repaint vs Composite]]
- [[../A1-Deep-Frontend/A1.1-Browser-Rendering/A1.1.6-Chrome-Rendering-tab|A1.1.6 — Chrome Rendering tab на практике]]

## A1.2 — Event Loop и Concurrency

Как браузер выполняет JS параллельно рендерингу и сетям.

- [[../A1-Deep-Frontend/A1.2-Event-Loop-и-Concurrency/A1.2.1-Event-loop-в-деталях|A1.2.1 — Event loop в деталях]]
- [[../A1-Deep-Frontend/A1.2-Event-Loop-и-Concurrency/A1.2.2-Microtasks-vs-Macrotasks|A1.2.2 — Microtasks vs Macrotasks]]
- [[../A1-Deep-Frontend/A1.2-Event-Loop-и-Concurrency/A1.2.3-Scheduler-и-idle-callback|A1.2.3 — Scheduler и idle callback]]
- [[../A1-Deep-Frontend/A1.2-Event-Loop-и-Concurrency/A1.2.4-Web-Workers|A1.2.4 — Web Workers]]
- [[../A1-Deep-Frontend/A1.2-Event-Loop-и-Concurrency/A1.2.5-SharedArrayBuffer-и-Atomics|A1.2.5 — SharedArrayBuffer и Atomics]]
- [[../A1-Deep-Frontend/A1.2-Event-Loop-и-Concurrency/A1.2.6-Service-Workers-как-runtime|A1.2.6 — Service Workers как runtime]]

## A1.3 — Memory и GC

Как JS-движок хранит объекты, когда и почему чистит память.

- [[../A1-Deep-Frontend/A1.3-Memory-и-GC/A1.3.1-Модель-памяти-JS|A1.3.1 — Модель памяти JS]]
- [[../A1-Deep-Frontend/A1.3-Memory-и-GC/A1.3.2-V8-hidden-classes|A1.3.2 — V8 hidden classes]]
- [[../A1-Deep-Frontend/A1.3-Memory-и-GC/A1.3.3-GC-алгоритмы|A1.3.3 — GC алгоритмы]]
- [[../A1-Deep-Frontend/A1.3-Memory-и-GC/A1.3.4-Memory-leaks|A1.3.4 — Memory leaks: closures, listeners, detached DOM]]
- [[../A1-Deep-Frontend/A1.3-Memory-и-GC/A1.3.5-Chrome-Memory-Profiler|A1.3.5 — Chrome Memory Profiler в деталях]]

## A1.4 — React Performance 2026

Новая модель React: компилятор, streaming, selective hydration.

- [[../A1-Deep-Frontend/A1.4-React-Performance-2026/A1.4.1-React-Compiler-что-делает|A1.4.1 — React Compiler: что делает]]
- [[../A1-Deep-Frontend/A1.4-React-Performance-2026/A1.4.2-Когда-Compiler-ломается|A1.4.2 — Когда React Compiler ломается]]
- [[../A1-Deep-Frontend/A1.4-React-Performance-2026/A1.4.3-Suspense-streaming-глубже|A1.4.3 — Suspense streaming глубже]]
- [[../A1-Deep-Frontend/A1.4-React-Performance-2026/A1.4.4-Selective-hydration|A1.4.4 — Selective hydration]]
- [[../A1-Deep-Frontend/A1.4-React-Performance-2026/A1.4.5-useTransition-и-useDeferredValue|A1.4.5 — useTransition и useDeferredValue в продакшне]]
- [[../A1-Deep-Frontend/A1.4-React-Performance-2026/A1.4.6-React-Profiler-практика|A1.4.6 — React Profiler — практика]]

## Практика

- **A-P1 Performance Rescue** _(скоро)_ — большой проект после Track 1. Медленный репозиторий → Lighthouse 95+.

## Связанные темы в других MOC

_Track 2–6 в разработке — ссылки добавятся._
