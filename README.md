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




## エイリアス作成：例
git config --global alias.co commit  
git config --global alias.st status  
git config --global alias.br branch  
git config --global alias.ch checkout  