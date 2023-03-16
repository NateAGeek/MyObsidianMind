## One-Period Binomial Model
A one-period binomial model is when the outcome of a possibility is skewed to one possibility. If it was not then there any skew then the model is not random and is "uninteresting". 

![[../../../../NotebookAssets/Pasted image 20230309145150.png]]
The context here $S_0$ is the current time of the model, aka the current price, where as the $S_1(H\ or\ T)$ is probability of the outcome one unit of time in the future. This gives us a model where in this context H represents a probability of asset price increase while T represents a asset price decrease. 

We can represent this these possible outcome numbers in relation to $S_0$ as the **up factor** and **down factor**. These factors can be mathematically $u = \frac{S_1(H)}{S_0}$  and $d = \frac{S_1(T)}{S_0}$ . Where d < u, as if it is not then technically the labels should be switch

Further item to consider in the model is the interest rate $r$ of a dollar yielding or debiting based on investing or borrowing(long/short). This yield can be represented as 1 + r, where $r > -1$. 

In markets [[Arbitrage]] is the trading strategy that requires zero money, has zero change of loosing money, and has a positive probability of making money. The rule defined of [[Arbitrage]] is as follows $0 < d < 1+r < u$. Where the downside is greater than 0 but less than the rate of interest earned, that is less than the possible upside. These constraints describe an arbitrage opportunity.

_NOTE: Although arbitrage is found in markets it is typically fleeting. As someone discovers it and removes it thought trading it..._

## Example of Model Definitions
Given the context of an asset currently priced in a 4, and has an up factor of 2 and a down factor of 1/2. We get the following binomial possibility.
![[../../../../NotebookAssets/Pasted image 20230309161411.png]]

#### Variable Definitions 
* $S_0$ = $4$
    * Asset starting price
    * $S_1(H\ or\ T)$: representing the outcome of the asset at one unit time in the future
* $X_0$ = $1.20
    * The capital put forth
* $\Delta_0 = \frac{1}{2}$
    * shares bought of asset
* $B_0 = (X_0 - \Delta_0S_0)$
    * Borrowed capital from money markets
* $r = \frac{1}{4}$
    * Interest rate of borrowed capital from money markets
* $O_0 = (1+r)B_0$
    * The owed cost of borrowed capital at time 0

In the context of the example.
1) We will first buy half a share at $4, totaling to $2.
2) We only have $1.20 so we need to seek capital from the money markets and barrow $0.80 at a rate of $\frac{1}{4}$.
3) That leaves us with an owed amount of $0.80 * $\frac{1}{4}$ = $1
4) Since owed money is a debt, owed $1 becomes -$1 in our profit
5) In state of return of H is $8 * $\frac{1}{2}$ = $4, and paying back the interest owed of -$1, we would have a portfolio $3
6) In state of return of T is $2  * $\frac{1}{2}$ = $1, and paying back the interest owed of -$1, we would have a portfolio $0

Formula
$$
\begin{align}
X_1(H) &= \Delta_0S_1(H) + O_0 = 3 \\
X_1(T) &= \Delta_0S_1(T) + O_0 = 0
\end{align}
$$

If we also add in the context of a European Call Option K at strike 5. We can determine if we simulated the option with money markets as a borrower. When K = 5, $(S_1(H) - K)^+ = 3$ or $(S_1(T) - K)^+ = 0$. So we were able to get the same return using money markets as if we were to hold a Call Option to expiration at time one, with a strike of 5. That means we can replicate the option strategy with money markets or use money markets to replicate the outcome of the option strategy.

#### Potential Arbitrage Opportunity 
In this context if the option was price at more or less than $1.20, then we would have a profit opportunity. Since base on the example we  As we could long or short the simulated trade with money markets and make the difference in profit without risking any money technically. This would be considered an arbitrage.

### Solving For a More General Derivative at $V_0$
The goal for reverse engineering price of a derivative at time zero, is to determine its equivalent portfolio. This allows to determine if the derivative is miss priced and could lead to a risk free profit arbitrage. 

In order to solve to $V_0$ we need to do it reverse from the potential outcomes from $V_1(H)$ and $V_1(T)$. We can start by assuming a matching portfolio created, example above, the following have to be true $X_1(H) = V_1(H)$ and $X_1(T) = V_1(T)$ since we will assume that the market is efficient and there is not an arbitrage between the money market portfolio and the derivates alternative. 

First we must define what $X_1$ is in relation to the money market portfolio. We can do this with the following equation. Where $\Delta_0S_1$ represents our position at time 1 and $(1+r)(X_0 - \Delta_0S_0)$ our negative cost from borrowing from the money markets. 
$$
\begin{align}
X_1 &= \Delta_0S_1 + (1+r)(X_0 - \Delta_0S_0) \\
    &= \Delta_0S_1 + X_0(1+r) - \Delta_0S_0(1+r) \\
    &= \Delta_0S_1 - \Delta_0S_0(1+r) + X_0(1+r) \\
    &= \Delta_0(S_1 - S_0(1+r)) + X_0(1+r) \\
    &= X_0(1+r) + \Delta_0(S_1 - S_0(1+r))\\
    Simplified: \\
X_1 &= X_0(1+r) + \Delta_0(S_1 - S_0(1+r))
\end{align}
$$

We can then define the following equations
$$
\begin{align}
    X_0(1+r) + \Delta_0(S_1(H) - S_0(1+r)) &= V_1(H) \\
    X_0(1+r) + \Delta_0(S_1(T) - S_0(1+r)) &= V_1(T)
\end{align}
$$
To properly reflect the solve for how we reflect the initial money market portfolio we need to calculate the $X_0$ and $\Delta_0$.

Calculating $\Delta_0$ is fairly simple. This ends up being the [[Delta Hedging Formula]]
$$
\begin{align}
V_1(H) - V_1(T) &= X_0(1+r) + \Delta_0(S_1(H) - S_0(1+r)) -  X_0(1+r) + \Delta_0(S_1(T) - S_0(1+r)) \\ 
V_1(H) - V_1(T) &= X_0(1+r) - X_0(1+r) + \Delta_0(S_1(H) - S_0(1+r)) + \Delta_0(S_1(T) - S_0(1+r)) \\
V_1(H) - V_1(T) &= \Delta_0(S_1(H) - S_0(1+r)) + \Delta_0(S_1(T) - S_0(1+r)) \\
V_1(H) - V_1(T) &= \Delta_0S_1(H) - \Delta_0S_0(1+r) + \Delta_0S_1(T) - \Delta_0S_0(1+r) \\
V_1(H) - V_1(T) &= \Delta_0S_1(H) + \Delta_0S_1(T) - \Delta_0S_0(1+r) - \Delta_0S_0(1+r) \\
V_1(H) - V_1(T) &= \Delta_0S_1(H) + \Delta_0S_1(T) - 0 \\
V_1(H) - V_1(T) &= \Delta_0(S_1(H) - S_1(T)) \\
\frac{V_1(H) - V_1(T)}{S_1(H) - S_1(T)} &= \Delta_0 \\
\end{align}
$$
We now how how much shares we need properly replicate the position in the money market portfolio.

We need still need to solve for the $X_0$ required capital to mimic the derivative. This is a bit more complicated and we introduce what is known as the risk-neutral probabilities, $\tilde{p}$ and $\tilde{q} = 1 - \tilde{p}$ , to help us solve for the unknowns.

Multiplying $\tilde{p}$ by $X_0(1+r) + \Delta_0(S_1(H) - S_0(1+r)) = V_1(H)$, $\tilde{q}$ by $X_0(1+r) + \Delta_0(S_1(T) - S_0(1+r)) = V_1(T)$, and sum them we can have enough context to solve for $X_0$ in relation to the outcomes of $V_1(H)\ and\ V_1(T)$. 
$$
\begin{align}
\tilde{p}(X_0(1+r) + \Delta_0(S_1(H) - S_0(1+r))) &= \tilde{p}V_1(H) \\
\tilde{q}(X_0(1+r) + \Delta_0(S_1(T) - S_0(1+r))) &= \tilde{q}V_1(T) \\
\\
\tilde{p}(X_0(1+r) + \Delta_0(S_1(H) - S_0(1+r))) + \\
\tilde{q}(X_0(1+r) + \Delta_0(S_1(T) - S_0(1+r))) \\
&= \tilde{p}V_1(H) + \tilde{q}V_1(T) \\
\\
X_0(1+r) + \Delta_0([\tilde{p}S_1(H) + \tilde{q}S_1(T)] - S_0(1+r))) &= \tilde{p}V_1(H) + \tilde{q}V_1(T)
\\
\\
S_0 = \frac{1}{1 + r}[\tilde{p}S_1(H) + \tilde{q}S_1(T)] \\
\\
\\
X_0(1+r) = \tilde{p}V_1(H) + \tilde{q}V_1(T) \\
X_0 = \frac{1}{1+r}[\tilde{p}V_1(H) + \tilde{q}V_1(T)]
\end{align}
$$
Now we need to solve for $\tilde{p}$ and $\tilde{q} = 1 - \tilde{p}$  to resolve the full relation for $X_0$

Knowing $S_0 = \frac{1}{1 + r}[\tilde{p}S_1(H) + \tilde{q}S_1(T)]$ we can solve for $\tilde{p}$ and $\tilde{q} = 1 - \tilde{p}$ like so...
$$
\begin{align}
S_0 = \frac{1}{1 + r}[\tilde{p}uS_0 + \tilde{q}dS_0] = \frac{S_0}{1 + r}[\tilde{p}u + \tilde{q}d] \\
\tilde{p} = \frac{1 + r - d}{u-d} \\
\tilde{q} = \frac{u-1-r}{u-d}
\end{align}
$$

This now allows us to formulate:
$$
X_0 = \frac{V_1(H)(1 + r - d) + V_1(T)(u-1-r)}{(1+r)(u-d)}
$$

We can fully emulate the derivative outcome with a money market based portfolio.  

### Example
kinda an example with python how this would work... Only thing is I do not know how to incorporate buying with money market...
```python
S_0 = 4
S_1H = 8
S_1T = 2

V_1H = 8
V_1T = 2

r = 1/4
u = S_1H/S_0
d = S_1T/S_0

p = (1 + r - d)/(u - d)
q = (u - 1 - r)/(u - d)

X_0 = (p * V_1H + q * V_1T)/(1 + r) # Starting capital required
D_0 = (V_1H - V_1T) / (S_1H - S_1T)

print(f"Starting Capital {X_0}")
print(f"Number of Shares {D_0}")
print(X_0)
print(S_0)

if X_0 == S_0:
    print("Yeps X_0 = S_0")
```

## Multiple Binomial Models
Utilizing what we know about binomial models. We can extend them to multiple periods of time. 
![[../../../../NotebookAssets/Pasted image 20230318115200.png]]
Where the up and down factors are consistent. We develop a model with set degrees of price
