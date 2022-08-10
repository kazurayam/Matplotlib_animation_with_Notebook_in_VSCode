# Matplotlib FuncAnimation in Jupyter Notebook in Visual Studio Code

## 解決したい問題

[「ゼロから作るDeep Learning」斎藤康毅著 O'Reilly刊](https://www.oreilly.co.jp/books/9784873117584/)の「5.6 Affine/Softmaxレイヤの実装」を読んでいて引っかかった。そもそもAffine変換って何だっけ？Qiitaで"アフィン変換"を検索したら下記の記事を見つけた。

- [Qiita 完全に理解するアフィン変換 @koshain2](https://qiita.com/koshian2/items/c133e2e10c261b8646bf)

とてもためになる良い記事です。ところがAffine変換を学ぶ前に、僕の関心は脇道に逸れてしまった。この記事にこんなアニメーションが貼ってあった。

- ![サンプル](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.amazonaws.com%2F0%2F232088%2Fc78e7034-5baa-21ae-7fd0-a700ff4cd27b.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&w=1400&fit=max&s=90791f22bd00fc189485a39d7310e6cd)

このアニメーションをどうやって実装しているだろう？真似してみたい！と思った。記事にはPythonコードが掲載されていた。だからサンプルコードを写経すれば僕もすぐ真似できるだろうと思った。

しかしいざやってみるとPython環境を整えるのが面倒だった。というのも僕は個人的好みにより、下記のようなPython環境でアニメーションを動かしたかったから。

1. IDEとしてVisual Studio Codeを使いたい。
2. VSCodeの中でJupyter Notebookを使いたい。つまり名前が `*.ipynb` であるファイルを作って実行したい。
3. Notebookをエディタで開いた状態でpythonコードを選んでCtrl+Enterでrunすれば、Jupyter Server:Localがpythonコードを実行する、そしてNotebookの中でアニメーションが動くのが見られる、というようにしたい。
4. 作業プロジェクトのために固有のpython仮想環境を作りたい。pipenvを使って。
5. pipenvによる仮想環境に準備されたPythonインタプレタを使ってVSCodeの中のNotebookを動作させたい。つまり`"$ pipenv install opencv-python"`でインストールした`cv2`ライブラリを VSCodeの中のNotebookの中のpythonコードがimportできるようにしたい。

この条件を満足するためPythonとVSCodeをどのように設定したかを本記事でメモします。このメモは自分のためにです。きっとすぐ忘れるから。

## 解決方法

TODO

## 説明

TODO


