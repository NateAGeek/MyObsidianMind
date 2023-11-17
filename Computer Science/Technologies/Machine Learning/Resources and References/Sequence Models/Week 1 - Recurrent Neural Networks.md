
# Notation

## Indexing Notation
$x^{(i)<t>}$
Where i = the index in the training set
Where t = the index of the element in the sequence

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


Quiz Notes:
Representation in the selection of layer, word, etc
One to One and One to Many
Γu​ understanding, its size
Review the GRU and LSTM dimensionality with formula
Gradients and how they related to the models
