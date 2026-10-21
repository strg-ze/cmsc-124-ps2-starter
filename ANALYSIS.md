# Vector and Scalar Evaluation

## Trace of `clean_scores_scalar`:
Using the sample from the analysis.R: c(Ada = 8, Grace = NA_real_, Linus = 12, Barbara = 4), the scalar version makes evaluation order visible as the loop steps through the vector one index at a time. The loop reaches Grace at the second iteration. At that step, the loop extracts her single element, is.na(value) evaluates to TRUE, and her element is assigned 0 before the loop moves on to Linus and Barbara.

## Trace of `clean_scores_vector`:
1. `out <- scores * 2` gives `16, NA, 24, 8`. The NA and names are preserved.
2. `is.na(scores)` returns `F, T, F, F`. Replacing the flagged values with `0` gives `16, 0, 24, 8`.
3. `out > 20` returns `F, F, T, F`. Replacing the flagged values with `20` through it gives `16, 0, 20, 8`.


## 1. Which operations in the vector version act on all elements at once?
Since there is no loop, all operations act on all elements at once. `scores * 2` doubles them all, `is.na(scores)` and `out>20` test them all, and the index assignments replace all the flagged values at once.

## 2. Where does the scalar loop make evaluation order visible?
The evaluation order becomes visible inside the loop body, specifically at the line value <- scores[[i]]. Because the loop iterates using seq_along(scores), you can stop a debugger at that exact line and see it evaluate the vector element by element: i=1 for Ada, i=2 for Grace, i=3 for Linus, and i=4 for Barbara. Unlike the vector version which applies masks to the whole vector at once, the scalar code explicitly references a single index [[i]], making the sequence of individual evaluations visible step-by-step.

## 3. Give one concrete input where careless recycling would change the answer.
Given the sample, `scores * 2`, if it is carelessly written as `scores * c(2, 1)`, the multiplier vector has length 2 but `scores` has length 4, so R recycles it to `2, 1, 2, 1`. Now only Ada and Linus are doubled, and Barbara's stays 4 instead of becoming 8, and Grace stays NA. 

## 4. Which implementation would you keep in an R program, and what tradeoff does that choice make?
I would keep clean_scores_vector() because it is idiomatic, shorter, and runs in compiled code, so it is much faster on large datasets. The tradeoff is that it relies on every mask and operand having the right length, since R recycles silently, and on the NA fix running before the cap. The scalar version avoids that by handling one value at a time, but it is slower on large inputs and does more work in R code.
