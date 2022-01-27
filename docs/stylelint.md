
# StyleLint

Инструмент для статического анализа кода на CSS, SCSS, Sass, Less и SugarSS

- Понимает современный синтаксис;
- Правила подключаются опционально в конфигурационном файле;
- Расширяется плагинами.

## Установка

```sh
npm install -g stylelint # глобально
npm install -D stylelint # как зависимость для текущего проекта
```

## Примеры использования

```sh
stylelint --version # показать версию
stylelint --help # показать помощь по командам
stylelint "lib/*.css" # проверить все CSS-файлы в каталоге lib/
stylelint "lib/*.css" --fix # исправлять ошибки
stylelint "lib/*.css" --config "conf/.stylelintrc.json" # использовать указанный конфиг
stylelint "lib/**/*.css" --ignore-pattern "**/build/**" # рекурсивно, исключить build
echo "a { color: pink; }" | stylelint # проверить STDIN
```

## Настройки

По умолчанию StyleLint будет искать конфигурационный файл *.stylelintrc.json* в текущем каталоге.

Поведение:

- `warning` — применить правило с предупреждением
- `error` — применить правило с ошибкой

Пример конфигурационного файла:

```json
{
    "extends": "@dopustim/stylelint-config",
    "rules": {
        "max-line-length": [ 100, { "severity": "warning" } ]
    }
}
```

Как вариант, настройки можно указать в *package.json*:

```json
{
    "name": "mypackage",
    "version": "0.0.1",
    "stylelint": {
        "extends": "@dopustim/stylelint-config",
        "rules": {
            "max-line-length": [ 100, { "severity": "warning" } ]
        }
    }
}
```

Можно подключать плагины и пользоваться другими правилами:

```json
{
    "name": "mypackage",
    "version": "0.0.1",
    "stylelint": {
        "extends": "@dopustim/stylelint-config",
        "plugins": [
            "stylelint-scss"
        ],
        "rules": {
            "max-line-length": [ 100, { "severity": "warning" } ],
            "scss/dollar-variable-pattern": "^foo",
            "scss/selector-no-redundant-nesting-selector": true
        }
    }
}
```

## Отмена и включение правил

Чтобы игнорировать какие-либо файлы, можно указать их в *.stylelintignore* (синтаксис *.gitignore*), или в *package.json*:

```json
{
    "ignoreFiles": [
        "*.min.css"
    ]
}
```

Можно отменить проверку правил (всех, или указанных) для конкретного блока кода:

```css
/* stylelint-disable */
#root {
  color: pink !important;
}
/* stylelint-enable */

/* stylelint-disable selector-no-id, declaration-no-important */
#root {
  color: pink !important;
}
/* stylelint-enable selector-no-id, declaration-no-important */
```

Можно отменить проверку правил (всех, или указанных) для конкретной строки:

```css
#root { /* stylelint-disable-line */
  color: pink !important; /* stylelint-disable-line */
}

#root { /* stylelint-disable-line selector-no-id */
  color: pink !important; /* stylelint-disable-line declaration-no-important */
}
```

## Ошибки

Настройки

В зависимости от результатов, инструмент выдает код завершения:

| код | описание                              |
| --- | ------------------------------------- |
|  0  | ошибок нет                            |
|  1  | что-то пошло не так                   |
|  2  | как минимум одно правило не соблюдено |
| 78  | ошибка в настройках                   |
| 80  | не нашлись файлы для проверки         |

## Полезные ссылки

Настройки:

- [stylelint.io](https://stylelint.io/user-guide/rules/) — все правила с кратким описанием
- [@dopustim/stylelint-config](https://github.com/dopustim/stylelint-config) — образец конфигурации

Плагины для IDE:

- [SublimeLinter-stylelint](https://packagecontrol.io/packages/SublimeLinter-stylelint) — плагин для Sublime Text
- [linter-stylelint](https://atom.io/packages/linter-stylelint) — плагин для Atom
- [@id:shinnn.stylelint](https://marketplace.visualstudio.com/items?itemName=shinnn.stylelint) — плагин для Visual Studio Code

Плагины для таск-менеджеров:

- [grunt-stylelint](https://www.npmjs.com/package/grunt-stylelint) — плагин для Grunt
- [gulp-stylelint](https://www.npmjs.com/package/gulp-stylelint) — плагин для Gulp
- [stylelint-webpack-plugin](https://www.npmjs.com/package/stylelint-webpack-plugin) — плагин для Webpack
