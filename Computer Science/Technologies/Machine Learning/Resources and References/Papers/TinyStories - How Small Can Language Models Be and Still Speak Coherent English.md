

Something to note that kinda fit my theory about embeddings. 
_"This suggests that the embedding dimension is more crucial for capturing the meaning and the relations of words, while the number of layers is more crucial for capturing long-range dependencies in the generation."_ 

Good tips to check that the model is generalizing and not overfitting data:
* Exact memorization: This is the simplest and most obvious form of memorization, where the model simply copies an entire story or a large portion of it from the dataset, without changing anything. This can be easily detected by checking the similarity or the hash of the generated story with the stories in the dataset.
* Simple template matching: This is a slightly more sophisticated form of memorization, where the model changes some names or entities in a story from the dataset, but keeps the rest of the story the same. For example, the model might change the names of characters, or the location of the story, but keep the plot and the events the same. This can be detected and prevented by measuring the overlap of words and n-grams between the generated story and the stories in the dataset.
* Complex template matching: This is the most subtle and difficult form of memorization, where the model follows a more abstract pattern or structure from the dataset, keeping the general plot but changing the details and the specifics of the story. This is almost impossible to quantify, as it requires a deeper understanding and analysis of the content and the meaning of the stories, and how they relate to each other.