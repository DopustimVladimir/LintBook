---
description: The book describes tools for static code analysis
---

# LintBook (en)

**Lint** is a static code analysis tool written in C language by Stephen Johnson (Bell Labs) in 1978. Similar (Lint-like) tools are sometimes called Linters, and the analysis process is called Linting. One of the modern linters is \[Infer]\(https://fbinfer.com /) from Facebook, which supports C, C++ and Java.

Static code analysis is carried out without the actual execution of the programs under study. Linters are often used in code editors — the linter does its job and the editor highlights areas where there may be an error. The static analysis tool detects errors, potentially dangerous expressions, undesirable constructions, incorrect writing style and other garbage. Using a linter can help the development team write code correctly, neatly and consistently.

One of the important points is the ability to configure the analyzer for the needs of a specific project in a specific environment that requires a special approach to writing code. Thus, the programmer chooses what should be considered an error and in which case to display a warning.

There are many different linters, and the purpose of this guide is to provide a brief overview of some of them and provide configuration examples.

* [CoffeeLint](docs/coffeelint\_en.md) — for CoffeeScript
* [ESLint](docs/eslint\_en.md) — for JavaScript
* [PyLint](docs/pylint\_en.md) — for Python
* [StyleLint](docs/stylelint.md) — for CSS, Sass, Less, ...

## Примеры конфигурации

If you are on this page in order to download my configs:

* [@dopustim/stylelint-config](https://github.com/dopustim/stylelint-config) — StyleLint configuration example
* [@dopustim/eslint-config](https://github.com/dopustim/eslint-config) — ESLint configuration example
* [@dopustim/coffeelint-config](https://github.com/dopustim/coffeelint-config) — CoffeeLint configuration example
* [@dopustim/pylint-config](https://github.com/dopustim/pylint-config) — PyLint configuration example

## Лицензия

Before copying content from this resource, read the license

[LintBook Content License](LICENSE\_en.md)
