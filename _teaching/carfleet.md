---
title: "Car Fleet"
collection: datastructures
permalink: /datastructures/stacks/carfleet
date: 2025-07-08
---

Interesting question which has been recommened by neetcode and other places. I really could not get it right in the first place. May be, its just me, but once i was able to draw it out and visualize it. Was able to understand the concept. 

The question is mentioned here https://leetcode.com/problems/car-fleet/

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
Car speed = [1,2,3]

First to understand it, we need to draw it out . 

Target (20)
|
|   Car A (7,5):  ----------->
|   Car B (6,6):  -------------->
|
0

Time Axis →
[Car B]------------------>
   [Car A]------------------->
      (Car B catches up to Car A before target)