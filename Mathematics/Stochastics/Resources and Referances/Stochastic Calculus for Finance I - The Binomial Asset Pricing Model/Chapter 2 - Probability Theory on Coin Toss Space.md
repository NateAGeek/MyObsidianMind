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

### Definition 2.1.1
We can define **probability space** that consists of elements $w$ in $\Omega$ and a probability measure of $\mathbb{P}$ maps. 
We must define:
* $\Omega$ is a nonempty finite set
* $\mathbb{P}$ is a probability function
* $\mathbb{P}$ maps the element $w$ in $\Omega$ a number $[0, 1]$ 
We also must limit the total probability space to 1, as each element must have a final 
$$\sum_{w\in\Omega}\mathbb{P}(w) = 1$$


Once we have defined the logical **probability space** we can define subsets as follows:
$$
\mathbb{P}(A) = \sum_{w\in A}\mathbb{P}(w)
$$
We can then hold value that if two events are disjointed, then their events can be define as follows:
$$
\mathbb{P}(A \cup B) = \mathbb{P}(A) + \mathbb{P}(B)
$$
### Definition 2.2.1
Solving for the distribution of a set of outcomes. Basically converting the probabilities of the element space into a distribution

On the set here
$$
\Omega = \{HHH, HHT,HTH,HTT,THH,THT,TTH,TTT\}
$$
We can define the probability of $H$ vs $T$ to be $\frac{1}{2}$ with the probability of each element in $\Omega$ to be $\frac{1}{8}$, since there are 8 elements.

We then can define a function that will create a distribution of these elements for us to work with. For example, we have the functions $X$ and $Y$. Where the function $X$ produces how many 
$H$'s are in the element. $Y$ is simply the opposite such that it produces the number of $T$. This would create the following distribution in relation to $\tilde{\mathbb{P}}$. 

Examples of function $X$ probability distribution of $\tilde{\mathbb{P}}$
$$
\begin{align}
X(HHH) &= 3 \\
X(HHT) = X(HTH) = X(THH) &= 2 \\
X(HTT) = X(THT) = X(TTH) &= 1 \\
X(TTT) &= 0
\end{align}
$$
$$
\begin{aligned}
\tilde{\mathbb{P}} \{w\in\Omega; X(w) = 0\} = \tilde{\mathbb{P}}\{TTT\}= \frac{1}{8} \\
\tilde{\mathbb{P}} \{w\in\Omega; X(w) = 1\} = \tilde{\mathbb{P}}\{HTT,THT,TTH\}= \frac{3}{8} \\
\tilde{\mathbb{P}} \{w\in\Omega; X(w) = 2\} = \tilde{\mathbb{P}}\{HHT,HTH,THH\}= \frac{3}{8} \\
\tilde{\mathbb{P}} \{w\in\Omega; X(w) = 3\} = \tilde{\mathbb{P}}\{HHH\}= \frac{1}{8} \\
\end{aligned}
$$

```chart
    type: bar
    layout: rows
    beginAtZero: true
    labels: [0, 1, 2, 3]
    series:
        - title: X Distribution Tilde P
          data: [0.125, 0.375, 0.375, 0.125]
        - title: Y Distribution Tilde P
          data: [0.125, 0.375, 0.375, 0.125]
```

#### Utilizing different probability space rules

If we were to alter the probability space $\mathbb{P}$ such that $H$ has a $\frac{2}{3}$ and $T$ has a $\frac{1}{3}$. The distribution would be different for both $X$ and $Y$ on the in relation to the space $\mathbb{P}$. 

We need to calculate the Probability Space in relation to the $X$ function. For example we now need to treat each coin flip as an independent event with the new probability of happening.

$$
\begin{aligned}
\mathbb{P}\{TTT\} = \mathbb{P}(T) * \mathbb{P}(T) * \mathbb{P}(T) = (\frac{1}{3}) ^ 3 &= \frac{1}{27} \\ 
\mathbb{P}\{HTT,THT,TTH\} = \mathbb{P}(H) * \mathbb{P}(T) * \mathbb{P}(T) ... = ((\frac{1}{3} * \frac{1}{3}) * (\frac{2}{3}))^3 &= \frac{6}{27} \\ 
\mathbb{P}\{HHT,HTH,THH\} = \mathbb{P}(H) * \mathbb{P}(H) * \mathbb{P}(T) ... = (\frac{1}{3} * (\frac{2}{3} * \frac{2}{3}))^3 &= \frac{12}{27} \\ 
\mathbb{P}\{HHH\} = \mathbb{P}(H) * \mathbb{P}(H) * \mathbb{P}(H) = (\frac{2}{3})^3 &= \frac{8}{27} \\ 
\end{aligned}
$$

This gives us a new distribution to work with down below.

```chart
    type: bar
    layout: rows
    beginAtZero: true
    labels: [0, 1, 2, 3]
    series:
        - title: X Distribution P
          data: [0.03703703703, 0.22222222222, 0.44444444444, 0.29629629629]
        - title: Y Distribution P
          data: [0.29629629629, 0.44444444444, 0.22222222222, 0.03703703703]
```

### Definition 2.2.4
**Expected Value**: is defined as the average expected value of a probability distribution as the trials reach infinity. We can define it as below:
$$
\mathbb{E}[X] = \sum_{w\in\Omega}X(w)\mathbb{P}(w)
$$
In the context where the coin is fair, and we have a $\frac{1}{2}$ heads and $\frac{1}{2}$ tails