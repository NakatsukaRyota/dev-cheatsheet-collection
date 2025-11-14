# ruffチートシート
- [ruffチートシート](#ruffチートシート)
  - [インストール](#インストール)
  - [リンター](#リンター)
  - [フォーマット](#フォーマット)
  - [設定ファイル例（pyproject.toml）](#設定ファイル例pyprojecttoml)

## インストール
```
uv add -dev ruff
```

## リンター
```
ruff check .                  # Lint files in the current directory.
ruff check . --fix            # Lint files in the current directory and fix any fixable errors.
```

## フォーマット
```
ruff format                   # Format all files in the current directory.
```

## 設定ファイル例（pyproject.toml）
```
[tool.ruff]
line-length = 100

[tool.ruff.lint]
select = ["E", "F", "I", "B"]
ignore = ["E501", "E203",]
```
