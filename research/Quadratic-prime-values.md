# The complete list for Erdős problem 1140 under Dirichlet GRH

For a positive integer $n$ let $G(n)$ mean that $n-2a^2$ is prime for every nonnegative integer $a$ with $2a^2<n$. Under GRH for Dirichlet $L$-functions,

$$G(n)\quad\Longleftrightarrow\quad n\in\{2,5,7,13,31,61,181,199\}.$$

The original question asks whether there are infinitely many such $n$. Epure and Gica already give an unconditional negative answer, with at most one possible further value in their classification. The catalog-correction PR documents the original quantifier. The calculation here gives an alternative way to exclude every further value under the stated GRH. [Epure and Gica, Theorem 4.1 and Remark 2 on printed p. 258](https://ssmr.ro/bulletin/pdf/53-3/GicaEpure.pdf#page=8) · [Award catalog discussion](https://github.com/TheJustinSunPrize/awards/pull/4888)

## Effective bound

Putting $a=0$ shows that $n$ must be prime. For an odd prime $n$ put $L=\mathbb Q(\sqrt{2n})$. Its discriminant is $D=8n$ because the squarefree radicand $2n$ is $2\bmod 4$. Its Dedekind zeta function is $\zeta_L(s)=\zeta(s)L(s,\chi_D)$ with $\chi_D$ the quadratic Dirichlet character of conductor $D$. The RH input for this field therefore follows from Dirichlet GRH.

Apply the theorem of Grenié and Molteni with base field $\mathbb Q$, the identity class of the quadratic extension $L$ and $k=0$. The theorem gives an unramified split rational prime $\ell$ satisfying

$$\ell\le B(n)^2,\qquad B(n)=1.075\log(8n)+19.$$

Here the Galois group has order two and the identity class has size one. In particular $\ell\nmid 2n$. Splitting gives $(2n/\ell)=1$. Dividing a square root of $2n$ by $2$ modulo $\ell$ and choosing the smaller of the two positive representatives gives $1\le a\le(\ell-1)/2$ with $2a^2\equiv n\pmod\ell$. [Grenié and Molteni, theorem and its $k=0$ specialization on pp. 2–3](https://air.unimi.it/retrieve/dfa8b9a2-4b70-748b-e053-3a05fe0a3a96/45-molteni-Conditional_upper_bound_for_the_k-th_prime_ideal_with_given_Artin_symbol.pdf#page=3)

For $n\ge10^6$, the function $B(n)^4/n$ is decreasing, since its derivative has the sign of $4(1.075)-B(n)$. At $10^6$ we have $\log(8\cdot10^6)<16$, hence $B(10^6)<37$. Since $37^4=1\,874\,161<1\,999\,999$, it follows that $B(n)^4+1<2n$ throughout this range. Thus

$$2a^2+\ell\le\frac{(\ell-1)^2}{2}+\ell=\frac{\ell^2+1}{2}<n.$$

The positive integer $n-2a^2$ is a multiple of $\ell$ greater than $\ell$. It is composite, as required.

## Finite verification

The following standalone Python code checks every $1\le n<10^6$. The sieve marks all primes by crossing out multiples starting at $p^2$. For each prime $n$ the upper bound on $a$ is exactly $\lfloor\sqrt{\lfloor(n-1)/2\rfloor}\rfloor$. All operations use integers.

~~~python
from math import isqrt

limit = 1_000_000
prime = bytearray([1]) * limit
prime[0:2] = b"\0\0"
for p in range(2, isqrt(limit - 1) + 1):
    if prime[p]:
        start = p * p
        count = (limit - 1 - start) // p + 1
        prime[start::p] = bytes(count)

solutions = []
for n in range(2, limit):
    if prime[n]:
        last = isqrt((n - 1) // 2)
        if all(prime[n - 2 * a * a] for a in range(1, last + 1)):
            solutions.append(n)

assert sum(prime) == 78_498
assert solutions == [2, 5, 7, 13, 31, 61, 181, 199]
print(solutions)
~~~

The proof of the finite range includes the prime $2$, for which $a=0$ is the only eligible index. The conclusion above $10^6$ uses only the quadratic-field specialization of the cited theorem.
