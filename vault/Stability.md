---
aliases:
  - stable
  - unstable
  - stability
---
Stability is a property of the algorithm, not the underlying math. If an algorithm is unstable, you can restructure it to make it stable.

Stability: getting nearly the right answer to nearly the right question

Backward stability: getting exactly the right answer to nearly the right question. Backward stability is generally the best we can hope for in numerical computation. Every backward stable algorithm is stable, but not every stable algorithm is backward stable.

If an algorithm is backward stable, its relative error is bounded by the problem's [[Conditioning|condition number]] and [[Machine Epsilon]]. Relative error is less than or equal to relative condition number multiplied by machine epsilon.

It is rarely possible for an algorithm to be backward stable when the output space is higher-dimensional than the input space.

One issue that causes instability is subtracting two very similar floating-point numbers. This destroys relative accuracy by cancelling out leading digits and leaving behind only noise. When an algorithm leads to cancellation, you must restructure the algorithm algebraically. Using more precise data types masks the symptoms without fixing the underlying issue.