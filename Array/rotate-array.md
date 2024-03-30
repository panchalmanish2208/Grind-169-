# Rotate Array
### Question
Given an integer array nums, rotate the array to the right by k steps, where k is non-negative.

1. Example 1:
```
Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```
2. Example 2:
```
Input: nums = [-1,-100,3,99], k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
```
Constraints:
```
1 <= nums.length <= 105
-231 <= nums[i] <= 231 - 1
0 <= k <= 105
 ```
**Follow up:**

Try to come up with as many solutions as you can. There are at least three different ways to solve this problem.
Could you do it in-place with O(1) extra space?

### Solutions
* **Approach 0** Using Splice
  * Runtime: 77 ms, faster than 73.92% of JavaScript online submissions for Rotate Array.
  * Memory Usage: 57 MB, less than 69.04% of JavaScript online submissions for Rotate Array.
  - Calculate effective rotation steps: 
  - Compute k %= nums.length
  **Example Walkthrough:**
  - Input: nums = [1, 2, 3, 4, 5, 6, 7], k = 3
  - Effective rotation steps: k %= 7 = 3
  - Splice last k elements: [5, 6, 7]
  - Splice them to the beginning of the array: [5, 6, 7, 1, 2, 3, 4]
  - Resulting rotated array: [5, 6, 7, 1, 2, 3, 4]

  ```js
  var rotate = function (nums, k) {
    const len = nums.length
    k = (k % len)
    
    let end = nums.splice(len - k)

    nums.splice(0,0,...end)
  };
  ```
* **Approach 1** Using Reverse (O(1))
  * Runtime: 99 ms, faster than 7.38% of JavaScript online submissions for Rotate Array.
  * Memory Usage: 59.9 MB, less than 29.19% of JavaScript online submissions for Rotate Array.
  - Calculate effective rotation steps: 
  - Compute k %= nums.length to handle cases where k > array length
  - Define reverse function: Reverses elements between given indices
  - Reverse entire array: Brings last k elements to front, first n-k elements to end
  - Reverse first k elements: Places them at end of array
  - Reverse remaining elements: Shifts them to beginning of array

  Example Walkthrough:
  - Input array: nums = [1, 2, 3, 4, 5, 6, 7], k = 3
  - Effective rotation steps: k %= 7 = 3
  - Reverse entire array: [7, 6, 5, 4, 3, 2, 1]
  - Reverse first k elements: [5, 6, 7, 4, 3, 2, 1]
  - Reverse remaining elements: [5, 6, 7, 1, 2, 3, 4]
  - Resulting rotated array: [5, 6, 7, 1, 2, 3, 4]
```js
let reverse = function(nums, start, end){
    while(start<end){
        [nums[start], nums[end]] = [nums[end], nums[start]]
        start++;
        end--;
    }
}

var rotate = function(nums, k) {
    let n = nums.length;
    k%=n;
    reverse(nums,0, n-1);
    reverse(nums,0, k-1);
    reverse(nums,k, n-1);
    return nums;
}
```
  
* **Approach 2** Using Extra Space

  - Calculate effective rotation steps:
    - Take modulo of k with array length (k %= nums.length)
    - Reason: Ensure effective rotation even if k is larger than array length
  - Create new array rotated
    - Reason: To store rotated elements without modifying original array
  - Iterate original array elements:
    - Calculate new index after rotation: (i + k) % nums.length
    - Reason: Determine correct position for each element after rotation
    - Assign original element to calculated index in rotated array
  - Populate rotated array, copy elements back to nums array
    - Reason: Update original array with rotated elements

```js
  var rotate = function(nums, k) {
    // for(let i=0; i<k; i++){
    //     nums.unshift(nums.pop());
    // }
    
    // using extra space
    const n = nums.length;
    k%=n;
    const rotated = [];
    for(let i=0; i<n; i++){
        rotated[(i+k)%n] = nums[i];
    }
    for(let i =0; i<n; i++){
        nums[i] = rotated[i];
    }
    return nums;
  };
 ```

* **Approach 3** Using unshift (Not Recommend)
  * All testcaes pased but Time Rate Exceed
  * ```js
     for(let i=0; i<k; i++){
         nums.unshift(nums.pop());
    }
    ```
