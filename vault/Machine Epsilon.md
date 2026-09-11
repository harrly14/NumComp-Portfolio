Machine Epsilon, denoted as $\epsilon_{m}$, defines the physical limit of a computer's precision. It is the gap between the number 1 and the very next representable [[Floating-Point Arithmetic| floating-point]] number. It represents the maximum possible relative error introduced by a single rounding operation in the computer's hardware.

| data type | exponent bits | mantissa bits | $\epsilon_{m}$ |
| --------- | ------------- | ------------- | -------------- |
| double    | 11            | 52            | 1.11e-16       |
| single    | 8             | 23            | 5.96e-8        |
| half      | 5             | 10            | 4.88e-4        |
| bfloat16  | 8             | 7             | 3.91e-3        |
