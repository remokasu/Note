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
1. list, tupleを入力したとき文字列になる。<br>
    → ただし、この使い方は想定されていない。<br>
    プラグインで行列演算に対応するため、list形式は入力可能にしたほうがいい.<br>
    stack内のlistの要素にアクセスする方法も必要になってくるかもしれない.

<br>

2. 数値に代入できる
    ~~~ bash
    stacker:0> 5 = 10
    5 10
    Variable '5' assigned with value 10: 10
    stacker:1> 5 5 *
    [100]
    ~~~
    これは、内部では変数をすべて辞書型で管理しているため、`{5:10}`ということが発生している。<br>
    修正は簡単だけど、なんとなく面白いので放置しておく。

<br>

2. 入力をevalしているのはよろしくない．`evaluate_token_or_return_str()`関数を修正する．<br>
    いろいろ出来て便利だろ程度に思っていたけど，予想以上に副作用が大きい．<br>
    → `ast.literal_eval()`を使うことにした．本当は`eval()`で訳の分からない動作をすることを機能の一つとしていたかったけど，今後追加するかもしれない予約語がPython固有のものと被ると都合が悪いのでやめる．変なことをするならばプラグインで．


## plugins
本体とは別に更新していくスタイルで．<br>
(https://github.com/remokasu/stacker-plugins)

* 単位変換プラグインを作成．コマンドが少々使いにくい．
    ~~~ bash
    > m/s 10 km/h cu
    ~~~
    cu: convert unit

* 一部のシェルコマンドを実行できるプラグインを追加．<br>

    * `vim`と入力するとフリーズする問題を修正．インタラクティブなコマンドは打ち込めないようにするべきか．そもそもこれは電卓なのであり...(2023-04-29)

* 行列演算
    * stacker本体の入力と表示を改善しないと使い物にならない．<br>
    * matmulとdotの違いはなんだっけ


<hr>

## Traffic
* 2023 04/14 ~ 04/27
    * 146 Clones (Thank You! ❤️)
    * 43 Unique cloners (Thank You! ❤️❤️❤️)
    * 792 Views
    * 4 Unique visitors

<hr>

## その他
* `stacker`の名前は既に使用されており、不服ながら登録名は`pystacker`に。パッケージ名は`stacker`のまま。

* なんでRPNなのに代入構文だけ中置記法(例) `x = 2` にしてしまったんだろう...?<br>
そもそもRPNで代入とはいつたい?<br>
かといって、`2 x =`という記述はキモすぎるが.<br>
`2 x assign` とかにするか...?

* プラグインとかやっているうちに，ちょっと発散してきた．一度仕様を整理する．

* 結果表示，すこし改善したい.現状はlistオブジェクトをprint()してるだけなので．