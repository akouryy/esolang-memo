|fn|`[]`|`(x →)`|
|-|-|-|
| `pure`<sup>A</sup> <br> `return`<sup>M</sup> | `(:[])` <br> `\a → [a]` | `const` <br> `\a x → a` |
| `a → m a` | `a → [a]` | `a → x → a` |
| `>>=`<sup>M</sup> | `concatMap` | `\f g x → g (f x) x` |
| `m a → (a → m b) → m b` | `[a] → (a → [b]) → [b]` | `(x → a) → (a → x → b) → x → b` |
| `=<<`<sup>M</sup> <br> `flip (>>=)`<sup>M</sup> | `flip concatMap` | `\g f x → g (f x) x` |
| `(a → m b) → m a → m b` | `(a → [b]) → [a] → [b]` | `(a → x → b) → (x → a) → x → b`
| `<*>`<sup>A</sup> | `\fs as → [f a \| f <- fs, a <- as]` | `\g f x → g x (f x)` |
| `m (a → b) → m a → m b` | `[a → b] → [a] → [b]` | `(x → a → b) → (x → a) → x → b` |
| `<$>`<sup>F</sup> <br> `fmap`<sup>F</sup> | `map` | `.` |
| `(a → b) → m a → m b` | `(a → b) → [a] → [b]` | `(a → b) → (x → a) → x → b` |
| `(id =<<)`<sup>M</sup> | `concat` | `\f x → f x x` <br> `(id >>=)` |
| `m (m a) → m b` | `[[a]] → [a]` | `(x → x → a) → x → a`