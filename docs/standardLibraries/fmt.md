# printf: prints formatted output

sprintf converts and formats a variable number of arguments as is specified by a
`format string`. In it's basic form, a format string may just be a literal. In
case arguments are meant to be formatted, a `directive` is contained in the
format string, preceded by a '%' character:

    %<verb>

E.g. the verb `s` indicates the directive should be replaced by the string
representation of the argument in the corresponding position of the argument
list. E.g.:

    Hello %s!

applied to the arguments "World" yields "Hello World!"

The meaning of the format string is modelled after [POSIX][1] format strings as
well as well as [Golang format strings][2]. Both contain elements specific to
the respective programming language that don't apply to JavaScript, so they can
not be fully supported. Furthermore we implement some functionality that is
specific to JS.

## Verbs

The following verbs are supported:

| Verb  | Meaning                                                        |
| ----- | -------------------------------------------------------------- |
| `%`   | print a literal percent                                        |
| `t`   | evaluate arg as boolean, print `true` or `false`               |
| `b`   | eval as number, print binary                                   |
| `c`   | eval as number, print character corresponding to the codePoint |
| `o`   | eval as number, print octal                                    |
| `x X` | print as hex (ff FF), treat string as list of bytes            |
| `e E` | print number in scientific/exponent format 1.123123e+01        |
| `f F` | print number as float with decimal point and no exponent       |
| `g G` | use %e %E or %f %F depending on size of argument               |
| `s`   | interpolate string                                             |
| `T`   | type of arg, as returned by `typeof`                           |
| `v`   | value of argument in 'default' format (see below)              |
| `j`   | argument as formatted by `JSON.stringify`                      |

## Width and Precision

Verbs may be modified by providing them with width and precision, either or both
may be omitted:

    %9f    width 9, default precision
    %.9f   default width, precision 9
    %8.9f  width 8, precision 9
    %8.f   width 9, precision 0

In general, 'width' describes the minimum length of the output, while
'precision' limits the output.

| verb      | precision                                                       |
| --------- | --------------------------------------------------------------- |
| `t`       | n/a                                                             |
| `b c o`   | n/a                                                             |
| `x X`     | n/a for number, strings are truncated to p bytes(!)             |
| `e E f F` | number of places after decimal, default 6                       |
| `g G`     | set maximum number of digits                                    |
| `s`       | truncate input                                                  |
| `T`       | truncate                                                        |
| `v`       | truncate, or depth if used with # see "'default' format", below |
| `j`       | n/a                                                             |

Numerical values for width and precision can be substituted for the `*` char, in
which case the values are obtained from the next args, e.g.:

    sprintf ("%*.*f", 9,8,456.0)

is equivalent to

    sprintf ("%9.9f", 456.0)

## Flags

The effects of the verb may be further influenced by using flags to modify the
directive:

| Flag  | Verb      | Meaning                                                                    |
| ----- | --------- | -------------------------------------------------------------------------- |
| `+`   | numeric   | always print sign                                                          |
| `-`   | all       | pad to the right (left justify)                                            |
| `#`   |           | alternate format                                                           |
| `#`   | `b o x X` | prefix with `0b 0 0x`                                                      |
| `#`   | `g G`     | don't remove trailing zeros                                                |
| `#`   | `v`       | ues output of `inspect` instead of `toString`                              |
| `' '` |           | space character                                                            |
| `' '` | `x X`     | leave spaces between bytes when printing string                            |
| `' '` | `d`       | insert space for missing `+` sign character                                |
| `0`   | all       | pad with zero, `-` takes precedence, sign is appended in front of padding  |
| `<`   | all       | format elements of the passed array according to the directive (extension) |

## 'default' format

The default format used by `%v` is the result of calling `toString()` on the
relevant argument. If the `#` flags is used, the result of calling `inspect()`
is interpolated. In this case, the precision, if set is passed to `inspect()` as
the 'depth' config parameter

## Positional arguments

Arguments do not need to be consumed in the order they are provided and may be
consumed more than once. E.g.:

    sprintf("%[2]s %[1]s", "World", "Hello")

returns "Hello World". The presence of a positional indicator resets the arg
counter allowing args to be reused:

    sprintf("dec[%d]=%d hex[%[1]d]=%x oct[%[1]d]=%#o %s", 1, 255, "Third")

returns `dec[1]=255 hex[1]=0xff oct[1]=0377 Third`

Width and precision may also use positionals:

    "%[2]*.[1]*d", 1, 2

This follows the golang conventions and not POSIX.

## Errors

The following errors are handled:

Incorrect verb:

    S("%h", "") %!(BAD VERB 'h')

Too few arguments:

    S("%d") %!(MISSING 'd')"

[1]: https://pubs.opengroup.org/onlinepubs/009695399/functions/fprintf.html
[2]: https://golang.org/pkg/fmt/
[3]: https://console.spec.whatwg.org/#object-formats
