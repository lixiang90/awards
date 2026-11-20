# A uniform lower bound for least prime factors in short intervals

**JSP-000375 · Erdős problem 462 · 21 November 2026**

Let $P^-(m)$ be the least prime divisor of $m>1$. Assume the Riemann hypothesis for the Riemann zeta function. There are absolute constants $C,c>0$ and $x_0$ such that every real $x\ge x_0$ satisfies

$$
\sum_{\substack{x<m\le x+C\sqrt{x}(\log x)^2\\m\ \mathrm{composite}}}
       \frac{P^-(m)}{m}\ \ge c .
$$

In fact it suffices to count products of two distinct primes $p<q$ with $\sqrt{x}/2<p\le 3\sqrt{x}/4$ and $4\sqrt{x}/3<q\le 3\sqrt{x}$. The constant $C$ is chosen once for all $x$. All logarithms are natural. This implies the lower bound in the prize catalog and also covers the inclusive lower endpoint in Erdős and Graham's formulation. [Erdős and Graham, printed p. 92](https://mathweb.ucsd.edu/~ronspubs/80_11_number_theory.pdf#page=88) · [JSP-000375](https://github.com/TheJustinSunPrize/awards/blob/10e0ab6e7503b6db769029d7d68cc4ca42c011d7/problems/catalog-0301-0400.md#JSP-000375)

## Proof

Write $\psi(t)=\sum_{n\le t}\Lambda(n)$, where $\Lambda$ is the von Mangoldt function. The Selberg integral bound under RH gives an absolute $K>0$ such that, for large $X$ and $1\le h\le X$,

$$
\int_0^{3X}\!|\psi(t+h)-\psi(t)-h|^2\,dt
       \le K Xh(\log X)^2. \tag{1}
$$

Indeed the fixed-length bound up to $Y$ is $O(Yh\log^2(2Y/h))$ for $1\le h\le Y$. Take $Y=3X$. [Goldston and Suriajaya, equations (15) and (17)](https://arxiv.org/pdf/2110.14250#page=4) · [Saffari and Vaughan](https://doi.org/10.5802/aif.649)

Fix $A=1+640K$. Set $X=\sqrt{x}$, $H=A(\log X)^2$ and $h=H/2$. In all that follows $X$ is sufficiently large for this fixed $A$. Put $J=\lfloor X/(4H)\rfloor$. For $0\le j<J$ let

$$
u_j=X/2+jH,\qquad v_j=x/u_j,\qquad
I_j=(u_j,u_j+H],\qquad Q_j=(v_j,v_j+H].
$$

The intervals $I_j$ are disjoint and lie in $(X/2,3X/4]$. The intervals $Q_j$ lie in $(4X/3,3X]$ and are disjoint, since consecutive left endpoints are separated by

$$v_j-v_{j+1}=\frac{X^2H}{u_ju_{j+1}}\ge\frac{16}{9}H.$$

Every pair $p\in I_j,\ q\in Q_j$ satisfies $x<pq\le x+4XH$. Indeed $u_jv_j=x$ and $(u_j+H)(v_j+H)-x=H(u_j+v_j+H)\le4XH$ for large $X$. Thus each rectangle of paired intervals lies inside the required product range.

Call a bin $(b,b+H]$ deficient if $\psi(b+H)-\psi(b)<H/4$. For each $t\in[b,b+h]$ its subinterval $(t,t+h]$ then has $\psi$-mass less than $H/4=h/2$. The integral in (1) over $[b,b+h]$ is at least $H^3/32$. Summing over either disjoint family gives at most $16KX(\log X)^2/H^2$ deficient bins per family. Consequently, at most

$$
32K\frac{X(\log X)^2}{H^2}
 =\frac{32K}{A}\frac XH
 <\frac{X}{20H}
$$

indices have a deficient bin on either side. Also discard every index for which either bin contains a proper prime power $r^k$, $k\ge2$. Below $3X$ there are $O(\sqrt X\log X)$ such powers, by counting bases and exponents. Each belongs to at most one bin per family. The number of indices discarded here is $o(X/H)$ and hence at most $X/(20H)$ for large $X$. Since $J\ge X/(5H)$ eventually, at least $X/(10H)$ indices remain.

For every remaining index each bin contains at least $H/(4\log(3X))$ primes, since its $\psi$-mass is at least $H/4$ and consists entirely of primes of weight at most $\log(3X)$. Each product $m=pq$ so obtained has $p<q$. Its contribution is $1/q\ge1/(3X)$. Unique factorization and disjointness of the $I_j$ count every product once. We conclude that

$$
\sum_{\substack{x<m\le x+4XH\\m\ \mathrm{composite}}}\frac{P^-(m)}m
 \ge \frac{X}{10H}
       \left(\frac{H}{4\log(3X)}\right)^2\frac1{3X}
 =\frac{H}{480\log^2(3X)}
 \ge\frac A{1920}.
$$

Here $\log(3X)\le2\log X$ for $X\ge3$. Finally $4XH=A\sqrt{x}(\log x)^2$. Taking $C=A$ and $c=A/1920$ proves the theorem. All bounds are uniform in the starting point $x$.

## Sources and attribution

The question is due to Paul Erdős and Ronald Graham. The short-interval mean-square theorem is classical. Xu Zhang's October 2026 revision gives a uniform result under its bounded-fluctuation Hypothesis 1.5. The paired intervals above use only the ordinary RH input (1). The large constant permitted by the original question makes the union of the two exceptional sets small enough. [Zhang, Hypothesis 1.5 and Theorem 1.7](https://arxiv.org/html/2608.24930v2#S1)

Levent Alpöge announced an upstream proof with Claude on 20 November 2026. The pinned Lean entry explicitly states the ordinary RH used here. This deduction takes that theorem as an input and has not independently checked the upstream development. The downstream argument was developed with OpenAI Codex for the submitting GitHub account lixiang90. Verification of the upstream result, the downstream reasoning and priority is requested from the prize reviewers. [Alpöge's announcement](https://alpo.ge/remark.pdf) · [Pinned upstream theorem](https://github.com/CocoSgt/riemann-hypothesis-lean/blob/7cbf7a0c32fca1badf05931879a37c3f8a2b03b4/src/Main.lean#L4)
