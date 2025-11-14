# Gitチートシート

---
## Gitを設定する
### ユーザーネームとメールアドレスを登録する
```bash
git config --global user.name "Your Name"
git config --global user.email "yourname@email.com"
```

### メインのブランチを`main`に変更する
```bash
git config --global init.defaultBranch main
```

---
## Gitを開始する


### Gitを開始したいディレクトリに移動し、コミットを行う
```bash
git init
git add -A
git commit -m "Initial commit"
```

### originにURL先のリポジトリを紐づけ
```bash
git remote add origin URL
git remote -v
```

### originリポジトリにcommitをpush
```bash
git push -u origin main
```

### GitHubでREADME.mdを作っていた場合
pushを行う前にリモートのREADME.mdを取り込む
```bash
git pull origin main --rebase
```

---

## Git difftoolを使用する

difftoolを使用することでcommit前に変更点をビジュアルに確認できる
### 使用するツールを設定する
```bash
git config diff.tool ツール名（winmergeなど）
```

### ツールを使用するたびに確認を求められないようにする
```bash
git config --global difftool.prompt false
```

### ツールを使用する
```bash
git difftool file_name
```

---

## WSL2でGitを最新版にアップデートする

### パッケージのアップデートとアップグレード
```bash
sudo apt update && sudo apt upgrade -y
```

### 新しいGitのPPA(Personal Package Archive）をシステムに追加する
```bash
sudo add-apt-repository ppa:git-core/ppa
```

### パッケージをアップデート
```bash
sudo apt update
```

### PPAから最新のGitをインストール
```bash
sudo apt install git -y
```

### 最新のGitのバージョンを確認
```bash
git --version
```
### 依存関係により、不要になったパッケージを削除
```bash
sudo apt autoremove -y
```
---
## `git push`しようとしたときに、`The requested URL returned error: 403`と表示されたら

1. `.git/config`ファイルをvimなどで開く<br>

2. `[remote "origin"]`以下の`url=`で始まっている部分を探す<br>

3. `url = https://github.com/NakatsukaRyota/library.git`を`url = ssh://git@github.com/NakatsukaRyota/library.git`に変更して保存<br>

4. 再度`git push origin main`を実行する<br>
