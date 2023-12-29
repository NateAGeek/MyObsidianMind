
## Basic Model
#### Sequence to Sequence Model
**Encoding**: Is a network that takes in an input sequence
**Decoding**: Is a network that takes the output of the Encoding and produces the labels 

For example, we could want to encode a french sentence and then given the english label we could train weights to find the relation between the input and output. This is an example of a **Sequence to Sequence** model.

#### Image Captioning
This is kinda similar to Image Captioning. Given a series of images, we can convert a image into a ConvNet then, we can encode an image and then we can take that encoding and feed it to a RNN that will generate the caption.

## Picking the Most Likely Sentence
#### Conditional Language Model
So, a classical language model would be a RNN that feeds sequence into unit by unit. However, this would be the generative aspect of $P(y^{<1>},...,y^{<T_y>})$. This is basically asking what is the probability of the output given the series of inputs. Then, you can add in the conditional aspects to the network, in this context decoder. 

So it changes from $P(y^{<1>},...,y^{<T_y>}|x^{<1>},...,x^{<T_x>})$ this basically is given the output of the probability of y, what is the original input of x. We can conditionally learn this information in a Machine Translation task.

You don't want to sample it at random, what you want to do is find the maximum of that be translation in the probability.

##### Not to use Greedy Search
We don't use greedy search for each expected $y$ output. Since these $y$ outputs just use the first one, it does not optimize on the whole sequence.

## Beam Search
While Greedy would only pick the first best one. Beam search has a parameter of the "Beam Width" that will collectively account for multiple possible best options. 

So basically you take those best probabilities and then continue to predict the next best option. You do that for all of the samples in the Beam Width. This gives you the probability of $P(y^{<1>}, y^{<2>}|x)$. However, once we see in our recursive step a word that is up the chain, then we can dismiss that chain up and the best probable sequence already contains it within context.

![[../../../../../NotebookAssets/Pasted image 20231203150636.png]]

## Refinements of Beam Search
#### Length Normalization
Basically the function tries to maximize the next best word given the series and the output of the sequence.
$$
\begin{equation} \underset{y}{\mathrm{arg\,max}} \prod_{t=1}^{T_y} P(y^{<t>} | x, y^{<1>}, \dots, y^{<t-1>}) \end{equation}
$$
 However, since we are multiplying a series of probabilities, it can quickly go to zero. This leads the to the beam width to prefer short sequences compared to probably longer more accurate ones. We can fix this by normalizing it across all the sequence max length.
$$
\begin{equation}
\frac{1}{T_y^\alpha} \sum_{t=1}^{T_y} \log P(y^{<t>} | x, y^{<1>}, \ldots, y^{<t-1>})
\end{equation}
$$
Alpha is a param that you can fine toon as well

## Error Analysis in Beam Search
![[../../../../../NotebookAssets/Pasted image 20231203153254.png]]
Basically we take our base case and make sure that we are choosing the correct output. If we are not then we can use the results from the Beam Search to deduce the reason we are not achieving our expected output and what would be the culprit.

The cases are stated. But for textual review: 
* if our probability of correct output > probability of prediction, then it is probably beam search failing.
* if our probability of correct output <= probability of prediction, then it is RNN models fault.

You could determine if Beam is at fault, and if so then you can expand the beam width.

## Bleu Score
Basically we give credit to words based on the max amount it appears in references. So, if there sentence has "the" twice, then the credit is capped at two. So if the length of the output is 7 we cap the credit of the Machine Output to 2/7. 

#### Bigrams
Bigrams are the sampling of pairs in the sentence, forward and backward. we then use the same idea for single words, but we count how many of the bigram words appear in the whole sentence.
![[../../../../../NotebookAssets/Pasted image 20231203154529.png]]

![[../../../../../NotebookAssets/Pasted image 20231203154729.png]]
General formula for n-gram bigram.

We then combine these together
![[../../../../../NotebookAssets/Pasted image 20231203154830.png]]
This gives us a final scoring translation for multiple references.

## Attention Model Intuition
The idea behind the attention context is to have an RRN that selectively has weights to the most important context to the sentence and statements. It breaks down the whole phrasing chunk by chunk to determine its relation to predictive output.

On a more programatic level. The attentions are what defines the input to the next context. That will get fed into the leading RRN. These attentions per token in the sequence, are then learned and used to better predict sequence that is more accurate. 

![[../../../../../NotebookAssets/Pasted image 20231214173756.png]]

### Computing Attention
![[../../../../../NotebookAssets/Pasted image 20231214174446.png]]
It is a little hard to explain in words. This diagram shows that basically we learn the attention via a mini neural network. We use back propagation to learn the attention for each phrase. You also, want to make sure your attentions are equal to one to keep them within the normalization of items to pay attention to.

## Speech Recognition

You can convert sounds into spectrum grams to then process and determine transcript. 