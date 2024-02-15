

Given the weights and profits of ‘N’ items, we are asked to put these items in a knapsack which has a capacity ‘C’. The goal is to get the maximum profit out of the items in the knapsack. Each item can only be selected once, as we don’t have multiple quantities of any item.

Let’s take the example of Merry, who wants to carry some fruits in the knapsack to get maximum profit. Here are the weights and profits of the fruits:

Items: { Apple, Orange, Banana, Melon }
Weights: { 2, 3, 1, 4 }
Profits: { 4, 5, 3, 7 }
Knapsack capacity: 5

![image](https://github.com/panchalmanish2208/Grind-169-/assets/48235415/f9981d79-cede-4939-a2f4-9df9c83c604a)
All green boxes have a total weight that is less than or equal to the capacity (7), and all the red ones have a weight that is more than 7. The best solution we have is with items [B, D] having a total profit of 22 and a total weight of 7.
Here is the code for the brute-force solution:
![image](https://github.com/panchalmanish2208/Grind-169-/assets/48235415/69021ff2-900f-407c-af02-aad0629c5ae0)
![image](https://github.com/panchalmanish2208/Grind-169-/assets/48235415/db796b8e-cb42-4fc8-8531-8042a5d57d7e)

### Time and Space complexity
The time complexity of the above algorithm is exponential **O(2<sup>n</sup>)**, where ‘n’ represents the total number of items. This can also be confirmed from the above recursion tree. 
As we can see, we will have a total of ‘31’ recursive calls – calculated through **(2<sup>n</sup>) + (2<sup>n</sup>) -1**, which is asymptotically equivalent to O((2<sup>n</sup>))
The space complexity is O(n). This space will be used to store the recursion stack. Since the recursive algorithm works in a depth-first fashion, which means that we can’t have more than ‘n’ recursive calls on the call stack at any time.
Let’s visually draw the recursive calls to see if there are any overlapping sub-problems. As we can see, in each recursive call, profits and weights arrays remain constant, and only capacity and currentIndex change. For simplicity, let’s denote capacity with ‘c’ and currentIndex with ‘i’:

![image](https://github.com/panchalmanish2208/Grind-169-/assets/48235415/dc20f34b-9401-489f-bd82-7dd8ac59a01d)
We can clearly see that ‘c:4, i=3’ has been called twice. Hence we have an overlapping sub-problems pattern. We can use Memoization to efficiently solve overlapping sub-problems.

## Top-down Dynamic Programming with Memoization #
Memoization is when we store the results of all the previously solved sub-problems and return the results from memory if we encounter a problem that has already been solved.

Since we have two changing values (capacity and currentIndex) in our recursive function knapsackRecursive(), we can use a two-dimensional array to store the results of all the solved sub-problems. As mentioned above, we need to store results for every sub-array (i.e. for every possible index ‘i’) and for every possible capacity ‘c’.


## Bottom-up Dynamic Programming 
Let’s try to populate our `dp[][]` array from the above solution by working in a bottom-up fashion. Essentially, we want to find the maximum profit for every sub-array and for every possible capacity. 
This means that `dp[i][c]` will represent the maximum knapsack profit for capacity ‘c’ calculated from the first ‘i’ items.

So, for each item at index ‘i’ (0 <= i < items.length) and capacity ‘c’ (0 <= c <= capacity), we have two options:

Exclude the item at index ‘i’. In this case, we will take whatever profit we get from the sub-array excluding this item =>  `dp[i-1][c]`
Include the item at index ‘i’ if its weight is not more than the capacity. In this case, we include its profit plus whatever profit we get from the remaining capacity and from remaining items => `profit[i] + dp[i-1][c-weight[i]]`
Finally, our optimal solution will be maximum of the above two values:

    dp[i][c] = max (dp[i-1][c], profit[i] + dp[i-1][c-weight[i]])

![image](https://github.com/panchalmanish2208/Grind-169-/assets/48235415/e19101e3-018f-420d-94e7-f0fe2e452871)

### Time and Space complexity 
The above solution has the time and space complexity of **O(N∗C)**, where ‘N’ represents total items and ‘C’ is the maximum capacity.

### How can we find the selected items? #
As we know, the final profit is at the bottom-right corner. Therefore, we will start from there to find the items that will be going into the knapsack.

As you remember, at every step we had two options: include an item or skip it. If we skip an item, we take the profit from the remaining items (i.e. from the cell right above it); if we include the item, then we jump to the remaining profit to find more items.

Let’s understand this from the above example:
![image](https://github.com/panchalmanish2208/Grind-169-/assets/48235415/70dcb11f-7825-46c4-99b8-add55ff76733)

1. ‘22’ did not come from the top cell (which is 17); hence we must include the item at index ‘3’ (which is item ‘D’).
2. Subtract the profit of item ‘D’ from ‘22’ to get the remaining profit ‘6’. We then jump to profit ‘6’ on the same row.
3. ‘6’ came from the top cell, so we jump to row ‘2’.
4. Again ‘6’ came from the top cell, so we jump to row ‘1’.
5. ‘6’ is different than the top cell, so we must include this item (which is item ‘B’).
6. Subtract the profit of ‘B’ from ‘6’ to get profit ‘0’. We then jump to profit ‘0’ on the same row. As soon as we hit zero remaining profit, we can finish our item search.
7. Thus the items going into the knapsack are {B, D}.
Let’s write a function to print the set of items included in the knapsack.

### Challenge #
##### Can we improve our bottom-up DP solution even further? Can you find an algorithm that has **O(C)** space complexity?
* The solution above is similar to the previous solution, the only difference is that we use 
  * `i%2` instead if `i` and
  * `(i-1)%2` instead if `i-1`. 
* This solution has a space complexity of O(2∗C)=O(C), where ‘C’ is the maximum capacity of the knapsack.

```js
//top bottom
function solveKnapsackRecursive(profits, weights,capacity){
    let dp = []
function knapsack(profits, weights, capacity, currentIndex){
    //
    if(capacity<=0 || currentIndex >= profits.length) return 0;

    dp[currentIndex] = dp[currentIndex] || [];
    if(typeof dp[currentIndex][capacity] !== 'undefined'){
        return dp[currentIndex][capacity];
    }
    let profit1 = 0;
    if(weights[currentIndex]<= capacity){
        profit1 = profits[currentIndex] + knapsack(profits, weights, capacity- weights[currentIndex], currentIndex+1)
    } 
    let profit2 = knapsack(profits, weights, capacity, currentIndex+1);
     dp[currentIndex][capacity] = Math.max(profit1,  profit2)

    return dp[currentIndex][capacity];
}
    return knapsack(profits, weights, capacity, 0);
}

//Bottom-ups or Tabulation
/*
* create 2-D array where no.of columns-capacity +1 & no. of rows - weights.length 
* filled 1st column with 0 profitas it's for capacity = 0 so no profit
* filled 1st row with with profit[0] if it less then the corresponding capacity
* Formula's to use    
    * use profit1 = profits[i] + dp[i-1][c-weight[i]] 
    * profit2 = dp[i-1][c]
    * dp[i][c] = Max(profit1, profit2)
*return dp[n-1][c]
* Method to select elements included for the max profit
* check the element in just one above row in the same column
* if both the element are same then go to the above column
*if not subtract the profit of the total profit until it becomes 
* And stop when i<0 
*/
function solveKnapsackIterative(profits, weights, capacity){
    let n = profits.length;
    let dp = Array(n).fill(0).map(()=>Array(capacity+1).fill(0));
    //console.log(dp);
    for(let i=0; i<n; i++){
        dp[i][0]= 0;
    }
    for(let c=0; c<capacity+1 ; c++){
        if(weights[0]<=c) dp[0][c] = profits[0];
    }
    let profit1;
    let profit2;
    for(let i=1; i<n; i++){
        for(let c=1;c<capacity+1;c++){
            profit1 = 0;
            profit2 = 0;
            if(weights[i]<=c){
                profit1 = profits[i] + dp[i-1][c-weights[i]]
            }
            profit2 = dp[i-1][c]
            dp[i][c] = Math.max(profit1, profit2);
        }
    }
    console.table(dp);

    let totalProfit = dp[n-1][capacity];
    let selectedWeights = ' ';
    let remainingCapacity = capacity;
    for(let i=n-1; i>0; i--){
        if(totalProfit!==dp[i-1][remainingCapacity]){
            selectedWeights = `${weights[i]} ${selectedWeights}`;
            remainingCapacity -= weights[i];
            totalProfit -= profits[i];
        }

    }
    console.table(selectedWeights)
    return dp[n-1][capacity];
}


// solution with O(C) complexity
function solveKnapsackIterative2(profits, weights, capacity){
    let n = profits.length;
    let dp = Array(2).fill(0).map(()=>Array(capacity+1).fill(0));
    //console.log(dp);
    for(let c=0; c<capacity+1 ; c++){
        if(weights[0]<=c) dp[0][c] = dp[1][c] = profits[0];
    }
    let profit1;
    let profit2;
    for(let i=1; i<n; i++){
        
        for(let c=1;c<capacity+1;c++){
            profit1 = 0;
            profit2 = 0;
            if(weights[i]<=c){
                profit1 = profits[i] + dp[(i-1)%2][c-weights[i]]
            }
            profit2 = dp[(i-1)%2][c]
            dp[i%2][c] = Math.max(profit1, profit2);
        }
        console.table(dp);
    }
    return dp[(n-1)%2][capacity];
}

let profits = [1, 6, 10, 16]
let weights = [1, 2, 3, 5]
// console.log(`Total knapsack profit --->${solveKnapsack(profits, weights, 7)}`)
//console.log(`Total knapsack profit --->${solveKnapsackIterative2(profits, weights, 7)}`)
```
### Chalenge 2
This space optimization solution can also be implemented using a single array. It is a bit tricky, but the intuition is to use the same array for the previous and the next iteration!

If you see closely, we need two values from the previous iteration: dp[c] and dp[c-weight[i]]

Since our inner loop is iterating over c:0-->capacity, let’s see how this might affect our two required values:

When we access dp[c], it has not been overridden yet for the current iteration, so it should be fine.
dp[c-weight[i]] might be overridden if “weight[i] > 0”. Therefore we can’t use this value for the current iteration.
To solve the second case, we can change our inner loop to process in the reverse direction: c:capacity-->0. This will ensure that whenever we change a value in dp[], we will not need it again in the current iteration.

Can you try writing this algorithm?
![image](https://github.com/panchalmanish2208/Grind-169-/assets/48235415/315752cd-0362-46ce-8f1f-b234a4cd662c)
![image](https://github.com/panchalmanish2208/Grind-169-/assets/48235415/dbc28c1c-7b6f-42f8-b18c-85b7b0507973)

