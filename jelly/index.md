# Jelly

esolang [Jelly](https://github.com/DennisMitchell/jellylanguage) (LICENSE: [MIT](https://github.com/DennisMitchell/jellylanguage/blob/master/LICENSE.txt)) の [wiki](https://github.com/DennisMitchell/jellylanguage/wiki) の要約

- ₀₁₂₊ はこのmd中では零項、単項、二項、マクロを表す注釈。プログラム中には含めない。

## index
- [index.md](https://github.com/akouryy/esolang-memo/blob/master/jelly/index.md) 本家wikiの要約
- [tips.md](https://github.com/akouryy/esolang-memo/blob/master/jelly/tips.md) 言語仕様を理解するつもりがない場合や時間がないとき用の細かい知見

## 関数(`link`)

- Jellyの関数は、既存の関数を[ポイントフリー](http://d.hatena.ne.jp/melpon/20111031/1320024473)に合成(`chain`: 連鎖)することで作成される。
- 合成のパターン(各関数の並び方)によって引数がどう各関数に与えられるかが定まる。
- 関数の引数の数は 0 (`niladic`: 零項), 1 (`monadic`: 単項), 2 (`dyadic`: 二項) のいずれかである。
  - ユーザー定義関数では定義時には項数は定まらず、呼び出し時に定まる。

## プログラムの構造

- 1行に1つ関数を定義する。最後の行がmain関数。
  - ゴルフではmain関数しかない場合が多いが、その場合でも下の連鎖の章は深く理解する必要がある。
- 関数を呼び出す際に引数の数を指定する(項数によって関数を呼び出す文字が異なる)。
- 関数は「1つ上/下の関数」や「n番目の関数」を表すマクロ(`quick`)で参照し、呼び出す。
  - [`¢`₊, `Ŀ`₊](https://github.com/DennisMitchell/jellylanguage/wiki/Quicks) など。

## リテラル

## 連鎖

ここがJellyの本質。

### 零項鎖 (`niladic chain`)

- `A B C ... X`₀ という連鎖は零項の文脈で評価されると、
  - `A₀` が零項なら単項の `B C ... X`₁ に `A₀` を適用する。
  - そうでないなら単項の `A B C ... X`₁ に数値 `0` を適用する。

### 単項鎖 (`monadic chain`)

- `A B C ... X`₁ という連鎖は単項の文脈で、
  - これが定鎖(`LCC`: leading constant chain)なら零項の文脈で評価する。
    - 定鎖とは、項数を並べた文字列が正規表現 `/^0(1|02|20)*$/` にマッチするような連鎖である。
  - そうでないなら引数を `a`(定数), aを初期値とする変数を `v` とおいて、左から順に次の評価を行う。
    - 残っている関数を左から `P,Q,R,…` としたとき、それらの項数を前方一致で判定し、以下の結果を `v` に代入する。
      - `220` に適合し、かつ `R,…` が定鎖のとき、`(v P₂ a) Q₂ R₀`。
      - `21` に適合するとき、`v P₂ Q₁(a)`。
      - `20` に適合するとき、`v P₂ Q₀`。
      - `02` に適合するとき、`P₀ Q₂ v`。
      - `2` に適合するとき、`v P₂ a`。
      - `1` に適合するとき、`P₁(v)`。
      - `0` に適合するとき、`P₀`。副作用として元の `v` を出力する。

### 二項鎖 (`dyadic chain`)

- `A B C ... X`₂ という連鎖は二項の文脈で、
  - 引数を `x`, `y` とおく。
  - 変数 `v` をとる。
  - 関数を左から `P,Q,R,…` としたとき、それらの項数を前方一致で判定し、以下の結果を `v` の初期値とする。
    - `222` に適合するとき、`x P₂ y`。
    - `1` に適合し、かつそれ以降が以降が定鎖の時、`P₁`。
    - それ以外のとき、`x`。
  - 左から順に次の評価を行う。
    - 残っている関数を左から `P,Q,R,…` としたとき、それらの項数を前方一致で判定し、以下の結果を `v` に代入する。
      - `220` に適合し、かつ `R,…` が定鎖のとき、`(v P₂ x) Q₂ R₀`。
      - `22` に適合するとき、`v P₂ (x Q₂ y)`。
      - `20` に適合するとき、`v P₂ Q₀`。
      - `02` に適合するとき、`P₀ Q₂ v`。
      - `2` に適合するとき、`v P₂ y`。
      - `1` に適合するとき、`P₁(v)`。
      - `0` に適合するとき、`P₀`。副作用として元の `v` を出力する。

## 連鎖のネスト

- `A /₂ B C /₀ D E F /₁ G` から `A (B C)₂ (D E F)₀ G₁` ができるイメージで、連鎖をグループ化して小連鎖(`sub-chain`)を作ることができる。
  - [`ø`, `ɓ`](https://github.com/DennisMitchell/jellylanguage/wiki/Syntax#other-syntax-characters) など。
  - TODO: `)` を理解する
- 連鎖の連鎖の連鎖(3重)は定義できない。別の関数として定義する。

### 関数合成

https://github.com/DennisMitchell/jellylanguage/wiki/Tutorial#62making-compound-links

- 直前の関数列から条件を満たす最小限の部分をまとめて、一つの関数と見なせるようにするマクロ。
- 上の連鎖ネストとは異なり、局所的な合成を達成できる。
