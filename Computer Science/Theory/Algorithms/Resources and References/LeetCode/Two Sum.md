My solution was:
```rust
impl Solution {
    pub fn two_sum(nums: Vec<i32>, target: i32) -> Vec<i32> {
        for i in 0..nums.len() {
            for j in i + 1..nums.len() {
                if nums[i] + nums[j] == target {
                    return vec![i as i32, j as i32];
                }
            }
        }
        return vec![]
    }
}
```

Basically is sum $n^2$... But someone made a hashmap like system that was cool.
```rust
impl Solution {
    pub fn two_sum(nums: Vec<i32>, target: i32) -> Vec<i32> {
        use std::collections::HashMap;
        
        let mut seen: HashMap<i32, i32> = HashMap::with_capacity(nums.len());
        for (i, v) in nums.iter().enumerate() {
            let complement = target - v;
            match seen.get(&complement) {
                Some(&i2) => return vec![i as i32, i2 as i32],
                None => seen.insert(*v, i as i32),
            };
        }
        unreachable![]
    }
}
```
Basically we store the complement to each value subtracted from the target. That is a nice way to see what number is the complement to the value we are searching.

For example if the target was 11
[8, 2, 3, 6, 10]
the first complement would be 11 - 8 = 3, so if there is a 3 then we know we found our complement to the target, however, since there is not we store the v and the index of that value. continue on we have 11 - 2 = 4. Although 4 would be a solution, in the list we do not have 4, since the problem stated we can only have one solution. 11 -  3 = 8, and since we have the index of 8 as 0, we can now return the the stored index and the current one. 