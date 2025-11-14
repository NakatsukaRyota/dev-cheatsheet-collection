# Python プロジェクト開始ガイド
（uv  / ruff / pre-commit 統合）

---

- [Python プロジェクト開始ガイド](#python-プロジェクト開始ガイド)
  - [1. プロジェクトの作成（uv）](#1-プロジェクトの作成uv)
  - [2. Python バージョンの固定（uv）](#2-python-バージョンの固定uv)
  - [3. 依存管理：パッケージの追加（uv）](#3-依存管理パッケージの追加uv)
  - [4. ruff の設定（Lint \& Format）](#4-ruff-の設定lint--format)
  - [5. Git 初回コミット](#5-git-初回コミット)
  - [6. pre-commit の設定（自動 Lint/Format）](#6-pre-commit-の設定自動-lintformat)
  - [7. スクリプトの実行（依存含む）](#7-スクリプトの実行依存含む)
  - [8. パッケージ同期（環境再現用）](#8-パッケージ同期環境再現用)
  - [9. requirements.txt（必要なら）](#9-requirementstxt必要なら)
  - [10. 依存関係ツリーの表示](#10-依存関係ツリーの表示)
- [プロジェクト構成例](#プロジェクト構成例)

## 1. プロジェクトの作成（uv）

プロジェクトディレクトリを作成し、初期化する。

```bash
uv init my-project
cd my-project
```

## 2. Python バージョンの固定（uv）
必要な Python をインストール：
```
uv python install 3.13
```
このプロジェクトで使う Python を固定：
```
uv python pin 3.13
```
## 3. 依存管理：パッケージの追加（uv）
本番用パッケージ
```
uv add requests
```
開発用パッケージ（ruff, pre-commit など）
```
uv add --dev ruff
uv add --dev pre-commit
```
## 4. ruff の設定（Lint & Format）
`pyproject.toml` に追加：
```
[tool.ruff]
line-length = 100

[tool.ruff.lint]
select = ["E", "F", "I", "B"]
ignore = ["E203", "E501"]  # Black 互換用推奨設定
```
ruff の動作テスト
```
uv run ruff check .
uv run ruff format .
```

## 5. Git 初回コミット
.gitignoreを作成
```
# Python-generated files
__pycache__/
*.py[oc]
*.pyo
*.pyd
*.so
*.egg-info/
build/
dist/
wheels/

# Virtual environments
.venv/

# Ruff cache
.ruff_cache/

# uv lock backups（将来的に生成されることがある）
uv.lock.bak

# VSCode
.vscode/
*.code-workspace

# Environment variables
.env
.env.*
*.env

# Logs
*.log

# pytest cache
.pytest_cache/

# Jupyter (もし使う場合)
.ipynb_checkpoints/

# macOS
.DS_Store

# Windows
Thumbs.db
ehthumbs.db

# MyPy cache（今後使う可能性が高い）
.mypy_cache/
```

Git初期化
```
git init
git add .
git commit -m "Initial project setup"
```
## 6. pre-commit の設定（自動 Lint/Format）
`.pre-commit-config.yaml` を作成
```
repos:
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.11.11
    hooks:
      - id: ruff-check
        args: [ --fix ]
      - id: ruff-format
```
Git フックをインストール
```
uv run pre-commit install
```
初回のみ全ファイルをチェック
```
uv run pre-commit run --all-files
```
## 7. スクリプトの実行（依存含む）
```
uv run main.py
```
## 8. パッケージ同期（環境再現用）
他環境でプロジェクトを再構築する場合：
```
uv sync
```
## 9. requirements.txt（必要なら）
```
uv pip freeze > requirements.txt
```
## 10. 依存関係ツリーの表示
```
uv tree
```

# プロジェクト構成例
```
my-project/
├── .ruff_cache/               # ruff のキャッシュ（Git ignore 推奨）
├── .venv/                     # uv が作る仮想環境（Git ignore）
│
├── .gitignore                 # Git で除外するファイル一覧
├── .pre-commit-config.yaml    # pre-commit の設定（自動 lint / format）
├── .python-version            # uv が使う Python のバージョン固定
├── uv.lock                    # uv の lock file（環境再現に使用）
│
├── pyproject.toml             # 依存関係と ruff 設定の中心
├── README.md                  # プロジェクト説明
│
└── main.py                    # 実行ファイル（今後 src/ に移してもOK）
```
