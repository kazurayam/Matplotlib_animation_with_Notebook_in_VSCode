# Matplotlib FuncAnimation in Jupyter Notebook in Visual Studio Code

## 解決したい問題

[「ゼロから作るDeep Learning」斎藤康毅著 O'Reilly刊](https://www.oreilly.co.jp/books/9784873117584/)の「5.6 Affine/Softmaxレイヤの実装」を読んでいて引っかかった。そもそもAffine変換って何だっけ？Qiitaで"アフィン変換"を検索したら下記の記事を見つけた。

- [Qiita 完全に理解するアフィン変換 @koshain2](https://qiita.com/koshian2/items/c133e2e10c261b8646bf)

とてもためになる記事です。ところがAffine変換を学ぶ前に、僕の関心は脇道に逸れてしまった。というのもこの記事にこんなアニメーションが貼ってあったから。

 ![サンプル](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.amazonaws.com%2F0%2F232088%2Fc78e7034-5baa-21ae-7fd0-a700ff4cd27b.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&w=1400&fit=max&s=90791f22bd00fc189485a39d7310e6cd)

このアニメーションを真似してみたい！と思った。記事にはPythonコードが掲載されていた。だからサンプルコードを写経しさえすればよくて、僕もすぐ作れるだろうと思った。

しかしいざやってみると、Python環境を整えるのが意外に面倒だった。というのも僕は個人的好みにより、下記のような環境でアニメーションを動かしたかったから。

1. IDEとしてVisual Studio Code＋Python pluginを使いたい。
2. VSCodeの中でJupyter Notebookを使いたい。つまり名前が `*.ipynb` であるファイルを作って実行したい。
3. Notebookをエディタで開いた状態でpythonコードを選んでCtrl+Enterでrunする。Jupyter Server:Localがpythonコードを実行して、エディタの中でアニメーションが動くのが見られる、としたい。
4. ただし作業プロジェクトのために固有のpython仮想環境を作って使いたい。pipenvで。
5. `"$ pipenv install opencv-python"`でインストールした`cv2`ライブラリを VSCodeの中のNotebookの中のpythonコードがimportできるようにしたい。つまりpipenvで作った仮想環境の中のPythonインタプレタを使ってVSCodeの中のNotebookを動作させたい。

この条件を満足するような環境をどのように作ったかをここでメモします。このメモは自分のためにです。きっとすぐ忘れるから。

##　環境の準備

何はともあれmacOSにPython3をインストールした。具体的な手順は[こちら](https://github.com/kazurayam/MyPythonProjectTemplate#python%E5%87%A6%E7%90%86%E7%B3%BB%E3%82%92macos%E3%81%AB%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%81%99%E3%82%8B)を参照のこと。

pipenvをインストールしてPython仮想環境を作れるようにした。具体的な手順は[こちら](https://github.com/kazurayam/MyPythonProjectTemplate#pycliapp%E3%82%B5%E3%83%96%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E3%81%9F%E3%82%81%E3%81%ABpython%E4%BB%AE%E6%83%B3%E7%92%B0%E5%A2%83%E3%82%92%E4%BD%9C%E3%82%8B-----pipenv)を参照のこと。

プロジェクトのためにディレクトリを作った。

```
$ mkdir Matplotlib_FuncAnimation_In_Notebook_In_VSCode
$ cd Matplotlib_FuncAnimation_In_Notebook_In_VSCode
```

プロジェクトのためにPython仮想環境を作った。
```
$ pipenv --python 3
```

いま作ったPython仮想環境がどのパスにあるかを調べるには次のコマンドを実行する。

```
$ pipenv --venv
/Users/myname/.local/share/virtualenvs/Matplotlib_FuncAnimation_In_Notebook_In_VS-yX4ZY5tX
```

プロジェクトが依存するライブラリ群を仮想環境にインストールした。

```
$ pipenv install numpy
$ pipenv install matplotlib
$ pipenv install notebook
$ pipenv install opencv-python
```

[完全に理解するアフィン変換](https://qiita.com/koshian2/items/c133e2e10c261b8646bf)のサンプルコードを参考に、`animation_shift_x.ipynb`を書いた。

```

```

## 手こずった問題と解決方法

わたしが手こずった問題とその解決方法を列挙します

###

ipykernel



###　VSCodeの中のNotebookをどのPythonインタープレタで実行するかを指定したいが、どうやればいいのかわからなかった



VSCodeの中でNotebookすなわち　*.ipynbファイルを実行するのに、プロジェクト固有の仮想環境のPythonインタープレタを使いたい。しかしOSレベルでデフォルトになっているPythonインタープレタが参照されてしまう。

どのPythonインタープレタを使うか、ファイル毎に指定する必要がある

### VSCodeの中のNotebookの中で　アニメーションが動かなかった

ipymplマジックを宣言する必要がある


### Python仮想環境

[](https://github.com/kazurayam/MyPythonProjectTemplate#pycliapp%E3%82%B5%E3%83%96%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E3%81%9F%E3%82%81%E3%81%ABpython%E4%BB%AE%E6%83%B3%E7%92%B0%E5%A2%83%E3%82%92%E4%BD%9C%E3%82%8B-----pipenv)

## 説明

TODO


