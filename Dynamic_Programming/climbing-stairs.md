# Climbing Stairs
### Questions
You are climbing a staircase. It takes n steps to reach the top.
Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?
Example 1:
Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
Example 2:
Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
 

Constraints:

1 <= n <= 45

## Attempted approach (Not recommended)

```js
/**
 * @param {number} n
 * @return {number}
 */
var climbStairs = function(n) {
    let r = []
    let result = climbStairsRecursive(n, r);
    console.log(result)
};

function climbStairsRecursive(n, r){
    let s1;
    let s2;
    
    if(n===0){
        return r;
    }
    if(n>=1){
        
        r.push(1);
        s1 = climbStairsRecursive(n-1, r)
    }
    if(n>=2){
        r.pop();
        r.push(2);
        s2 = climbStairsRecursive(n-2, r)
    }
    let result = []
    result.push(s1);
    result.push(s2);
}
```
