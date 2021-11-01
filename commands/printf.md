---
description: print format
---

# printf

## Introduction

La fonction printf permet des affichages formatés sur stdout

## Syntaxe

```
int starwars = 3;
printf("starwars %d", starwars);
```

### descripteurs

| specifier | Output                                                                                                                                                                                                    | Example      |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ |
| `d`or `i` | Signed **d**ecimal** i**nteger                                                                                                                                                                            | 392          |
| `u`       | **U**nsigned decimal integer                                                                                                                                                                              | 7235         |
| `o`       | Unsigned **O**ctal                                                                                                                                                                                        | 610          |
| `x`       | Unsigned he**x**adecimal integer, lowercase                                                                                                                                                               | 7fa          |
| `X`       | Unsigned he**x**adecimal integer, uppercase                                                                                                                                                               | 7FA          |
| `f`       | Decimal **f**loating point, lowercase                                                                                                                                                                     | 392.65       |
| `F`       | Decimal **f**loating point, uppercase                                                                                                                                                                     | 392.65       |
| `e`       | Scientific notation (mantissa/**e**xponent), lowercase $$exp \in ]- \infty, -5] \cup [4,\infty[$$                                                                                                         | 3.9265e+2    |
| `E`       | Scientific notation (mantissa/**e**xponent), uppercase $$exp \in ]- \infty, -5] \cup [4, \infty[$$                                                                                                        | 3.9265E+2    |
| `g`       | Use the shortest representation: `%e` ou `%f`                                                                                                                                                             | 392.65       |
| `G`       | Use the shortest representation: `%E` ou `%F`                                                                                                                                                             | 392.65       |
| `a`       | Hex**a**decimal flo**a**ting point, lowercase                                                                                                                                                             | -0xc.90fep-2 |
| `A`       | Hex**a**decimal flo**a**ting point, uppercase                                                                                                                                                             | -0XC.90FEP-2 |
| `c`       | **C**haracter                                                                                                                                                                                             | a            |
| `s`       | **S**tring of characters                                                                                                                                                                                  | sample       |
| `p`       | **P**ointer address                                                                                                                                                                                       | b8000000     |
| `n`       | <p><strong>N</strong>othing printed </p><ul><li>the corresponding argument must be a pointer to a signed int.</li><li>The number of characters written so far is stored in the pointed location</li></ul> |              |
| `%`       | A % followed by another % character will write a single % to the stream                                                                                                                                   | %            |

{% hint style="info" %}
Il est important de noter que le descripteur définit le type et l’interprétation de la valeur correspondante mais ne fait pas de conversion de type
{% endhint %}

Optionnellement, les descripteurs peuvent être complétés par des drapeaux pour plus de contrôle avec la syntaxe `%[flags][width][.precision][length]descripteur`.

#### flags

| Specifier | Action                                                                                                                                                                                                                                                                                                                                                                                                            |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-`       | Left-justify within the given field width; Right justification is the default (see width sub-specifier).                                                                                                                                                                                                                                                                                                          |
| `+`       | Forces to precede the result with a plus or minus sign (**+ **or **-**) even for positive numbers. By default, only negative numbers are preceded with a **-** sign.                                                                                                                                                                                                                                              |
| ` `       | If no sign is going to be written, a blank space is inserted before the value.                                                                                                                                                                                                                                                                                                                                    |
| `#`       | Used with `o`,`  x  `or` X` specifiers the value is preceded with 0, 0x or 0X respectively for values different than zero. Used with `e`, `E `and `f`, it forces the written output to contain a decimal point even if no digits would follow. By default, if no digits follow, no decimal point is written. Used with `g` or `G` the result is the same as with `e` or`  E  `but trailing zeros are not removed. |
| `0`       | Left-pads the number with zeroes (0) instead of spaces, where padding is specified                                                                                                                                                                                                                                                                                                                                |

#### width

| Width    | Description                                                                                                                                                                                          |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `number` | Minimum number of characters to be printed. If the value to be printed is shorter than this number, the result is padded with blank spaces. The value is not truncated even if the result is larger. |
| `*`      | The width is not specified in the format string, but as an additional integer value argument preceding the argument that has to be formatted.                                                        |

#### precision

| Specifier | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `.number` | <ul><li>For integer specifiers (<code>d</code>,<code> i</code>,<code> o</code>,<code> u</code>,<code> x</code>,<code> X</code>)</li><li>precision specifies the minimum number of digits to be written. If the value to be written is shorter than this number, the result is padded with leading zeros. The value is not truncated even if the result is longer. A precision of 0 means that no character is written for the value 0. For<code> e</code>, <code>E</code> and f specifiers</li><li>this is the number of digits to be printed after the decimal point. For <code>g</code> and <code>G</code> specifiers</li><li>This is the maximum number of significant digits to be printed. For <code>s</code> </li><li>this is the maximum number of characters to be printed. By default all characters are printed until the ending null character is encountered. </li><li>For c type it has no effect. When no precision is specified, the default is 1. If the period is specified without an explicit value for precision, 0 is assumed.</li></ul> |
| `.*`      | The precision is not specified in the format string, but as an additional integer value argument preceding the argument that has to be formatted.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

#### length

| Specifier | Description                                                                                                                                                                                     |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `h`       | The argument is interpreted as a short int or unsigned short int (only applies to integer specifiers: `i, d, o, u, x, X`).                                                                      |
| `l`       | The argument is interpreted as a **long int **or **unsigned long int** for integer specifiers (`i, d, o, u, x,X`), and as a wide character or wide character string for specifiers `c` and `s`. |
| `L`       | The argument is interpreted as a **long double** (only applies to floating point specifiers: `e, E, f, g,G`).                                                                                   |
| `zu`      | size\_t                                                                                                                                                                                         |

## Utilisation



