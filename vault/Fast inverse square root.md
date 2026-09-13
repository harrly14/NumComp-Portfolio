Fast inverse square root was an algorithm to quickly estimate $\frac{1}{\sqrt{ x }}$ for the video game Quake 3. The code is: 

```c
float Q_rsqrt( float number )
{
	long i;
	float x2, y;
	const float threehalfs = 1.5F;

	x2 = number * 0.5F;
	y  = number;
	i  = * ( long * ) &y;                       // evil floating point bit level hacking
	i  = 0x5f3759df - ( i >> 1 );               // what the fuck?
	y  = * ( float * ) &i;
	y  = y * ( threehalfs - ( x2 * y * y ) );   // 1st iteration
//	y  = y * ( threehalfs - ( x2 * y * y ) );   // 2nd iteration, this can be removed

	return y;
}
```

This algorithm works by treating the problem as a rootfinding problem and running one iteration of [[Newton's method]] on a really good initial guess. 

The line `i  = * ( long * ) &y;` converts the initial number to a 32-bit integer. The next line `i  = 0x5f3759df - ( i >> 1 );` first right shits the integer, which (due to the way floating-points are interpreted) leads to dividing the exponent of the initial number by 2, and then subtracts that from `0x5f3759df`. This magic number constant is chosen so that the upper part of the constant encodes for the exponent bias adjustment needed and the lower part helps fine-tune the mantissa. These two steps combine to create a really good initial guess (at least for the hardware at the time) for the answer. Finally, the algorithm uses an optimized version of $g(x)$ from Newton's Method to get closer from the initial guess to the right answer. The final line would run another iteration of Newton's Method, but it commented out because the approximation was already good enough for the purposes.