---
title: "When do stochastic processes that are modifications become indistinguishable?"
date: 
slug: 
type: posts
draft: true
maths: true
categories:
  - 
tags:
  - 
---
# When do stochastic processes that are modifications become indistinguishable?

I first found this problem during my first few days as a PhD student on the book by Karatzas and Shreve [1], a staple for people working with continuous time stochastic processes. This is the very first problem in said book.

**Problem 1.1.5:** Let $Y$ be a *modification* of $X$, and suppose that both processes have a.s. *right-continuous* paths. Then $X$ and $Y$ are *indistinguishable*.

And as stupid as I was at the time (not that much has changed ever since) the definition of *modification* and *indistinguishability* were, funnily enough, indistinguishable to me. Let us check those definitions, shall we?

**Definition (modifications):** $Y$ is a modification of $X$ if, for every point $t$, a.s. the equality $X_t = Y_t$ holds. I.e.

$$\mathbb{P}[X_t = Y_t] = 1$$

**Definition (indistinguishability):** $X$ and $Y$ are indistinguishable if almost all their *sample paths* agree. I.e.

$$\mathbb{P}[X_t = Y_t; \forall t \geq 0] = 1$$.

Probably you can already see what I could not at first sight, but if not allow me to elaborate.
In my mind you the only difference here was where the cuantification $\forall t \geq 0$ was placed what is the difference if we have it inside or outside the application of the probability measure, well it turns out it makes all the difference.

To understand this, it's easier to think in terms of *events on a sample space*: modifications talk about the event $\{X_t = Y_t\}$ for all individual points $t \geq 0$, whereas indistinguishability deals with the event $\{X_t = Y_t; \forall t \geq 0\}$. Does this make it different for you now? No? Well, let us paint a picture.

ADD A PICTURE

The picture above is very revealing. Remember that a stochastic process can be though as a function $Z: \Omega \times (0, \infty) \to \mathbb{R}$, where $\Omega$ is the sample space and it's what gives the randomness to the stochastic process. For a fixed $\omega$, the map $Z_\cdot(\omega)$ is a function of time which we call sample path (sample path associated to $\omega$ you could say). On the figure above you see one sample path of $X$ in purple and one sample path of $Y$ in green, and also you see the points $X_t$ and $Y_t$ marked with an $\times$ and a $\circ$ respectively. So, what modifications take into account is that you can go over each point $t$ and find out that the event $X_t = Y_t$ happens for each sample path. Whereas indistinguishability takes the entire sample from $X$ and $Y$ paths and tell you that all of them are the same across time.

Now that this is clearer, let us recall the definition of right-continuity and finish this problem:

**Definition (right-continuity)$^{[2]}$:** A function $f:\mathbb{R} \to \mathbb{R}$ is right-continuous if for every $t \in \mathbb{R}$ the limit

$$\lim_{s \to t^{+}} f(s)$$

exists and it's equal to $f(t)$.

We can see this on a picture:

ADD A PICTURE

Finally, let's solve the problem.

***Proof:***
Since the processes have sample paths a.s. right-continous we have

$$\mathbb{P}[\lim_{s \to t^{+}} X_s = X_t; \forall t \geq 0] = 1$$

and similarly for $Y$, and since $Y$ is a modification of $X$ we get

$$\mathbb{P}[\lim_{s \to t^{+}} X_s = X_t = Y_t = \lim_{s \to t^{+}} Y_s; \forall t \geq 0] = 1,$$

hence proved.

Very simple, isn't it? Well that's how this thing goes, like many things in mathematics it's just a matter of understanding your tools.

## References
[1] I. Karatzas and S. E. Shreve, Brownian motion and stochastic calculus, Second edition. in Graduate texts in mathematics, no. 113. New York ; Springer-Verlag, 1991.

[2] E. Zakon, Mathematical Analysis. I, Updated edition. in The Zakon Series on Mathematical Analysis. West Lafayette, IN: University of Windsor : The Trillia Group, 2004.
