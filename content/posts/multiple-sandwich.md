---
title: "Multiple Sandwich"
date: 2024-10-30T08:18:07Z
draft: false
maths: true
---
> **Problem:** Consider an array `A` of length `m` with only non-negative integer entries, then take the sum of the entries of `A` and denote it by `s`.
And find the smallest number `p` that is a multiple of `m` and is greater or equal than `s`.

This was a teeny tiny part of a timed coding question that I blew because I decided to, as any good mathematician would do, overthink it.
So I decided to document it since anyway the damage is done.

My first *grug* thought was to use a while loop that which stops when we find a multiple of `m` that is greater or equal than `s`.
But then I realized that, I am sure the following holds:

> **Proposition:** Let $m, n \in \mathbb N$ such that $m \geq n \geq 0$ then there exists $k \in \mathbb N$ such that
$$kn \leq m \leq (k+1)n.$$

Meaning that for any pair of numbers we can sandwich one in between consecutive multiples of the other.

That proposition is true, and after my time ran out to solve to overall problem, I decided to prove it.
But in a reckless move I decided to use that result in my code without having mathematical evidence that it was going to work.

The way I used it was to take the sum `s = sum(A)` and the length `m = length(A)` of the array `A`
---which I will denote as the functions `sum` and `lenght` for pseudo code's sake---
and take its integer division quotient, this is `floor(sum(A) / length(A)`.
So, in this way the smallest multiple of `m` that is greater than or equal to `s` is either  `floor(sum(A) / length(A)) * sum(A)` or  `(floor(sum(A) / length(A) + 1) * sum(A)` depending on whether or not `s` is a multiple of `m`.
The pseudo code would look like this:
```
if floor(sum(A) / length(A)) * sum(A) < sum(A)
    then return (floor(sum(A) / length(A)) + 1) * sum(A)
else return floor(sum(A) / length(A)) * sum(A)
```
You could of course recover instead the factor that makes the multiple you are after, which is actually more akin to what I needed.
But the pseudo code and the approach is basically the same.

So yeh, there you go.
The point is that we cannot use a mathematical result without a proof, so here is my proof to the proposition above.

> *Proof:* If $m$ is a multiple of $n$ then obviously we can find some $k$ such that $m = kn$ or $m = (k+1)n$ and the equalities hold.
If $m$ is not a multiple of $n$, we know that in particular for any $a, b \in \mathbb N$ where $b \neq 0$ there are $r, q \in \mathbb N$ such that $a = bq + r$ for $r < b$.
This is called the [division with remainder theorem](https://en.wikipedia.org/wiki/Euclidean_division)---also called Euclidean division.
So, let $a = m$ and $b = n$ and we have that $m = qn + r$ for $r < n$.
It's obvious then that $m > qn$ since $r > 0$.
Moreover, since $r < n$ we have that $m < qn + n = (q + 1)n$.

You may find an either more elegant or more jarring proof, but it's true and now I can rest.
