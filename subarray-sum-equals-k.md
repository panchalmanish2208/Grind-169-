# Subarray Sum Equals K
### Question
Given an array of integers nums and an integer k, return the total number of subarrays whose sum equals to k.
A subarray is a contiguous non-empty sequence of elements within an array.
- Example 1:
```
Input: nums = [1,1,1], k = 2
Output: 2
```
- Example 2:
```
Input: nums = [1,2,3], k = 3
Output: 2
```
- Constraints:
```
1 <= nums.length <= 2 * 104
-1000 <= nums[i] <= 1000
-107 <= k <= 107
```

### Approach - [Prefix Sum](https://github.com/panchalmanish2208/Grind-169-/blob/main/Algorithms/prefix-sum.md)

### Solution
#### Soln
- Explanation: Since the new problem does not ask for index but total number instead, we can change our hashmap to "sum k: number of prefix sums that sums up to k".
```js
var subarraySum = function(nums, k) {
    let prefixSum = {
        0:1 // since empty array's sum is 0
    }
    let runningSum = 0;
    let count =0;
    let complement;
    for(let i=0;i<nums.length; i++){
        runningSum += nums[i];
        complement = runningSum - k;
        if(prefixSum[complement]!==undefined){
            count+=prefixSum[complement];
            
        }
        if(prefixSum[runningSum]!==undefined){
            prefixSum[runningSum] += 1;
        }
        else{
            prefixSum[runningSum] =1;
        }
        
    }
    return count;
    
};
```

#### (My attempted Solution) 
- Wrong Answer
- 64 / 93 test cases passed.

![image](https://github.com/panchalmanish2208/Grind-169-/assets/48235415/74025f93-3065-4dd3-b491-ee9e01c909fc)

 ```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var subarraySum = function(nums, k) {
    let prefixSum = {
        0:0 
    }
    let runningSum = 0;
    let count =0;
    let complement;
    for(let i=0;i<nums.length; i++){
        if(k===0){
            count+=1 // since empty array's sum is 0
        }
        runningSum += nums[i];
        complement = runningSum - k;
        if(prefixSum[complement]!==undefined){
            count+=1;
            
        }
        prefixSum[runningSum] =i;
        
    }
    return count;
    
};
```
