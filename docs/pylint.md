---
description: Инструмент для статического анализа кода на Python
---

# PyLint (ru)

* Понимает современный синтаксис;
* Правила настраиваются в конфигурационном файле;
* Расширяется плагинами.

## Установка

```bash
pip install pylint
```

## Примеры использования

```bash
pylint --version # показать версию
pylint --help # показать помощь по командам
pylint "lib/*.py" # проверить все Python-файлы в каталоге lib/
pylint "lib/*.py" --rcfile="conf/.pylintrc" # использовать указанный конфиг
pylint "lib/**/*.py" --ignore-patterns="**/build/**" # рекурсивно, исключить build
echo "a=2" | pylint --from-stdin demo # проверить STDIN
```

## Настройки

По умолчанию PyLint будет искать конфигурационный файл _.pylintrc_ в текущем каталоге.

```bash
pylint --generate-rcfile > ".pylintrc" # генерация файла конфигурации
```

Классификация ошибок:

* `С` — нарушение стандартов программирования (Convention)
* `R` — требуется рефакторинг (Refactor)
* `W` — предупреждение (Warning)
* `E` — ошибка (Error)
* `F` — ошибка в процессе выполнения Pylint (Fatal)

Пример конфигурационного файла:

```toml
[MASTER]
iignore-patterns=^.*test.py$
jobs=4

[MESSAGES CONTROL]
# C0103 - Name doesn't conform to naming style
# C0111 - Missing docstring
disable=C0103,C0111

[FORMAT]
expected-line-ending-format=LF
ignore-long-lines=^.*token.*$
indent-after-paren=4
indent-string='    '
max-line-length=100
max-module-lines=500
```

## Отмена и включение правил

Можно отменить проверку правил (всех, или указанных) для конкретного блока кода:

```python
# pylint: disable=all
def action(unused):
    pass
# pylint: enable=all

# pylint: disable=unused-argument
def action(unused):
    pass
# pylint: enable=unused-argument
```

Можно отменить проверку правил (всех, или указанных) для конкретной строки:

```python
def action(unused): # pylint: disable=all
    pass # pylint: disable=all

def action(unused): # pylint: disable=unused-argument
    pass # pylint: disable=unused-argument
```

## Ошибки

В зависимости от результатов, инструмент выдает код завершения:

| код | описание                          |
| --- | --------------------------------- |
| 0   | ошибок нет                        |
| 1   | обнаружено нарушение "Fatal"      |
| 2   | обнаружено нарушение "Error"      |
| 4   | обнаружено нарушение "Warning"    |
| 8   | обнаружено нарушение "Refactor"   |
| 16  | обнаружено нарушение "Convention" |
| 32  | внутренняя ошибка при выполнении  |

## Полезные ссылки

Настройки:

* [pylint.readthedocs.io](https://pylint.readthedocs.io/en/latest/technical\_reference/features.html) — все правила с кратким описанием
* [@dopustim/pylint-config](https://github.com/dopustim/pylint-config) — образец конфигурации

Плагины для IDE:

* [SublimeLinter-pylint](https://packagecontrol.io/packages/SublimeLinter-pylint) — плагин для Sublime Text
* [linter-pylint](https://atom.io/packages/linter-pylint) — плагин для Atom
* [@id:fnando.linter](https://marketplace.visualstudio.com/items?itemName=fnando.linter) — плагин для Visual Studio Code
