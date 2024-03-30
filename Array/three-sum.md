# Three Number Sum

### Question
Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

**Example 1:**

Input: nums = [-1,0,1,2,-1,-4]

Output: [[-1,-1,2],[-1,0,1]]

Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.

nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.

nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.

The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.

**Example 2:**

Input: nums = [0,1,1] Output: []

Explanation: The only possible triplet does not sum up to 0.

**Example 3:**

Input: nums = [0,0,0] Output: [[0,0,0]]

Explanation: The only possible triplet sums up to 0.

**JavaScript Code**
```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var threeSum = function(nums) {
    if(nums.length === 0) return [];
    nums = nums.sort((a,b)=>a-b);
    let res = [];
    for(let i =0 ; i<nums.length-2; i++){
        if(i>0 && nums[i]=== nums[i-1]) continue;
        let j = i+1;
        let k = nums.length-1;
        
        while(j<k){
            let sum = nums[i] + nums[j] + nums[k];
            if(sum ===0){
                res.push([nums[i], nums[j], nums[k]]);
                while(nums[j]===nums[j+1]) j++;
                while(nums[k]===nums[k-1]) k--;
                j++;
                k--;
            }
            else if(sum < 0){
                j++;
            }
            else{
                k--;
            }
        }
    }
    return res;
};
```
### Explanation of threeSum Function
- **Function Signature:**
  - The function `threeSum` takes an array `nums` as input and returns an array of arrays representing all unique triplets in `nums` that sum up to zero.
- **Initialization:**
  - The `res` array is initialized to store the resulting triplets.
- **Base Case:**
  - If `nums` is empty (`nums.length === 0`), the function returns an empty array `[]`. This handles the edge case where there are no elements in the input array.
- **Sorting:**
  - The `nums` array is sorted in ascending order using the `sort` method with a comparator function. Sorting is essential for efficient traversal and duplicate avoidance.
- **Iterating Through `nums` Array:**
  - The function iterates through the sorted `nums` array using a `for` loop with index `i`. The loop runs from 0 to the second-to-last index (`nums.length - 2`).
- **Avoiding Duplicates:**
  - Within the loop, if `i` is greater than 0 and `nums[i]` is equal to the previous element `nums[i-1]`, the function skips to the next iteration using `continue`. This step avoids duplicate triplets in the result.
- **Two Pointers Technique:**
  - Two pointers `j` and `k` are initialized to `i+1` and `nums.length-1`, respectively. These pointers represent the start and end of the remaining array after excluding the current element at index `i`.
- **Moving Pointers:**
  - Inside a `while` loop, the pointers `j` and `k` are adjusted based on the sum of elements at indices `i`, `j`, and `k`.
- **Sum Comparison:**
  - If the sum of elements at indices `i`, `j`, and `k` equals zero, a valid triplet is found, and it is added to the `res` array. Duplicates are skipped by incrementing and decrementing `j` and `k` accordingly.
- **Moving Pointers Based on Sum:**
  - If the sum is less than zero, `j` is incremented to move towards a larger element. If the sum is greater than zero, `k` is decremented to move towards a smaller element.
- **Returning Result:**
  - Finally, the function returns the `res` array containing all unique triplets that sum up to zero.
**Reasoning:**
- Sorting the array allows efficient traversal and duplicate avoidance.
- The two-pointer technique reduces time complexity from O(n^3) to O(n^2).
- Avoiding duplicates within the loop further optimizes the solution.

- **Example Walkthrough:**
  - For the input `nums = [-1, 0, 1, 2, -1, -4]`:
    - After sorting: `[-4, -1, -1, 0, 1, 2]`
    - Iterating through the array:
      - At `i = 0`, `nums[i] = -4`, `j = 1`, `k = 5`
        - Sum = -4 + -1 + 2 = -3, which is less than zero. Increment `j`.
      - At `i = 0`, `nums[i] = -4`, `j = 2`, `k = 5`
        - Sum = -4 + -1 + 2 = -3, still less than zero. Increment `j`.
      - At `i = 0`, `nums[i] = -4`, `j = 3`, `k = 5`
        - Sum = -4 + 0 + 2 = -2, less than zero. Increment `j`.
      - At `i = 0`, `nums[i] = -4`, `j = 4`, `k = 5`
        - Sum = -4 + 1 + 2 = -1, less than zero. Increment `j`.
      - At `i = 0`, `nums[i] = -4`, `j = 5`, `k = 5`
        - Sum = -4 + 2 + 2 = 0, equals zero. Add `[-4, 1, 2]` to `res`.
          - Increment `j` to skip over duplicate.
          - Decrement `k` to skip over duplicate.
      - At `i = 1`, `nums[i] = -1`, `j = 2`, `k = 5`
        - Sum = -1 + 0 + 2 = 1, greater than zero. Decrement `k`.
      - At `i = 1`, `nums[i] = -1`, `j = 2`, `k = 4`
        - Sum = -1 + 0 + 1 = 0, equals zero. Add `[-1, 0, 1]` to `res`.
          - Increment `j` to skip over duplicate.
          - Increment `k` to skip over duplicate.
      - At `i = 2`, `nums[i] = -1`, `j = 3`, `k = 4`
        - Sum = -1 + 1 + 1 = 1, greater than zero. Decrement `k`.
      - The process continues until all unique triplets summing to zero are found.

