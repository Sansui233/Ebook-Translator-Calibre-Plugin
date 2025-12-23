# Development Guide

## Prerequisites

- **Calibre** >= 5.0.0 - [Download from calibre-ebook.com](https://calibre-ebook.com/download)
- **Python** >= 3.10 (for development tools; Calibre provides its own Python runtime)
- **uv** - Fast Python package manager - [Install from astral.sh](https://docs.astral.sh/uv/)

## Setup Development Environment

Install development dependencies(just for type checking)

```sh
uv sync
```

## Debug

Change directory into plugin project and make sure `calibre-customize` is in the environment variable.

```sh
calibre-customize -b . # register plugin from current folder
calibre-customize -l | grep "Ebook Translator" # check if plugin installed
calibre-debug -g # open calibre with debug mode
```

one line debug command

```sh
calibre-debug -s; calibre-customize -b /path/to/your/plugin/folder; calibre
```

## Running Tests


```bash
calibre-debug test.py # Run all tests
calibre-debug test.py test_element.py # Run specific test file
calibre-debug test.py test_merge # Run specific test method (pattern matching)
```

## Building the Plugin

To create a distributable plugin file:

1. Ensure all changes are committed
2. Create a ZIP file of the plugin directory (excluding development files)
3. Rename the ZIP file with `.zip` extension to `.zip` (Calibre plugins use ZIP format)

```bash
# Example build script (adjust as needed)
zip -r ebook-translator.zip . \
  -x "*.pyc" \
  -x "__pycache__/*" \
  -x ".git/*" \
  -x "tests/*" \
  -x ".venv/*" \
  -x "*.egg-info/*"
```

## Resources

- [Calibre Plugin Development](https://manual.calibre-ebook.com/plugins.html)
- [calibre-customize tool](https://manual.calibre-ebook.com/generated/en/calibre-customize.html)
