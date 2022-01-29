---
description: A tool for static analysis of CSS, Sass, Less and other CSS-like code
---

# StyleLint (en)

* Understands modern syntax;
* Rules are connected optionally in the configuration file;
* Expanded by plugins.

## Installation

```bash
npm install -g stylelint # globally
npm install -D stylelint # as a dependency for the current project
```

## Usage examples

```bash
stylelint --version # show the version
stylelint --help # show help about commands
stylelint "lib/*.css" # check all CSS files in the lib/ directory
stylelint "lib/*.css" --fix # fix errors
stylelint "lib/*.css" --config "conf/.stylelintrc.json" # use the specified config
stylelint "lib/**/*.css" --ignore-pattern "**/build/**" # recursively, exclude build
echo "a { color: pink; }" | stylelint # check STDIN
```

## Settings

By default, StyleLint will search for the configuration file _.stylelintrc.json_ in the current directory.

Behaviour:

* `warning` — apply a rule with a warning
* `error` — apply a rule with an error

Example of a configuration file:

```json
{
    "extends": "@dopustim/stylelint-config",
    "rules": {
        "max-line-length": [ 100, { "severity": "warning" } ]
    }
}
```

Alternatively, the settings can be specified in _package.json_:

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

You can connect plugins and use other rules:

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

## Cancellation and inclusion of rules

To ignore any files, you can specify them in the _.stylelintignore_ file (syntax _.gitignore_), or in _package.json_:

```json
{
    "ignoreFiles": [
        "*.min.css"
    ]
}
```

You can cancel the validation of the rules (all or specified) for a specific block of code:

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

You can cancel the validation of the rules (all or specified) for a specific line:

```css
#root { /* stylelint-disable-line */
  color: pink !important; /* stylelint-disable-line */
}

#root { /* stylelint-disable-line selector-no-id */
  color: pink !important; /* stylelint-disable-line declaration-no-important */
}
```

## Error codes

Depending on the results, the tool outputs a completion code:

| code | description                       |
| ---- | --------------------------------- |
| 0    | no errors                         |
| 1    | something went wrong              |
| 2    | at least one rule is not followed |
| 78   | error in settings                 |
| 80   | there were no files to check      |

## Useful links

Settings:

* [stylelint.io](https://stylelint.io/user-guide/rules/) — all rules with a brief description
* [@dopustim/stylelint-config](https://github.com/dopustim/stylelint-config) — sample configuration

IDE Plugins:

* [SublimeLinter-stylelint](https://packagecontrol.io/packages/SublimeLinter-stylelint) — Sublime Text plugin
* [linter-stylelint](https://atom.io/packages/linter-stylelint) — Atom plugin
* [@id:shinnn.stylelint](https://marketplace.visualstudio.com/items?itemName=shinnn.stylelint) — Visual Studio Code plugin

Task Manager Plugins:

* [grunt-stylelint](https://www.npmjs.com/package/grunt-stylelint) — Grunt plugin
* [gulp-stylelint](https://www.npmjs.com/package/gulp-stylelint) — Gulp plugin
* [stylelint-webpack-plugin](https://www.npmjs.com/package/stylelint-webpack-plugin) — Webpack plugin
