---
layout: post
title:  "Solving Least Squares"
date:   2023-10-04 10:00:00 -0700
categories: math optimization
---

In this post, we'll derive the closed-form solution for a linear least squares problem using LaTeX math notation.

## Problem Statement

Given a system of linear equations represented by $$Ax = b$$, where:
- $$A$$ is an $$m \times n$$ matrix
- $$x$$ is an $$n \times 1$$ vector of unknowns
- $$b$$ is an $$m \times 1$$ vector

We want to find $$x$$ that minimizes the sum of squared residuals:

$$ \min_{x} \|Ax - b\|_2^2 $$

## Derivation

1. Expand the squared L2 norm:

   $$ \|Ax - b\|_2^2 = (Ax - b)^T(Ax - b) $$

2. Expand the right-hand side:

   $$ (Ax - b)^T(Ax - b) = x^TA^TAx - x^TA^Tb - b^TAx + b^Tb $$

3. Take the derivative with respect to $$x$$ and set it to zero:

   $$ \frac{\partial}{\partial x}(x^TA^TAx - x^TA^Tb - b^TAx + b^Tb) = 0 $$

4. Simplify:

   $$ 2A^TAx - 2A^Tb = 0 $$

5. Solve for $$x$$:

   $$ A^TAx = A^Tb $$
   
   $$ x = (A^TA)^{-1}A^Tb $$

## Closed-Form Solution

The closed-form solution for the least squares problem is:

$$ x = (A^TA)^{-1}A^Tb $$

This solution is also known as the normal equation.

## Implementation in Python

Here's a simple Python implementation using NumPy:

{% highlight python %}
import numpy as np

def least_squares_solution(A, b):
    return np.linalg.inv(A.T @ A) @ A.T @ b

# Example usage
A = np.array([[1, 1], [1, 2], [1, 3]])
b = np.array([2, 4, 5])

x = least_squares_solution(A, b)
print("Solution:", x)
{% endhighlight %}

This post demonstrates how to derive and implement the closed-form solution for a linear least squares problem. The LaTeX math notation helps in clearly presenting the mathematical steps involved in the derivation.