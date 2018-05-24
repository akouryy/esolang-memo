# Jelly 知見

- より良い(短い)方法があれば教えてください。
- ₀₁₂₊ はこのmd中では零項、単項、二項、マクロを表す注釈であり、プログラム中に含める必要はありません。

## index
- [index.md](https://github.com/akouryy/esolang-memo/blob/master/jelly/index.md) 本家wikiの要約
- [tips.md](https://github.com/akouryy/esolang-memo/blob/master/jelly/tips.md) 言語仕様を理解するつもりがない場合や時間がないとき用の細かい知見

## デバッグしたい

(debug; pretty print; pp; output)

- `Ṙ`₁
- [index.md](https://github.com/akouryy/esolang-memo/blob/master/jelly/index.md) を読んでいないと分かりにくいが、特に二項関数の直後に置くと意図しない値を出力しうるので注意。

## 入力したい

(input; gets; getchar; toint; to_i; chomp; split; lines)

- 一文字読む: `ƈ`₀
- 一行読む: `ɠ`₀
- 一行読んでeval (Python 2の `input()`): `Ɠ`₀
- 全部読む: `ƈƈ¹Ð¿`₀₍₀₁₎₊
- 全部読んで行ごとの配列にする: `ƈƈ¹Ð¿Ỵ`₀₍₀₁₎₊₁
- 全部読んで行ごとの配列にして末尾の空行を消す: `ƈƈ¹Ð¿ỴṖ`₀₍₀₁₎₊₁₁

## 最後の余分な出力を消したい

(pop; ignore; discard; hide; disable; erase; remove; delete; extra; superfluous; unnecessary; last; end; trailing; output; write; print)

Jellyでは、main関数の評価結果が最後に出力されてしまう。プログラムの途中で出力命令を呼んでいた場合、この機能は迷惑。
しかしJellyはスタック型言語ではなく関数型言語なので、他の(一見)似た言語のように`pop`命令は存在しない。

- 途中ではなく最後に全て出力する。
  - 関数型言語であることを考えると最も自然。
  - `¡`₊ の代わりに `Ð¡`₊、`¿`₊ の代わりに `Ð¿`₊ を用いる。
  - 改行区切り(`Y`₁), 空白区切り(`K`₁), 空文字列区切り(`j“”`₂₀)を用いる。
- 最後は空文字列を出力するようにする。
  - 上の策がどうしてもうまくいかないときに使用。
  - プログラムの最後に `x0`₂₀ をつけると空文字列=空配列が得られる。
