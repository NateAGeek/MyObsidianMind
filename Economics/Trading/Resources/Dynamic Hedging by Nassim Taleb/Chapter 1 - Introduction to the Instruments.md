# Derivatives
## Derivative
A derivative is a security that is tied to an underlying asset. It is dependent on the underlying asset for its value, and can a **linear** or **nonlinear** correlation to the asset. 

A **linear derivative** is a derivative of an asset that has a set linear convergence to a price/payoff. An example is a future contract will have a set value at maturity, and does not have to deal with strikes.

A **nonlinear derivative** is a derivative that does not have a linear convergence to a price/payoff. Rather the derivative value is determined by a complex structure that could be as simple as going "into the money" of a strike point. These are also time dependent and "space" dependent. Note, space is technically used here as where the price point falls  for the contract over time.

### _Option Wizard: Greeks_
**[[../../Option Delta|Delta]]:** The sensitivity of the contract to the change of the underlying asset
**[[../../Option Gamma|Gamma]]:** The change of delta relative to the underlying asset price
**[[../../Option Vega|Vega]]:** The sensitivity to option price relative to implied volatility of the asset
**[[../../Option Theta|Theta]]:** The options change to the passing of time
**[[../../Option Rho|Rho]]:** Sensitivity to option price to interest rates/divs

**Derivative Convexity**
There are many different convexity structures when it comes to derivatives. They all have different structures to represent their payoff models.

![[../../../../NotebookAssets/Pasted image 20220711135713.png]]
The method for determining is with the [[../../../../Mathematics/Jensen's Inequality|Jensen's Inequality]] to show convexity across the derivative price to underlying asset. 

**Synthetic Security**: Are a weighted collection of two or more instruments. An example of a synthetic security is the S&P 500. S&P 500 is a collection of the "top" 500 companies that cumulatively represent a weighted value of those 500 companies. 0


