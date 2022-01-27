
# CoffeeLint

Инструмент для статического анализа кода на CoffeeScript

- Понимает современный синтаксис;
- Правила подключаются опционально в конфигурационном файле;
- Расширяется плагинами.

## Установка

```sh
npm install -g @coffeelint/cli # глобально
npm install -D @coffeelint/cli # как зависимость для текущего проекта
```

## Примеры использования

```sh
coffeelint --version # показать версию
coffeelint --help # показать помощь по командам
coffeelint "lib/*.coffee" # проверить все CoffeeScript-файлы в каталоге lib/
coffeelint "lib/*.coffee" --rules "conf/.coffeelintrc.json" # использовать указанный конфиг
coffeelint "lib/**/*.coffee" --ignore-pattern "**/build/**" # рекурсивно, исключить build
echo "a=2" | npx coffeelint -s # проверить STDIN
```

## Настройки

По умолчанию CoffeeLint будет искать конфигурационный файл *.coffeelintrc.json* в текущем каталоге.

```sh
coffeelint --makeconfig > ".coffeelintrc.json" # генерация файла конфигурации
```

Поведение:

- `ignore` — отменить правило
- `warn` — применить правило с предупреждением
- `error` — применить правило с ошибкой

Пример конфигурационного файла:

```json
{
    "extends": "@dopustim/coffeelint-config",
    "max_line_length": { "value": 100, "limitComments": true, "level": "warn" }
}
```

Как вариант, настройки можно указать в *package.json*:

```json
{
    "name": "mypackage",
    "version": "0.0.1",
    "coffeelintConfig": {
        "extends": "@dopustim/coffeelint-config",
        "indentation": {
            "value": 2,
            "level": "warn"
        }
    }
}
```

## Отмена и включение правил

Чтобы игнорировать какие-либо файлы, можно указать их в файле *.coffeelintignore* (синтаксис *.gitignore*).

Можно отменить проверку правил (всех, или указанных) для конкретного блока кода:

```coffee
# coffeelint: disable
alert "foo"
# coffeelint: enable

# coffeelint: disable=no_implicit_parens
alert "foo"
# coffeelint: enable=no_implicit_parens
```

Можно отменить проверку правил (всех, или указанных) для конкретной строки:

```coffee
alert "foo" # coffeelint: disable-line

alert "foo" # coffeelint: disable-line=no_implicit_parens
```

## Ошибки

В зависимости от результатов, инструмент выдает код завершения:

| код | описание                              |
| --- | ------------------------------------- |
|   0 | ошибок нет                            |
|   1 | как минимум одно правило не соблюдено |
|   2 | ошибка в настройках                   |

## Полезные ссылки

Настройки:

- [coffeelint.org](http://www.coffeelint.org/#options) — все правила с кратким описанием
- [@dopustim/coffeelint-config](https://github.com/dopustim/coffeelint-config) — образец конфигурации

Плагины для IDE:

- [SublimeLinter-coffeelint](https://packagecontrol.io/packages/SublimeLinter-coffeelint) — плагин для Sublime Text
- [linter-coffeelint](https://atom.io/packages/linter-coffeelint) — плагин для Atom
- [@id:slb235.vscode-coffeelint](https://marketplace.visualstudio.com/items?itemName=slb235.vscode-coffeelint) — плагин для Visual Studio Code

Плагины для таск-менеджеров:

- [grunt-coffeelint](https://www.npmjs.com/package/grunt-coffeelint) — плагин для Grunt
- [gulp-coffeelint](https://www.npmjs.com/package/gulp-coffeelint) — плагин для Gulp
- [coffeelint-loader](https://www.npmjs.com/package/coffeelint-loader) — плагин для Webpack
