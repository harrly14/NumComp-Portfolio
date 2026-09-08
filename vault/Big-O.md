Big-O notation is a tool used to describe limiting behavior of a function. In numerical computation, it is specifically used to quantify how rapidly an approximation error shrinks as a step size approaches zero.

The standard CS use of big-O is the limit as $n$ approaches infinity. This often measures time or memory cost and is dominated by the term with the biggest exponent. In numerical computation, we look the opposite way. We look at the limit as a step size $h$ approaches zero. 

An $O(n^{2})$ algorithm means that as a dataset gets massive, the execution time grows proportionally to the square of the input size. You want the exponent to be as small as possible.

An $O(h^{2})$ approximation means that as the step size gets extremely small, the error shrinks proportionally to the square of the step size. You want the exponent to be as big as possible.

The polynomial scaling of error directly dictates an algorithm's rate of [[Convergence|convergence]].