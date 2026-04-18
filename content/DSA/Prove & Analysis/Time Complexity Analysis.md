Review of time limit:

$f= O(g)$ (**Big-O**): $\exists k \in \R_{0},(\exists n_0 \in \N(\forall n\in \N. (n > n_0\implies f(n)\le kg(n))))$

-   we can use big-O to describe functions' **upper bound** by some common function where as larger input there exists such $k$ times the function upper the current function
-   aka $f \le g$

$f = \Omega(g)$ (**Big-Omega**): $\exists k \in \R_{>0},(\exists n_0 \in \N(\forall n\in \N. (n > n_0\implies f(n)\ge kg(n))))$

-   we can use big-Omega to describe functions' **lower bound** by some common function where as larger input there exists such $k$ times the function lower the current function
-   $f\ge g$

 $f = \Theta(g)$ (**Big-Theta**): $\exists k_1,k_2 \in \R_{>0},(\exists n_0 \in \N(\forall n\in \N. (n > n_0\implies k_1g(n)\le f(n)\le k_2g(n))))$

-   There exist another function bounded function in some area $k_1,k_2$ as larger input
-   $f=O(g) \land f = \Omega(g)\iff f = \Theta(g)$
-   $f\approx g$

$f = o(g)$ (**Little-o**): $\forall k \in \R_{>0},(\exists n_0 \in \N(\forall n\in \N. (n > n_0\implies f(n) < kg(n))))$

$f = \omega(g)$ (**Little-omega**): $\forall k \in \R_{>0},(\exists n_0 \in \N(\forall n\in \N. (n > n_0\implies f(n) > kg(n))))$

$log$ in time limit analysis is always stand for $log_2$ and we always use $\varphi$ to present the golden ratio

$1 < log(n) < n^{0.001} < n < nlog(n) < n^{1.001} < n^{1000} < 1.001^{n} < 2^n$ for $lim_{n\to \infty}$
