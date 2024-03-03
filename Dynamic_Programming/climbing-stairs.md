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

## Attempted approach (Not recommended & not completed)

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

## Recursion approach
**Note**: Geting Time Limit Exceeded not use this well
```js
function climbingStairsRecursion(n){
    
    if(n===1) return 1;
    if(n===2) return 2;
    if(n===0) return 0;
    let n1 = climbingStairsRecursion(n-1);
    let n2 = climbingStairsRecursion(n-2);
     return n1 + n2;
}
```

## Recursion with Memoization (58 ms)

![image](https://github.com/panchalmanish2208/Grind-169-/assets/48235415/24ca6101-79a7-443f-ad68-795e4019e163)


```js
var climbStairs = function(n) {
    
    // let result = climbingStairsRecursion(n);
    
    let dp = [];
    dp[0] = 0;
    dp[1] = 1;
    dp[2] = 2;
    let result = climbingStairsMemoization(dp, n);
    console.log(result);
    return result;
};

function climbingStairsMemoization(dp, n){
    if(dp[n] === undefined){
        dp[n] = climbingStairsMemoization(dp, n-1) + climbingStairsMemoization(dp, n-2);
        return dp[n];
    }
    return dp[n];
}

```



## Tabulation And Bottom Up Approach

![image](https://github.com/panchalmanish2208/Grind-169-/assets/48235415/314d1759-c8c1-439b-a897-bc22e60c369d)

```js
var climbStairs = function(n) {
    
    // let result = climbingStairsRecursion(n);
    
    // let dp = [];
    // dp[0] = 0;
    // dp[1] = 1;
    // dp[2] = 2;
    // let result = climbingStairsMemoization(dp, n);
    // console.log(result);
    
    let result = climbingStairsTabulation(n);
    return result;
};

function climbingStairsTabulation(n){
    dp = [];
    dp[0] = 0;
    dp[1] = 1;
    dp[2] = 2;
    
    for(let i=3; i<=n; i++){
        dp[i] = dp[i-1] +  dp[i-2];
    }
    // console.table(dp);
    return dp[n];
}
```
## DP - Fibonacci Number - Optimize Space Complexity

![image](https://github.com/panchalmanish2208/Grind-169-/assets/48235415/4fe71acb-24f6-4f36-aa91-e80ec7e1b0e1)

```js
//Space Optimed
var climbStairs = function(n) {
    let result = climbingStairsSpaceOptimized(n);
    return result;
};

function climbingStairsSpaceOptimized(n){
    let first = 1;
    let second = 2;
    let third;
    if(n===1) return 1;
    for(let i=3; i<=n; i++){
        third =  first + second;
        first = second;
        second = third;
    }
    return second;
}
```
