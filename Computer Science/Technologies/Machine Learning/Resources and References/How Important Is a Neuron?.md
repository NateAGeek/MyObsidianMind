## Overview
The paper attempts to find a method to attribute how much a inner hidden layer or unit has as an impact on the output of the model. They use their concept called "conductance" to describe how each layer provides attribution to the output. Basically they use the chain rule to decompose how each layer affects the output with the [[Axiomatic Attribution for Deep Networks| integrated gradient]]. 

### Conductance
