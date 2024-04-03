## Overview

## Discretization
Need to review this... But basically it is a way to solve the formulation of a function that recurrently requires its previous output in a discrete way. We use this method I think for RNN since they are no discrete formulations of recurrent processes. However, with this formulation we are able to then discretly work with them.
TODO though need to better review how this relates to the Mamba Architecture...
[22:21](https://youtu.be/8Q_tqwpTpVU?t=1341)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_bb8f5333-d54a-4b6d-a048-4455ff5caeaa.jpeg)
We can do the approximation at timestamps for the formulation of the output of the system.
### Using this to help during training
So, with RRNs since we need to compute each token one by one doing this process seems to be a throttle on the learning performance. 
## Convolutional Computation Method
We expand the Discretization formulation to improve the performance of learning at training time. To prevent doing RRN processing one by one. 

[29:12](https://youtu.be/8Q_tqwpTpVU?t=1752)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_dd86c33f-46a3-41f9-a1e1-b50b474b7d8c.jpeg)
Little hard for me to understand but when we expand the formulation we can develop a kernel that will allow us to convol the input and the output of the solution. So when we build this kernel we can parallelize the computations. 
[30:51](https://youtu.be/8Q_tqwpTpVU?t=1851)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_df1d51dc-dc77-4978-a192-6e0b9d36b50f.jpeg)The Expansion leads to us making K...
We can then do this over our series of inputs to quickly produce outputs. This increases the performance of learning and then our training speeds increase.

### Tie this together with State Space Models, Discretization, Recurrent Computation, and Finally Convolutional Formulation for increase in traininng.
Soooooo... Basically RNN are good at doing sequence modeling of relations of input data. However, they have one minor issue is that they are recursive by nature. This is not really too bad of an issue at inference time, but it does not scale well as you increase the length. This is especially apparent when you begin training. As you need to recursively calculate token by token output or training.

[12:59](https://youtu.be/8Q_tqwpTpVU?t=779)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_1e9dc18e-95d2-49e8-b370-a734e7e048c4.jpeg)

We can instead discretization of the formulation to expand and develop a discrete formulation of the RNN value at timestamps, instead of calculating the whole step by step process analytically. We basically estimate the solution with a delta parameter to formulate a function. 

[21:57](https://youtu.be/8Q_tqwpTpVU?t=1317)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_9dc3ef86-a87b-4a50-a2ec-3d453f3b97bd.jpeg)


Expanding further, we then realize that base on the estimated function we can start to expand it per item. This leads to the discovery of a conv net that can be applied to the input to calculate the output. This can be parallel now and calculated faster on the GPU. Leading to better performance to learn.

[29:59](https://youtu.be/8Q_tqwpTpVU?t=1799)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_9c2124c2-580c-42bb-ab32-8c87d328fe7d.jpeg)

[28:36](https://youtu.be/8Q_tqwpTpVU?t=1716)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_90fdf878-eca1-4f21-810c-e6c13f68c2ac.jpeg)
[32:35](https://youtu.be/8Q_tqwpTpVU?t=1955)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_14072652-a3e7-4dd3-b9a8-5fc48f041ae1.jpeg)
BOOM, QED MFS!
## Vector Time
[39:40](https://youtu.be/8Q_tqwpTpVU?t=2380) need to review A, but it gives SSM context...
## HIPPO Theory
[40:25](https://youtu.be/8Q_tqwpTpVU?t=2425)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_a5adb5e3-96ef-4219-a087-9da82a980e67.jpeg)
[42:19](https://youtu.be/8Q_tqwpTpVU?t=2539)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_0737f967-215b-4f35-988c-641252b08e3a.jpeg)sooooo... this matrix is good at carrying info from previous states forward, with more accurate data closer and less that is further.
## Mamba Model
SSM and S4 Models did not perform well on Copying and Selective Copying.
Although Copying can be done by the SSM model, it does not work well for S4. This is because the SSM can just learn a basic form of a convolutional and transfer over the data copying it over.
#### Induction Head
in SSM and S4 they have trouble content aware reasoning, they can not look back and context and determine the next best fit.
## Selective Scan
So the B Matrix is no longer fixed, it is unique per token. 
### [50:06](https://youtu.be/8Q_tqwpTpVU?t=3006)
### ![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_c3a95c15-68af-4721-9193-67ff32fd8919.jpeg)
### Scan method
You can basically use the previous state as a cache and sum onto it. 
[53:21](https://youtu.be/8Q_tqwpTpVU?t=3201)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_83c29c3b-b20c-4e32-b0a5-fffc8ab053ba.jpeg)Basically that Prefix Sum Array problem.
### Parallelized Scan
[55:58](https://youtu.be/8Q_tqwpTpVU?t=3358)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_3a886dcc-2566-4956-9245-5f94a904a27f.jpeg)
Basically because summing has the associative property. "Sweep up". We decrease the runtime fron O(N) to O(N/T)
### They made some custom magic to make it faster
Kernel fusion, scan, and some other tricks. They utilized formatting the input into a batch that can be stored in the SRAM of the GPU leading to greater speeds.
**Kernel Fusion: **They basically fuse all the cuda kernel into one to prevent the gpu from moving data back and forth between fast and slow ram.

**Recomputation: **Basically instead of saving the values of each weight, for back propagation, into ram They just recompute it bc it can be faster.

## Model
### Mamba Block
[01:09:00](https://youtu.be/8Q_tqwpTpVU?t=4140)
![](https://storage.googleapis.com/askify-screenshot/Ha2U8XK4TEg7sjGTotwOE6lw1jM2/extension_screenshots/screenshot_default_a97e03a0-0274-4d37-a7ca-af12b3a6bbe2.jpeg)
