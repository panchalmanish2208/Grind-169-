# Contiguous Array
### Question
Given a binary array nums, return the maximum length of a contiguous subarray with an equal number of 0 and 1.
+ Example 1:
```
Input: nums = [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with an equal number of 0 and 1.
```

+ Example 2:
```
Input: nums = [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```
+ Constraints:
  + 1 <= nums.length <= 105
  + nums[i] is either 0 or 1.
 
### Approach - [Prefix Sum](https://github.com/panchalmanish2208/Grind-169-/blob/main/Algorithms/prefix-sum.md)
- Implementation utilizes a hashmap (dictionary) and single pass through the array
- Advantage of prefix sum concept, storing indices where each sum first occurs
- Step-by-step breakdown of code:

  1. Initialize s to 0, tracking running count (prefix sum) of 1s and 0s
  2. Initialize ans to 0, storing maximum subarray length found
  3. Create hashmap mp with initial key-value pair {0: -1}
  4. Iterate through array, updating s for each element at index i:
      - Update s based on element value: s += 1 if v == 1 else -1
      - Check if s exists in mp:
          - If yes, update ans with current length (i - mp[s])
          - If no, add s to mp with index i (mp[s] = i)
  5. Return ans as maximum length of longest contiguous subarray with equal 0s and 1s

- Algorithm relies on prefix sum pattern, monitoring changes in running sum
- Hashmap efficiently tracks indices where sums first occur for constant-time subarray length calculation

##### Example Walkthrough

  - Input array: nums = [0, 1, 0, 1, 1, 0, 0]
  - Initialize s = 0, ans = 0, and hashmap mp with {0: -1}
  - Iteration over array, updating s, mp, and ans:
    - i = 0, nums[i] = 0, s = -1, mp = {0: -1, -1: 0}, ans = 0
    - i = 1, nums[i] = 1, s = 0, mp = {0: -1, -1: 0}, ans = 2
    - i = 2, nums[i] = 0, s = -1, mp = {0: -1, -1: 0}, ans = 2
    - i = 3, nums[i] = 1, s = 0, mp = {0: -1, -1: 0}, ans = 4
    - i = 4, nums[i] = 1, s = 1, mp = {0: -1, -1: 0, 1: 4}, ans = 4
    - i = 5, nums[i] = 0, s = 0, mp = {0: -1, -1: 0, 1: 4}, ans = 6
    - i = 6, nums[i] = 0, s = -1, mp = {0: -1, -1: 0, 1: 4}, ans = 6
- Final result: Longest subarray [1, 0, 1, 1, 0, 0], starting from index 1 to index 6, length = 6

### Solution
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
// prefix sum
var findMaxLength = function(nums) {
    let prefixSum ={
        0: -1
    }
    // console.log(prefixSum[0])
    let maxLength = 0;
    let runningSum = 0;
    let length =0
    for(let i =0; i<nums.length; i++){
        runningSum += nums[i]===0 ? -1:1;
        if(prefixSum[runningSum]!==undefined){
            length = i - prefixSum[runningSum];
            maxLength = Math.max(maxLength, i- prefixSum[runningSum]);
        }
        else{
            prefixSum[runningSum] = i;
        }
    }
    return maxLength;
};
```
