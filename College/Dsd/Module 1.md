# Introduction to Digital System Design

==Founded by George Bool (1815-1864)==
## Two types
### Analog system design
it's input varies continuously. Analog system uses physical waves to traverse and is calculated using sine waves.
### Design system design
It's output varies in discrete levels. These levels are one of either two states, those are,
- High State - 1,
- Low State - 0.
These are calculated with Square waves. 

| Analog Signals                         | Digital Signals                       |
| -------------------------------------- | ------------------------------------- |
| Continuous and Time Varying            | Can only exist in two states (1 or 0) |
| Difficult Troubleshooting              | Easy Troubleshooting                  |
| Easily affected by environmental noise | Stable and less prone to noise        |
| Uses more power                        | Uses Less power                       |
| In the form of Sine wave               | In the form of Square wave            |

***
# Logic Gates
These uses Three basic operations, they are
- Sum - (+)
- Product - (\*)
- Complement (A\`)

## AND Gate

| | TruthTable | |
| ---------- | --- | ------ |
| A          | B   | Y |
| 0          | 0   | 0      |
| 0          | 1   | 0      |
| 1          | 0   | 0      |
| 1          | 1   | 1       |

## OR Gate

| | TruthTable |     |
| ----- | ---------- | --- |
| A     | B          | Y   |
| 0     | 0          |0     |
| 0     | 1          |1     |
| 1     | 0          |1     |
| 1     | 1           |   1  |

***
# Boolean Algebra
## Variable
A symbol that represent a logical quantity.
## Complement
The Inverse of that Variable.
## Literal
A Variable or a Complement. 

### Boolean Addition
Equivalent to OR operation. 

***
***
# Note
In the concept of Sum and Carry, 

| A   | B   | Sum | Carry |
| --- | --- | --- | ----- |
| 0   | 0   | 0   | 0     |
| 0   | 1   | 1   | 0      |
| 1   | 0   | 1     | 0      |
| 1   | 1   | 0    | 1      |

since for the first three values, Addition of A and B results in either 0 or 1 which is readily available to be represented in binary values (0 and 1) and there's no carry.

But in the case of A = 1 and B = 1,
Addition of A and B results in 2, which should be converted to it's binary form **1 O**
$$ 1+1 = 2 =  (1)2^1 + (0)2^0 = 1 0 $$
So, 1 is taken as carry and 0 is considered as the sum of A and B.
***
***
## Basic laws
### Commutative laws
- Addition 
$$ A+B = B+A $$
- Multiplication 
$$ AB = BA $$
### Associative laws
- Addition 
$$ A + (B+C) = (A + B) + C $$
- Multiplication 
$$ A(BC) = (AB)C $$
### Distributive Law
$$ A(B+C) = AB + AC $$
## Rules of Boolean Algebra

| Rules                 |                            |
| --------------------- | -------------------------- |
| $$ A + 0 = A  $$            | $$ A * A = A $$           |
| $$ A + 1 = 1     $$         | $$ A * \bar{A} = 0 $$          |
| $$ A * 0 = 0       $$      | $$ \bar{\bar{A}} = A $$    |
| $$ A * 1 = A $$            | $$ A + AB = A $$           |
| $$ A + A = A $$             | $$ A + \bar{A}B = A + B $$ |
| $$ A + \bar{A} = 1 $$ | $$ (A + B)(A + C) = A + BC $$ |

## Demorgan's Theorem
$$ \overline{XY} = \overline{X} + \overline{Y} $$
$$ \overline{X + Y} = \overline{X}*\overline{Y} $$

***
#  K-map (Karnaugh Map)
Intended to represent the function in it's Sum of Products form
#### Always try to group the highest component,
- Octet (8) --> 1 literal
- Quad (4) --> 2 literals
- Pair (2)   --> 3 literals
- Cell (1)    --> 4 literals

### Example

$$ 00 = \overline{AB} $$
$$ 01 = \overline{A}B $$
$$ 11 = AB $$
$$ 10 = A\overline{B} $$

$$  \overline{ABCD} + \overline{AB}C\overline{D}+ A\overline{B}\overline{CD} + A\overline{B}C\overline{D} = \overline{ABD}(C+\overline{C}) + A\overline{BD}(C+\overline{C}) $$
$$ \overline{ABD} + A\overline{BD} = \overline{BD}(A+\overline{A})   $$
$$ = \overline{BD} $$
## Code Conversion 

#### Binary to Gray code 
==11011==

- write the M.S.B directly,
$$ = 1  $$
- xor the digits with each other starting from the most significant bit,
$$ 1 \oplus 1 \oplus 0 \oplus 1 \oplus 1 $$
$$ 1 \oplus 1 = 0, $$
$$ 1 \oplus 0 = 1, $$
$$ \ 0 \oplus 1 = 1, $$
$$ 1 \oplus 1 = 0, $$
so the answer from binary to gray code is
$$ 11011 \implies 1 0 1 1 0  $$
#### Gray code to binary
==0101110==

- write the M.S.B directly,
$$ = 0 $$
- xor the answer with the next digit in the question,
$$ 0 \oplus 1 = 1 $$
$$ 1 \oplus 0 = 1 $$
$$ 1 \oplus 1 = 0 $$
$$ 0 \oplus 1 = 1 $$
$$ 1 \oplus 1 = 0 $$
$$ 0 \oplus 0 = 0 $$
so the answer form gray code to binary is,
$$ 0101110 \implies 0110100 $$

### Don't care Conditions
don't care boxes are represented with a cross within them, This means that they can't be ignored from grouping if they don't help us in pairing a higher form of grouping than that's currently possible

***
# Half Adder
- 2 inputs, 2 outputs, Sum and Carry
### Truth Table
| A   | B   | Sum | Carry |
| --- | --- | --- | ----- |
| 0   | 0   | 0   | 0     |
| 0   | 1   | 1   | 0     |
| 1   | 0   | 1   | 0     |
| 1   | 1   | 0   | 1     |

### K-map 
- Sum
$$ Y = \overline{A}B + A\overline{B} $$
- Carry
$$ Y = AB $$
# Full Adder
- 3 inputs, 2 outputs, Sum and Carry
### Truthtable

| A   | B   | C   | Sum | Carry |
| --- | --- | --- | --- | ----- |
| 0   | 0   | 0   | 0   | 0     |
| 0   | 0   | 1   | 1   | 0     |
| 0   | 1   | 0   | 1   | 0     |
| 0   | 1   | 1   | 0   | 1     |
| 1   | 0   | 0   | 1   | 0     |
| 1   | 0   | 1   | 0   | 1     |
| 1   | 1   | 0   | 0   | 1     |
| 1   | 1   | 1   | 1   | 1      |

### K-map
- Sum
$$ Y = A\overline{BC} + \overline{AB}C + ABC + \overline{A}B\overline{C} $$
$$ = \overline{B}(A\overline{C} + \overline{A}C) + B(AC + \overline{AC}) $$
Now, 
$$ A\overline{C} + \overline{A}C = A \oplus C $$
and,
$$ AC + \overline{AC} = A \overline{\oplus} C$$
so this can collectively be written as,
$$ Y = \overline{B}(A \oplus C) + B(\overline{A \oplus C}) $$
$$ \implies B \oplus A \oplus C = A \oplus B \oplus C $$
- Carry
$$ Y = AB + BC + AC $$

# Half Subtractor
- 2 inputs, 2 outputs, Difference and Borrow
## Truthtable

| A   | B   | Difference | Borrow |
| --- | --- | ---------- | ------ |
| 0   | 0   | 0          | 0      |
| 0   | 1   | 1          | 1      |
| 1   | 0   | 1          | 0      |
| 1   | 1   | 0          | 0      | 
$$ Difference = A \oplus B $$
$$ Borrow = \overline{A}B $$
# Full Subtractor
- 3 inputs, 2 outputs, Difference and Borrow
## Truthtable

| A   | B   | C   | Difference | Borrow |
| --- | --- | --- | ---------- | ------ |
| 0   | 0   | 0   | 0          | 0      |
| 0   | 0   | 1   | 1          | 1      |
| 0   | 1   | 0   | 1          | 1      |
| 0   | 1   | 1   | 0          | 1      |
| 1   | 0   | 0   | 1          | 0      |
| 1   | 0   | 1   | 0          | 0      |
| 1   | 1   | 0   | 0          | 0      |
| 1   | 1   | 1   | 1          | 1       |

## K-map
- Difference
$$ Difference = A \oplus B \oplus C $$
- Borrow
$$ Borrow = \overline{A}B + BC + \overline{A}C $$
***
# Shifters

##### ==Left Shifters for all the below types are the same==
### Left Shifter

## Logical Shifters

- Right Shifter

## Arithmetic Shifters
- Right Shifter

## Barrel Shift
- Right Shifter
