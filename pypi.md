[TOP](./README.md)


PyPI登録トライ時のメモ

参考：https://zenn.dev/sikkim/articles/490f4043230b5a

## ソースコード配布物を作成

~~~bash
python setup.py sdist
~~~
--formats オプションで圧縮ファイル形式を指定できるらしい


* chatGPT

このコマンドは、Pythonのプロジェクトをソースディストリビューション（source distribution）形式でパッケージングするために使用されます。ソースディストリビューションとは、ソースコードや必要なリソース、ドキュメントなどを含むアーカイブ形式のパッケージであり、開発者やユーザーがプロジェクトをビルド・インストールするために使用することができます。

setup.pyは、Pythonパッケージングのためのメタデータを含むファイルであり、sdistは、ソースディストリビューションを作成するsetuptoolsのコマンドです。このコマンドを実行すると、プロジェクトのソースコードや必要なリソース、ドキュメントなどが含まれるアーカイブ形式のパッケージが作成され、後で開発者やユーザーがプロジェクトをビルド・インストールしたり、配布したりできます。


## Wheelパッケージをビルド

~~~bash
python setup.py bdist_wheel
~~~

* chatGPT

このコマンドは、Pythonのプロジェクトをwheel形式でパッケージングするために使用されます。wheelは、Pythonのパッケージングフォーマットであり、pipを使用してPythonパッケージをインストールする際に使用されます。

setup.pyは、Pythonパッケージングのためのメタデータを含むファイルであり、bdist_wheelは、Wheel形式のバイナリパッケージを作成するsetuptoolsのコマンドです。このコマンドを実行すると、プロジェクトの依存関係やコードなどが含まれるWheelファイルが作成され、後でpipを使用して配布したり、別の環境にインストールしたりできます。

~~~bash
twine check dist/*
~~~

## テスト環境にアップロード
~~~bash
twine upload --repository testpypi dist/*
~~~

## 本番環境にアップロード
~~~bash
twine upload --repository pypi dist/*
~~~

テスト環境アップに失敗しても本番環境ではアップできる場合あり。<br>
なぜだろう？