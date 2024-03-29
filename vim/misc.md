# Vim

## 特殊文字対応表

| Vim上の表示 | キー入力 |
| ----------- | -------- |
| `<12>`      | `<cR>`   |
| `<1b>`      | `<c[>`   |
|             |          |





## その他のテクニック

* エラーが出るまで無限ループ: `qx•@xq@x`
  * 10回以下なら普通にやった方が得、100回以下なら同じ: `qx•q9@x`
  * `I•<ESC>u9@.`: 直前に^がある場合省略できて得
* 行ごとの多重ループ: `:%norm<cF>•<CR>ZZ`
* 置換
  * 区切り文字はほかの記号でもいい。例: `:s!foo!bar!g<CR>`, `:s[foo[bar<CR>`
  * 一回置換において、`:*s/•/•/<CR>` の最後の `/` はいらない
  * 一回置換において、置換後の文字列が空なら `:*s/•/<CR>` の2つ目の `/` もいらない
  * 毎行置換において、各行の置換が一個なら `:%s/•/•/g<CR>` の `g` はいらない (すると当然 `/` もいらない)
* 削除
  * 空行削除: `dd` → `J`
* ビジュアルモードで `r*` はカーソルの下に文字がないところには * を置かない
* `<cR>ρ` を `.` などで繰り返しても最初の `ρ` レジスタ の値が繰り返されるだけだが、`<cR><cO>"` を繰り返すと毎回その時点の `ρ` の値が使われる



## my cheatsheet

|      |      |      |
| ---- | ---- | ---- |
|      |      |      |
|      |      |      |
|      |      |      |

