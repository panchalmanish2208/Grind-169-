# Longest Consecutive Sequence

### Question
Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.
You must write an algorithm that runs in O(n) time.

+ Example 1:
```
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```
+ Example 2:
```
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
``` 
+ Constraints:
```
0 <= nums.length <= 105
-109 <= nums[i] <= 109
```
### Solution

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var longestConsecutive = function(nums) {
    if(nums.length ===0) return 0;
    let numsSorted = nums.sort((a,b)=> a-b);
    console.log(numsSorted)
    let count =0;
    let maxLength = 0;
    for(let i=0; i<nums.length; i++){
        maxLength = Math.max(count, maxLength)
        if(numsSorted[i] + 1 === numsSorted[i+1]){
           count++;
        }
        else if (numsSorted[i] === numsSorted[i+1]){
            count =  count;
        }
        else{
            count =  0;
        }
    
    }
    return maxLength+1;
};
```
