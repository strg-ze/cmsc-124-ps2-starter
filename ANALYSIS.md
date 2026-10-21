# Vector and Scalar Evaluation

##Trace of clean_scores_scalar:
Using the sample from the analysis.R: c(Ada = 8, Grace = NA_real_, Linus = 12, Barbara = 4), the scalar version makes evaluation order visible as the loop steps through the vector one index at a time. The loop reaches Grace at the second iteration. At that step, the loop extracts her single element, is.na(value) evaluates to TRUE, and her element is assigned 0 before the loop moves on to Linus and Barbara.

##Trace of clean_score_vector:

## 1. Which operations in the vector version act on all elements at once?

## 2. Where does the scalar loop make evaluation order visible?
The evaluation order becomes visible inside the loop body, specifically at the line value <- scores[[i]]. Because the loop iterates using seq_along(scores), you can stop a debugger at that exact line and see it evaluate the vector element by element: i=1 for Ada, i=2 for Grace, i=3 for Linus, and i=4 for Barbara. Unlike the vector version which applies masks to the whole vector at once, the scalar code explicitly references a single index [[i]], making the sequence of individual evaluations visible step-by-step.

## 3. Give one concrete input where careless recycling would change the answer.

## 4. Which implementation would you keep in an R program, and what tradeoff does that choice make?
I would keep the vectorized implementation (clean_scores_vector) in an R program because it is idiomatic, requires fewer lines of code, and runs much faster on large datasets. The tradeoff is readability and memory: the vector code creates temporary whole-vectors in the background, which can be harder for beginners to read and uses slightly more memory.