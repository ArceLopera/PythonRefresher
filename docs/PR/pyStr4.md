“**Format specifications**” are used within replacement fields contained within a format string to define how individual values are presented.

A general convention is that an empty format specification produces the same result as if you had called str() on the value. A non-empty format specification typically modifies the result.

The general form of a standard format specifier is:

| format_spec       | [[fill]align][sign][#][0][width][grouping_option][.precision][type] | 
| :---        |    :----:   | 
| fill   | any character        |
| align   | "<" , ">" , "=" , "^"        |
| sign   | "+" , "-" , " "        |
| width    | digit+        |
| grouping_option   | "_" , ","        |
| precision   | digit+        |
| type   | "b", "c" , "d" , "e" , "E" , "f" , "F" , "g" , "G" , "n" , "o" , "s" , "x" , "X" , "%"        |

##Fill

If a valid align value is specified, it can be preceded by a fill character that can be any character and defaults to a space if omitted. It is not possible to use a literal curly brace (“{” or “}”) as the fill character in a formatted string literal or when using the str.format() method. However, it is possible to insert a curly brace with a nested replacement field. This limitation doesn’t affect the format() function.

##Align

The meaning of the various alignment options is as follows:

| Option      | Meaning     |
| ----------- | ----------- |   
| '<'      | Forces the field to be left-aligned within the available space (this is the default for most objects)       | 
| '>'   | 	Forces the field to be right-aligned within the available space (this is the default for numbers)        | 
| '='      | Forces the padding to be placed after the sign (if any) but before the digits. This is used for printing fields in the form ‘+000000120’. This alignment option is only valid for numeric types. It becomes the default for numbers when ‘0’ immediately precedes the field width       | 
| '^'   | Forces the field to be centered within the available space        | 

``` py
'{:>30}'.format('right aligned')
```

```
                 right aligned
```
``` py
'{:*^30}'.format('centered')  # use '*' as a fill char
```
```
***********centered***********
```


##Sign

Note that unless a minimum field width is defined, the field width will always be the same size as the data to fill it, so that the alignment option has no meaning in this case.

The sign option is only valid for number types, and can be one of the following:

| Option      | Meaning     |
| ----------- | ----------- |   
| '+'      | indicates that a sign should be used for both positive as well as negative numbers.       | 
| '-'   | 	indicates that a sign should be used only for negative numbers (this is the default behavior).        | 
| space      | indicates that a leading space should be used on positive numbers, and a minus sign on negative numbers. | 

``` py
'{:+f}; {:+f}'.format(3.14, -3.14)  # show it always
```
```
+3.140000; -3.140000
```

``` py
'{: f}; {: f}'.format(3.14, -3.14)  # show a space for positive numbers
```
```
 3.140000; -3.140000
```

``` py
'{:-f}; {:-f}'.format(3.14, -3.14)  # show only the minus -- same as '{:f}; {:f}'
```
```
3.140000; -3.140000
```

##\# and , and _ Option
###'#' option
The '#' option causes the “alternate form” to be used for the conversion. The alternate form is defined differently for different types. This option is only valid for integer, float and complex types. For integers, when binary, octal, or hexadecimal output is used, this option adds the respective prefix '0b', '0o', '0x', or '0X' to the output value. For float and complex the alternate form causes the result of the conversion to always contain a decimal-point character, even if no digits follow it. Normally, a decimal-point character appears in the result of these conversions only if a digit follows it. In addition, for 'g' and 'G' conversions, trailing zeros are not removed from the result.
``` py
'Integer in Octal: {:#o}'.format(1234567)
```
```
Correct answers: 0o4553207
```
``` py
'Integer in Octal: {:o}'.format(1234567)
```
```
Correct answers: 4553207
```
###',' option
The ',' option signals the use of a comma for a thousands separator. For a locale aware separator, use the 'n' integer presentation type instead. see [PEP378](https://www.python.org/dev/peps/pep-0378/)

``` py
'{:,}'.format(1234567890)
```
```
1,234,567,890
```
``` py
format(1234.5, "08,.1f")
```
```
01,234.5
```
###'_' option
The '_' option signals the use of an underscore for a thousands separator for floating point presentation types and for integer presentation type 'd'. For integer presentation types 'b', 'o', 'x', and 'X', underscores will be inserted every 4 digits. For other presentation types, specifying this option is an error.
``` py
#{:10_} for a width of 10 with _ separator.
format(1234.5, "08_.1f")
```
```
01_234.5
```

##Width
width is a decimal integer defining the minimum total field width, including any prefixes, separators, and other formatting characters. If not specified, then the field width will be determined by the content.

When no explicit alignment is given, preceding the width field by a zero ('0') character enables sign-aware zero-padding for numeric types. This is equivalent to a fill character of '0' with an alignment type of '='.

Changed in version 3.10: Preceding the width field by '0' no longer affects the default alignment for strings.

##Precision

The precision is a decimal integer indicating how many digits should be displayed after the decimal point for presentation types 'f' and 'F', or before and after the decimal point for presentation types 'g' or 'G'. For string presentation types the field indicates the maximum field size - in other words, how many characters will be used from the field content. The precision is not allowed for integer presentation types.



``` py
points = 19
total = 22
'Correct answers: {:.2%}'.format(points/total)
```
```
Correct answers: 86.36%
```

##Type
The type determines how the data should be presented.

### for strings
The available string presentation types are:

| Type      | Meaning     |
| ----------- | ----------- |   
| 's'      |String format. This is the default type for strings and may be omitted.       | 
| None   | The same as 's'.        |

### for integers
The available integer presentation types are:

| Type      | Meaning     |
| ----------- | ----------- |   
| 'b'      |	Binary format. Outputs the number in base 2.      | 
| 'c'   | Character. Converts the integer to the corresponding unicode character before printing.       |
| 'd'      |	Octal format. Outputs the number in base 8.      | 
| 'o'   | Character. Converts the integer to the corresponding unicode character before printing.       |
| 'x'      |	Hex format. Outputs the number in base 16, using lower-case letters for the digits above 9.      | 
| 'X'   | Hex format. Outputs the number in base 16, using upper-case letters for the digits above 9. In case '#' is specified, the prefix '0x' will be upper-cased to '0X' as well.       |
| 'n'      |	Number. This is the same as 'd', except that it uses the current locale setting to insert the appropriate number separator characters.      | 
| None   | The same as 'd'.       |

In addition to the above presentation types, integers can be formatted with the floating point presentation types listed below (except 'n' and None). When doing so, float() is used to convert the integer to a floating point number before formatting.

###for float and decimal
The available presentation types for float and Decimal values are:

| Type      | Meaning     |
| ----------- | ----------- |   
| 'e'      |Scientific notation. For a given precision p, formats the number in scientific notation with the letter ‘e’ separating the coefficient from the exponent. The coefficient has one digit before and p digits after the decimal point, for a total of p + 1 significant digits. With no precision given, uses a precision of 6 digits after the decimal point for float, and shows all coefficient digits for Decimal. If no digits follow the decimal point, the decimal point is also removed unless the # option is used.     | 
| 'E'   | Scientific notation. Same as 'e' except it uses an upper case ‘E’ as the separator character.     |
| 'f'      |	Fixed-point notation. For a given precision p, formats the number as a decimal number with exactly p digits following the decimal point. With no precision given, uses a precision of 6 digits after the decimal point for float, and uses a precision large enough to show all coefficient digits for Decimal. If no digits follow the decimal point, the decimal point is also removed unless the # option is used.      | 
| 'F'  | Fixed-point notation. Same as 'f', but converts nan to NAN and inf to INF.       |
| 'g'      |	General format. For a given precision p >= 1, this rounds the number to p significant digits and then formats the result in either fixed-point format or in scientific notation, depending on its magnitude. A precision of 0 is treated as equivalent to a precision of 1. The precise rules are as follows: suppose that the result formatted with presentation type 'e' and precision p-1 would have exponent exp. Then, if m <= exp < p, where m is -4 for floats and -6 for Decimals, the number is formatted with presentation type 'f' and precision p-1-exp. Otherwise, the number is formatted with presentation type 'e' and precision p-1. In both cases insignificant trailing zeros are removed from the significand, and the decimal point is also removed if there are no remaining digits following it, unless the '#' option is used. With no precision given, uses a precision of 6 significant digits for float. For Decimal, the coefficient of the result is formed from the coefficient digits of the value; scientific notation is used for values smaller than 1e-6 in absolute value and values where the place value of the least significant digit is larger than 1, and fixed-point notation is used otherwise. Positive and negative infinity, positive and negative zero, and nans, are formatted as inf, -inf, 0, -0 and nan respectively, regardless of the precision.      | 
| 'G'   | General format. Same as 'g' except switches to 'E' if the number gets too large. The representations of infinity and NaN are uppercased, too.|
| 'n'      |	Number. This is the same as 'g', except that it uses the current locale setting to insert the appropriate number separator characters. | 
| '%'   | Percentage. Multiplies the number by 100 and displays in fixed ('f') format, followed by a percent sign.       |
| None   | For float this is the same as 'g', except that when fixed-point notation is used to format the result, it always includes at least one digit past the decimal point. The precision used is as large as needed to represent the given value faithfully. For Decimal, this is the same as either 'g' or 'G' depending on the value of context.capitals for the current decimal context. The overall effect is to match the output of str() as altered by the other format modifiers.       |
