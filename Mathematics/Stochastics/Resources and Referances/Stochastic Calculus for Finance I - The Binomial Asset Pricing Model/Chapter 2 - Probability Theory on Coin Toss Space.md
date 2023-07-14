**Finite Probability Space**: is a space where we have a finite amount of outcomes

In context we define a set of elements of outcomes, such as a series of possible coin flips. 

$$
\Omega = \{HHH,HHT,HTH,HTT,THH,THT,TTH,TTT\}
$$
We can defined the probability of $H$ as $p$ and the probability of $T$ as $q$, where $q = 1 - p$. We can define the individual elements as $w$(where a sequence of three tosses would be $w = w_1w_2w_3$). The example of $\Omega$ independent elements we could define the probability as follows.

$$
\begin{align}
\mathbb{P}(HHH) &= p^3, \mathbb{P}(HHT) = p^2q, \mathbb{P}(HTH) = p^2q, \mathbb{P}(HTT) = pq^2 \\
\mathbb{P}(THH) &= p^2q, \mathbb{P}(THT) = pq^2, \mathbb{P}(TTH) = pq^2, \mathbb{P}(TTT) = q^3
\end{align}
$$
We can then define a subset of probabilities such that 
$$
"First\ Toss\ is\ Heads" = \{w\in \Omega;w_1=H\} = \{HHH, HHT, HTH, HTT\}
$$
This can then to define the probability as follows
$$
\begin{align}
\mathbb{P}(First\ Toss\ is\ Heads)&=\mathbb{P}(HHH) + \mathbb{P}(HHT) + \mathbb{P}(HTH) + \mathbb{P}(HTT)\\ &= p^3 + p^2q + p^2q+pq^2\\ &= p^2(p+q) + pq(p+q) \\
&=p^2 + pq \\
&=p(p+q) \\
&=p
\end{align}
$$
**_Note: since $q = 1 - p$, then $p+q = 1$.**_

