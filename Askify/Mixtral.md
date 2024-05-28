## Sliding Window Attention
### Casual Mask
When we are dealing with the attention matrix, we want to apply a mask to make sure that words and specific intervals are being applied to each other and does not apply the future words to the current context. This prevents a bias of seeing it in the future.
[11:58](https://youtu.be/UiX8K-xBUpE?t=718)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_892d7fbd-b3c6-47bd-be70-a817ccbcde30.jpeg)We convert the negative infinity to 0 with the softmax function. Making sure that the future value are 0s.
[13:35](https://youtu.be/UiX8K-xBUpE?t=815)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_1ff8e8f7-a045-4277-83e2-d8855b4c9a35.jpeg)The sliding window basically applies a mask for the words before the observed word. This prevents an over fitting on the relating words further apart from the main word.
_Note:Because of we use multiple heads, by some degree from the other heads, words will have some relation to previous words but it would be as strong. Like Chair will have some relation to The(index 1) in another head..._
[17:40](https://youtu.be/UiX8K-xBUpE?t=1060)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_db7d5ba0-35ff-4977-b389-20b92fb9fc86.jpeg)Concept is related to the Receptive Field.
So we are not directly applying the tokens down the layers. However, since the receptive field affect is happening, by association of the sliding window we are passing some previous information from the earlier tokens down. 
[32:04](https://youtu.be/UiX8K-xBUpE?t=1924)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_c2c2bf9d-4bac-4719-b320-eca1a13cbe92.jpeg)
## KV Cache
You can review the basic KV Cache in the LLaMa model notes. But basically store the output of previous tokens to compute next, instead of trying to recompute the previous tokens.
### Rolling Buffer
When you are using the sliding window attention you actually get an advantage of not needing to keep all the QK^T values in the calculation of the attention. 
[45:53](https://youtu.be/UiX8K-xBUpE?t=2753)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_86e9d028-c838-4223-a77c-0dd99cec8236.jpeg)
So as seen here the blacked out regions are no longer needed for calculating the attention, as they are outside of the sliding window from the attention sliding mask.
## Pre-fill and Chunking
TODO: Need to review. But basically it seems like the we prefill the caching chunk for the KV Cache base on the frame...

## Mixture of Experts
So, the mixture of experts layer is a set of feed forward layers that become "experts" of the analyzing the output of attentions. This then will basically be gated to control what expert to use and the weights(opinions) will be added to the output tokens. The Mixtral uses the top two
[01:03:04](https://youtu.be/UiX8K-xBUpE?t=3784)
#### ![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_3f74a9de-365c-4639-b806-957910372dd3.jpeg)Mistral Model Sharding
They mention in the original paper of taking the model and breaking it up into chunks to run layers on specific GPUs. This has some disadvantages in the sense that each gpu is running sequentially.
[01:05:59](https://youtu.be/UiX8K-xBUpE?t=3959)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_a9ece9aa-b4bb-46fe-a6a6-70cf4bd7b855.jpeg)Umar goes into details of doing a parallelism approach.
## Pipeline Parallelism
[01:06:52](https://youtu.be/UiX8K-xBUpE?t=4012)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_ae93c1c2-475d-43fb-af4d-82d077a7edbb.jpeg)The problem is that this runs in sequence from GPU to GPU.
### Better Scheduling
[01:08:58](https://youtu.be/UiX8K-xBUpE?t=4138)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_03d22718-8752-449c-b0b5-d50181d24acd.jpeg)Basically we just batch them smaller, so that when the 2nd gpu is running we can then take the first gpu to calculate the second batch. Just becomes more effective.
**Gradient Accumulation**
basically accumulate the mini batches and then resolve the gradients at the end.
## XFormers
We are batching a series of prompts that allows the model to process multiple prompts at once. 
[01:17:20](https://youtu.be/UiX8K-xBUpE?t=4640)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_8ed7aae1-670c-4d2f-8d52-4ebb22ce8c39.jpeg)We concat the tokens into one mega prompt. This allows us to better process the whole sequence. However, this leads to a difficult ability to know what to mask and where to append the next prediction of the prompts.
### xformers BlockDiagonalCausalMask
Basically creates this super mask that will mask out parts of the matrix that can be attention of specific spots
[01:19:05](https://youtu.be/UiX8K-xBUpE?t=4745)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_4b2f2316-acea-4a0a-8213-ed4f10c17fa7.jpeg)
