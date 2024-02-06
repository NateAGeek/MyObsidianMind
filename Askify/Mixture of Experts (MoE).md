## Overview
Mixture of experts are a mix of different "experts", gated feedforward network, that will help route the best fit "expert" to mix and output the predicted token. 
Each token is fed to a specific expert, this routing is done via a gate that is a linear network(at least in the Mixtrual model). This is then based on the max number of experts the input is fed through them and then mixed, via mult/dot. This is softmax to
