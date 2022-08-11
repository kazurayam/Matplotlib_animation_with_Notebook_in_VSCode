# Matplotlibでアニメーションする --- Notebookで, Visual Studio Codeの中で

## 解決したい問題

[「ゼロから作るDeep Learning」斎藤康毅著 O'Reilly刊](https://www.oreilly.co.jp/books/9784873117584/)の「5.6 Affine/Softmaxレイヤの実装」を読んでいて引っかかった。そもそもAffine変換って何だっけ？Qiitaで"アフィン変換"を検索したら下記の記事を見つけた。

- [Qiita 完全に理解するアフィン変換 @koshain2](https://qiita.com/koshian2/items/c133e2e10c261b8646bf)

とてもためになりそうな記事だが、Affine変換を学ぶ前に僕の関心は脇道に逸れてしまった。というのも、この記事に次のようなアニメーションが貼ってあったから。

 ![shift-x](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.amazonaws.com%2F0%2F232088%2Fc78e7034-5baa-21ae-7fd0-a700ff4cd27b.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&w=1400&fit=max&s=90791f22bd00fc189485a39d7310e6cd)

このアニメーションをどうやって作るのか、作り方を知りたい！と思った。記事にPythonコードが掲載されていたからそれを写経しさえすればすぐ作れそうだった。ただしわたしは自分好みのPython環境でアニメーションを動かしたいと思った。すなわち

1. IDEとして[Visual Studio Code](https://code.visualstudio.com/)を使いたい。もちろん[Python for VSCode](https://code.visualstudio.com/docs/languages/python)を入れて。
2. VSCodeの中で [Notebook](https://code.visualstudio.com/docs/datascience/jupyter-notebooks) すなわちファイル名が `*.ipynb` であるファイルをエディタで作って実行したい。
3. Notebookをエディタで開き、pythonコードを選んで Ctrl+Enter で run する。するとJupyter Server:Localがpythonコードを実行して、その結果としてアニメーションがNotebookの中で動く。こういう操作をしたい。
4. ただし作業プロジェクトのために固有のpython仮想環境を作って使いたい。 [pipenv](https://pypi.org/project/pipenv/) で。具体例を挙げるならば `"$ pipenv install opencv-python"` でインストールした [`cv2`](https://pypi.org/project/opencv-python/) ライブラリを VSCodeの中のNotebookの中のpythonコードがimportできるようにしたい。そのためにはpipenvで作った仮想環境の中のPythonインタプレタを使ってVSCodeの中のpythonコードを実行することが必要である。

試行錯誤したあげく望ましい実行環境を構築することができた。どのように環境を作ったか、ここに自分のためにメモします。

わたしが使っているOSはmacOS v12.3です。

##　準備1 pipenv

何はともあれmacOSにPython3をインストールした。具体的な手順は[こちら](https://github.com/kazurayam/MyPythonProjectTemplate#python%E5%87%A6%E7%90%86%E7%B3%BB%E3%82%92macos%E3%81%AB%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%81%99%E3%82%8B)を参照のこと。

pipenvをインストールした。Python仮想環境を作れるように。具体的な手順は[こちら](https://github.com/kazurayam/MyPythonProjectTemplate#pycliapp%E3%82%B5%E3%83%96%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E3%81%9F%E3%82%81%E3%81%ABpython%E4%BB%AE%E6%83%B3%E7%92%B0%E5%A2%83%E3%82%92%E4%BD%9C%E3%82%8B-----pipenv)を参照のこと。

## 準備2 本プロジェクトのためにディレクトリと仮想環境を作った

```
$ mkdir Matplotlib_animation_with_Notebook_in_VSCode
$ cd Matplotlib_animation_with_Notebook_in_VSCode
$ export PRJDIR=$(pwd)
```

以下でプロジェクトのディレクトリを示す必要がある場合、文を短くするため`$PRJDIR`と記すことにする。

本プロジェクトのためにPython仮想環境を作った。

```
$ cd $PRJDIR
$ pipenv --python 3
Creating a virtualenv for this project...
Pipfile: /Users/kazurayam/github/Matplotlib_animation_with_Notebook_in_VSCode/Pipfile
Using /usr/local/bin/python3.9 (3.9.13) to create virtualenv...
⠋ Creating virtual environment...

✔ Successfully created virtual environment!
Virtualenv location: /Users/kazurayam/.local/share/virtualenvs/Matplotlib_animation_with_Notebook_in_VSCo-zSMskZBS
```

上記コマンドによってPython仮想環境が作られるが、それがどのパスにあるかを調べるには次のコマンドを実行する。

```
$ pipenv --venv
/Users/kazurayam/.local/share/virtualenvs/Matplotlib_animation_with_Notebook_in_VSCo-zSMskZBS
```

本プロジェクトが依存するライブラリ群を仮想環境にインストールした。

```
$ cd $PRJDIR
$ pipenv install numpy
$ pipenv install matplotlib
$ pipenv install notebook
$ pipenv install opencv-python
```

どれも大きいライブラリなので数分かかった。

## 準備3 どのPythonインタープレタが使われたかを確認するためのスクリプト print_sys.py

[`print_sys.py`](https://github.com/kazurayam/Matplotlib_animation_with_Notebook_in_VSCode/blob/master/print_sys.py)と[`print_sys.ipynb`](https://github.com/kazurayam/Matplotlib_animation_with_Notebook_in_VSCode/blob/master/print_sys.ipynb)を書いた。中身はたった2行のpythonコードである。

```
import sys
print(sys.executable)
```

`sys.executable`はpythonコードを実行するのに使われているPythonインタープレタのファイルパスを示す。

## Step1 マシンのデフォルトのPython環境でどう動くか

素朴なやり方。コマンドラインで`print_sys.py`を実行してみた。

```
$ cd $PRJDIR
$ python print_sys.py
/Users/kazurayam/.pyenv/versions/anaconda3-4.4.0/bin/python
```

### Ste2 プロジェクト専用のPython仮想環境でどう動くか

pipenv runを介して`print_sys.py`を実行してみた。

```
$ cd $PRJDIR
$ pipenv run python print_sys.py
/Users/kazurayam/.local/share/virtualenvs/Matplotlib_animation_with_Notebook_in_VSCo-zSMskZBS/bin/python
```

一番目で使われたPythonインタープレタと二番目のPythonインタープレタのパスが違う。一番目のパスは仮想環境ではない。二番目のパスがこのプロジェクトのために準備した仮想環境の中のPythonインタープレタである。


### Step3 Jupyterでどう動くか

コマンドラインでJupyterを起動した。

```
$ cd PRJDIR
$ jupyter notebook
```

そのあとJupyterの中で`print_sys.ipynb`をCtrl+Enterして実行した。

![jupyter_print_sys](./docs/images/jupyter_print_sys.png)

一番目の検証と同じパスが表示された。これはわたしの予想と一致する。

### Step4 Jupyter+仮想環境でどう動くか

コマンドラインでpipenv runを介してJupyterを起動した。

```
$ cd PRJDIR
$ pipenv run jupyter notebook
```

そのあとJupyterの中で`print_sys.ipynb`をCtrl＋Enterで実行した。

![jupyter_pipenv_run](./docs/images/jupyter_pipenv_run.png)

あれれ？Step2と同じく仮想環境のPythonインタープレタのパスが表示されるだろうと予想していたが、そうはならなかった。Step1と同じパスが表示された。なぜこう動作したのか？コマンドラインからJupyterを起動するときにプロジェクト固有の仮想環境の中のPythonインタープレタを使いたい時、どこをどうすべきなのか、わたしはまだわかっていない。きっとどこかに設定とかコマンドラインのパラメータとかがあるのだろうが、わたしは知らない。

>本記事が目標とするのはVSCodeの中でNotebookを動かすことです。Jupyterの中でNotebookを動かす場合のことは構わないことにします。

### Step5 VSCode+Notebook -> ipykernelが必要

デスクトップアイコンをダブルクリックしてVSCodeを起動し、その中でNotebook `print_sys.ipynb` を開いた。pythonコードを実行してみた。

![VSCode_print_sys_out_of_venv](docs/images/VSCode_print_sys_out_of_venv.png)

上のスクリーリーンショットの中でAと印した箇所を見てほしい。一番目の検証と同じPythonインタープレタのパスが表示されている。これは本プロジェクトのための仮想環境ではなくて、わたしのマシンのデフォルトになっているPythonインタープレタのパスだ。

Bと印した箇所を見てほしい。`import cv2`がエラーになっている。私のマシンのデフォルトになっているPython実行環境にopencv-pythonをインストールしていないから、エラーになっているのだ。

VSCodeでNotebook `print_sys.ipynb` を開いたとき、マシンのデフォルトのPythonインタープレタではなく、このプロジェクト専用の仮想環境のなかのPythonインタープレタを使いたい。そのことをどうやってVSCodeに指図すればいいのだろうか？ーーーあちこちググった。あげく下記の1行を見つけた。

https://code.visualstudio.com/docs/datascience/jupyter-notebooks

>Next, select a kernel using the kernel picker in the top right.

Notebookを開いた画面の右上にkernel pickerがある、これをクリックせよ、といっている。


クリックしてみると、選択可能なPythonインタープレタのパス候補が表示された。その中にこのプロジェクト専用の仮想環境の中のPythonインタープレタ（その中にopencv-pythonがインストール済みである）も列挙されていた。

![VSCode_print_sys_specify_kernel](docs/images/VSCode_print_sys_specify_kernel.png)

候補リストの中からプロジェクト専用の仮想環境を選んだ。そうしたら警告ダイアログが表示された。

![VSCode_ipykernel_is_required](docs/images/VSCode_ipykernel_is_required.png)

```
Running cells with 'Python 3.9.13 ('Matplotlib_animation_with_Notebook_in_VSCo-zSMskZBS')' requires ipykernel package.
Run the following command to install 'ipykernel' into the Python environment.
Command: '/Users/kazurayam/.local/share/virtualenvs/Matplotlib_animation_with_Notebook_in_VSCo-zSMskZBS/bin/python -m pip install ipykernel -U --force-reinstall'
```

[ipykernel](https://pypi.org/project/ipykernel/)パッケージが必要だからインストールしなさいと警告している。

そこでメッセージに表示された通りのコマンドを実行して、プロジェクト専用の仮想環境にipykernelをインストールした。

```
$ cd $PRJDIR
$ /Users/kazurayam/.local/share/virtualenvs/Matplotlib_animation_with_Notebook_in_VSCo-zSMskZBS/bin/python -m pip install ipykernel -U --force-reinstall
```

プロジェクト専用のPython仮想環境にipykernelがインストールされた。VSCodeの中でNotebookを開き、仮想環境のPythonインタープレタを指定するとipykernelが動いて、Notebookのpythonコードを実行できるようになった。仮想環境にインストール済みの他のパッケージ（numpyやcv2）もimportできるようになった。

![cv2 imported](docs/images/VSCode_ipykernel_cv2_installed.png)

### Step6 VSCode+Notebook アニメーションをGIFファイルに保存した

[]()

### Step7

### Step8

### VSCodeの中のNotebookの中で　アニメーションが動かなかった

ipymplマジックを宣言する必要がある


### Python仮想環境

[](https://github.com/kazurayam/MyPythonProjectTemplate#pycliapp%E3%82%B5%E3%83%96%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E3%81%9F%E3%82%81%E3%81%ABpython%E4%BB%AE%E6%83%B3%E7%92%B0%E5%A2%83%E3%82%92%E4%BD%9C%E3%82%8B-----pipenv)

## 説明

TODO


