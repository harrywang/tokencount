# Publishing Guide for tokencount

This guide explains how to publish the tokencount package to PyPI.

## Prerequisites

1. Create accounts on [PyPI](https://pypi.org/) and [Test PyPI](https://test.pypi.org/) (recommended for testing)
2. Install required tools:
   ```bash
   pip install build twine
   ```

## Steps to Publish

### 1. Configure PyPI Credentials

Create a `.pypirc` file in your home directory:

```bash
# Create or edit the file
nano ~/.pypirc
```

Add the following content (replace with your actual tokens):

```
[distutils]
index-servers =
    pypi
    testpypi

[pypi]
username = __token__
password = your_pypi_token_here

[testpypi]
repository = https://test.pypi.org/legacy/
username = __token__
password = your_testpypi_token_here
```

### 2. Build the Package

From the root directory of the project:

```bash
python -m build
```

This will create both source distribution and wheel files in the `dist/` directory.

### 3. Test Your Package (Recommended)

Upload to Test PyPI first:

```bash
twine upload --repository testpypi dist/*
```

Then install from Test PyPI to verify it works:

```bash
pip install --index-url https://test.pypi.org/simple/ tokencount
```

### 4. Publish to PyPI

Once you've verified everything works:

```bash
twine upload dist/*
```

### 5. Verify Installation

```bash
pip install tokencount
tokencount --help
```

## Updating the Package

1. Update the version number in `tokencount/__init__.py` and `setup.py`
2. Rebuild and upload following steps 2-4 above

## Troubleshooting

- If you get an error about the package already existing, make sure you've updated the version number
- If you get authentication errors, check your `.pypirc` file and ensure your tokens are correct
