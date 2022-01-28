
# ESLint

A tool for static analysis of JavaScript code

- Understands modern syntax;
- Rules are connected optionally in the configuration file;
- Expanded by plugins.

## Installation

```sh
npm install -g eslint # globally
npm install -D eslint # as a dependency for the current project
```

## Usage examples

```sh
eslint --version # show the version
eslint --help # show help about commands
eslint "lib/*.js" # check all JavaScript files in the lib/ directory
eslint "lib/*.js" --fix # fix errors
eslint "lib/*.js" --config "conf/.eslintrc.json" # use the specified config
eslint "lib/**/*.js" --ignore-pattern "**/build/**" # recursively, exclude build
echo 'a=2' | eslint --stdin # check STDIN
```

## Settings

By default, ESLint will search for the configuration file *.eslintrc.json* in the current directory.

```sh
eslint --init # generate a configuration file
```

Behaviour:

- `0`, or `off` — cancel the rule
- `1`, or `warn` — apply a rule with a warning
- `2`, or `error` — apply a rule with an error

Example of a configuration file:

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

Alternatively, the settings can be specified in *package.json*:

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

You can connect plugins and use other rules:

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

## Environment

The `no-undef` rule is very useful because it allows you to catch a potential `ReferenceError` error (referring to a variable that does not exist). But sometimes the program implicitly uses environment variables from the global scope.

The set of available global variables depends on the environment:

- `browser` — Browser global objects
- `es2020` — ES2020 global objects
- `node` — Node.js global objects
- `mocha` — Mocha global objects
- `jasmine` — Jasmine global objects
- `jquery` — jQuery global objects
- `mongo` — MongoDB global objects
- `atomtest` — Atom editor tests global objects
- `webextensions` — WebExtensions global objects

You can specify the environment in *package.json*:

```json
{
    "env": {
        "browser": true
    }
}
```

You can specify the environment in the comments:

```js
/* eslint-env browser */
console.log(window)
```

You can specify global variables in *package.json*:

```json
{
    "globals": {
        "num1": "writable",
        "num2": "readonly"
    }
}
```

You can specify global variables in the comments:

```js
/* global num1:writable, num2:readonly */
num1 = 1
console.log(num1 + num2)
```

## Cancellation and inclusion of rules

To ignore any files, you can specify them in the *.eslintignore* file (syntax *.gitignore*), or in *package.json*:

```json
{
    "ignorePatterns": [
        "*.min.js"
    ]
}
```

You can cancel the validation of the rules (all or specified) for a specific block of code:

```js
/* eslint-disable */
alert('foo')
/* eslint-enable */

/* eslint-disable no-alert, quotes */
alert('foo')
/* eslint-enable no-alert, quotes */
```

You can cancel the validation of the rules (all or specified) for a specific line:

```js
alert('foo') // eslint-disable-line

alert('foo') // eslint-disable-line no-alert, quotes
```

## Error codes

Depending on the results, the tool outputs a completion code:

| code | description                           |
| ---- | ------------------------------------- |
|    0 | no errors                             |
|    1 | at least one rule is not followed     |
|    2 | error in settings                     |

## Useful links

Settings:

- [eslint.org](https://eslint.org/docs/rules/) — all rules with a brief description
- [@dopustim/eslint-config](https://github.com/dopustim/eslint-config) — sample configuration

IDE Plugins:

- [SublimeLinter-eslint](https://packagecontrol.io/packages/SublimeLinter-eslint) — Sublime Text plugin
- [linter-eslint](https://atom.io/packages/linter-eslint) — Atom plugin
- [@id:dbaeumer.vscode-eslint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) — Visual Studio Code plugin

Task Manager Plugins:

- [grunt-eslint](https://www.npmjs.com/package/grunt-eslint) — Grunt plugin
- [gulp-eslint](https://www.npmjs.com/package/gulp-eslint) — Gulp plugin
- [eslint-webpack-plugin](https://www.npmjs.com/package/eslint-webpack-plugin) — Webpack plugin
