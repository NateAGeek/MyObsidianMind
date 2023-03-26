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

### Deep Reinforcement Learning
We can take an input state and feed it into a neural network. This will allow us to build a NN that can learn and determine the optimal Q-function output given the state input. We then pick the maximal Q-function.

#### Using Bellman Equation to Learning and Train our NN
We can generate a series of of X and Ys with Bellman Equation. 
![[../../../../../NotebookAssets/Pasted image 20230325162005.png]]
Although, we can not determine $max_{a'}Q(s', a')$ at the start. We can give an initial guess that the algorithm will progressively optimize. 
![[../../../../../NotebookAssets/Pasted image 20230325163134.png]]

### Deep Q algorithm

![[../../../../../NotebookAssets/Pasted image 20230325163700.png]]

### Update to the deep learning model to improve performance of learning q-function

![[../../../../../NotebookAssets/Pasted image 20230325163555.png]]

## ϵ-greedy policy
We can try to pick a action with some minor greed policy. This allows us to learn new things that might not have been the best guess initially.
![[../../../../../NotebookAssets/Pasted image 20230325164038.png]]

## Mini Batching
Mini batching is taking a random series of examples to rapidly test the model on. This random small selection, can improve the performance of the training. This batching can maybe random or slowly incremental of series.

## Soft Updates
Soft updates are used to nudge the W and B of the model slightly with new W and Bs. This helps let the reinforcement model to converge more lightly to a result. 

## Code Example

Building the Model of the Q-Function, that will provide train what we want to train the model on developing.
```python
# UNQ_C1
# GRADED CELL

# Create the Q-Network
q_network = Sequential([
    ### START CODE HERE ### 
    tf.keras.layers.Input(state_size),
    tf.keras.layers.Dense(64, activation="relu"),
    tf.keras.layers.Dense(64, activation="relu"),
    tf.keras.layers.Dense(num_actions, activation="linear")
    ### END CODE HERE ### 
    ])

# Create the target Q^-Network
target_q_network = Sequential([
    ### START CODE HERE ### 
    tf.keras.layers.Input(state_size),
    tf.keras.layers.Dense(64, activation="relu"),
    tf.keras.layers.Dense(64, activation="relu"),
    tf.keras.layers.Dense(num_actions, activation="linear")
    ### END CODE HERE ###
    ])

### START CODE HERE ### 
optimizer = tf.keras.optimizers.Adam(learning_rate=ALPHA)
### END CODE HERE ###
```

We can then compute the loss function on the the current q_network and what our target_q_network is
```python
# UNQ_C2
# GRADED FUNCTION: calculate_loss

def compute_loss(experiences, gamma, q_network, target_q_network):
    """ 
    Calculates the loss.
    
    Args:
      experiences: (tuple) tuple of ["state", "action", "reward", "next_state", "done"] namedtuples
      gamma: (float) The discount factor.
      q_network: (tf.keras.Sequential) Keras model for predicting the q_values
      target_q_network: (tf.keras.Sequential) Keras model for predicting the targets
          
    Returns:
      loss: (TensorFlow Tensor(shape=(0,), dtype=int32)) the Mean-Squared Error between
            the y targets and the Q(s,a) values.
    """

    # Unpack the mini-batch of experience tuples
    states, actions, rewards, next_states, done_vals = experiences
    
    # Compute max Q^(s,a)
    max_qsa = tf.reduce_max(target_q_network(next_states), axis=-1)
    
    # Set y = R if episode terminates, otherwise set y = R + γ max Q^(s,a).
    ### START CODE HERE ### 
    y_targets = rewards + ((1 - done_vals) * (gamma * max_qsa))
    ### END CODE HERE ###
    
    # Get the q_values and reshape to match y_targets
    q_values = q_network(states)
    q_values = tf.gather_nd(q_values, tf.stack([tf.range(q_values.shape[0]),
                                                tf.cast(actions, tf.int32)], axis=1))
        
    # Compute the loss
    ### START CODE HERE ### 
    loss = tf.keras.losses.MSE(y_targets, q_values)
    ### END CODE HERE ### 
    
    return loss
```

We can then use TF package to run gradient decent on the of our weights of our q function
```python
@tf.function
def agent_learn(experiences, gamma):
    """
    Updates the weights of the Q networks.
    
    Args:
      experiences: (tuple) tuple of ["state", "action", "reward", "next_state", "done"] namedtuples
      gamma: (float) The discount factor.
    
    """
    
    # Calculate the loss
    with tf.GradientTape() as tape:
        loss = compute_loss(experiences, gamma, q_network, target_q_network)

    # Get the gradients of the loss with respect to the weights.
    gradients = tape.gradient(loss, q_network.trainable_variables)
    
    # Update the weights of the q_network.
    optimizer.apply_gradients(zip(gradients, q_network.trainable_variables))

    # update the weights of target q_network
    utils.update_target_network(q_network, target_q_network)
```

full example of using the reinforcement model to learn lunar 
```python
start = time.time()

num_episodes = 2000
max_num_timesteps = 1000

total_point_history = []

num_p_av = 100    # number of total points to use for averaging
epsilon = 1.0     # initial ε value for ε-greedy policy

# Create a memory buffer D with capacity N
memory_buffer = deque(maxlen=MEMORY_SIZE)

# Set the target network weights equal to the Q-Network weights
target_q_network.set_weights(q_network.get_weights())

for i in range(num_episodes):
    
    # Reset the environment to the initial state and get the initial state
    state = env.reset()
    total_points = 0
    
    for t in range(max_num_timesteps):
        
        # From the current state S choose an action A using an ε-greedy policy
        state_qn = np.expand_dims(state, axis=0)  # state needs to be the right shape for the q_network
        q_values = q_network(state_qn)
        action = utils.get_action(q_values, epsilon)
        
        # Take action A and receive reward R and the next state S'
        next_state, reward, done, _ = env.step(action)
        
        # Store experience tuple (S,A,R,S') in the memory buffer.
        # We store the done variable as well for convenience.
        memory_buffer.append(experience(state, action, reward, next_state, done))
        
        # Only update the network every NUM_STEPS_FOR_UPDATE time steps.
        update = utils.check_update_conditions(t, NUM_STEPS_FOR_UPDATE, memory_buffer)
        
        if update:
            # Sample random mini-batch of experience tuples (S,A,R,S') from D
            experiences = utils.get_experiences(memory_buffer)
            
            # Set the y targets, perform a gradient descent step,
            # and update the network weights.
            agent_learn(experiences, GAMMA)
        
        state = next_state.copy()
        total_points += reward
        
        if done:
            break
            
    total_point_history.append(total_points)
    av_latest_points = np.mean(total_point_history[-num_p_av:])
    
    # Update the ε value
    epsilon = utils.get_new_eps(epsilon)

    print(f"\rEpisode {i+1} | Total point average of the last {num_p_av} episodes: {av_latest_points:.2f}", end="")

    if (i+1) % num_p_av == 0:
        print(f"\rEpisode {i+1} | Total point average of the last {num_p_av} episodes: {av_latest_points:.2f}")

    # We will consider that the environment is solved if we get an
    # average of 200 points in the last 100 episodes.
    if av_latest_points >= 200.0:
        print(f"\n\nEnvironment solved in {i+1} episodes!")
        q_network.save('lunar_lander_model.h5')
        break
        
tot_time = time.time() - start

print(f"\nTotal Runtime: {tot_time:.2f} s ({(tot_time/60):.2f} min)")
```

