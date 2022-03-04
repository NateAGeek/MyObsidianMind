




# Overview
Vulkan Queues ( also know as VkQueue) are used to prepare [Vulkan Command Buffers] to execute on the GPU, they are executed in order that are sent to the Queue. Queues can execute independently unless a [Vulkan Semaphore] is used. There are Queue Families that specifically handle different tasks. GPUs tend to have multiple different Queues to work with and allows you to select what Queue you want to send commands to for parallel work.

## Queue Families
* Graphics
    * These Queues can process all VkCmdDraw*
* Compute
    * These Queues can process all the VkCmdDispatch*
* Transfer
    * These Queues can process all the VkCmdCopy*
* Sparse
    * VkQueueBindSparse
* Protected
    * Need to review.
* // Need to explore but saw 1.1 had video encoding and decoding flags?

Reference of the Family Flags as of 1.3
```
// Provided by VK_VERSION_1_0
typedef enum VkQueueFlagBits {
    VK_QUEUE_GRAPHICS_BIT = 0x00000001,
    VK_QUEUE_COMPUTE_BIT = 0x00000002,
    VK_QUEUE_TRANSFER_BIT = 0x00000004,
    VK_QUEUE_SPARSE_BINDING_BIT = 0x00000008,
  // Provided by VK_VERSION_1_1
    VK_QUEUE_PROTECTED_BIT = 0x00000010,
} VkQueueFlagBits;
```

# Resources
https://stackoverflow.com/questions/55272626/what-is-actually-a-queue-family-in-vulkan
https://vkguide.dev/docs/chapter-1/vulkan_command_flow/#:~:text=Queues%20in%20Vulkan%20are%20an,queues%20may%20execute%20at%20once.
https://www.khronos.org/registry/vulkan/specs/1.3/html/