# 3Sum Closest
### Question
Given an integer array nums of length n and an integer target, find three integers in nums such that the sum is closest to target.
Return the sum of the three integers.
You may assume that each input would have exactly one solution.

- Example 1:
```
Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```
- Example 2:
```
Input: nums = [0,0,0], target = 1
Output: 0
Explanation: The sum that is closest to the target is 0. (0 + 0 + 0 = 0).
```
- Constraints:
```
3 <= nums.length <= 500
-1000 <= nums[i] <= 1000
-104 <= target <= 104

```

### Solution
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var threeSumClosest = function(nums, target) {
    nums.sort((a, b) => a - b); // Sort the array in ascending order
    let closestSum = nums[0] + nums[1] + nums[2]; // Initialize closest sum
    
    for (let i = 0; i < nums.length - 2; i++) {
        let left = i + 1; // Pointer for the element to the right of nums[i]
        let right = nums.length - 1; // Pointer for the last element in the array
        
        while (left < right) {
            const currentSum = nums[i] + nums[left] + nums[right]; // Calculate current sum
            if (Math.abs(target - currentSum) < Math.abs(target - closestSum)) {
                closestSum = currentSum; // Update closest sum if current sum is closer to target
            }
            if (currentSum < target) {
                left++; // Move left pointer to increase the sum
            } else {
                right--; // Move right pointer to decrease the sum
            }
        }
    }
    
    return closestSum;
};
```
### Explanation
#### ThreeSum Closest Algorithm Explanation

1. Sort `nums` in ascending order.
2. Initialize `closestSum` with the sum of the first three elements.
3. Use a two-pointer approach to find the closest sum to the target.
4. Update `closestSum` if the current sum is closer to the target.
5. Move pointers based on the sum's relation to the target.
6. Repeat until all combinations are explored.
7. Return `closestSum`.

#### Example Walkthrough:
   - Given nums = [-1, 2, 1, -4] and target = 1:
     - Sorted nums: [-4, -1, 1, 2]
     - Initial closestSum = -4 + (-1) + 1 = -4.
     - Update closestSum to 2 when encountering [-1, 1, 2].
     - Return closestSum = 2.
