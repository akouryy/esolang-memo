# dc

[Esolang wiki](https://esolangs.org/wiki/Dc)  
[ちょっと古いかもしれないソースコード](https://github.com/fivepiece/gnu-bc/tree/master/dc)

* AtCoder では GNU 版が使われている(2020/6/10)。

* このページではスタックを追加順(下(底)→上の順)で表記している。

## 仕様

* [Esolang wiki](https://esolangs.org/wiki/Dc) にまとまっている。
* wikiにない機能:
  * `~` (divmod)
    * a b | `~` → a/b a%b
  * `R` (rotate)
    * a b c | `3R` → b c a
    * a b c d | `4R` → b c d a
      * このように、正整数 n に対しては n 番目の値を一番上に引っ張ってくる動作を示す。
    * a b c | `_3R` → c a b
    * a b c d | `_4R` → d a b c
      * このように、負整数 -n に対しては一番上の値を n 番目に埋める動作を示す。

## 条件分岐

* 正負:
  `【a:負のとき】【b:非負のとき】【スタックにゴミを残さない計算】vkp`
  * 負の平方根がpopと同値である(新たな値がスタックに載らない)ことを利用

* 条件分岐後すぐ出力:
  `【a:偽のとき】【b:真のとき】【スタックにゴミを残さない計算】【op:<=>】0rp`
    * 0 は未使用か数値が格納されているレジスタであれば違う名前でもいい。
  * 例: [abc164_b の提出](https://atcoder.jp/contests/abc164/submissions/12436783) `[No][Yes]?_3R1-r/*<0rp`
  * 真のとき、レジスタ 0 の値(未使用=0)を評価した結果(0)がスタックにプッシュされ(a b 0)、swap をかけた結果(a 0 b)の一番上 b を出力する。
  * 偽のとき、何もプッシュされず、swap をかけた結果(b a)の一番上 a を出力する。

* 絶対値(abs):
  `【値】d*v`
  * 二乗→平方根

* 大きい方(max):
  `【値x】sV【値y】dlV>V`
  * xが大きいならスタックは y x に、yが大きいならスタックは y になる
