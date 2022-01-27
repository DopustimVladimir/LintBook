
# ESLint

Инструмент для статического анализа кода на JavaScript

- Понимает современный синтаксис;
- Правила подключаются опционально в конфигурационном файле;
- Расширяется плагинами.

## Установка

```sh
npm install -g eslint # глобально
npm install -D eslint # как зависимость для текущего проекта
```

## Примеры использования

```sh
eslint --version # показать версию
eslint --help # показать помощь по командам
eslint "lib/*.js" # проверить все JavaScript-файлы в каталоге lib/
eslint "lib/*.js" --fix # исправлять ошибки
eslint "lib/*.js" --config "conf/.eslintrc.json" # использовать указанный конфиг
eslint "lib/**/*.js" --ignore-pattern "**/build/**" # рекурсивно, исключить build
echo 'a=2' | eslint --stdin # проверить STDIN
```

## Настройки

По умолчанию ESLint будет искать конфигурационный файл *.eslintrc.json* в текущем каталоге.

```sh
eslint --init # генерация файла конфигурации
```

Поведение:

- `0`, или `off` — отменить правило
- `1`, или `warn` — применить правило с предупреждением
- `2`, или `error` — применить правило с ошибкой

Пример конфигурационного файла:

```json
{
    "extends": "@dopustim/eslint-config",
    "env": {
        "browser": true,
        "es2020": true,
        "node": true
    },
    "parserOptions": {
        "sourceType": "module",
        "ecmaVersion": 2020
    },
    "rules": {
        "max-len": [ 1, { "code": 100 } ]
    }
}
```

Как вариант, настройки можно указать в *package.json*:

```json
{
    "name": "mypackage",
    "version": "0.0.1",
    "eslintConfig": {
        "extends": "@dopustim/eslint-config",
        "env": {
            "browser": true,
            "es2020": true,
            "node": true
        },
        "parserOptions": {
            "sourceType": "module",
            "ecmaVersion": 2020
        },
        "rules": {
            "max-len": [ 1, { "code": 100 } ]
        }
    }
}
```

Можно подключать плагины и пользоваться другими правилами:

```json
{
    "plugins": [
        "react"
    ],
    "extends": [
        "@dopustim/eslint-config",
        "plugin:react/recommended"
    ],
    "env": {
        "browser": true,
        "es2020": true
    },
    "parserOptions": {
        "sourceType": "module",
        "ecmaVersion": 2020,
        "ecmaFeatures": {
            "jsx": true
        }
    },
    "rules": {
        "max-len": [ 1, { "code": 100 } ],
        "react/prop-types": 0
    },
    "settings": {
        "react": {
            "version": "17.0.2"
        }
    }
}
```

## Окружение

Правило `no-undef` очень полезное, поскольку позволяет поймать потенциальную ошибку `ReferenceError` (обращение к переменной, которая не существует). Но бывает так, что программа неявно использует переменные окружения из глобальной области.

Набор доступных глобальных переменных зависит от окружения:

- `browser` — глобальные объекты браузера
- `es2020` — глобальные объекты ES2020
- `node` — глобальные объекты Node.js
- `mocha` — глобальные объекты Mocha
- `jasmine` — глобальные объекты Jasmine
- `jquery` — глобальные объекты jQuery
- `mongo` — глобальные объекты MongoDB
- `atomtest` — глобальные объекты тестов редактора Atom
- `webextensions` — глобальные объекты WebExtensions

Можно указать окружение в *package.json*:

```json
{
    "env": {
        "browser": true
    }
}
```

Можно указать окружение в комментариях:

```js
/* eslint-env browser */
console.log(window)
```

Можно указать глобальные переменные в *package.json*:

```json
{
    "globals": {
        "num1": "writable",
        "num2": "readonly"
    }
}
```

Можно указать глобальные переменные в комментариях:

```js
/* global num1:writable, num2:readonly */
num1 = 1
console.log(num1 + num2)
```

## Отмена и включение правил

Чтобы игнорировать какие-либо файлы, можно указать их в файле *.eslintignore* (синтаксис *.gitignore*), или в *package.json*:

```json
{
    "ignorePatterns": [
        "*.min.js"
    ]
}
```

Можно отменить проверку правил (всех, или указанных) для конкретного блока кода:

```js
/* eslint-disable */
alert('foo')
/* eslint-enable */

/* eslint-disable no-alert, quotes */
alert('foo')
/* eslint-enable no-alert, quotes */
```

Можно отменить проверку правил (всех, или указанных) для конкретной строки:

```js
alert('foo') // eslint-disable-line

alert('foo') // eslint-disable-line no-alert, quotes
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

- [eslint.org](https://eslint.org/docs/rules/) — все правила с кратким описанием
- [@dopustim/eslint-config](https://github.com/dopustim/eslint-config) — образец конфигурации

Плагины для IDE:

- [SublimeLinter-eslint](https://packagecontrol.io/packages/SublimeLinter-eslint) — плагин для Sublime Text
- [linter-eslint](https://atom.io/packages/linter-eslint) — плагин для Atom
- [@id:dbaeumer.vscode-eslint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) — плагин для Visual Studio Code

Плагины для таск-менеджеров:

- [grunt-eslint](https://www.npmjs.com/package/grunt-eslint) — плагин для Grunt
- [gulp-eslint](https://www.npmjs.com/package/gulp-eslint) — плагин для Gulp
- [eslint-webpack-plugin](https://www.npmjs.com/package/eslint-webpack-plugin) — плагин для Webpack
