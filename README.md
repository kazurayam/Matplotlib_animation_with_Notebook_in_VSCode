# Matplotlib FuncAnimation in Jupyter Notebook in Visual Studio Code

## 解決したい問題

[「ゼロから作るDeep Learning」斎藤康毅著 O'Reilly刊](https://www.oreilly.co.jp/books/9784873117584/)の「5.6 Affine/Softmaxレイヤの実装」を読んでいて引っかかった。そもそもAffine変換って何だっけ？Qiitaで"アフィン変換"を検索したら下記の記事を見つけた。

- [Qiita 完全に理解するアフィン変換 @koshain2](https://qiita.com/koshian2/items/c133e2e10c261b8646bf)

とても良い記事でした。ためになる。ところが数学的解説を学ぶよりも以前に、私の関心は横道にそれてしまいました。というのもこの記事にこんな画像が貼ってあった。

- ![サンプル](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.amazonaws.com%2F0%2F232088%2F3a92a0a5-67fc-bdb7-57f8-0b30c0e48ad9.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&w=1400&fit=max&s=cb264195c0216e5146dbe90a17054d3b)

このアニメーション画像をどうやって実装したんだろう？僕も真似してみたい！と思った。記事にはOpenCVライブラリを呼び出して図形をAffine変換するPythonコードが掲載されていた。だから僕もすぐ真似できるだろうと思った。

しかしいざやってみるとPython環境を整えるのが面倒だった。というのも僕は下記のようなPython環境でアニメーションを動かしたかったから。

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


