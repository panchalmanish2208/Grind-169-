# Prefix Sum
### What is Prefix Sum?
The prefix sum of an array at index 'i' is the sum of all numbers from index '0' to 'i'. By computing and storing the prefix sum of an array, you can easily answer queries about the sum of any subarray in constant time.

### Prefix Sum vs. Sliding Window
Both prefix sum and sliding window are techniques to solve subarray-related problems. The choice between them depends on the nature of the problem:

Prefix sum is generally used for problems that ask about the sum of subarrays, as it allows for constant-time range sum queries.
The sliding window is typically utilized for problems related to contiguous subarrays of a certain size or condition, e.g., maximum sum of a subarray of size 'k'.

### Dive Deeper into Subarray Sum Problems
Understanding how to manipulate subarrays is key to mastering many algorithms.

#### Subarray with Given Sum
The subarray sum problem, as showcased above, tries to find a contiguous subarray that sums up to a particular number.

#### Zero Sum Subarrays
A variant of the subarray sum problem is finding subarrays that sum to zero. This can be solved using the prefix sum approach and hashing.

#### Longest Subarray with Sum k
In some problems, instead of finding any subarray with a given sum, you might be tasked with finding the longest subarray with a specific sum. This is a slight twist but can be approached using similar methods.

#### Smallest Subarray with Sum Greater Than a Given Value
Another variant would be to find the smallest subarray whose sum is greater than a given value.

#### Maximum Sum of Subarrays of Size k
To find the maximum sum of all subarrays of a specific size 'k', you can utilize the sliding window technique.

#### Suffix Sum
Just as we have prefix sum that calculates the sum from the beginning to a specific index, we can also calculate suffix sum, which calculates the sum from a particular index to the end of the array.


#### Practice Problem: Subarray Sum
Given an array of integers and an integer target, find a subarray that sums to target and return the start and end indices of the subarray.
Input: arr: 1 -20 -3 30 5 4 target: 7
Output: 1 4
Explanation: -20 - 3 + 30 = 7. The indices for subarray [-20,-3,30] is 1 and 4 (right exclusive).


#### Explanation
- Subarray sum [i, j] = Prefix sum[j] - Prefix sum[i - 1]
- Prefix sum: cumulative sum from index 0 to i
- Efficient subarray sum calculation: Constant time using prefix sums
- Maintain dictionary: Prefix_sum: index while iterating through array
- If prefix_sum - target in dictionary, subarray found
![image](https://github.com/panchalmanish2208/Grind-169-/assets/48235415/053d8796-3890-4a2a-96bf-6b84fba28e70)
#### JavaScript Code
```js
function subarraySum(arr, target) {
    // prefix_sum 0 happens when we have an empty array
    const prefixSums = new Map([[0, 0]]);
    let curSum = 0;
    for (let i = 0; i < arr.length; i++) {
        curSum += arr[i];
        const complement = curSum - target;
        if (prefixSums.has(complement)) {
            return [prefixSums.get(complement), i + 1];
        }
        prefixSums.set(curSum, i + 1);
    }
}
```
