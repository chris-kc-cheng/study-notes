# Texas Instruments TI-36X Pro

TI-36X Pro is a non-graphing, non-programmable scientific calculator.

## Layout

Hover over the key to see its functions
| | | | | |
|:------:|:----:|:--------:|:-:|:-:|
|[**`2nd`**](## "2nd function")|[`mode`](## "Change Angle, numeric notation, decimal notation, complex number results, number base, and display mode, or return to Home screen")| [`delete`](## "Delete or insert a character at the cursor") | [`🡄`](## "Scroll left") | [`🡅`](## "Scroll up") |
|[`ln log`](## "Logarithm of a number to the base e, 10 or another number, or numberic derivative")|[`math`](## "Math and matrix menu")|[`data`](## "Data editor, or statistics, regression, and distribution menu") | [`🡇`](## "Scroll down") | [`🡆`](## "Scroll right") |
|[`e° 10°`](## "Raise e or 10 to the power, or numeric integral")| [`EE`](## "Scientific notation, or vector menu") |[`!`](## "Factorial, combinations, permutations, or random menu") | [`table`](## "Function table, or expression evaluation") | [`clear`](## "Clear characters on entry line, or clear an error message") |
| [`πᵉᵢ`](## "Pi, Euler's number, imaginary unit, or complex menu") | [`sin`](## "Toggle between sine, hyperbolic sine, and their inverses, or solve numeric equation") | [`cos`](## "Toggle between cosine, hyperbolic cosine, and their inverses, or select between quadratic of cubic equation solver")|[`tan`](## "Toggle between tangent, hyperbolic tangent, and their inverses, or solve system of linear equations")|[`÷`](## "Divide, or percentage")|
| [`x°`](## "Raise to the power, or n-th root") | [`믐`](## "Simple fraction, or inverse")  | [`(`](## "Open parthenthesis, or scientific constants") | [`)`](## "Close parthenthesis, or recall the stored operation") | [`×`](## "Multiply, or store a sequence of operations") |
| [`x²`](## "Square, or square root")   | [`7`](## "7, or enter a mixed number") | [`8`](## "8, or conversions menu") | [`9`](## "9, base conversion or boolean logic") | [`−`](## "Minus, or lighten the screen") |
| [`xyzt`](## "Cycle through or clear variables to 0") | [`4`](## "4 or D") | [`5`](## "5 or E") | [`6`](## "6 or F") | [`+`](## "Plus, or darken the screen") |
| [`sto→`](## "Store or recall variable") | [`1`](## "1 or A") | [`2`](## "2 or B") | [`3`](## "3 or C") | [`🢐 🢒≈`](## "Toggle the display result") |
| [`on`](## "Turn on or off the calculator")   | [`0`](## "0, or reset the calculator") | [`.`](## "Decimal point, or comma to separate arguments in functions") | [`(-)`](## "Toggle the sign, or recall the value of ans") | [`enter`](## "Evaluate an expression or select a menu option") |

## Calculator Operations

| Operation | Keystroke |
|-----------|-----------|
| Switch on | `on`      |
| Switch off| `2nd` `on`|
| Darken screen | `2nd` `+`|
| Lighten screen | `2nd` `-`|


## Answer Toggle

Press the `🢐 🢒≈` key to toggle the display result

| Example | Answer | Keystroke | Note |
|---------|--------|-----------|------|
| $5^2\pi$ | $25\pi$ | 5`x²` `πᵉᵢ` `enter` | Exact pi
|          | $78.53981634$ | `🢐 🢒≈` | Decimal
| $\sqrt{1+1}$ | $\sqrt{2}$ | `2nd` `x²` 1 `+` 1 `enter` | Exact square root
|              | $1.414213562$ | `🢐 🢒≈` | Decimal
| $\frac{10-1}{4}$ | $\frac{9}{4}$ | `믐` 10 `−` 1 `🡇` 4 `enter` | Fraction
|                  | $2.25$ | `🢐 🢒≈` | Decimal
|                  | $2\frac{1}{4}$ | `math` 1 `enter` | Mixed number `🢒ⁿ/d Uⁿ/d🢐 🢒`


## Examples

| Example | Answer | Keystroke | Note |
|---------|--------|-----------|------|
| $\sqrt{3^2+4^2}$ | $5$ | `2nd` `x²` 3 `x²` `+` 4 `x²` `enter`
| $100\times(1-25\%)$ | $75$ | 100 `(` 1 `−` 25 `2nd` `÷` `)` `enter` | `×` is optional

## Math Functions

You may use the arrow keys and `enter` to select a function instead of using the shortcuts

| Function| Example | Answer | Keystroke |
|---------|-------------|---------|--------|
| lcm(    | Least common multiple of 6 and 8 | $24$ | `math` `2` 6 `2nd` `.` 8 `enter`
| gcd(    | Greatest common divisor of 24 and 36 | $12$ | `math` `3` 24 `2nd` `.` 36 `enter`
| ▸Pfactor| Prime factors of 36 | $2^2\times3^2$ | 36 `math` `4` `enter`
| sum(    | Summation $\sum_{i=1}^{3}{x}$ | $6$ | `math` `5` 1 `🡆` 3 `🡆` `x` `enter`
| prod(   | Product $\prod_{i=1}^{4}{x}$ | $24$ | `math` `6` 1 `🡆` 4 `🡆` `x` `enter`

## Probability

| Function     | Example | Answer | Keystroke | Notes |
|--------------|---------|--------|-----------|-------|
| Factorial $n!=\prod_{k=1}^{n}$   | $4!$    | $24$  | 4 `!` `enter` | 
| Combinations ${}^nC_k=\frac{n!}{r!(n-r)!}$ | ${}^4C_2$ | $6$ | 4 `!` `!` 2 `enter` | Order doesn't matter |
| Permutations ${}^nP_k=\frac{n!}{(n-r)!}$ | ${}^4P_2$ | $12$ | 4 `!` `!` `!` 2 `enter` | Order matters |

## Numeric equation solver

Solve $x - 2y = -11$ when $x = 1$

| Step | Description | Keystroke |
|------|-------------|-----------|
| 1 | Select [num-solv] | `2nd` `sin` |
| 2 | Left side | `xyzt` `−` 2 `xyzt` `xyzt` `🡆` |
| 3 | Right side | `(-)` 11 `enter` |
| 4 | Variable x | 1 |
| 5 | Solve y | `🡇` `🡇` `🡆` `enter`
| 6 | Solution: $y=6$ | 
| 7 | Quit | `2nd` `mode`

## Polynomial solver

### Quadratic equation

Solve $x^2-5x+6=0$

| Step | Description | Keystroke |
|------|-------------|-----------|
| 1 | Select [poly-solv] | `2nd` `cos` |
| 2 | Select quadratic equation | `1` |
| 3 | Enter equations | 1 `🡇` |
| 4 | | `(-)` 5 `🡇` |
| 5 | | 6 `🡇` |
| 6 | Solve | `enter`
| 7 | Solutions 1: $x_1=2$ | `🡇`
| 8 | Solutions 2: $x_2=3$ | 
| 9 | Quit | `2nd` `mode`

## System of linear equations

### 2×2 system

$$
\begin{cases} 
  2x + 3y = 8 \\
  4x - y = 2
\end{cases}
$$

| Step | Description | Keystroke |
|------|-------------|-----------|
| 1 | Select [sys-solv] | `2nd` `tan` |
| 2 | Select 2×2 linear equations | `1` |
| 3 | Enter coefficients | 2 `enter` |
| 4 | | `+` 3 `enter` |
| 5 | | 8 `enter` |
| 6 | | 4 `enter` |
| 5 | | 8 `enter` |
| 6 | | `−` 1 `enter` |
| 7 | | 2 `enter` |
| 8 | Solve | `enter`
| 9 | Solutions: $x=1, y=2$ | 
| 10 | Quit | `2nd` `mode`


## Reference

1. [Guide Book](https://education.ti.com/html/eguides/scientifics/EN/TI-36X-Pro-guidebook-en.html)