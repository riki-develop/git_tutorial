# git_tutorial

## 初期化→Pushまで
git init  
git commit -m "first commit"  
git branch -M main  
git remote add origin https://github.com/〇〇〇〇  
git push -u origin main  

## ローカル(ワークツリー)とリポジトリの状態を確認
git status  

## 変更差分を確認
git diff  
※ローカル(ワークツリー)とステージングエリアの変更差分を確認  

git diff --staged  
※ステージングエリアとリポジトリの変更差分を確認  

## 削除
git rm  
※<ファイル名>＃ファイルごと削除  

git rm -r  
※<ディレクトリ名>＃ファイルごと削除  

git rm --cached  
※<ファイル名>＃ファイルを残したい時(リポジトリからだけ削除)  

## ファイルの移動を記録
git mv <旧ファイル> <新ファイル>  

## ファイルへの変更を取り消す
git checkout -- <ファイル名>  
git checkout -- <フォルダ名>  
### 全部取り消す
git checkout -- .  

## ステージした変更を取り消す
git reset HEAD <ファイル名>  
git reset HEAD <ファイル名>  
### 全部取り消す
git reset HEAD .  

## 直前の変更をやり直す
git commit --amend  
※注意点：リモートリポジトリにpushしたコミットはやり直しNG！  

## エイリアス作成：例
git config --global alias.co commit  
git config --global alias.st status  
git config --global alias.br branch  
git config --global alias.ch checkout  


# GitHub(リモート)とのやり取り  

## リモートを表示(確認)
git remote  
git remote -v  

## リモートリポジトリを追加
git remote add <リポジトリ名> <リポジトリURL>  
###  例：
git remote add bak https://github.com/riki-develop/git_tutorial_bak.git  

## gitから情報を取ってくる
git fetch <リモート名>  
git fetch origin  
### ブランチの内容を確認
git branch -a  
### ブランチの切り替え
git checkout remotes/origin/ブランチ名(main)  
### 元のブランチに戻る
git checkout main  
### リモートの情報をワークツリー（ローカル）に取り込む
git merge origin/main  

## リモートから情報を取得してmergeする
git pull <リモート名> <ブランチ名>  
git pull origin main  
↓  
### 上記、省略可
git pull  
↓  
### 下記、同じ意味合い
git fetch origin main  
git merge origin/main  

## ※プルの注意点
### ブランチが複数ある場合「現在のブランチ」に内容が上書きされるので「現在のブランチ」をしっかり確認した上でプルする必要がある。

## リモートの詳細情報を確認
git remote show <リモート名>  
### 例
git remote show origin  

## リモートを変更
git remote rename <旧リモート名> <新リモート名>  
### 例
git remote rename bak new_bak  
## リモートを削除
git remote rm <リモート名>  
### 例
git remote rm new_bak

# ブランチとマージ

## ブランとは
並行して複数機能を開発する仕組  
ブランチはコミットを指し示したポインタ  
HEADは「今自分がいるブランチ」を指し示したポインタ  
コミットしたらブランチが指し示すコミットファイルが変わる  
## ブランチの作成
git branch <ブランチ名>
### 例
git branch feature  
### ブランチの一覧を表示
git branch  
git branch -a  
### 現状の確認
git log --oneline --decorate

## ブランチの切り替え
git checkout <既存ブランチ名>  
### 例
git checkout feature  
### ブランチを新規作成して且つ切り替える
git checkout -b <ブランチ名>  

## マージとは
他人(別ブランチ)の変更内容を取り込む作業  
git merge <ブランチ名>  
git merge <リモート名/ブランチ名>  
### 例
git merge featuer  
git merge origin/main  
※作業中のブランチにマージ  
## マージには3種類ある
### Fast Foward：早送りになるマージ
ブランチが枝分かれしてなかった時はブランチのポインタを前に進めるだけ  
### Auto Merge：基本的なマージ
枝分かれして開発していた場合、マージコミットという新しいコミットを作る  

## コンフリクトについて
複数人で同じ箇所を変更➝ gitはどちらを優先すべきか判断できない  
### 解決方法
git status  
※状況確認  
↓  
対象ファイルの編集  
### コンフリクトを起きにくくする運用ルール
・複数人で同じファイルを変更しない  
・pullやmergeする前に変更中の状態をなくしておく(commitやstashしておく)  
・pullする時は、pullするブランチに「移動」してからpullする  
・コンフリクトしても慌てない  

## ブランチを変更
git branch -m <ブランチ名>  
### 例
git branch -m new_branch  
※自分が作業しているブランチの名前を変更  
## ブランチを削除
git branch -d <ブランチ名>  
### 例
git branch -d feature  
※mainにマージされていない変更が残っている場合は削除しない  
## 強制削除
git branch -D <ブランチ名>  

## ブランチを利用した開発の流れ
mainブランチをリリース用ブランチに、  
開発はトピックブランチを作成して進めるのが基本。  

## リモートブランチとは
リモートのブランチの状態へのポインタ  
リモートブランチは<リモート>/<ブランチ>で参照できる  
git fetch  
git branch -a  

# プルリクエストの流れ
git pull origin main  
※リモートから最新情報を持ってくる  
git checkout -b <ブランチ名>  
※ブランチを切る  
ファイル変更  
↓
git add <ファイル名>  
git commit -m ""  
git push origin <ブランチ名>  
↓
GitHub上でプルリクエスト作成  
諸々修正を完了させGitHub上でブランチをマージ  
不要になったブランチを削除  
↓
git checkout main  
※ブランチをメインに戻す  
git pull origin main  
※リモートの最新情報をローカルに反映  
git branch -d <不要ブランチ名>  
※不要になったブランチを削除  

# GitHub Flow の流れ
マスター→ブランチを切る  
↓  
開発→プルリク  
↓  
マスターへマージ→本番デプロイ  

## 実践
git branch  
※今いるブランチを確認  
git status  
※ファイルに変更が無いか確認  
git pull origin main  
※ファイルの状況を最新にする  
↓  
git checkout -b <ブランチ名>  
※ブランチを切る  
開発（作業）  
↓  
git add .  
git commit -m ""  
git push origin <ブランチ名>  
↓  
GitHubへ  
プルリク→修正→マスターへマージ→不要ブランチを削除  
↓  
ターミナルにて後片付け  
  
git checkout main  
※ブランチをマスターに戻す  
git pull origin main  
※リモートから最新情報を取得  
git branch -d <不要ブランチ名>  
※不要ブランチを削除  

## リベース
git rebase <ブランチ名>  
※別ブランチの内容を統合したい時に<マージと使い分ける>…  