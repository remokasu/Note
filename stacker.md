[TOP](./README.md)


# Stackerの開発メモ

<hr>

## github
https://github.com/remokasu/stacker

<hr>

## PyPI
https://pypi.org/project/pystacker/

<hr>

## 予定
- ~~プラグイン機能の追加~~(2023-04/22 完了)
- テストケース

<hr>

## バグ
1. (value)と入力したとき
    ~~~ bash
    stacker 0> (4)
    [(4+0j)]
    ~~~

<br>

2. list, tupleを入力したとき文字列になる。<br>
    → ただし、この使い方は想定されていない。<br>
    プラグインで行列演算に対応するため、list形式は入力可能にしたほうがいい.<br>
    stack内のlistの要素にアクセスする方法も必要になってくるかもしれない.

<br>

3. 数値に代入できる
    ~~~ bash
    stacker:0> 5 = 10
    5 10
    Variable '5' assigned with value 10: 10
    stacker:1> 5 5 *
    [100]
    ~~~
    これは、内部では変数をすべて辞書型で管理しているため、`{5:10}`ということが発生している。<br>
    修正は簡単だけど、なんとなく面白いので放置しておく。


<hr>

## plugins
* 単位変換プラグインを作成．コマンドが少々使いにくい．
    ~~~ bash
    > m/s 10 km/h
    ~~~
* 一部のシェルコマンドを実行できるプラグインを追加．<br>
何を目指しているのやら．


## その他
* `stacker`の名前は既に使用されており、不服ながら登録名は`pystacker`に。パッケージ名は`stacker`のまま。

* なんでRPNなのに代入構文だけ中置記法(例) `x = 2` にしてしまったんだろう...?<br>
そもそもRPNで代入とはいつたい?<br>
かといって、`2 x =`という記述はキモすぎるが.<br>
`2 x assign` とかにするか...?