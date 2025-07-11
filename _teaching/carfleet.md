---
title: "Car Fleet"
collection: datastructures
permalink: /datastructures/stacks/carfleet
date: 2025-07-08
---

This is an interesting problem from [LeetCode's Car Fleet](https://leetcode.com/problems/car-fleet/). While it may seem complex at first, visualizing the problem helps understand the concept better. Let's break it down step by step.

# Question 
There are n cars at given miles away from the starting mile 0, traveling to reach the mile target.

You are given two integer array position and speed, both of length n, where position[i] is the starting mile of the ith car and speed[i] is the speed of the ith car in miles per hour.

A car cannot pass another car, but it can catch up and then travel next to it at the speed of the slower car.

A car fleet is a car or cars driving next to each other. The speed of the car fleet is the minimum speed of any car in the fleet.

If a car catches up to a car fleet at the mile target, it will still be considered as part of the car fleet.

Return the number of car fleets that will arrive at the destination.

======

# Examples

Car positions = [7,5,2]
Car speed = [5,6,3]

Let's visualize this with a simple diagram:

```
Target = 20 miles
                                        
0   1   2   3   4   5   6   7   8  ... 20
                |       |       |      
                C3      C2      C1
                (3)     (6)     (5)    
```

Initial state:
- Car 1 (C1) at position 7, speed 5 mph
- Car 2 (C2) at position 5, speed 6 mph
- Car 3 (C3) at position 2, speed 3 mph

After sorting by position (reverse order), we calculate time to target for each car:
1. C1: (20-7)/5 = 2.6 hours
2. C2: (20-5)/6 = 2.5 hours
3. C3: (20-2)/3 = 6.0 hours

Analysis:
- C2 would catch up to C1 (2.5 < 2.6), forming a fleet at C1's speed
- C3 takes much longer (6.0 hours) and won't catch up

Result:
- Fleet 1: C1 + C2 (moving at speed 5)
- Fleet 2: C3 (moving at speed 3)

Therefore, 2 fleets will arrive at the target.

# Solution

Let's implement the solution in Python. The key idea is to:
1. Sort cars by position in reverse order (rightmost cars first)
2. Calculate time to target for each car
3. Use a stack to track potential fleets
4. Compare arrival times to determine if cars will form a fleet

```python
from collections import deque
from typing import List


class CarFleet:
    def findMaxCarFleets(self, target: int, position: List[int], speed: List[int]) -> int:
        # Combine position and speed into pairs and sort by position (descending)
        combined_pairs = [(pos, spd) for pos, spd in zip(position, speed)]
        combined_pairs.sort(reverse=True)
        
        stack = deque()
        
        # Process each car from right to left
        for pos, spd in combined_pairs:
            # Calculate time to reach target
            time_to_target = (target - pos) / spd
            stack.append(time_to_target)
            
            # If current car catches up to the car in front (takes less time),
            # they form a fleet, so we can remove the current car
            if len(stack) >= 2 and stack[-1] <= stack[-2]:
                stack.pop()
        
        return len(stack)
```

## Time and Space Complexity
- Time Complexity: O(n log n) due to sorting
- Space Complexity: O(n) for the stack

## Key Points
1. We sort by position in reverse order to process rightmost cars first
2. For each car, we calculate its time to reach the target
3. If a car would reach the target faster than the car in front, it means they'll form a fleet
4. The number of elements in our stack at the end represents the number of fleets