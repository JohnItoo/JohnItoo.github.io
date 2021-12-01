---
layout: post
title:  No Unique Powers of Two
author: John Ohue
summary: Trying to prove that no unique powers of 2 sum to give a power of 2
comments: true
image: images/john-ohue.jpeg
publish: true
---


{% include head.html %}


# Lemma:
No unique/pair distinct powers of 2 would be able to sum to give any power of 2. In other words,
a number that is a power of 2, cannot be represented as a sum of a unique set of powers of 2.

More formally: $$ \sum_{i=0}^{i=n-1} 2^{i} = 2^n -1 ----- (1) $$

# Proof: 
We will prove that this holds for all powers of 2

Base case:
Let n = 1 and i = 0;
$$ 2^0 = 1$$  and $$2^1 - 1 = 1$$


Let us  prove that this also holds when the upper bound of the summation is n rather than n-1

i.e $$ \sum_{i=0}^{i=n} 2^{i} $$ = $$ 2^{(n+1)} -1 $$.  

 $$ \sum_{i=0}^{i=n} 2^{i} $$  =  $$\sum_{i=0}^{i=n-1} 2^{i}$$  + $$2^n$$

 substituting equation 1 into the above we get

 $$\sum_{i=0}^{i=n} 2^{i}$$  =  $$2^n -1$$  + $$2^n$$   = $$2^n  + 2^n - 1$$

$$\sum_{i=0}^{i=n} 2^{i}$$   = $$2$$ • $$2^n$$ - 1 = $$2^{n+1} - 1$$


This can also be verified with the sum of a geometric series formula.

$$\sum_{i=0}^{i=n-1} ar^{i}$$ = $$a * (\dfrac{1-ar^n}{1-ar})$$

Where a = 1 and r = 2, equation then becomes

$$\sum_{i=0}^{i=n-1} 2^{i}$$ = $$1 * (\dfrac{1-2^n}{1-2})$$

$$\sum_{i=0}^{i=n-1} 2^{i}$$ = $$ (1 - 2^n) * (\dfrac{1}{1-2})$$

Thus
$$\sum_{i=0}^{i=n-1} 2^{i} = 2^n -1$$# 


Some problems where this was applied is :

[Tricky Sum](https://codeforces.com/contest/598/problem/A)

[Valery Against Everyone](https://codeforces.com/contest/1438/problem/B)

                           
  
