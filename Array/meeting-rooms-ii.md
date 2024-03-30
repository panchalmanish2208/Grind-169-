# Meeting Rooms II

## Problem Statement

- Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), find the minimum number of conference rooms required.

#### Example Test Case 1

- **Input**
  - intervals = [[0, 30],[5, 10],[15, 20]]
- **Output**
  - 2
- **Explanation**
  - There are two meeting rooms:
    - Room 1: [0, 30] (occupied by the first meeting)
    - Room 2: [5, 10] (occupied by the second meeting)
  - The third meeting ([15, 20]) can be accommodated in Room 1, as it starts after the first meeting ends. Thus, a minimum of 2 meeting rooms are required.

#### Example Test Case 2

- **Input**
  - intervals = [[0, 30],[5, 10],[15, 20],[25, 35]]
- **Output**
  - 2
- **Explanation**
  - There are two meeting rooms:
    - Room 1: [0, 30] (occupied by the first and fourth meetings)
    - Room 2: [5, 10], [15, 20] (occupied by the second and third meetings)
  - All meetings are accommodated within two rooms, so the minimum number of rooms required is 2.

#### Example Test Case 3

- **Input**
  - intervals = [[0, 5],[2, 10],[9, 12],[15, 20]]
- **Output**
  - 2
- **Explanation**
  - There are two meeting rooms:
    - Room 1: [0, 5], [9, 12] (occupied by the first and third meetings)
    - Room 2: [2, 10], [15, 20] (occupied by the second and fourth meetings)
  - All meetings are accommodated within two rooms, so the minimum number of rooms required is 2.
 
### Solution
#### Explanation of minMeetingRooms Function

- **Function Signature:**
  - Takes an array of meeting time intervals (`intervals`) and returns the minimum number of conference rooms required.
- **Sorting:**
  - Sorts the `intervals` array by start time using `sort`.
- **Iterating Through Meetings:**
  - Iterates through the sorted meetings, starting from the second one.
- **Checking for Available Room:**
  - Compares start times with end times to determine if a meeting can be accommodated in an existing room.
- **Updating or Adding Room:**
  - Updates the end time of an existing room or adds a new room if necessary.
- **Result:**
  - Returns the length of the `rooms` array, representing the minimum number of conference rooms required.
- **Time Complexity:**
  - O(n log n) due to the sorting operation.
- **Space Complexity:**
  - O(n) due to the `rooms` array storing end times.

```js
/**
 * Function to find the minimum number of conference rooms required.
 * @param {number[][]} intervals Array of meeting time intervals.
 * @return {number} Minimum number of conference rooms required.
 */
function minMeetingRooms(intervals) {
    // If no meetings, return 0
    if (intervals.length === 0) return 0;
    
    // Sort the meetings by start time
    intervals.sort((a, b) => a[0] - b[0]);
    
    // Initialize an array to keep track of end times of meetings
    const rooms = [];
    
    // Add the end time of the first meeting to rooms array
    rooms.push(intervals[0][1]);
    
    // Iterate through the sorted meetings starting from the second one
    for (let i = 1; i < intervals.length; i++) {
        const nextMeeting = intervals[i];
        let found = false;
        
        // Check if the current meeting can reuse an existing room
        for (let j = 0; j < rooms.length; j++) {
            if (nextMeeting[0] >= rooms[j]) {
                // If the start time of current meeting is after or equal to the end time of a meeting in a room,
                // then update the end time of that room with the end time of current meeting
                rooms[j] = nextMeeting[1];
                found = true;
                break;
            }
        }
        
        // If no existing room is found for the current meeting, add a new room
        if (!found) {
            rooms.push(nextMeeting[1]);
        }
    }
    
    // The number of rooms required is equal to the length of the rooms array
    return rooms.length;
}

```
