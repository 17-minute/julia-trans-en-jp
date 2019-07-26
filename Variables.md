原文は[こちら](https://docs.julialang.org/en/v1.1/manual/variables/)

 ## Variables / 変数 

| 原文（英語） | 訳文（日本語） |
|---|---|
| A variable, in Julia, is a name associated (or bound) to a value. | Juliaにおける変数とは、ある値に関連づけられた（結びつけられた）任意の名前を指します。 |
| It's useful when you want to store a value (that you obtained after some math, for example) for later use. | 変数は、ある値（例えば計算によって得られたもの）を後で使うために格納する際に便利です。 |
| For example: | 例を示します。|

```Julia
# Assign the value 10 to the variable x
# 値10を変数xに代入
julia> x = 10
10

# Doing math with x's value
# xの値で計算
julia> x + 1
11

# Reassign x's value
# xの値を再代入
julia> x = 1 + 1
2

# You can assign values of other types, like strings of text
# テキストの文字列といった他の型の値も代入可能
julia> x = "Hello World!"
"Hello World!"
```

| 原文（英語） | 訳文（日本語） |
|---|---|
| Julia provides an extremely flexible system for naming variables. | Juliaは非常に柔軟な変数の命名システムを提供しています。|
|Variable names are case-sensitive, and have no semantic meaning (that is, the language will not treat variables differently based on their names). | 変数名は大文字と小文字の区別があり、それには意味論上の意味がありません（すなわち、言語は変数をその意味に基づいて異なるものとして扱いません）。|


```Julia
julia> x = 1.0
1.0

julia> y = -3
-3

julia> Z = "My string"
"My string"

julia> customary_phrase = "Hello world!"
"Hello world!"

julia> UniversalDeclarationOfHumanRightsStart = "人人生而自由，在尊严和权利上一律平等。"
"人人生而自由，在尊严和权利上一律平等。"
```

| 原文（英語） | 訳文（日本語） |
|---|---|
| Unicode names (in UTF-8 encoding) are allowed: | Unicodeでの命名（UTF-8でのエンコード）も可能です。 |

```Julia
julia> δ = 0.00001
1.0e-5

julia> 안녕하세요 = "Hello"
"Hello"
```

| 原文（英語） | 訳文（日本語） |
|---|---|
| In the Julia REPL and several other Julia editing environments, you can type many Unicode math symbols by typing the backslashed LaTeX symbol name followed by tab. | JuliaのREPLと他のJulia編集環境の中にはタブに続けてバックスラッシュつきのLaTeX記号名をタイプすることで多くのUnicodeの数学用英数字記号を使えるものがあります。 |
| For example, the variable name `δ` can be entered by typing `\delta`-tab, or even `α̂₂` by `\alpha`-tab-`\hat`-tab-`\_2`-tab. (If you find a symbol somewhere, e.g. in someone else's code, that you don't know how to type, the REPL help will tell you: just type `?` and then paste the symbol.) | 例えば、`δ`という名の変数は`\delta`-tabをタイプすることで入力でき、 `α̂₂` も`\alpha`-tab-`\hat`- tab-`\_2`-tabで入力できます。 （他の人のコードなどでタイプの仕方がわからない記号があった場合は、REPLのヘルプが教えてくれます。`?`をタイプした後、その記号をペーストしてください。）|
| Julia will even let you redefine built-in constants and functions if needed (although this is not recommended to avoid potential confusions): | Juliaでは必要に応じてビルトイン定数や関数を再定義することもできます（とはいえ、これは混乱を避けるために推奨しません）。|

```julia
julia> pi = 3
3

julia> pi
3

julia> sqrt = 4
4
```
| 原文（英語） | 訳文（日本語） |
|---|---|
| However, if you try to redefine a built-in constant or function already in use, Julia will give you an error: | しかし、すでに使用されているビルトイン定数や関数を再定義しようとすると、Juliaはエラーを返します。|

```julia
julia> pi
π = 3.1415926535897...

julia> pi = 3
ERROR: cannot assign a value to variable MathConstants.pi from module Main

julia> sqrt(100)
10.0

julia> sqrt = 4
ERROR: cannot assign a value to variable Base.sqrt from module Main
```

## Allowed Variable Names / 使用可能な変数名

| 原文（英語） | 訳文（日本語） |
|---|---|
| Variable names must begin with a letter (A-Z or a-z), underscore, or a subset of Unicode code points greater than 00A0; in particular, [Unicode character categories](http://www.fileformat.info/info/unicode/category/index.htm) Lu/Ll/Lt/Lm/Lo/Nl (letters), Sc/So (currency and other symbols), and a few other letter-like characters (e.g. a subset of the Sm math symbols) are allowed.  | 変数名の頭文字は英文字（AからZ、あるいはaからz）、アンダーバー、00A0より大きいUnicodeコードポイントのサブセット。中でも特に、U[nicode文字のカテゴリ](http://www.fileformat.info/info/unicode/category/index.htm)（訳注: 未翻訳）Lu、Ll、Lt、Lm、Lo、Nl（文字）、ScとSo（通貨や他の記号類）、その他少数の文字様記号（例えばSmの数学用英数字記号のサブセット）である必要があります。|
| Subsequent characters may also include ! and digits (0-9 and other characters in categories Nd/No), as well as other Unicode code points: diacritics and other modifying marks (categories Mn/Mc/Me/Sk), some punctuation connectors (category Pc), primes, and a few other characters. | 2文字目以降の文字は他のUnicodeのコードポイントと同様に、!とアラビア数字（カテゴリNdやNoに含まれる0から9までの数字とその他の文字）を含むことがあります。つまり、発音区別符号や他の修飾符号（カテゴリMn、Mc、Me、Sk）や句読点の一部（カテゴリPc）、プライム記号、そしてその他少数の文字です。|

| 原文（英語） | 訳文（日本語） |
|---|---|
| Operators like `+` are also valid identifiers, but are parsed specially. | `+`のような演算子もまた有効な識別子ですが、特別な方法で解析されます。|
| In some contexts, operators can be used just like variables; for example `(+)` refers to the addition function, and `(+) = f` will reassign it. | 前後関係によっては、演算子は単に変数のように使われます。例えば、`(+)`は加算する働きがあることを表しますが、`(+) = f`はそれに再代入します。|
| Most of the Unicode infix operators (in category Sm), such as `⊕`, are parsed as infix operators and are available for user-defined methods (e.g. you can use `const ⊗ = kron` to define ⊗ as an infix Kronecker product). |`⊕`のようなUnicodeの二項演算子（カテゴリSm内）のほとんどは二項演算子として解析され、ユーザ定義のメソッドに利用できます（例: `const ⊗ = kron`を中置記法のクロネッカー積と定義できます）。|
| Operators can also be suffixed with modifying marks, primes, and sub/superscripts, e.g. `+̂ₐ″` is parsed as an infix operator with the same precedence as `+`.| 演算子末尾には修飾符号、プライム記号、そして下つき文字や上つき文字をつけることも可能です。例えば、`+̂ₐ″`は`+`と同じオペレータ順位を持つ二項演算子として解析されます。|
| The only explicitly disallowed names for variables are the names of built-in statements: |明らかに使用不可とされる唯一の変数名は、ビルトインのステートメント名です。|

```Julia
julia> else = false
ERROR: syntax: unexpected "else"

julia> try = "No"
ERROR: syntax: unexpected "="
```

| 原文（英語） | 訳文（日本語） |
|---|---|
| Some Unicode characters are considered to be equivalent in identifiers. | Unicode文字の中には識別子と同等とみなされるものがあります。 |
| Different ways of entering Unicode combining characters (e.g., accents) are treated as equivalent (specifically, Julia identifiers are NFC-normalized). | Unicodeの結合文字（例: アクセント記号）の表現方法が異なっていても等価とみなされます（はっきり言えば、Juliaの識別子は正規化形式Cです）。|
| The Unicode characters `ɛ` (U+025B: Latin small letter open e) and µ (U+00B5: micro sign) are treated as equivalent to the corresponding Greek letters, because the former are easily accessible via some input methods. | Unicode文字ɛ（U+025B: ラテン文字の小文字オープンe)と`µ`（U+00B5: マイクロを表す記号)は対応するギリシャ文字と等価とみなされます。というのも、前者はある入力方法を使えば容易に使えるからです。|

## Stylistic Conventions

| 原文（英語） | 訳文（日本語） |
|---|---|
|While Julia imposes few restrictions on valid names, it has become useful to adopt the following conventions: | Juliaには有効な命名に関しての制約はほとんどありませんが、以下の慣例を採用することが有用とされています。|
| - Names of variables are in lower case. | - 変数名が小文字である。|
| - Word separation can be indicated by underscores (`'_'`), but use of underscores is discouraged unless the name would be hard to read otherwise. | - 単語の区切り文字がアンダーバー (`'_'`)で示されている。しかし、アンダーバーがなくてもその名前が難なく読める場合はアンダーバーの使用はしないほうがよい。|
| - Names of `Type`s and `Module`s begin with a capital letter and word separation is shown with upper camel case instead of underscores. |- `型`名や`モジュール`名が大文字で始まっており、単語の区切り文字がアンダーバーではなくキャメルケースで示されている。 |
| - Names of `function`s and `macro`s are in lower case, without underscores. | - `関数`名や`マクロ`名が小文字であり、アンダーバーが使用されていない。|
| - Functions that write to their arguments have names that end in `!`. These are sometimes called "mutating" or "in-place" functions because they are intended to produce changes in their arguments after the function is called, not just return a value. | - `!`で終わる名前の引数に書く関数。これらは「mutating（変化する）関数」や「in-place（インプレース）関数」と呼ばれることもある。というのも、これらは単に値を返すのではなく、関数を呼び出した後に引数に変化をもたらすことを意図したものだからである。|
| For more information about stylistic conventions, see the [Style Guide](https://docs.julialang.org/en/v1.1/manual/style-guide/#Style-Guide-1). | スタイルに関する慣例についての詳細は、[スタイルガイド](https://docs.julialang.org/en/v1.1/manual/style-guide/#Style-Guide-1)（訳注: 未翻訳）を参照ください。|

| 原文（英語） | 訳文（日本語） |
|---|---|
| Previous: Getting Started | 前: さあ、始めよう |
| Next: Integers and Floating-Point Numbers | 次: 整数と浮動小数点数 |
