# test1からの引き継ぎ
新規リポジトリを用意したところから
# 遠隔にオリジンとなるファイルを格納したリポジトリを作成
ローカルでipynbを（ipynb-py-convert test.py test2.ipynbして）作成（作成方法はなんでもいい）  
そのファイルをローカルからGITHUBの作成してあったこの新規リポジトリ(test２）に（masterとして）アップロード  
# ローカルにcloneして作業してpush
アップロードしたファイルのブランチ(test2_dev)をcreateする  
`git clone git@github.com:kuni923/test2.git`  
ローカルのワークスペースにtest2フォルダができる  
`git add test2.ipynb`  
確認`git status`  
エディターで開く`code test2.ipynb`      
ローカルのVSCODEで修正（1行追加）最初うまく開けない    
確認`git status`　　  
修正ファイルを`git add test2.ipynb`　　  
確認`git status`  
commitする`git commit -m Message test2.ipynb`  　　  
とりあえず`git status`  
リモートリポジトリを確認`git remote -v`  
pushする`git push origin master`    　      
cloneしたマスターをpushして更新した。　　
