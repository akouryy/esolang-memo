# テンプレ短縮法

## 移動

| 行\列        | 先頭 | 非空先頭                  | 現在                   | 非空末尾 | 末尾  |
| ------------ | ---- | ------------------------- | ---------------------- | -------- | ----- |
| **1**        |      | `gg`; cf.`{`; cf.画面上端 |                        |          |       |
| **2**        |      | `:2<CR>`                  |                        |          |       |
|              |      |                           |                        |          |       |
| **現在-1**   |      | `-`                       |                        |          |       |
| **現在**     | `0`  | `^`, `_`                  |                        | `$`      | `g_`  |
| **現在+1**   |      | `+`                       |                        | `2$`     | `2g_` |
| **現在+4**   |      |                           | (現在=画面上端) `<cE>` |          |       |
|              |      |                           |                        |          |       |
| **画面上端** |      | `H`                       |                        |          |       |
| **画面中央** |      | `M`                       |                        |          |       |
| **画面下端** |      | `L`                       |                        |          |       |
|              |      |                           |                        |          |       |
| **最後-1**   |      | `G-`                      |                        |          |       |
| **最後**     |      | `G`                       |                        | cf. `}`  |       |

## 2文字→1文字

* `$`
  * `$a` → `A`
* `^`
  * `^i` → `I`
* `c`
  * `c$` → `C`
  * `cc` → `S`

* `d`
  * `d$` → `D`
  * `dd` → `J` (空行)
  * `dh` → `X`
  * `dl` → `x`
* `g`
  * `gg` → `H` (スクロール上端)
* `j`
  * `j^` → `+`
* `k`
  * `k^` → `-`

* `y`
  * `yy` → `Y`
