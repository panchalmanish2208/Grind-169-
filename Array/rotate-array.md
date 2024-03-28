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
