# codiff-action

A GitHub Action that posts a structural call-graph diff as a comment on every pull request.

Instead of reviewing hundreds of changed lines, your team sees which functions were added, modified, or removed — and how they connect across files — rendered as a Mermaid diagram that GitHub renders natively.

The comment is created on PR open and updated on every subsequent push. If there are no structural changes, the action stays silent.

## Usage

```yaml
# .github/workflows/codiff.yml
name: codiff

on:
  pull_request:
    types: [opened, synchronize, reopened]

permissions:
  pull-requests: write

jobs:
  codiff:
    runs-on: ubuntu-latest
    steps:
      - uses: issahammoud/codiff-action@v1
```

Add this file to your repo and every PR will automatically receive a structural diff comment.

## Inputs

| Input | Description | Default |
|---|---|---|
| `token` | GitHub token with `pull-requests: write` | `github.token` |
| `python-version` | Python version to use | `3.11` |
| `silent-on-empty` | Stay silent when no structural changes detected | `true` |

## Supported languages

Python and TypeScript.

## How it works

On each PR event, the action checks out the repository, installs [codiff](https://github.com/issahammoud/codiff), and runs a structural diff between the PR base and head commits. The result is posted as a PR comment (or updated if one already exists). No LLM, no embeddings, fully offline.

## Requirements

- Python 3.11+
- Repositories with Python or TypeScript code
