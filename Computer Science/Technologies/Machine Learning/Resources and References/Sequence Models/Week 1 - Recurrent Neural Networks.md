
# Notation

## Indexing Notation
Superscript $[l]$ denotes an object associated with the $l^{th}$ layer. 
Superscript $(i)$ denotes an object associated with the $i^{th}$ example. 
Superscript $\langle t \rangle$ denotes an object at the $t^{th}$ time 
step. 
Subscript $i$ denotes the $i^{th}$ entry of a vector.

**Example**:  
$a^{(2)[3]<4>}_5$ denotes the activation of the 2nd training example (2), 3rd layer [3], 4th time step <4>, and 5th entry in the vector.

$Tx^{(i)}$
where i = the index of the train example. However, Tx is an array of how lengths of input sample. So this selects how long the input sequence is for the input sample.

### Vocabulary
 is a way in which we encode the words for the network. We try to encode them via a tokenizing them. To tokenize them in the slides we increment an ID to each word alphabetically. Basically making the index of the vocabulary the ID of the word.

Example Array:

|word   |index|
|--------|-----|
| aaron  | 0   |
| and    | 1   |
| ...    | ... |
| harry  | 4025|
| potter | 6820|
| ...    | ... |
| zulu   | 10,000 |

### **One Hot**
Encoding vector is know as a vector with 1 single spot and the rest set to 0s.
With the example above encoding for harry:

| word   | encoding | index |
| ------ | -------- | ----- |
| aaron  |  0  | 0           |
| and    |  0  | 1           |
| ...    |  0  | ...         |
| harry  |  1  | 4025        |
| potter |  0  | 6820        |
| ...    |  0  | ...         |
| zulu   |  0  | 10,000      |


## Recurrent Neural Networks

At the core the ideas is to take the an initial output of an activation (zero by default) and feed it into a network. The output of that network (with weights $Way$) will go into the sequence prediction of $\tilde{y}^{<1>}$... $\tilde{y}^{<t>}$. The network will take in the sequence of $x$ at $x^{<1>}$... $x^{<t>}$ that has the parameters of $Wax$. Also, the activation output will continue through the network, and this is labeled as $Waa$. 


![[../../../../../NotebookAssets/Pasted image 20231116185029.png]]
_Note the diagram provided is of a single layer with 4 units._
#### Simplify the Equations
For calculating $a^{<t>}$ we have the following formulation base on the diagram
$$
\begin{align}
a^{<t>} &= g(W_{aa} a^{<t-1>} + W_{ax} x^{<t>} + b_a) \\
\hat{y}^{<t>} &= g(W_{ya} a^{<t>} + b_y)
\end{align}
$$

This can be simplified via combining $Waa$ and $Wax$ into one big weight matrix $Wa$ and also combining $a^{<t-1>}$ and $x^{t}$. 

$$
\begin{align}
W_a &= \begin{bmatrix} W_{aa} & W_{ax} \end{bmatrix} \\
[a^{<t-1>}, x^{<t>}] &=
\begin{bmatrix}
a^{<t-1>} \\
x^{<t>}
\end{bmatrix} \\
a^{<t>} &= g(W_{a} [a^{<t-1>}, x^{<t>}] + b_a) \\
\end{align}
$$
## Forward Propagation
![[../../../../../NotebookAssets/Pasted image 20231116193705.png]]
Basically you define a loss function that is applied to the output of $\hat{y}$ and then you sum all the losses from the sequences and that gives you your final loss.

## Different Types of RNNs

**Many to Many**: Is given a sequence of $x^{<1 ... t>}$ outputs a sequence of $\hat{y}^{<1...t>}$
**Many to One**: is given a sequence of $x^{<1 ... t>}$ we get a single out put of $\hat{y}$
**One to One**: is a just a single item of $x$ outputs a single value of $\hat{y}$
**One to Many**: is given a single input of $x$ output a sequence of $\hat{y}^{<1...t>}$. This is done by feeding each output of the unit to next one as the input. 
**Many to Many Sequence Extension**: In this context the there is an encoder that takes in a sequence of $x$ and then an decoder that outputs $\hat{y}$

![[../../../../../NotebookAssets/Pasted image 20231116194843.png]]
## Language Model and the Many to Many

Basically you want to tokenize each word into a key. You can also add in custom ones such as \<EOS> (End of Sentence) or \<UNK> (Unknown). 

Basically the goal of the model is to predict the $\hat{y}$ of each item. This can be represented probabilistically $P(\hat{y}^{<4>}\ |\ [\hat{y}^{<1>}, \hat{y}^{<2>}, \hat{y}^{<3>}])$. 

## Sampling Novel Sequences
Basically you train the model like a normal **Many to Many** network. Then you do "Sampling" for the new prediction. So given the output $\hat{y}$ you feed it in as the next sequence of $x$. This allows you to generate base on pervious results. It is also suggested to randomly choose from the preview softmax of possibilities randomly in the same distribution. 

## Vanishing Gradients with RNNs
The issue with the basic RNN described is that is can lead to challenges of the model learning long distance relations in the sequences. The example gives:

*The **cat**, which already ate ..., **was** full.
The **cats**, which already ate ..., **were** full.*

The example is that the cat and cats are so far from the tense of verb base on the the cat noun being singular or plural. The network would have trouble learning this distance and relation since the sequence just feeds $x^{<t>}$ one by one. 

The basic RNN has many localize influences and can't access data really far back in the sequence. 

#### Exploding Gradients 
The lecture suggests to clip the gradients to prevent them form exploding out of the context

## SimpleRNN
A single RNN Cell diagram is as follows

This is the same as the following formulas:
$$
\begin{align}
a^{<t>} &= g(W_{a} [a^{<t-1>}, x^{<t>}] + b_a) \\
\hat{y}^{<t>} &= g(W_{ya} a^{<t>} + b_y)
\end{align}
$$
Where each of these cells are then linked up feeding $a^{<t>}$. 
![[../../../../../NotebookAssets/Pasted image 20231118133015.png]]

The cells can be any arbitrary length of the sequence. The $W_{aa}$, $W_{ax}$, and $W_{ay}$ are shared through the whole sequence of cells and feed back into each other via $a^{<t>}$. The activation of the previous result is passed into the next item in the sequence. 

## GRU


$$
\begin{align}
c^{<t>} &= a^{<t>} \\
\tilde{c}^{<t>} &= tanh(W_{cx}x^{<t>} + W_{cc}c^{<t-1>} + b_c) \\
\Gamma_u &= \sigma(W_{ux}x^{<t>} + W_{uc}c^{<t-1>} + b_u) \\
c^{<t>} &= \Gamma_u * \tilde{c}^{<t>} + (1 - \Gamma_u) * c^{<t-1>}

\end{align}
$$
Compared to the Simple RNN cells. We now introduce a new series of weight that is the update gate ($\Gamma_u$).
This acts as a switch that learns base on the input and the previous word, if we should override the activation candidate ($\tilde{c}$) with the previous activation($c$). 

## LSTM
![[../../../../../NotebookAssets/Pasted image 20231117220135.png]]

There are now

Quiz Notes:
Representation in the selection of layer, word, etc
One to One and One to Many
Γu​ understanding, its size
Review the GRU and LSTM dimensionality with formula
Gradients and how they related to the models
