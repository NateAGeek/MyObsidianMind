Ok, so bit of a tricky one for me... I was thinking on doing a two pointer, one from the left and one from the right and increments to get all perm pairs... 
```rust
use std::cmp::min;

impl Solution {
    pub fn array_pair_sum(nums: Vec<i32>) -> i32 {
        let mut max = min(nums[0], nums[1]) + min(nums[nums.len()-2], nums[nums.len()-1]);
        for i in 0..nums.len()/2 {
            let left_min = min(nums[0], nums[i]);
            let right_min = min(nums[nums.len() - 1], nums[nums.len() - 1 - i]);
            if left_min + right_min > max {
                max = left_min + right_min
            } 
        }
        
        let inner_min = min(nums[nums.len()/2], nums[nums.len()/2 + 1]);
        let out_min = min(nums[0], nums[nums.len() - 1]);
        if inner_min + out_min > max {
            max = inner_min + out_min
        } 
            
        return max;
    }
}
```
One of the tricks was to use sort? 