# StrLiterals

[![Build Status](https://travis-ci.org/JuliaString/StrLiterals.jl.svg?branch=master)](https://travis-ci.org/JuliaString/StrLiterals.jl)

[![Coverage Status](https://coveralls.io/repos/github/JuliaString/StrLiterals.jl/badge.svg?branch=master)](https://coveralls.io/github/JuliaString/StrLiterals.jl?branch=master)

[![codecov.io](http://codecov.io/github/JuliaString/StrLiterals.jl/coverage.svg?branch=master)](http://codecov.io/github/JuliaString/StrLiterals.jl?branch=master)

The StrLiterals package is an attempt to bring a cleaner string literal syntax to Julia, as well as having an easier way of producing formatted strings, borrowing from both Python and C formatted printing syntax.  It also adds support for using LaTex, Emoji, HTML, or Unicode entity names that are looked up at compile-time.
This builds on the previous work in StringUtils and StringLiterals, but is based on the new Strs.jl package

Currently, it adds a Swift style string macro, `f"..."`, which uses the Swift syntax for
interpolation, i.e. `\(expression)`.  This means that you never have to worry about strings with
the $ character in them, which is rather frequent in some applications.
Also, Unicode sequences are represented as in Swift, i.e. as `\u{hexdigits}`, where there
can be from 1 to 6 hex digits. This syntax eliminates having to worry about always outputting
4 or 8 hex digits, to prevent problems with 0-9,A-F,a-f characters immediately following.

It also adds a string macro that instead of building a string, can print the strings and interpolated values directly, without having to create a string out of all the parts.
Finally, there are uppercase versions of the macros, which also supports the legacy sequences, $ for string interpolation, `\x` followed by 1 or 2 hex digits, `\u` followed by 1 to 4 hex digits, and `\U` followed by 1 to 8 hex digits.

The [StrFormat](https://github.com/JuliaString/StrFormat.jl) package adds type-based, C-style, and Python-style formatting, using the following escape characters (after `\`): `%` and `{`.
See the package for more details.

The [StrEntities](https://github.com/JuliaString/StrEntities.jl) package adds Emojis (starting with `\:` and ending with `:`), LaTeX entities (starting with `\<` and ending with `>`) similar to the Julia REPL, as well as HTML entities (starting with `&`, anding with `;`), and Unicode entities (starting with `\N{` and ending with `}` (similar to Python strings)
See the package for more details.

* `\` can be followed by: 0, $, ", ', \, a, b, e, f, n, r, t, u, v, (
(as well as any added by other packages, such as `StrFormat` or `StrEntities`)
In the legacy modes, x and U are also allowed after the `\`.
Unsupported characters give an error (as in Swift, and in recent Julia versions).

* `\0` outputs a nul byte (0x00) (note: as in Swift, octal sequences are not supported, just the nul byte)
* `\a` outputs the "alarm" or "bell" control code (0x07)
* `\b` outputs the "backspace" control code (0x08)
* `\e` outputs the "escape" control code (0x1b)
* `\f` outputs the "formfeed" control code (0x0c)
* `\n` outputs the "newline" or "linefeed" control code (0x0a)
* `\r` outputs the "return" (carriage return) control code (0x0d)
* `\t` outputs the "tab" control code (0x09)
* `\v` outputs the "vertical tab" control code (0x0b)

* `\u{<hexdigits>}` is used to represent a Unicode character, with 1-6 hex digits.

* `\(expression)` simply interpolates the value of the expression, the same as `$(expression)` in standard Julia string literals.
