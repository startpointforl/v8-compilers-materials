# V8 Compilers — Additional Materials

Подборка полезных материалов по работе движка V8 и его компиляторов по мотивам доклада “Ignition, Sparkplug, Maglev, TurboFan: как компилирует V8”.

## Моя серия статей про V8

Материалы из Telegram-канала https://t.me/startpoint_dev

- Погружение в V8. Часть 1. История  
  https://telegra.ph/V8-part-1-08-30

- Погружение в V8. Часть 2. Из чего состоит движок  
  https://telegra.ph/V8-part-2-09-13

- Погружение в V8. Часть 3. Парсинг, AST и анализ кода  
  https://telegra.ph/V8-part-3-09-16

- Погружение в V8. Часть 4. Управление памятью и GC  
  https://telegra.ph/V8-part-4-09-27

- Погружение в V8. Часть 5. Скрытые оптимизации  
  https://telegra.ph/V8-part-5-10-05

- Погружение в V8. Часть 6. От среды к среде  
  https://telegra.ph/V8-part-6-10-11

## Общие ресурсы

- Блог Franziska Hinkel (разработчицы из V8)  
  https://www.fhinkel.rocks/

- Её статья "How do I get started with V8 development"  
  https://www.fhinkel.rocks/posts/How-do-I-get-Started-with-V8-Development

- Официальный блог V8  
  https://v8.dev/blog

## Сборка и запуск V8 локально

### Установка и запуск

- jsvu — инструмент для установки V8  
  https://github.com/GoogleChromeLabs/jsvu

- Презентация с полезными флагами  
  https://docs.google.com/presentation/d/1oODBv84iABK3a8FScPr6X185D5Szm8AmJwtw-3g1uAg/edit?slide=id.g2966240bcd2_0_23#slide=id.g2966240bcd2_0_23

### Alias для удобного запуска

Пример для bash/zsh:

```
alias v8="$HOME/.jsvu/v8"
alias v8-debug="$HOME/.jsvu/v8-debug"
```

После этого можно запускать:

```
v8 file.js  
v8-debug file.js
```

### Поиск флагов

```
v8 --help | grep -i baseline  
v8 --help | grep -i maglev  
v8 --help | grep -i turbofan
```

## Ignition (Interpreter)

- Доклад  
  https://www.youtube.com/watch?v=r5OWCtuKiAk

- Презентация к этому докладу  
  https://docs.google.com/presentation/d/1OqjVqRhtwlKeKfvMdX6HaCIu9wpZsrzqpIVIwQSuiXQ

- Статья из блога V8  
  https://v8.dev/blog/ignition-interpreter

## Bytecode

- Understanding V8's Bytecode  
  https://www.fhinkel.rocks/posts/Understanding-V8-s-Bytecode

- Другая статья с разбором байткода  
  https://www.alibabacloud.com/blog/599188

- Видеоразборы байткода  
  https://www.youtube.com/live/lP82yJRujLM
  https://www.youtube.com/live/n79z4l2Qrp4

### Просмотр байткода

```
v8 --print-bytecode file.js
```

Дополнительно:

```
v8 --print-bytecode --print-bytecode-filter=foo file.js
```

(печать байткода только для функции foo)

## Sparkplug (Baseline Compiler)

- Описание из блога V8  
  https://v8.dev/blog/sparkplug

### Трассировка baseline-компиляции

```
v8 --trace-baseline file.js
```

## Maglev (Mid-tier Compiler)

- Описание из блога V8  
  https://v8.dev/blog/maglev

### Трассировка оптимизаций

```
v8 --trace-opt file.js  
```

## TurboFan (Optimizing Compiler)

- Статья из блога V8 про переход с Sea of Nodes на Confrol-Flow Graph представление  
  https://v8.dev/blog/leaving-the-sea-of-nodes

### Трассировка TurboFan

```
v8 --trace-opt file.js  
```

## Smi и Pointer Compression

- Что такое "Small Integer (Smi)"  
  https://www.fhinkel.rocks/posts/V8-Internals-How-Small-is-a-Small-Integer

- Статья из блога V8 про оптимизацию "Pointer Compression"  
  https://v8.dev/blog/pointer-compression

## Hidden Classes и Inline Caches

- Hidden Classes  
  https://v8.dev/docs/hidden-classes

- Inline Caches  
  https://mrale.ph/blog/2012/06/03/explaining-js-vms-in-js-inline-caches.html

## Elements Kinds (Массивы)

- Elements kinds  
  https://v8.dev/blog/elements-kinds

### Отладка

Запуск с natives: `v8 --allow-natives-syntax file.js`  
В коде: `%DebugPrint(array)`

## Tiering: переход между компиляторами

- Статья про пороговые значения переходов  
  https://community.intel.com/t5/Blogs/Tech-Innovation/Client/Profile-Guided-Tiering-in-the-V8-JavaScript-Engine/post/1679340

- Сами пороговые значения в коде V8  
  https://source.chromium.org/chromium/chromium/src/+/main:v8/src/flags/flag-definitions.h  
  Поиск в исходниках: `invocation_count_for_`

## 🤝 Автор

**Настя Котова** — [@startpoint_dev](https://t.me/startpoint_dev)  
Фронтендер с лапками