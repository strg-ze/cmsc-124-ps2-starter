# Reasoning Before Execution

Write the rule behind each case before you commit your predictions. Replace
every placeholder line below with one to three sentences that name the rule
producing that case's value, type, length, and dimensions. One rule is enough.
After you run and find a miss, add a short correction entry under that case in a
later commit.

## P01
The coercion ladder runs logical, integer, double, character. The third value
is a double, so the `TRUE` becomes `1` and the integer `2` becomes double. The value is
[1,2,3.5] with length three and no dimensions.


## P02
The coercion ladder runs logical, integer, double, character. The second value
is a string, so the `1L` becomes `"1"` and the `TRUE` becomes `"TRUE"`. The value is
["1","2","TRUE",] with length two and no dimensions.


## P03
R applies most arithmetic operators element by element and if one operand is shorter, R repeats (recycles) it. So `1` is added to `10`, `2` is added to `20`, then repeats as `1` is added to `30` and `2` is added to `40`. The type is still integer, the value is [11,22,31,42] with length four and no dimensions.


## P04
A vector can be named and positive indices select positions. `[c(3L,1L)]` selects position 3 and 1.Since `first=8L` is simply naming, the type is still integer, the value is [third=9,first=8] with length two and no dimensions. 

## P05
Negative indices exclude positions. `[-2L]` includes all positions but position 2. The type is still integer, the value is [4,9] with length 2 and no dimensions.

## P06
A logical index selects positions where the corresponding logical value is TRUE, and the single bar in `a|b` computes logical OR at every position. For the second element `NA_integer_`, is.na() is TRUE and NA_integer > 10L evaluates to NA, TRUE|NA is TRUE, so its index is selected. For the third element, `12L` is not NA but it's greater than 10, FALSE|TRUE is TRUE, so its index is selected.

## P07
A factor stores integer codes and carries a set of level labels. `"low"` becomes code 1 and `"high"` becomes code 2. In c("low", "high", "low") it points to the integer code [1,2,1].

## P08
A list can have elements with any type. 

## P09
A data frame is a list with a constraint that the length of each of its vectors must be the same. With 2 vectors, each with 2 elements in P09, this gives a dimension of 2x2.

## P10
A matrix is an atomic vector with a dim attribute. `1:6` creates integers from 1 to 6 with 2 elements for each row. This reuses the recycling rule from P03 for addition.

## P11
NA is a missing value and arithmetic with a missing operand usually produces a missing result. So, the value is NA and the type comes from the operands which is a double.

## P12
mean() accepts an  `na.rm` argument that removes missing values. This way NA_real_ is removed and the mean of 8 and 10 is evaluated which is 9. The type comes from the operands which is a double.

## P13
Integers from 1 to 3 is mapped to x. Position 2 is selected and the value in this position is changed to 2.5. The coercion ladder changes the type from integer to double when 2.5 was added to the vector.

## P14
ifelse(test, yes, no) makes one choice per position and takes the value from yes where test is TRUE and no from where test is FALSE. Adjusted values higher than 15 are changed to 15. Since the operands are double, the type remains a double.

## P15
Array 1:8 creates a vector with integers from 1 to 8 with dimensions 2x2x2. 

## P16
R indices begin at 1. Index 0 selects nothing and returns a zero length result of the same atomic type.
