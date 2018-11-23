* [Data.Functor](http://hackage.haskell.org/package/base-4.12.0.0/docs/Data-Functor.html)
* [Control.Applicative](http://hackage.haskell.org/package/base-4.12.0.0/docs/Control-Applicative.html)
* [Control.Monad](http://hackage.haskell.org/package/base-4.12.0.0/docs/Control-Monad.html)

|fn|`[]`|`(x →)`|
|-|-|-|
| `pure`<sup>A</sup> <br> `return`<sup>M</sup> | `(:[])` <br> `\a→[a]` | `const` <br> `\a x→a` |
| `a → m a` | `a → [a]` | `a → x → a` |
| `>>=`<sup>M</sup> | `concatMap` | `\f g x→g (f x) x` |
| `m a → (a → m b) → m b` | `[a] → (a → [b]) → [b]` | `(x → a) → (a → x → b) → x → b` |
| `=<<`<sup>M</sup> <br> `flip (>>=)`<sup>M</sup> | `flip concatMap` | `\g f x→g (f x) x` |
| `(a → m b) → m a → m b` | `(a → [b]) → [a] → [b]` | `(a → x → b) → (x → a) → x → b`
| `<*>`<sup>A</sup> | `\fs as→[f a \| f←fs, a←as]` | `\g f x→g x (f x)` |
| `m (a → b) → m a → m b` | `[a → b] → [a] → [b]` | `(x → a → b) → (x → a) → x → b` |
| `<$>`<sup>F</sup> <br> `fmap`<sup>F</sup> | `map` | `.` |
| `(a → b) → m a → m b` | `(a → b) → [a] → [b]` | `(a → b) → (x → a) → x → b` |
| `(id =<<)`<sup>M</sup> | `concat` | `\f x→f x x` <br> `(id >>=)` |
| `m (m a) → m b` | `[[a]] → [a]` | `(x → x → a) → x → a`
| `>>`<sup>M</sup> | repeat <br> `\a b→take (length a * length b) $ cycle b` | `flip const` <br> `\f g x→g x` |
| `m a → m b → m b` | `[a] → [b] → [b]` | `(x → a) → (x → b) → x → b` |
| `sequence`<sup>M</sup> <br> `mapM id`<sup>M</sup> | cartesian product | `\fs x→[f x \| f←fs]` |
| `t (m b) → m (t b)` <br> `[m b] → m [b]` | `t [b] → [t b]` <br> `[[b]] → [[b]]` | `t (x → b) → x → t b` <br> `[x → b] → x → [b]` |
| `mapM`<sup>M</sup> <br> `sequence.map`<sup>M</sup> | cartesian product of map | `\f as x→[f a x \| a←as]` |
| `(a → m b) → t a → m (t b)` <br> `(a → m b) → [a] → m [b]` | `(a → [b]) → t a → [t b]` <br> `(a → [b]) → [a] → [[b]]` | `(a → x → b) → t a → x → t b` <br> `(a → x → b) → [a] → x → [b]` |
