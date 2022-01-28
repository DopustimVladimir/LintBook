
# PyLint

A tool for static analysis of Python code

- Understands modern syntax;
- The rules are configured in the configuration file;
- Expanded by plugins.

## Installation

```sh
pip install pylint
```

## Usage examples

```sh
pylint --version # show the version
pylint --help # show help about commands
pylint "lib/*.py" # check all Python files in the lib/ directory
pylint "lib/*.py" --rcfile="conf/.pylintrc" # use the specified config
pylint "lib/**/*.py" --ignore-patterns="**/build/**" # recursively, exclude build
echo "a=2" | pylint --from-stdin demo # check STDIN
```

## Settings

By default, PyLint will search for the configuration file *.pylintrc* in the current directory.

```sh
pylint --generate-rcfile > ".pylintrc" # generate a configuration file
```

Classification of errors:

- `С` — violation of programming standards (Convention)
- `R` — refactoring required (Refactor)
- `W` — warning (Warning)
- `E` — error (Error)
- `F` — error during Pylint execution (Fatal)

Example of a configuration file:

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

## Cancellation and inclusion of rules

You can cancel the validation of the rules (all or specified) for a specific block of code:

```py
# pylint: disable=all
def action(unused):
    pass
# pylint: enable=all

# pylint: disable=unused-argument
def action(unused):
    pass
# pylint: enable=unused-argument
```

You can cancel the validation of the rules (all or specified) for a specific line:

```py
def action(unused): # pylint: disable=all
    pass # pylint: disable=all

def action(unused): # pylint: disable=unused-argument
    pass # pylint: disable=unused-argument
```

## Error codes

Depending on the results, the tool outputs a completion code:

| code | description                     |
| ---- | ------------------------------- |
|    0 | no errors                       |
|    1 | detected "Fatal" violation      |
|    2 | detected "Error" violation      |
|    4 | detected "Warning" violation    |
|    8 | detected "Refactor" violation   |
|   16 | detected "Convention" violation |
|   32 | internal error during execution |

## Useful links

Settings:

- [pylint.readthedocs.io](https://pylint.readthedocs.io/en/latest/technical_reference/features.html) — all rules with a brief description
- [@dopustim/pylint-config](https://github.com/dopustim/pylint-config) — sample configuration

IDE Plugins:

- [SublimeLinter-pylint](https://packagecontrol.io/packages/SublimeLinter-pylint) — Sublime Text plugin
- [linter-pylint](https://atom.io/packages/linter-pylint) — Atom plugin
- [@id:fnando.linter](https://marketplace.visualstudio.com/items?itemName=fnando.linter) — Visual Studio Code plugin
