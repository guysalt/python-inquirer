[![PyPI](https://img.shields.io/pypi/v/inquirer.svg)][pypi status]
[![Status](https://img.shields.io/pypi/status/inquirer.svg)][pypi status]
[![Python Version](https://img.shields.io/pypi/pyversions/inquirer)][pypi status]
[![License](https://img.shields.io/pypi/l/inquirer)][license]
[![Black](https://img.shields.io/badge/code%20style-black-000000.svg)][black]
<br>
[![Read the documentation at https://python-inquirer.readthedocs.io/](https://img.shields.io/readthedocs/python-inquirer/latest.svg?label=Read%20the%20Docs)][read the docs]
[![Tests](https://github.com/magmax/python-inquirer/workflows/Tests/badge.svg)][tests]
[![Codecov](https://codecov.io/gh/magmax/python-inquirer/branch/main/graph/badge.svg)][codecov]
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)][pre-commit]

[pypi status]: https://pypi.org/project/inquirer/
[read the docs]: https://python-inquirer.readthedocs.io/
[tests]: https://github.com/magmax/python-inquirer/actions?workflow=Tests
[codecov]: https://app.codecov.io/gh/magmax/python-inquirer
[pre-commit]: https://github.com/pre-commit/pre-commit
[black]: https://github.com/psf/black

# python-inquirer

Collection of common interactive command line user interfaces, based on [Inquirer.js].

## Goal and Philosophy

Born as a [Inquirer.js] clone, it shares part of the goals and philosophy.

So, **Inquirer** should ease the process of asking end user **questions**, **parsing**, **validating** answers, managing **hierarchical prompts** and providing **error feedback**.

You can [download the python-inquirer code from GitHub] or [download the wheel from Pypi].

### Platforms support

Python-inquirer supports mainly UNIX-based platforms (eq. Mac OS, Linux, etc.). Windows has experimental support, please let us know if there are any problems!

## Installation

```sh
pip install inquirer
```

## Documentation

Documentation has been moved to [magmax.org/python-inquirer](https://magmax.org/python-inquirer/).

But here you have a couple of usage examples:

### Text

```python
import re

import inquirer
questions = [
  inquirer.Text('name', message="What's your name"),
  inquirer.Text('surname', message="What's your surname"),
  inquirer.Text('phone', message="What's your phone number",
                validate=lambda _, x: re.match('\+?\d[\d ]+\d', x),
                )
]
answers = inquirer.prompt(questions)
```

### Editor

Like a Text question, but used for larger answers. It opens external text editor which is used to collect the answer.

The environment variables $VISUAL and $EDITOR, can be used to specify which editor should be used. If not present inquirer fallbacks to `vim -> emacs -> nano` in this order based on availability in the system.

External editor handling is done using great library [python-editor](https://github.com/fmoo/python-editor).

Example:

```python
import inquirer
questions = [
  inquirer.Editor('long_text', message="Provide long text")
]
answers = inquirer.prompt(questions)
```

### List

Shows a list of choices, and allows the selection of one of them.

Example:

```python
import inquirer
questions = [
  inquirer.List('size',
                message="What size do you need?",
                choices=['Jumbo', 'Large', 'Standard', 'Medium', 'Small', 'Micro'],
            ),
]
answers = inquirer.prompt(questions)
```

List questions can take one extra argument `carousel=False`. If set to true, the answers will rotate (back to first when pressing down on last choice, and down to last choice when pressing up on first choice)

### Checkbox

Shows a list of choices, with multiple selection.

Example:

```python
import inquirer
questions = [
  inquirer.Checkbox('interests',
                    message="What are you interested in?",
                    choices=['Computers', 'Books', 'Science', 'Nature', 'Fantasy', 'History'],
                    ),
]
answers = inquirer.prompt(questions)
```

Checkbox questions can take one extra argument `carousel=False`. If set to true, the answers will rotate (back to first when pressing down on last choice, and down to last choice when pressing up on first choice)

### Path

Like Text question, but with builtin validations for working with paths.

Example:

```python
import inquirer
questions = [
  inquirer.Path('log_file',
                 message="Where logs should be located?",
                 path_type=inquirer.Path.DIRECTORY,
                ),
]
answers = inquirer.prompt(questions)
```

## Contributing

Contributions are very welcome.
To learn more, see the [Contributor Guide].

## License

Copyright (c) 2014-2021 Miguel Ángel García ([@magmax_en]), based on [Inquirer.js], by Simon Boudrias ([@vaxilart])

Distributed under the terms of the [MIT license][license].

<!-- github-only -->

[license]: https://github.com/magmax/python-inquirer/blob/main/LICENSE
[@magmax_en]: https://twitter.com/magmax_en
[@vaxilart]: https://twitter.com/vaxilart
[contributor guide]: CONTRIBUTING.md
[download the python-inquirer code from github]: https://github.com/magmax/python-inquirer
[download the wheel from pypi]: https://pypi.python.org/pypi/inquirer
[examples/]: https://github.com/magmax/python-inquirer/tree/master/examples
[inquirer.js]: https://github.com/SBoudrias/Inquirer.js
