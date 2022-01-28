
# CoffeeLint

A tool for static analysis of CoffeeScript code

- Understands modern syntax;
- Rules are connected optionally in the configuration file;
- Expanded by plugins.

## Installation

```sh
npm install -g @coffeelint/cli # globally
npm install -D @coffeelint/cli # as a dependency for the current project
```

## Примеры использования

```sh
coffeelint --version # show the version
coffeelint --help # show help about commands
coffeelint "lib/*.coffee" # check all CoffeeScript files in the lib/ directory
coffeelint "lib/*.coffee" --rules "conf/.coffeelintrc.json" # use the specified config
coffeelint "lib/**/*.coffee" --ignore-pattern "**/build/**" # recursively, exclude build
echo "a=2" | npx coffeelint -s # check STDIN
```

## Settings

By default, CoffeeLint will search for the configuration file *.coffeelintrc.json* in the current directory.

```sh
coffeelint --makeconfig > ".coffeelintrc.json" # generating a configuration file
```

Behaviour:

- `ignore` — cancel the rule
- `warn` — apply a rule with a warning
- `error` — apply a rule with an error

Example of a configuration file:

```json
{
    "extends": "@dopustim/coffeelint-config",
    "max_line_length": { "value": 100, "limitComments": true, "level": "warn" }
}
```

Alternatively, the settings can be specified in *package.json*:

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

## Cancellation and inclusion of rules

To ignore any files, you can specify them in the file *.coffeelintignore* (syntax *.gitignore*).

You can cancel the validation of the rules (all or specified) for a specific block of code:

```coffee
# coffeelint: disable
alert "foo"
# coffeelint: enable

# coffeelint: disable=no_implicit_parens
alert "foo"
# coffeelint: enable=no_implicit_parens
```

You can cancel the validation of the rules (all or specified) for a specific line:

```coffee
alert "foo" # coffeelint: disable-line

alert "foo" # coffeelint: disable-line=no_implicit_parens
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

- [coffeelint.org](http://www.coffeelint.org/#options) — all rules with a brief description
- [@dopustim/coffeelint-config](https://github.com/dopustim/coffeelint-config) — sample configuration

IDE Plugins:

- [SublimeLinter-coffeelint](https://packagecontrol.io/packages/SublimeLinter-coffeelint) — Sublime Text plugin
- [linter-coffeelint](https://atom.io/packages/linter-coffeelint) — Atom plugin
- [@id:slb235.vscode-coffeelint](https://marketplace.visualstudio.com/items?itemName=slb235.vscode-coffeelint) — Visual Studio Code plugin

Task Manager Plugins:

- [grunt-coffeelint](https://www.npmjs.com/package/grunt-coffeelint) — Grunt plugin
- [gulp-coffeelint](https://www.npmjs.com/package/gulp-coffeelint) — Gulp plugin
- [coffeelint-loader](https://www.npmjs.com/package/coffeelint-loader) — Webpack plugin
