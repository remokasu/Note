[TOP](./README.md)


# PyPI登録トライ時のメモ

参考：https://zenn.dev/sikkim/articles/490f4043230b5a

## ソースコード配布物を作成

~~~bash
python setup.py sdist
~~~
--formats オプションで圧縮ファイル形式を指定できるらしい


* chatGPT

このコマンドは、Pythonのプロジェクトをソースディストリビューション（source distribution）形式でパッケージングするために使用されます。ソースディストリビューションとは、ソースコードや必要なリソース、ドキュメントなどを含むアーカイブ形式のパッケージであり、開発者やユーザーがプロジェクトをビルド・インストールするために使用することができます。

setup.pyは、Pythonパッケージングのためのメタデータを含むファイルであり、sdistは、ソースディストリビューションを作成するsetuptoolsのコマンドです。このコマンドを実行すると、プロジェクトのソースコードや必要なリソース、ドキュメントなどが含まれるアーカイブ形式のパッケージが作成され、後で開発者やユーザーがプロジェクトをビルド・インストールしたり、配布したりできます。

<br>
<hr>

## Wheelパッケージをビルド

~~~bash
python setup.py bdist_wheel
~~~

* chatGPT

このコマンドは、Pythonのプロジェクトをwheel形式でパッケージングするために使用されます。wheelは、Pythonのパッケージングフォーマットであり、pipを使用してPythonパッケージをインストールする際に使用されます。

setup.pyは、Pythonパッケージングのためのメタデータを含むファイルであり、bdist_wheelは、Wheel形式のバイナリパッケージを作成するsetuptoolsのコマンドです。このコマンドを実行すると、プロジェクトの依存関係やコードなどが含まれるWheelファイルが作成され、後でpipを使用して配布したり、別の環境にインストールしたりできます。


<br>
<hr>

## チェック
~~~bash
twine check dist/*
~~~

* chatGPT

Twineプロジェクトのビルド済みファイル（.htmlファイル）をチェックするために使用されます。

具体的には、 twine check コマンドは、指定したパターン（dist/*）に一致するファイルを見つけ、それらのファイルをTwineの適切なバージョンで作成されたものであるかどうかを確認します。これには、ファイル内で使用されているTwineの要素が有効であるか、文法的に正しいかどうか、およびプロジェクト内で定義されたすべてのパスが正しいかどうかを確認することが含まれます。

このコマンドを使用することで、Twineプロジェクトのビルドが正しく機能することを確認でき、エラーを修正することができます。


<br>
<hr>

## テスト環境にアップロード
~~~bash
twine upload --repository testpypi dist/*
~~~

<br>
<hr>

## 本番環境にアップロード
~~~bash
twine upload --repository pypi dist/*
~~~

テスト環境アップに失敗しても本番環境ではアップできる場合あり。<br>
なぜだろう？

<br>
<hr>

## バージョンの表記、バージョンアップの簡易ガイドライン
例）Version 1.0.0<br>
この数値は、左から メジャーバージョン.マイナーバージョン.パッチバージョン

- メジャーバージョン
重要な変更や大規模なアップデートがある場合に上昇。過去のバージョンとの互換性がないことが多い。

- マイナーバージョン
小さな機能追加や改良が行われた場合に上昇。通常、過去のバージョンとの互換性がある。

- パッチバージョン
バグ修正などの小さな変更が行われた場合に上昇。通常、過去のバージョンとの互換性がある。

<br>
<hr>

## setup.py
Stackerのsetup.pyはこんな感じで、見様見真似。正直どのような書き方が最適なのかは分からない。

### 重要
* version が以前PyPIに登録したものと同じであるとき、PyPIアップロードに失敗するっぽい
* README.mdの内容をPyPIのパッケージのトップページに表示させたいとき、`long_description_content_type='text/markdown'` を設定しないと内容が表示されない。つまりMarkdown形式ファイルの内容をトップに表示させるなら必須
* モジュール内で、他のディレクトリを参照するときは `package_data={'stacker': ['data/*', 'plugins/*']}` のように、モジュールからの相対パスで指定する。<br>
モジュール本体でも変更必要。→ `Stacker`のプログラムをみて思い出せ
* 起動方法 <br>
`python -m <package_name>` ではなく、ターミナルで`<package_name>`だけで起動させるには`entry_points`を指定する

~~~python
from codecs import open
from os import path

from setuptools import find_packages, setup

here = path.abspath(path.dirname(__file__))

with open('README.md', 'r', encoding='utf-8') as f:
    long_description = f.read()

with open('LICENSE', 'r', encoding='utf-8') as f:
    license = f.read()


with open('requirements.txt', 'r', encoding='utf-8') as f:
    install_requires = f.read()

setup(
    author='remokasu',
    name="pystacker",
    version="1.2.0",
    license=license,
    url='https://github.com/remokasu/stacker',
    install_requires=install_requires,
    packages=find_packages(),
    package_data={'stacker': ['data/*', 'plugins/*']},
    description='Stacker: RPN Calculator in Python',
    long_description=long_description,
    long_description_content_type='text/markdown',
    keywords='reverse-polish-calculator rpn terminal-app',
    entry_points={
        "console_scripts": [
            "stacker = stacker.stacker:main",
        ],
    },
)
~~~


<br>
<hr>

## その他
PyPIの読み方、僕は`パイパイ`派なんですけど、世間的にはいろいろ読み方の派閥があるっぽい。