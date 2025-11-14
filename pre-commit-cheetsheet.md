# pre-commitチートシート

- [pre-commitチートシート](#pre-commitチートシート)
  - [インストール](#インストール)
  - [設定ファイルを作成](#設定ファイルを作成)
  - [gitフックをインストール](#gitフックをインストール)
  - [全ファイルに一度だけ手動実行（初期チェックなどに）](#全ファイルに一度だけ手動実行初期チェックなどに)


## インストール
```
uv add --dev pre-commit
```

## 設定ファイルを作成
.pre-commit-config.yamlを作成
例
```
repos:
- repo: https://github.com/astral-sh/ruff-pre-commit
  # Ruff version.
  rev: v0.11.11
  hooks:
    # Run the linter.
    - id: ruff-check
      args: [ --fix ]
    # Run the formatter.
    - id: ruff-format
```

## gitフックをインストール
```
uv run pre-commit install
```

## 全ファイルに一度だけ手動実行（初期チェックなどに）
```
uv run pre-commit --all-files
```
