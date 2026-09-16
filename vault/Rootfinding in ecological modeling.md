The below writeup refer's to the research of my friend and colleague, Logan Jones and uses it as a jumping off point to understand **some** of how numerical computation is used in ecological modeling. This writeup is in no way designed to be comprehensive or exhaustively say how the two fields interact, as I'm sure there are many many ways they do. Instead, I focus in on a couple annotations I made on his research poster (below) and the concepts and connections I learned from those threads. You can also find a digital twin of Logan's research poster here: [https://loganmjones.github.io/CAD-CADP-explorer/](https://loganmjones.github.io/CAD-CADP-explorer/?utm_source=chatgpt.com)

![[Logan's poster marked up.png]]
(image is blurry/unreadable due to file size constraints. sorry!)

# Stability, stability, and stability
Logan's poster points at two different meanings of stability distinct from the definition of [[Stability|numerical stability]] we learned in class. Directly in the poster, he referrences "structural stability," and he alludes to another concept of stability called "dynamical stability" often used in the field of ecological modeling. These three definitions are each distinct, but also similar.[^1]

To understand what those other uses of stability meant, I looked into how stability is discussed in ecological modeling. What I learned was that ecological literature distinguishes between perturbing the state of a system, such as species abundances, and perturbing the parameters or conditions under which the system exists.[^2] This distinction helped me separate dynamical and structural stability from the numerical stability we have talked about in class.

As we have learned in class, stability is often used in Numerical Computation to describe an algorithm getting nearly the right answer to nearly the right question (or in the case of backward stability getting exactly the right answer to nearly the right question). In numerical stability, you perturb a computation slightly and ask if the algorithm still gets an accurate result.

Dynamical stability asks a different question about the modeled system. In ecological models, a dynamically stable state is one that the system returns to after being perturbed. Ecological literature distinguishes this from structural stability, which instead asks whether coexistence persists as the conditions or model parameters change. [^2]

Structural stability is particularly important for Logan's project and is defined as an ecosystem being able to survive in a wide range of thermal conditions. This is consistent with ecological uses of structural stability as the range or volume of parameter space compatible with coexistence.[^1][^2]

| stability type       | what is being perturbed                     | what is being changed                             |
| -------------------- | ------------------------------------------- | ------------------------------------------------- |
| numerical stability  | numerical inputs                            | algorithm output                                  |
| dynamical stability  | ecosystem state (like population densities) | trajectory returns toward the same state or cycle |
| structural stability | environmantal parameters                    | viable community structure or coexistence         |
All three of these ideas involve a robustness against change, but the thing that is being changed is different. This distinction is important as structural stability is not just numerical stability applied to ecology. 
# Seasonal limit cycles as a rootfinding problem
Part of Logan's research project involved first simulating an ecological community until its densities reached a certain stable cycle called a limit cycle. This problem can be viewed as a [[Rootfinding]] problem. [^1]

Call the entire state of a community $x_k$ at some point in time $k$. A function $f(x)$ could represent the community one season later. When a stable season cycle is reached, $f(x^*) = x^*$. If we set $g(x) = f(x) - x$, we get $g(x) = 0$ when a stable season cycle is reached, which is rootfinding!

Additionally, the whole part of finding the stable season cycle can then be viewed as $x_k+1 = f(x_k)$, which is literally just [[Fixed-Point Iteration]]!

Moreover, this gives a bit of a connection to dynamical stability. In the fixed point iteration we studied, if each iteration moves values closer to the fixed point, then the iteration converges. In Logan's model the same basic question can be applied: if the community begins slightly away from the seasonal cycle, do the next seasons bring it back toward that cycle? The [[Convergence|convergence]] of fixed-point in this case also seems to be a usefal way of understanding the idea behind dynamical stability.[^2][^3]

I don't have a background with differential equations, and things quickly got out of my depth the more I tried to look into this, so I'm sure there's a lot more here that I'm only scratching the surface of.

# Continuation is repeated rootfinding as a parameter chagnes
To understand what Logan meant by "continuation," I read a bit of Anthony Yeates' explanation of parameter continuation. From what I learned, continuation involves following a branch of solutions to an equation of the form $g(x, \lambda) = 0$ while changing the parameter $\lambda$.[^4] Yeates first describes a simpler version where the parameter is changed by a small amount and the previous solution is used to start the next rootfinding calculation, which made the connection to rootfinding much clearer to me.[^4]

Figure 4 makes another connection to rootfinding. Logan changes the seasonal temperature amplitude T\_{amp} and uses continuation to trace how evolutionarily stable communities change with it.[^1]

Suppose that the conditions defining one of these solution was represented by 

$$g(x, t\_{amp} = 0)$$
At a particular value of $T\_{amp}$, finding the community means solving this rootfinding problem. Continuation then changes $T\_{amp}$ slightly and solves that new rootfinding problem. Information from one solution can be used to help find the next since similar parameter values often have similar solutions. Basic parameter continuation does this by using a previous solution as the starting point for the next root solve.[^4]

# Bifurcation Theory
After learning about continuation, I looked into bifurcation theory to understand what the resulting diagram was showing. The lecture notes I found describe bifurcations as "qualitative" changes in a system's dynamics as a parameter is changed, including fixed points being created, destroyed, or changing stability.[^5] 

Continuation also explains why Figure 4 is called a bifurcation diagram. A bifurcation occurs when changing a parameter causes a "qualitative" change in the solutions or their stability. One rootfinding example is $x^{2} - p =0$. For $p <0$ there are no real roots, for $p=0$ there is one root, and for $p > 0$ there are two. Where $p=0$, the structure of the solution set changes. A bifurcation diagram records this kind of change by plotting solutions against the parameter that is being changed.[^5]

Logan' Figure 4 can be interpreted through this framework of bifurcation, although the underlying ecological model is likely more complicated. The plotted trait branches show how the evolutionary stable community changes as $T_{amp}$ changse. Branches separate, disappear entirely, or become unstable in different regions.[^1]

From a numerical computation perspective, bifurcation analysis extends the rootfinding question. Instead of asking "where is a root", we ask "how do the roots and their stability change as a parameter changes." Numerical continuation provides a way to answer that question computationally. [^4][^5]


[^1]: Jones, Logan. *Predation, turnover & structural stability — Interactive Digital Twin*. https://loganmjones.github.io/CAD-CADP-explorer/

[^2]: Grilli, Jacopo, et al. "Feasibility and coexistence of large ecological communities." *Nature Communications* 8, 14389 (2017). https://doi.org/10.1038/ncomms14389

[^3]: Mushtaq, Asif. *Solving non-linear equations: Fixed point iterations*. NTNU course notes. https://wiki.math.ntnu.no/_media/ma2501/2016v/fixedpoint.pdf

[^4]: Yeates, Anthony. "Parameter continuation." November 8, 2018. https://maths.dur.ac.uk/users/anthony.yeates/posts/continuation.html

[^5]: *PH4208: Nonlinear Dynamics — Lecture Notes on Bifurcation*. January 10, 2014. https://students.iiserkol.ac.in/~mms15ms051/courses/PH4104/Lecture_Notes_on_Bifurcation.pdf