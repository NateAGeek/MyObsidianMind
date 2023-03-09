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
* $S_0 = $4$
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
