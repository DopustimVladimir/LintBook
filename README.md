---
description: Книга описывает инструменты для статического анализа кода
---

# LintBook (ru)

**Lint** — инструмент для статического анализа кода на языке C, написанный Стивеном Джонсоном (Bell Labs) в 1978 году. Подобные (Lint-like) инструменты иногда называют линтерами (Linters), а процесс анализа линтингом (Linting). Одним из современных линтеров является [Infer](https://fbinfer.com) от Facebook, который поддерживает C, C++ и Java.

Статический анализ кода проводится без реального выполнения исследуемых программ. Линтеры часто используются в редакторах кода — линтер выполняет свою работу и редактор подсвечивает области, где возможно есть ошибка. Инструмент для статического анализа выявляет ошибки, потенциально опасные выражения, нежелательные конструкции, некорректный стиль написания и прочий мусор. Использование линтера может помочь команде разработчиков писать код правильно, опрятно и согласованно.

Один из важных моментов — возможность настроить анализатор под нужды конкретного проекта в конкретной среде, требующей особенный подход к написанию кода. Таким образом, программист сам выбирает, что следует считать ошибкой и в каком случае выводить предупреждение.

Существует множество различных линтеров, а цель данного руководства — составить краткий обзор некоторых из них и представить примеры конфигурации.

* [CoffeeLint](docs/coffeelint.md) — для CoffeeScript
* [ESLint](docs/eslint.md) — для JavaScript
* [PyLint](docs/pylint.md) — для Python
* [StyleLint](docs/stylelint.md) — для CSS, Sass, Less, ...

## Примеры конфигурации

Если вы оказались на этой странице с целью скачать мои конфиги:

* [@dopustim/stylelint-config](https://github.com/dopustim/stylelint-config) — образец конфигурации StyleLint
* [@dopustim/eslint-config](https://github.com/dopustim/eslint-config) — образец конфигурации ESLint
* [@dopustim/coffeelint-config](https://github.com/dopustim/coffeelint-config) — образец конфигурации CoffeeLint
* [@dopustim/pylint-config](https://github.com/dopustim/pylint-config) — образец конфигурации PyLint

## Лицензия

Перед копированием контента из данного ресурса ознакомьтесь с лицензией

[Лицензия на содержимое LintBook](LICENSE.md)
