# Insert Interval

### Question

You are given an array of non-overlapping intervals intervals where intervals[i] = [starti, endi] represent the start and the end of the ith interval and intervals is sorted in ascending order by starti. You are also given an interval newInterval = [start, end] that represents the start and end of another interval.
Insert newInterval into intervals such that intervals is still sorted in ascending order by starti and intervals still does not have any overlapping intervals (merge overlapping intervals if necessary).
Return intervals after the insertion.

**Example 1:**

Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]

**Example 2:**

Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]

Output: [[1,2],[3,10],[12,16]]

Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].

**Approach**
- set start and end of newInterval as a and b.
- declare a result array
- Using single **For loop** will check start and end of each interval in intervals array
- for this loop we already created extra counter even we have "i". As when this loop completes then will lose the track of normal nonoverlapper intervals
- So first will check for the overlapping case
- For that first will check e > a
    + So if no then will directly push that interval in the resultant array as there is no overlap
    + And if yes that check for further condition as there are two cases 1) either a lies between s and e or 2) both s and e are greater then a & b
- Second will check for conditon s <= b
    + If yes that is b lies between s and e, then will replace the a & b of newInterval with min(s,a) & max(b,e)
    + If No that is there is no overlap
- Then will push the modified newInterval to the resultant array
- After that will create new loop to push remaining non-overlapped interval to resultant array using counter

**JavaScript Code**
```js
/**
 * @param {number[][]} intervals
 * @param {number[]} newInterval
 * @return {number[][]}
 */
var insert = function(intervals, newInterval) {
    let a = newInterval[0];
    let b = newInterval[1];
    let counter = 0;
    let length = intervals.length;
    let resultArray = []
    for(let i=0;i<length;i++){
        let s = intervals[i][0];
        let e = intervals[i][1];
        if(e<a){
            resultArray.push(intervals[i]);
            counter++
        }
        else if(s<=b){
            [a,b] = [Math.min(s,a), Math.max(e,b)];
            counter++
        }
    }
    resultArray.push([a,b]);
    
    for(counter;counter<length;counter++){
        resultArray.push(intervals[counter]);
    }
    return resultArray;
};
```

