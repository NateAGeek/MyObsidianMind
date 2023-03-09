## One-Period Binomial Model
A one-period binomial model is when the outcome of a possibility is skewed to one possibility. If it was not then there any skew then the model is not random and is "uninteresting". 

![[../../../../NotebookAssets/Pasted image 20230309145150.png]]
The context here $S_0$ is the current time of the model, aka the current price, where as the $S_1(H\ or\ T)$ is probability of the outcome one unit of time in the future. This gives us a model where in this context H represents a probability of asset price increase while T represents a asset price decrease. 

We can represent this these possible outcome numbers in relation to $S_0$ as the **up factor** and **down factor**. These factors can be mathematically $u = \frac{S_1(H)}{S_0}$  and $d = \frac{S_1(T)}{S_0}$ . Where d < u, as if it is not then technically the labels should be switch

Further item to consider in the model is the interest rate $r$ of a dollar yielding or debiting based on investing or borrowing(long/short). This yield can be represented as 1 + r, where $r > -1$. 

In markets [[Arbitrage]] is the trading strategy that requires zero money, has zero change of loosing money, and has a positive probability of making money. The rule defined of [[Arbitrage]] is as follows $0 < d < 1+r < u$. Where the downside is greater than 0 but less than the rate of interest earned, that is less than the possible upside. These constraints describe an arbitrage opportunity.

_NOTE: Although arbitrage is found in markets it is typically fleeting. As someone discovers it and removes it thought trading it..._

