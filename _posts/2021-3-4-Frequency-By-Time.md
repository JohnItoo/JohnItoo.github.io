---
layout: post
title: Frequency By Time
---

There is a technique to find the number of items in a system at any particular instance. Given the time of the entry of all items and the time of departure of these items, one can deduce the number of items at any time during the given period.



# Example : 

Person 1 enters a building at 2pm and leaves the building at 4pm

Person 2 enters a building at 3pm and leaves at 5pm

... in the format Ei, Di, and Vi (where Vi = the value of people/items entering the system at Ei and leaving at Di)

If you are given x unique time queries to find the number of people in the building at all those times, the Big-O complexity of a brute-force solution will be exponential O(max(Di) * Q) and given very large Qs, sometimes an algorithm based on this idea might not finish with reasonable time limits.

There are 2 basic techniques that can be modified to solve a problem of this type.

i) Current Sum technique

ii) Simulation and Prefix Sum technique



# Current Sum

- There exists an array say, arr with its length of at least max(Di) (The last time someone left the building/system) and all its indexes initialized to 0.


- Iterating over the queries modify the value of arr like so: 

arr[Ei]  +=  Vi and arr[Di] -= Vi (i.e at time Ei, Vi enters and at time Di, Vi leaves).


- Go over arr once more. It is important to see that if arr[t] != 0  and arr[t+1] == 0, arr[t+1] should be equal to arr[t] because there was no entry and departure between times t and t+1.

The time complexity of this is O(max(Di))



# Simulation and Prefix Sum

In this technique, you'd have a list of pairs say, building,  For each query, you will append two pairs to this list. i.e the {Ei, Vi} and {Di, -Vi}.

You'd then sort this list of pairs by the first item i.e (time) in the pairs.

Iterating over this list in one pass while keeping a variable of the current sum will help us deduce any information we might need.



Related Problems.

[Years](https://codeforces.com/problemset/problem/1424/G)

[Restaurant Customer](https://cses.fi/problemset/task/1619)

[Water Heater](https://atcoder.jp/contests/abc183/tasks/abc183_d)

[Little Girl and Maximum Sum](https://codeforces.com/problemset/problem/276/C)

