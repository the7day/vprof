[![Build Status](https://travis-ci.org/nvdv/vprof.svg?branch=master)](https://travis-ci.org/nvdv/vprof)
[![PyPI](https://img.shields.io/pypi/v/vprof.svg)](https://pypi.python.org/pypi/vprof/)

# vprof

vprof is a Python package providing rich and interactive visualizations for
various Python program characteristics such as running time and memory usage.
It supports Python 2.7, Python 3.4, Python 3.5 and distributed under BSD license.

The project is in active development and some of its features might not work as
expected.

## Screenshots
![flame-graph](http://i.imgur.com/ijC7wmj.png?1)
![memory-stats](http://i.imgur.com/3uUeWA2.png?1)
![code-heatmap](http://i.imgur.com/08umZI8.png?1)

## Contributing
All contributions are highly encouraged! You can add new features,
report and fix existing bugs and write docs and tutorials.
Feel free to open issue or send pull request!

## Prerequisites
The required dependencies to build ```vprof``` from source code:
 * Python 2.7, Python 3.4 or Python 3.5
 * `pip`
 * `npm` >= 3.3.12

`npm` is required to build `vprof` from sources only.

## Dependencies
All Python and `npm` module dependencies are listed in `package.json` and `requirements.txt`.

## Installation
`vprof` can be installed from PyPI

```sh
pip install vprof
```

To build `vprof` from sources, clone this repository and execute

```sh
python setup.py deps_install && python setup.py build_ui && python setup.py install
```

To install just `vprof` dependencies, run

```sh
python setup.py deps_install
```

## Usage

```sh
vprof -c <modes> <program>
```
`<modes>` is a combination of supported modes:

* `c` - CPU flame graph.

Shows CPU flame graph for `<program>`.

* `m` - memory graph.

Shows objects that are tracked by CPython GC and left in memory after code execution. Also shows process memory usage during execution of each line of `<program>`.

* `h` - code heatmap.

Displays all executed code of `<program>` with line execution count.

`<program>` can be Python source file (e.g. `testscript.py`) or path to package (e.g. `myproject/test_package`).

Use double quotes to run scripts with arguments:

```sh
vprof -c cmh "testscript.py --foo --bar"
```

Modes can be combined

```sh
vprof -c cm testscript.py
```

`vprof` can also profile functions. In order to do this,
launch `vprof` in remote mode:

```sh
vprof -r
```

`vprof` will open new tab in default web browser and then wait for stats.

To profile a function run

```python
from vprof import profiler

def foo(arg1, arg2):
    ...

profiler.run(foo, 'cmh', args=(arg1, arg2), host='localhost', port=8000)
```

where `cmh` is profiling mode, `host` and `port` are hostname and port of `vprof` server launched in remote mode. Obtained stats will be rendered in new tab of default web browser, opened by `vprof -r` command.

`vprof` can save profile to file and render profile from file.

```sh
vprof -c cmh --output-file profile.json
```

writes profile to file and

```sh
vprof --input-file profile.json
```
renders visualizations from previously saved file.

Check `vprof -h` for full list of supported parameters.

To show UI help, press `h` when visualizations are displayed in browser.

Also you can check `examples` directory for more profiling examples.

## Testing

Just run:

```sh
python setup.py test && python setup.py e2e_test
```

## License

BSD
