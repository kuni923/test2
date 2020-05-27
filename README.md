# test1からの引き継ぎで新規のリモートリポジトリを用意した（test2）ところから
* GitHubでリポジトリを作成した場合、それは リモート リポジトリとなります。 リポジトリをクローンして、コンピュータにローカルのコピーを作成し、ローカルとリモートの間で同期できます。
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
* アップロードしたファイルのブランチ(test2_dev)をcreateしたが、それは変更できなかった
# リモートのマスター以外のブランチをローカルで修正して変更する。
ここまでローカルではマスターしかいじれていない。ところで、.ipynbファイルはGoogle colaboratoryでGithubから直接開いて編集できる。編集後にGithubにコピーを保存でき、開くときにmaster以外のブランチも選べるので、リモートのリポジトリ（この場合Github）のoriginをいじれる（リポジトリのファイルはJyupiternote形式で最初から作っておく必要がある）。  
* ローカルのvscodeで同様のことができるようにする。
# git branchを使ってブランチを確認する。
`git branch`で現在ローカルにcloneしているブランチを知ることができる。やってみたら* masterしかない。アスタリスクはHEAD（現在いるブランチの意）  
`git branch -r`でGithubのリモートリポジトリのブランチを知ることができる。  
origin/HEAD -> origin/master  
origin/master  
origin/test2_dev  
アップロードしたファイルのブランチ(test2_dev)があることはわかる  
# マスター以外のブランチをローカルのVScodeにクローンする。--branch ブランチ名  
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
* それぞれマスターは異なるブランチとなっているためpushは注意   
`git push origin test2_dev`

# MISC
* VScodeでipynbをpyに変更して、ローカルリポジトリにいれて、gitにpushした。  
変換はエクスプローラーのファイルで右クリックメニューで変換  
`git status`でUntracked filesとしてtest2.pyができていることを確認  
`git add test2.py`する。 
ローカルリポジトリにコミット`git commit -m pyconvertfile test2.py`  
リモートリポジトリに`git push origin master`する。  
githubのtest2リポジトリにtest2.pyがあることを確認  
* ローカルリポジトリに複数のブランチをつくって、切り替えることもできる。  
`git checkout issue1`  
Switched to branch 'issue1'  
* --branch ブランチ名でcloneしたファイルを編集後にpushできない。  
error: src refspec master does not match any  
の解決は`git push origin branchname`, master以外のブランチのときにはブランチ名をclone --branch のブランチ名と一致させる。

# `Pull`を調べる。
* `clone`, `add`, `commit`, `push`, `branch`, `status`を理解した。  
例えば、Google colaboratoryで編集後にpushすると、ローカルのVSCODEのリポジトリとGitHubのリポジトリのファイルのバージョンが異なる。ローカルで編集する際に、Githubから最新のリポジトリをclone,add,commitしなおして編集後にpushしてリモートを更新しているが、大変つらい。  
ローカルリポジトリに新しいファイルを作って、pushしようとしたらpushできなかった。pullを使えとエラーメッセージに書いてあった。  
* `git pull origin master`でリモートのmaster（オリジン）とローカルリポジトリのmasterが同期された。  
その後に、さきほどのpush origin masterをしたら通った。

# Pushでエラーが出る状況をつくって、`pull`を練習する。
* Google colaboratoryでGithubのtest2.ipynbを開いて編集後、Githubにコピーを保存でGithubに変更を反映した。その時点で、Githubからcloneしているローカルリポジトリの`git status`をみると、リモートでの変更は知らないことを確認。その後、ローカルでローカルのファイルを変更して、再度`git status`すると、ローカルでの変更を検知している。  
Changes not staged for commit:  
  (use "git add <file>..." to update what will be committed)  
  (use "git checkout -- <file>..." to discard changes in working directory)    
        modified:   test2.ipynb  
no changes added to commit (use "git add" and/or "git commit -a")  
これを`add`, `commit -m`してローカルリポジトリを更新、その後`push`する。リモートとローカルの同期が取れていないので、pushでエラーがでる状況になった。  
`git pull origin master`の結果  
 Unmerged paths:  
  (use "git add <file>..." to mark resolution)  
        both modified:   test2.ipynb  
* `master`以外の`branch`を使えていないのが問題
 
# `master`しか使いこなせないうちは、最初に`pull origin master`でリモートとローカルを同期してから、ファイルの編集を始める。そうしないと、同期が困難。

# `master`以外の`branch`を理解する。
* `git branh -a`でリモートを含めてすべてのブランチを見ることができる。  
* `git checkout [<branch>]`  
To prepare for working on <branch>, switch to it by updating the index and the files in the working tree, and by pointing HEAD at the branch. Local modifications to the files in the working tree are kept, so that they can be committed to the <branch>.  
* If <branch> is not found but there does exist a tracking branch in exactly one remote (call it <remote>) with a matching name and --no-guess is not specified, treat as equivalent to  
`$ git checkout -b <branch> --track <remote>/<branch>`を理解する。    
 
# `git checkout`
単純にブランチを切り替える
* `git branch -a`  
*master  
remotes/origin/HEAD -> origin/master  
remotes/origin/master  
remotes/origin/test2_dev  
* `git checkout -b test2_dev --track remotes/origin/test2_dev`で既存ブランチをリモートまでtrackしてcheckout. remotes/はなくても大丈夫だと思う。    
Branch test2_dev set up to track remote branch test2_dev from origin.  
Switched to a new branch 'test2_dev'
* `git status`で確認すると切り替わっている。  
On branch test2_dev  
Your branch is up-to-date with 'origin/test2_dev'.  
nothing to commit, working tree clean  
* `git branch -a`  
master  
*test2_dev  
remotes/origin/HEAD -> origin/master  
remotes/origin/master  
remotes/origin/test2_dev  

# `git checkout -b` 
* -b <new_branch>  
Create a new branch named <new_branch> and start it at <start_point>; see git-branch[1] for details.  
* -B <new_branch>  
Creates the branch <new_branch> and start it at <start_point>; if it already exists, then reset it to <start_point>. This is equivalent to running "git branch" with "-f"; see git-branch[1] for details.

#ブランチを新規に作る
* ローカルのブランチから新規ブランチを作成する方法  
*ブランチを作りたいgitのディレクトリに入る   
`cd ディレクトリパス`  
*ブランチの一覧を確認    
`git branch -a`  
*ブランチを作る元のブランチに切り替える  
`git checkout master`ここではマスターに切り替えた。  
*新規ブランチを作成  
`git checkout -b 作成するブランチ名`      
*ブランチの一覧を確認    
`git branch -a`  

# ブランチのリモートへの登録
`git push -u origin 作成したブランチ名`  
eg. 
`git checkout -b test2_dev_test`  
`git push -u origin test2_dev_test`  
`git status -a`  
 master  
 test2_dev  
*test2_dev_test  
 remotes/origin/HEAD -> origin/master  
 remotes/origin/master  
 remotes/origin/test2_dev  
 remotes/origin/test2_dev_test  
* originやmasterはブランチ名のことなのか？ファイル名を書くのはだめなのか？　ー＞　ブランチ名を書く。
