# test1からの引き継ぎ
新規リポジトリを用意したところから
# 遠隔にオリジンとなるファイルを格納したリポジトリを作成
ローカルでipynbを（ipynb-py-convert test.py test2.ipynbして）作成（作成方法はなんでもいい）  
そのファイルをローカルからGITHUBの作成してあったこの新規リポジトリ(test２）に（masterとして）アップロード  
# ローカルにcloneして作業してpush
アップロードしたファイルのブランチ(test2_dev)をcreateする（これをローカルでいじりたい）    
ローカルにリポジトリをクローンする  
`git clone`  
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
アップロードしたファイルのブランチ(test2_dev)をcreateしたが、それは変更できなかった
# （脱線）VScodeでipynbをpyに変更して、ローカルリポジトリにいれて、gitにpushした。
変換はエクスプローラーのファイルで右クリックメニューで変換  
`git status`でUntracked filesとしてtest2.pyができていることを確認  
`git add test2.py`する。 
ローカルリポジトリにコミット`git commit -m pyconvertfile test2.py`  
リモートリポジトリに`git push origin master`する。  
githubのtest2リポジトリにtest2.pyがあることを確認
# Next リモートのマスターではなくブランチをローカルで修正して変更する。
ここまでローカルではマスターしかいじれていない。ところで、.ipynbファイルはGoogle colaboratoryでGithubから直接開いて編集できる。編集後にGithubにコピーを保存でき、開くときにmaster以外のブランチも選べるので、リモートのリポジトリ（この場合Github）のoriginをいじれる。リポジトリのファイルはJyupiternote形式で最初から作っておきたい。
ローカルのvscodeで同様のことができるようにする。
# git branchを使ってブランチを確認する。
`git branch`で現在ローカルにcloneしているブランチを知ることができる。やってみたら* masterしかない。アスタリスクはHEAD（現在いるブランチの意）  
`git branch -r`でGithubのリモートリポジトリのブランチを知ることができる。  
origin/HEAD -> origin/master  
origin/master  
origin/test2_dev  
アップロードしたファイルのブランチ(test2_dev)があることはわかる  
* これをローカルのVScodeにクローンする。--branch ブランチ名  
`git clone --branch test2_dev`  
でgithubのtest2リポジトリにあるtest2.pyをcloneしてローカルリポジトリを作れた。
フォルダが同じ名前なので紛らわしいが、先にcloneしたtest2のなかに、ネストしてtest2になっている。  
/test2$ ls  
README.md  test2  test2.ipynb  test2.py  
/test2$ git branch  
  *master  
/test2$ cd test2  
/test2$ git branch  
  *test2_dev  
それぞれマスターは異なるブランチとなっている。
`git push origin test2_dev`

# 補足
* ローカルリポジトリに複数のブランチをつくって、切り替えることもできる。  
`git checkout issue1`  
Switched to branch 'issue1'  
# メモ
# Google colaboratoryで編集後には、ローカルのVSCODEとは違うファイルができるので、ローカルで編集する際には、clone,add,commitしなおしてpushする。
# --branch ブランチ名でcloneしたファイルを編集後にpushできない。
error: src refspec master does not match any  
の解決は`git push origin branchname`, master以外のブランチのときにはブランチ名をclone --branch のブランチ名と一致させる。

