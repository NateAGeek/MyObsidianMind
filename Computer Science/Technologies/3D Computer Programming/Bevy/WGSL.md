## Overview
Bevy seems to primarily use WGSL to handle shaders


### Functions
* Uses `fn` to define them.
* We do type declaring via `(a: type)` and we define the output of the function via ` -> type`. 
* Function calls are basic `a();`
#### Entry Points
You can annotate the function and what their pipeline entry point is. So the current common supported one is `@vertex`, `@fragment` or `@compute`. 
- @vertex: Is the vertex in the shader pipeline that will process the vertexes that will be outputted. This can alter the geometry. 
- @fragment: Is the shader that controls the output of pixel color per frame
- @compute: Is a shader used for computing multiple groups. https://webgpufundamentals.org/webgpu/lessons/webgpu-compute-shaders.html
- 