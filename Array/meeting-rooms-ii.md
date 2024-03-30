# Meeting Rooms II

### Problem Statement

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
