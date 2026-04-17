# uv-python-setup

A GitHub Action that bootstraps a Python + [uv](https://github.com/astral-sh/uv) environment in one step: installs Python, installs uv, and runs `uv sync`. Supports private PyPI registries via named-index credentials without embedding secrets in URLs.

## Usage

### Public PyPI only

```yaml
- uses: jedi-knights/uv-python-setup@v0
  with:
    python-version: '3.13'
```

### With a private registry

```yaml
- uses: jedi-knights/uv-python-setup@v0
  with:
    python-version: '3.13'
    index-name: artifactory          # matches [[tool.uv.index]] name in pyproject.toml
    index-username: ${{ secrets.ARTIFACTORY_USER }}
    index-password: ${{ secrets.ARTIFACTORY_TOKEN }}
```

Credentials are exported as `UV_INDEX_<NAME>_USERNAME` / `UV_INDEX_<NAME>_PASSWORD` — no secrets embedded in URLs.

## Inputs

| Input | Required | Default | Description |
|---|---|---|---|
| `python-version` | no | `3.13` | Python version to install |
| `uv-version` | no | `latest` | uv version to install |
| `sync-args` | no | `--locked` | Arguments passed to `uv sync` |
| `index-name` | no | `''` | Private index name from `pyproject.toml` |
| `index-username` | no | `''` | Username for the private index |
| `index-password` | no | `''` | Password or token for the private index |
| `extra-index-url` | no | `https://pypi.org/simple` | Fallback index URL |
