## Reinforcement Learning
Is the structure of teaching an algorithm how to behave based on a reward function, a function that produces when the algorithm preforms correct actions for incorrect actions. This is different from supervised learning because we do not have the expected output. But rather an expected goal that the algorithm must learn.

We use a state and determine the reward factor of the algorithms performance. We try and teach to maximize the reward for the algorithm to follow.

### Return of reward
To encourage the algorithm to choose the most optimal reward, maybe not the best but the easiest to access. We can guide it to take the easiest route via a discount factor. The discount factor then is applied to the state causing larger/longer states to reward ratios to be reduced.

### Policy Function
A function that uses the reward to generate the best series of actions to follow.

### Q-function
Returns the optimal action to take. We try to max the Q function to then take the best actions.

### Bellman Equation
$$
    Q(s, a) = R(s) + \gamma(max_{a'}Q(s', a'))
$$

We try to determine the best optimal action to follow without calculating the whole system. Since we can just incrementally follow the chain of actions.

### Stochastic Environments
If our action system is not deterministic. We can take the average of the Q-function. We try to maximize the average over the actions. We can basically take on average the output of possible actions. 

![[../../../../../NotebookAssets/Pasted image 20230325152647.png]]

### Good Example problem for fully calculating Q from a given state.
![[../../../../../NotebookAssets/Pasted image 20230325153318.png]]

## Continuous State
Are states that can have varying degrees of dimensions of data. 