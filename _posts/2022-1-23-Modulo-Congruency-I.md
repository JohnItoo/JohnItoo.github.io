---
layout: post
title:  Solve 1 Modulo Congruency Problem
author: John Ohue
summary: This is the most common form of modulo congruency in algorithm problems.
publish : true
---
{% include head.html %}

<b> Statement </b>

When you have 2 numbers whose difference is divisible by m, then both numbers have the same modulo when divided by m. 

More formally,

if (|a-b|)  % k == 0, then a % k == b % k


 This is just the idea needed for some common modulo problems.
For more insight see [Wiki](https://en.wikipedia.org/wiki/Modular_arithmetic#:~:text=Contents-,1,Congruence,-1.1)

<b> Related Problems </b>
- [Divisibility of Differences](https://codeforces.com/problemset/problem/876/B)
- [Subarray Divisilibity](https://cses.fi/problemset/task/1662)

One interesting problem where this idea is a subproblem and serves as an optimisation is Leetcode's [Continuous Subarray Sum](https://leetcode.com/problems/continuous-subarray-sum/) problem.

A summary of the problem is: Given an array of numbers, check if there is a continuous subarray with more than one element and whose sum is a multiple of a given number k.

<b> How to think about this problem? </b>

Lets assume the length of the array is N, we want to find an optimal solution to this problem. 


A basic solution will be: for each element in the array, check if while moving to the right (and adding each element encountered), we get a sum divisible by k. This solution is an $$ O(N^2)$$ solution.

Can we do better with the time complexity? I will go all Obama and say <i> yes we can! </i> Infact the time constraints on the problem statement shows us we need to do better.

<b> How to do better? </b>

We can change this to a prefix sum problem, i.e do what we are doing in the previous solution but with a prefix sum array. This in itself doesn't optimise the solution. Infact, it is still an $$ O(N^2)$$ solution. 

Using Basic prefix sums. For each index in the prefix sum array we can check if a valid array ends here.

For instance array:

{23, 2, 4, 6, 7} will yield prefix sum array {0, 23, 25, 29, 35, 42}

if we fix any two indexes i and j (i < j) in our prefix array,
We know that prefix[j] - prefix[i] will give us the sum of original array[i] to orginal array[j-1].

So for every element we can find an array ending at this element, say at index j in $$ O(N^2)$$  by iterating i over the prefix sum array from the beginning and seeing if any sum will be divisible by K.

This just shows that this is $$ O(N^2)$$.

<b> Optimization </b>

Since we know we are just looking for any element that appeared to the left of our current element that (prefix[j] - prefix[i]) % k == 0, we can use our lemma we stated above. 

With this knowledge we can create a modulo array and mod each element in our prefix Sum

From the previous example our mod array will be

{0, 5, 1, 5, 5, 0}

While traversing the array we can keep the first index we see any modulo value in say a hashmap. If we see the same modulo value and the distance is >= 3 we have found an answer.

<b> C++ Code </b>

```
class Solution {
public:
    bool checkSubarraySum(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> prefixSum(n+1, 0);
        for(int i = 1; i <= n; i++) {
            prefixSum[i] = prefixSum[i-1] + nums[i-1];
        }
        vector<int> mods(n+1, 0);
        for(int i = 0; i <= n; i++) {
            mods[i] = prefixSum[i] % k;
        }
        unordered_map<int, int> seenModulos;
        
        for(int i = 0; i <= n; i++) {
            if(seenModulos.find(mods[i]) == seenModulos.end()) {
                seenModulos[mods[i]] = i;
                continue;
            }
            int firstOccurrenceIdx = seenModulos[mods[i]];
            if(firstOccurrenceIdx < i - 1) {
                return true;
            }
        }
        return false;
        
    }
};

```
I originally solved this problem in June 2021, and wrote about it on Leetcode [here](https://leetcode.com/problems/continuous-subarray-sum/discuss/1372238/number-theory-modulo-congruency-and-prefix-sums-on-c-code) 