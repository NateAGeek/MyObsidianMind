### Base LLM
Base LLMs are very unspecifically tuned and are just trying to predict the next best word. This can cause some issues with as the next best word could not always be what we want. For example if you asked what is the "capital of France?" it might rapidly try and ask "What is the president of France?" as those questions in the training set could be rapidly following. 

### Instruction Tuned LLM
These are more trained to handle instruction based requests. Like a direct question with answer. They are usually trained with a base model that has been curated to use Reinforcement Learning with Human Feedback. They attempt to be helpful, honest, and harmless.

