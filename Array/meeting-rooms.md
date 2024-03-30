# Meeting Rooms (Not run in leetcode)

### Question

Given an array of meeting time intervals where `intervals[i] = [start_i, end_i]`, determine if a person could attend all meetings.

#### Example 1

##### Input
```plaintext
intervals = [[0, 30], [5, 10], [15, 20]]
```
##### Output
```plaintext
true
```
#####  Explanation
The first meeting starts at 0 and ends at 30. The second meeting starts at 5 and ends at 10. The third meeting starts at 15 and ends at 20. The first meeting overlaps with the third meeting. Therefore, a person cannot attend all meetings without overlapping.

**Test Case 1**

*Input*
```
intervals = [[7, 10], [2, 4]]
```
*Output*
```
true
```
*Explanation*
The first meeting starts at 7 and ends at 10. The second meeting starts at 2 and ends at 4. The meetings do not overlap, so the person can attend all meetings.

**Test Case 2**

*Input*
```
intervals = [[0, 5], [5, 10], [10, 15]]
```
*Output*
```
true
```
*Explanation*
The first meeting starts at 0 and ends at 5. The second meeting starts at 5 and ends at 10. The third meeting starts at 10 and ends at 15. The meetings end and start exactly at the same time, so the person can attend all meetings without overlapping.

### Solution

#### **Solution 1**
**Explanation**
- This function efficiently checks for overlapping meetings by sorting intervals and iterating through them:
- **Sort and Iterate**: Sorts meetings by start time and iterates through.
- **Overlap Check**: Compares start time of each meeting with previous end time.
  - Returns `false` if overlap found.
- **Result**: Returns `true` if no overlaps detected.

```js
function canAttendMeeting(intervals){
    intervals.sort((a, b) => a[0] - b[0]); // Sort meetings by start time
    let end = intervals[0][1];
    for(let i = 1; i < intervals.length; i++) {
        if (intervals[i][0] < end) {
            return false; // Overlapping meetings
        }
        end = Math.max(end, intervals[i][1]); // Update the end time
    }
    return true; // No overlapping meetings
}

```
#### **My Attempted Solution*
Wrong Answer
For ex.
failed testcase - canAttendMeeting([[5, 10], [1, 4], [2, 3]]);
```js
function canAttendMeeting(intervals){
    let start = intervals[0][0];
    let end = intervals[0][1];
    let n = intervals.length;
    for(let i =1; i<n; i++){
        if(intervals[i][0]>end){
            start = intervals[i][0];
            end =intervals[i][1];
        }
        else if(start>intervals[i][1]){
            start = start;
            end = end;
        }
        else{
            return false;
        }
    }
    return true;
}
```
