## Complicity

### Quicksort

最好情况每次二分，最好时间复杂度$O(nlogn)$推导

$$
\begin{align*}
T(N) &= 2T(N/2) + O(N) = 2T(N/2) + cN \\
T(N)/N &= T(N/2)/(N/2) + c \\
T(N/2)/(N/2) &= T(N/4)/(N/4) + c \\
\downarrow \\
T(N)/N &= T(1)/1 + clogN \\
T(N) &= cNlogN = \mathcal{O}(NlogN)
\end{align*}
$$
平均复杂度推导
$$
\begin{align*}
T(N) &= sum(T(i) + T(n-i) + cN) \\
	 &= \frac{2}{N}\left[\sum_{j=0}^{\mathrm{N}-1} T(j)\right]+c N \\
N T(N) &= 2\left[\sum_{j=0}^{N-1} T(j)\right]+c N^{2} \\
(N-1) T(N-1) &= 2\left[\sum_{j=0}^{N-2} T(j)\right]+c(N-1)^{2} \\
&相减 \\
N T(N)-(N-1) T(N-1)&=2 T(N-1)+2 c N-c \\
&移项 \\
N T(N)&=(N+1) T(N-1)+2 c N \\
\\
\frac{T(N)}{N+1} &= \frac{T(N-1)}{N}+\frac{2 c}{N+1} \\
\frac{T(N-1)}{N} &= \frac{T(N-2)}{N-1}+\frac{2 c}{N} \\
&\vdots \\
\frac{T(2)}{3} &= \frac{T(1)}{2}+\frac{2 c}{3} \\
&累和 \\
\frac{T(N)}{N+1} &= \frac{T(1)}{2}+2 c \sum_{i=3}^{N+1} \frac{1}{i} \\
				 &= O(\sum \frac{1}{i}) \\
				 &= O(lnN) \\
T(N) &= O(NlogN)
\end{align*}
$$


### Quicksearch

仍然是每次二分，但只去遍历一边，最好时间复杂度$O(nlogn)$推导
$$
\begin{align*}
T(N) &= T(N/2) + cN \\
T(N/2) &= T(N/4) + cN/2 \\
\downarrow \\
T(N) &= T(1) + cN(1+1/2+1/4+ .. ) \\
	 &= 2cN = \mathcal{O}(N)
\end{align*}
$$
