# Gas Station
### Question

There are n gas stations along a circular route, where the amount of gas at the ith station is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from the ith station to its next (i + 1)th station. You begin the journey with an empty tank at one of the gas stations.

Given two integer arrays gas and cost, return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1. If there exists a solution, it is guaranteed to be unique

 

1. **Example 1:**
```
Input: gas = [1,2,3,4,5], cost = [3,4,5,1,2]
Output: 3
Explanation:
Start at station 3 (index 3) and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 4. Your tank = 4 - 1 + 5 = 8
Travel to station 0. Your tank = 8 - 2 + 1 = 7
Travel to station 1. Your tank = 7 - 3 + 2 = 6
Travel to station 2. Your tank = 6 - 4 + 3 = 5
Travel to station 3. The cost is 5. Your gas is just enough to travel back to station 3.
Therefore, return 3 as the starting index.
```
2. **Example 2:**

```
Input: gas = [2,3,4], cost = [3,4,3]
Output: -1
Explanation:
You can't start at station 0 or 1, as there is not enough gas to travel to the next station.
Let's start at station 2 and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 0. Your tank = 4 - 3 + 2 = 3
Travel to station 1. Your tank = 3 - 3 + 3 = 3
You cannot travel back to station 2, as it requires 4 unit of gas but you only have 3.
Therefore, you can't travel around the circuit once no matter where you start.
```
### Approach
- **Validation of Solution Existence**:
  - Calculate the sum of `gas[]` and subtract the sum of `cost[]`.
  - If the result is < 0, no round trip is possible due to insufficient gas.
- **Algorithm Overview**:
  - Initialize `totalTank` and `startingStation` to 0.
  - Iterate through `gas[]` and `cost[]`.
  - Determine `netCost` (`gas[i] - cost[i]`) and update `totalTank`.
- **Finding the Starting Station**:
  - Start at station 0 and evaluate `netCost`.
  - If `netCost` < 0, move to the next station.
  - Track `currentTank` to accumulate gas.
  - Update `startingStation` and reset `currentTank` when it becomes negative.
- **Solution Implementation**:
  - Iterate through `gas[]` and `cost[]`.
  - Update `totalTank` and `currentTank`.
  - If `currentTank` becomes negative, update `startingStation` and reset `currentTank`.
- **Explanation of the Example**:
  - Given `gas: [1, 2, 3, 4, 5]` and `cost: [3, 4, 5, 1, 2]`.
  - Initially, `totalTank = 0`.
  - Start at station 0: `netCost = 1 - 3 = -2` (invalid).
  - Move to station 1: `netCost = 2 - 4 = -2` (invalid).
  - Proceed to station 2: `netCost = 3 - 5 = -2` (invalid).
  - Continue to station 3: `netCost = 4 - 1 = 3` (potential starting point).
  - Update `startingStation` to 3 and `currentTank` to 3.
  - Reach station 4: `netCost = 5 - 2 = 3`, `currentTank` becomes 6.
  - Valid solution exists, with station 3 as the correct starting point.

### Solution 

```js
/**
 * @param {number[]} gas
 * @param {number[]} cost
 * @return {number}
 */
var canCompleteCircuit = function(gas, cost) {
    let totalTank = 0;
    let currentTank =0;
    let netCost =0;
    let start = 0;
    for(let i=0; i<gas.length; i++){
        netCost = gas[i] - cost[i];
        totalTank += netCost;
        currentTank +=netCost;
        if(currentTank<0){
            start= i+1;
            currentTank = 0 ;
        }
    }
    return totalTank>=0? start : -1;
};
```
