# Reasoning Before Execution

Write the rule behind each case before you commit your predictions. Replace
every placeholder line below with one to three sentences that name the rule
producing that case's value, type, length, and dimensions. One rule is enough.
After you run and find a miss, add a short correction entry under that case in a
later commit.

# Ethan

## P01
Coercion converts the elements into the highest based on the coercion ladder. In this case, the double 3.5 is the highest along the coercion ladder which converts TRUE into 1.0 and 2 into the double 2.0. Grader notation saves the values as [1,2,3.5], double as the type since a vector's type is just the types of its elements, a length of 3 since it just counts the number of elements and dim=none since a vector inherently has no dimensions.

## P02
Coercion converts the elements into the highest based on the coercion ladder. In this case, the character "2" is the highest along the coercion ladder which converts the integer 1 into "1" and the logical operator TRUE into "TRUE". Grader notation saves the values as ["1","2","TRUE"], and type=character due to coercion.

## P03
Adding two atomic vectors with non-equal lengths results in recycling. Since the second vector is shorter, its values are recycled: 1 is added to 10, then 2 is added to 20, then it recycles the values of the second vector adding 1 to 30, then adds 2 to 40. This results in [11,22,31,42].

## P04
The resulting vector uses c(3L, 1L) as the index and extracts the third then the first index of c(first = 8L, second = 5L, third = 9L). It then saves both the label and the value into the resulting vector which ends up as [third=9,first=8].

## P05
The value is [4,9] because a negative index just excludes whatever is on that index.

## P06
The value is [FALSE,TRUE,TRUE,TRUE] because is.na(x) evaluates the missing status of each element and x > 10L checks the magnitude, combining into a logical mask. The type is logical because it returns the result of the comparison.

Correction: I predicted [FALSE,TRUE,TRUE,TRUE] (logical, length 4) because I thought the expression evaluated the mask and replaced elements in the vector. R printed [NA,12] (integer, length 2).

## P07
The value is [1,2,1] because factor() converts the strings "low", "high", "low" into integer codes based on their level order.

Correction: I predicted [1,2,1] for the value. R printed factor[low,high,low];levels=[low,high]. My logic for the storage type was correct (integer), but I was unaware that the grader uses a specialized notation for factors inside quote().

## P08
The value is list{scores=[3,5],label=["A"]} because a list holds items of different types. The type is list because it is a generic vector container.

## P09
The value is data.frame[2x2]{id=[1,2],passed=[TRUE,FALSE]} because a data frame is created with two columns, id and passed. The type is list because, under the hood, a data frame is actually a list of columns. The length is 2 because length() counts the number of top-level elements (the columns), not the rows. The dim is 2x2 because it carries row and column dimensions.

## P10
The value is matrix[2x3](11,22,13,24,15,26) because R adds the shorter vector c(10,20) column-by-column to the matrix.

## P11
The value is [NA] because mean() of a vector containing a missing value returns a missing value.

Correction: I predicted logical as the type because i forgot that mean() returns a double type in R.

## P12
The value is [9] because na.rm = TRUE removes the missing value, and the mean of 8 and 10 is 9.

Correction: I predicted integer as the type because i forgot that mean() returns a double type in R.

## P13
The value is [1,2.5,3] because assigning the double 2.5 into the integer vector triggers mixed-mode assignment, replacing the second element. The type is double because the mixed-mode assignment forces R to widen the entire vector to double so the new value fits.

## P14
The value is [14,0,15,8] because missing values are replaced with 0, non-missing values are doubled, and anything over 15 is set to 15.

Correction: I predicted the type would be integer because all the values in the output (14, 0, 15, 8) look like whole numbers. R printed a type of double. I misread how the coercion ladder interacts with missing values: NA_real_ is inherently a double, which forces the entire scores vector to become double from the very first line.

## P15
The value is array[2x2x2](1,2,3,4,5,6,7,8) because 1:8 generates the sequence and R fills the array column-major. The dim is 2x2x2 because the dim argument specifies[2x2x2].

## P16
The value is [] because index 0L selects nothing, returning an empty vector. The type is integer because the original vector contained integers.

# Adrienne

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

Correction: 
I predicted: value: [1,2,1]
R predicted: value: factor[low,high,low];levels=[low,high]

I misinterpreted the integer codes in factor as the value of the `c()`. Integer codes are just how the value is stored in memory, and not the actual value R will predict.

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
