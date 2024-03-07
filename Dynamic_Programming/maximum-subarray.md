# Maximum Subarray

## Question
 Given an integer array nums, find the subarray with the largest sum, and return its sum.

Example 1:
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: The subarray [4,-1,2,1] has the largest sum 6.
Example 2:

Input: nums = [1]
Output: 1
Explanation: The subarray [1] has the largest sum 1.
Example 3:

Input: nums = [5,4,-1,7,8]
Output: 23
Explanation: The subarray [5,4,-1,7,8] has the largest sum 23.

## Problem Explanation
- We have to the max sum of the subarray among all the arrays
- Here subarray is a segment of contiguous elements within the array.
- If there is no -ve elements then max sum is entire sum each elements of array
- If there are -ve elements then there may be different sub arrays with different sum.

## Brute force approach using two nested loops

```js
var maxSubArray = function(nums) {
    //let result = maxSubArrayRecursive(nums, 0, 0);
    let n = nums.length;
    let maxSubarray = Number.MIN_SAFE_INTEGER;
    
    for(let i=0; i<n; i++){
        let subArraySum = 0;
        for(let j=i; j<n; j++){
            subArraySum +=  nums[j]
            maxSubarray = Math.max(maxSubarray, subArraySum);
        }
    }
    return maxSubarray;
};
```
## Kadane’s Algorithm
### What is Kadane’s Algorithm?
- Kadane’s Algorithm is a dynamic programming algorithm used to solve the maximum subarray problem.
- The maximum subarray problem is the task of finding the contiguous subarray within a one-dimensional array of numbers that has the largest sum.
- The subarray can be of any length, including the entire array. Kadane’s Algorithm works by scanning through the array and keeping track of the current subarray sum, updating it as it goes along.
- The algorithm returns the maximum subarray sum found.


### How Kadane’s Algorithm works
- Kadane’s Algorithm works by keeping track of two variables as it scans through the array: the current subarray sum and the maximum subarray sum seen so far.
- The algorithm starts by setting both variables to the value of the first element in the array.
- The algorithm then iterates through the array, adding each element to the current subarray sum.
- If the current subarray sum becomes negative, the algorithm resets it to zero, effectively discarding any negative subarrays.
- The maximum subarray sum seen so far is updated whenever the current subarray sum exceeds it.


