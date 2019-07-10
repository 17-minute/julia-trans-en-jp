https://docs.julialang.org/en/v1.1/manual/strings/

## Strings / 文字列

| 原文（英語） | 訳文（日本語） |
|---|---|
Strings are finite sequences of characters.
文字列は文字の文字が有限に連続したものです。

Of course, the real trouble comes when one asks what a character is.
もちろん、誰かが何の文字かとたずねたら困ったことになります。

The characters that English speakers are familiar with are the letters A, B, C, etc., 
together with numerals and common punctuation symbols.
英語話者になじみのある文字といえば、数字や一般的な句読点を含んだA、B、Cなどの文字です。

These characters are standardized together with a mapping to integer values between 0 and 127 by the ASCII standard.
この文字はASCII標準による0と127の間の整数の値とともに標準化されています。

There are, of course, many other characters used in non-English languages, 
including variants of the ASCII characters with accents and other modifications, 
related scripts such as Cyrillic and Greek, and scripts completely unrelated to ASCII and English, 
including Arabic, Chinese, Hebrew, Hindi, Japanese, and Korean.
もちろん、英語以外の言語では他に多くの文字があります。
強勢を表す記号や他の母音変化の記号があるASCII文字の異形を含め、
キリル文字やギリシャ文字で書かれたスクリプトに関して
ASCIIと英語に全く関係のないスクリプト
アラビア語、中国語、ヘブライ語、ヒンディー語、日本語、韓国語を含め、

The Unicode standard tackles the complexities of what exactly a character is, 
and is generally accepted as the definitive standard addressing this problem.

Depending on your needs, you can either ignore these complexities entirely 
and just pretend that only ASCII characters exist, or you can write code 
that can handle any of the characters or encodings that one may encounter 
when handling non-ASCII text.

Julia makes dealing with plain ASCII text simple and efficient, and handling Unicode is as simple and efficient as possible.

In particular, you can write C-style string code to process ASCII strings, 
and they will work as expected, both in terms of performance and semantics.

If such code encounters non-ASCII text, it will gracefully fail with a clear error message, 
rather than silently introducing corrupt results. When this happens, 
modifying the code to handle non-ASCII data is straightforward.





There are a few noteworthy high-level features about Julia's strings:

- The built-in concrete type used for strings (and string literals) in Julia is String.
This supports the full range of Unicode characters via the UTF-8 encoding.
(A transcode function is provided to convert to/from other Unicode encodings.)

- All string types are subtypes of the abstract type AbstractString, and external packages define additional AbstractString subtypes (e.g. for other encodings). If you define a function expecting a string argument, you should declare the type as AbstractString in order to accept any string type.

- Like C and Java, but unlike most dynamic languages, Julia has a first-class type for representing a single character, called AbstractChar. The built-in Char subtype of AbstractChar is a 32-bit primitive type that can represent any Unicode character (and which is based on the UTF-8 encoding).

- As in Java, strings are immutable: the value of an AbstractString object cannot be changed. To construct a different string value, you construct a new string from parts of other strings.

- Conceptually, a string is a partial function from indices to characters: for some index values, no character value is returned, and instead an exception is thrown. This allows for efficient indexing into strings by the byte index of an encoded representation rather than by a character index, which cannot be implemented both efficiently and simply for variable-width encodings of Unicode strings.

## Characters / 文字

A Char value represents a single character: it is just a 32-bit primitive type with a special literal representation and appropriate arithmetic behaviors, and which can be converted to a numeric value representing a Unicode code point. (Julia packages may define other subtypes of AbstractChar, e.g. to optimize operations for other text encodings.) Here is how Char values are input and shown:


```Julia
julia> 'x'
'x': ASCII/Unicode U+0078 (category Ll: Letter, lowercase)

julia> typeof(ans)
Char
```
You can easily convert a Char to its integer value, i.e. code point:

```Julia
julia> Int('x')
120

julia> typeof(ans)
Int64
```

On 32-bit architectures, typeof(ans) will be Int32. You can convert an integer value back to a Char just as easily:

```Julia
julia> Char(120)
'x': ASCII/Unicode U+0078 (category Ll: Letter, lowercase)
```
Not all integer values are valid Unicode code points, but for performance, the Char conversion does not check that every character value is valid. If you want to check that each converted value is a valid code point, use the isvalid function:

```Julia
julia> Char(0x110000)
'\U110000': Unicode U+110000 (category In: Invalid, too high)

julia> isvalid(Char, 0x110000)
false
```

As of this writing, the valid Unicode code points are U+00 through U+d7ff and U+e000 through U+10ffff. These have not all been assigned intelligible meanings yet, nor are they necessarily interpretable by applications, but all of these values are considered to be valid Unicode characters.

You can input any Unicode character in single quotes using \u followed by up to four hexadecimal digits or \U followed by up to eight hexadecimal digits (the longest valid value only requires six):

```Julia
julia> '\u0'
'\0': ASCII/Unicode U+0000 (category Cc: Other, control)

julia> '\u78'
'x': ASCII/Unicode U+0078 (category Ll: Letter, lowercase)

julia> '\u2200'
'∀': Unicode U+2200 (category Sm: Symbol, math)

julia> '\U10ffff'
'\U10ffff': Unicode U+10ffff (category Cn: Other, not assigned)
```
Julia uses your system's locale and language settings to determine which characters can be printed as-is and which must be output using the generic, escaped \u or \U input forms. In addition to these Unicode escape forms, all of C's traditional escaped input forms can also be used:

```Julia
julia> Int('\0')
0

julia> Int('\t')
9

julia> Int('\n')
10

julia> Int('\e')
27

julia> Int('\x7f')
127

julia> Int('\177')
127
```
You can do comparisons and a limited amount of arithmetic with Char values:

```Julia
julia> 'A' < 'a'
true

julia> 'A' <= 'a' <= 'Z'
false

julia> 'A' <= 'X' <= 'Z'
true

julia> 'x' - 'a'
23

julia> 'A' + 1
'B': ASCII/Unicode U+0042 (category Lu: Letter, uppercase)
```

## String Basics / 文字列の基本










