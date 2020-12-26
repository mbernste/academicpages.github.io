---
title: 'Matrix multiplication'
date: 2020-12-26
permalink: /posts/matrix_multiplication/
tags:
  - tutorial
  - mathematics
  - linear algebra
  - matrices
---

THIS POST IS CURRENTLY UNDER CONSTRUCTION

At a very high level, matrix multiplication is an operation between two [matrices](https://mbernste.github.io/posts/matrices/) that creates a new matrix.  For students introduced to matrix multiplication, it can be puzzling to learn that matrix multiplication does not simply entail computing the product of the each pair of corresponding entries between the two matrices. Rather, matrix multiplication is much more complicated: given two matrices $\boldsymbol{A}$ and $\boldsymbol{B}$, each column of the product matrix $\boldsymbol{AB}$ is formed by performing [matrix-vector multiplication](https://mbernste.github.io/posts/matrix_vector_mult/) between $\boldsymbol{A}$ and each column of $\boldsymbol{B}$: 

<span style="color:#0060C6">**Definition 1 (Matrix multiplication):** The product of an $m \times n$ matrix $\boldsymbol{A}$ **matrix multiplied** by a $n \times p$ matrix $\boldsymbol{B}$ is given by</span>
 
<center><span style="color:#0060C6">$$\boldsymbol{AB} := \begin{bmatrix} \boldsymbol{A}\boldsymbol{b}_{*,1} & \boldsymbol{A}\boldsymbol{b}_{*,2} & \dots & \boldsymbol{A}\boldsymbol{b}_{*,n} \end{bmatrix}$$</span></center>

<span style="color:#0060C6">where $\boldsymbol{b}_{*,i}$ is the $i$th column of $\boldsymbol{B}$.</span>

Note that this definition requires that if we multiply an $m \times n$ matrix by a $n \times p$ matrix, the result will be an $m \times p$ matrix where the number of rows is determined by the first matrix and the number of columns is determined by the second matrix.  Furthermore, we require that the number of columns of the first matrix be equal to the number of rows of the second matrix. If this doesn't hold, then matrix multiplication is not defined. More succinctly:

$$\boldsymbol{A}_{m \times n} \ \boldsymbol{B}_{n \times p} = (\boldsymbol{AB})_{m \times p}$$

This complicated definition begs the question, what is the intuition behind matrix vector multiplication? And, why is it defined this way?

Three perspectives for understanding matrix multiplication
---------------

There are at least three perspectives for which one can view matrix multiplication each depending on the perspective taken on each of the matrix factors. Recall we can view a matrix [via a number of perspectives](https://mbernste.github.io/posts/matrices/):

1. As a list of column vectors
2. As a list of row vectors
3. As a [linear transformation](https://mbernste.github.io/posts/matrices_linear_transformations/)

Given these various ways of possibly viewing each matrix factor, $\boldsymbol{A}$ and $\boldsymbol{B}$, we can view their product, $\boldsymbol{AB}$, as follows:

1. **Matrix multiplication computes a linear transformation on a set of vectors:** If we view $\boldsymbol{A}$ as a linear transformation and $\boldsymbol{B}$ as a list of column vectors, the columns of the product matrix $\boldsymbol{AB}$ are the results of transforming each column of $\boldsymbol{B}$ under $\boldsymbol{A}$. 
2. **Matrix multiplication computes the dot products for pairs of vectors:** This perspective follows from viewing $\boldsymbol{A}$ as an ordered list of row-vectors and viewing $\boldsymbol{B}$ as an ordered list of column-vectors. The product matrix $\boldsymbol{AB}$ then stores all of the pair-wise dot products between the rows of $\boldsymbol{A}$ and columns of $\boldsymbol{B}$.
3. **Matrix multiplication computes the composition of two linear transformations:** If we view both $\boldsymbol{A}$ *and* \boldsymbol{B}$ as linear transformations, then the product matrix is a linear transformation formed by taking the [composition](https://en.wikipedia.org/wiki/Function_composition) of linear transformations defined by $\boldsymbol{A}$ and $\boldsymbol{B}$.

Let's dig into each of these perspectives.

**Matrix multiplication computes a linear transformation on a set of vectors**

This perspective follows most directly from our definition of matrix multuiplication: If we view $\boldsymbol{A}$ as a linear transformation and we view the matrix $\boldsymbol{B}$ as an ordered list of column vectors 

$$\boldsymbol{B} := \begin{bmatrix} \boldsymbol{b}_{*,1} & \boldsymbol{b}_{*,2} & \dots & \boldsymbol{b}_{*,n} \end{bmatrix}$$

then each column of $\boldsymbol{AB}$ is computed by taking the linear transformation characterized by $\boldsymbol{A}$ of each $\boldsymbol{b}_{*,i}$:

$$\boldsymbol{AB} := \begin{bmatrix} \boldsymbol{A}\boldsymbol{b}_{*,1} & \boldsymbol{A}\boldsymbol{b}_{*,2} & \dots & \boldsymbol{A}\boldsymbol{b}_{*,n} \end{bmatrix}$$

**Matrix multiplication computes dot products for pairs of vectors**

If we view the matrix $\boldsymbol{A}$ as a list of row-vectors and the matrix $\boldsymbol{B}$ as a list of column vectors, then the product $\boldsymbol{AB}$ is the matrix that stores all of the pair-wise dot products of the vectors in $\boldsymbol{A}$ and $\boldsymbol{B}$.  More specifically, the $i,j$th element of $\boldsymbol{AB}$ is the the dot product between the $i$th row of $\boldsymbol{A}$ and the $j$th column of $\boldsymbol{B}$ (See Theorem 1 in the Appendix to this post).   This fact, often called the **row-column rule**, can be used for computing each element of $\boldsymbol{AB}$. This is illustrated below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/row_column_rule.png" alt="drawing" width="350"/></center>

**Matrix multiplication computes the composition of two linear transformations:**

If we view *both* $\boldsymbol{A}$ *and* $\boldsymbol{B}$ as linear transformations, then the matrix $\boldsymbol{AB}$ is the matrix that characterizes the linear transformation formed by the composition of the linear transformations characterized by $\boldsymbol{A}$ and $\boldsymbol{B}$ (See Theorem 2 in the Appendix to this post).   That is, given two linear transformations

$$\begin{align*}f(\boldsymbol{x}) &:= \boldsymbol{Ax} \\ g(\boldsymbol{x}) &:= \boldsymbol{Bx}\end{align*}$$

the matrix $\boldsymbol{AB}$ is the matrix that characterizes the composition $f \circ g$:

$$f \circ g(\boldsymbol{x}) := f(g(\boldsymbol{x})) = \boldsymbol{A}(\boldsymbol{Bx})$$

This is proven in Theorem 2 in the Appendix to this poast and is illustrated below:

<center><img src="https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/matrix_composition.png" alt="drawing" width="500"/></center>

Recall that a matrix's number of rows determines the dimensions of the vectors in its range and the number of columns correspond to the number of dimensions the domain.  Since $\boldsymbol{AB}$ characterizes the composition $f \circ g$, it follows that the matrix $\boldsymbol{AB}$ will map from the domain of $\boldsymbol{B}$ to the range of $\boldsymbol{A}$.

Properties of matrix multiplication
--------

Here are several properties of matrix multiplication that can be used in calculations and derivations involving matrices. For the sake of succinctness, we push all of the proofs to the Appendix of the blog post:

1. **Associative law for matrices** (Theorem 3): $\boldsymbol{A}(\boldsymbol{BC}) = (\boldsymbol{AB})\boldsymbol{C}$
2. **Commutative property of scalars** (Theorem 4): $r(\boldsymbol{AB}) = (r\boldsymbol{A})\boldsymbol{B} = \boldsymbol{A}(r\boldsymbol{B})$ where $r$ is a scalar. 
3. **Left distributive law** (Theorem 5): $\boldsymbol{A}(\boldsymbol{B} + \boldsymbol{C}) = \boldsymbol{AB} + \boldsymbol{AC}$
4. **Right distributive law** (Theorem 6): $(\boldsymbol{B} + \boldsymbol{C})\boldsymbol{A} = \boldsymbol{BA} + \boldsymbol{CA}$
5. **Identity** (Theorem 7): $\boldsymbol{I}_m\boldsymbol{A} = \boldsymbol{A} = \boldsymbol{AI}_n$

Appendix
--------

<span style="color:#0060C6">**Theorem 1 (Row-column rule):** Given an $m \times n$ matrix $\boldsymbol{A}$ and a $n \times p$ matrix $\boldsymbol{B}$, the $i,j$th element of $\boldsymbol{AB}$ is computed by $$\boldsymbol{a}_{i,*} \cdot \boldsymbol{b}_{*,j}$$, where $$\boldsymbol{a}_{i,*}$$ is the $i$th column of $\boldsymbol{A}$ and $$\boldsymbol{b}_{*,j}$$ is the $j$th column of $\boldsymbol{B}$.</span>

**Proof:**

$$\begin{align*}
\boldsymbol{AB} &=  \begin{bmatrix} \boldsymbol{A}\boldsymbol{b}_{*,1} & \boldsymbol{A}\boldsymbol{b}_{*,2} & \dots & \boldsymbol{A}\boldsymbol{b}_{*,n} \end{bmatrix} \\ &= \begin{bmatrix} \boldsymbol{a}_{*,1}b_{1,1} + \dots + \boldsymbol{a}_{*,n}b_{n,1} & \dots & \boldsymbol{a}_{*,1}b_{1,n} + \dots + \boldsymbol{a}_{*,n}b_{n,n} \end{bmatrix} \\ &= \begin{bmatrix} a_{1,1}b_{1,1} + \dots + a_{1,n} b_{n,1} & \dots & a_{1,1}b_{1,n} + \dots + a_{1,n}b_{n,n} \\
a_{2,1}b_{1,1} + \dots + a_{2,n} b_{n,1} & \dots & a_{2,1}b_{1,n} + \dots + a_{2,n}b_{n,n} \\
\vdots & \ddots & \vdots \\
a_{n,1}b_{1,1} + \dots + a_{n,n} b_{n,1} & \dots & a_{n,1}b_{1,n} + \dots + a_{n,n}b_{n,n}
\end{bmatrix} \\ &= \begin{bmatrix} \boldsymbol{a}_{1,*} \cdot \boldsymbol{b}_{*,1} & \dots & \boldsymbol{a}_{1,*} \cdot \boldsymbol{b}_{*,n} \\ \boldsymbol{a}_{2,*} \cdot \boldsymbol{b}_{*,1} & \dots & \boldsymbol{a}_{2,*} \cdot \boldsymbol{b}_{*,n} \\ \vdots & \ddots & \vdots \\ \boldsymbol{a}_{m,*} \cdot \boldsymbol{b}_{*,1} & \dots & \boldsymbol{a}_{m,*} \cdot \boldsymbol{b}_{*,n} \end{bmatrix} \end{align*}$$

$\square$


<span style="color:#0060C6">**Theorem 2:** Matrix multiplication between an $m \times n$ matrix $\boldsymbol{A}$ and a $n \times p$ matrix $\boldsymbol{B}$ results in a matrix $\boldsymbol{AB}$ such that given a vector $\boldsymbol{x} \in \mathbb{R}^m$, the following holds:</span> 

<center><span style="color:#0060C6">$$(\boldsymbol{AB})\boldsymbol{x} = \boldsymbol{A}(\boldsymbol{Bx})$$</span></center>

**Proof:** First, let's expand $\boldsymbol{Bx}$:

$$\begin{align*} \boldsymbol{Bx} &= \boldsymbol{b}_{*,1}x_1 + \boldsymbol{b}_{*,2}x_2 + \dots + \boldsymbol{b}_{*,n}x_n \\ &= \begin{bmatrix} b_{1,1}x_1 + b_{1,2}x_2 + \dots + b_{1,n}x_n \\ b_{2,1}x_1 + b_{2,2}x_2 + \dots + b_{2,n}x_n \\ \vdots \\ b_{n,1}x_1 + b_{n,2}x_2 + \dots + b_{n,n}x_n \end{bmatrix} \end{align*}$$

Now,

$$\begin{align*}(\boldsymbol{AB})\boldsymbol{x} &= \begin{bmatrix} \boldsymbol{A}\boldsymbol{b}_{*,1} & \boldsymbol{A}\boldsymbol{b}_{*,2} & \dots & \boldsymbol{A}\boldsymbol{b}_{*,n} \end{bmatrix} \boldsymbol{x} \\ &= \boldsymbol{A}\boldsymbol{b}_{*,1}x_1 + \boldsymbol{A}\boldsymbol{b}_{*,2}x_2 + \dots + \boldsymbol{A}\boldsymbol{b}_{*,n}x_n \\ &=  \left(\boldsymbol{a}_{*,1}b_{1,1} + \dots + \boldsymbol{a}_{*,n} b_{n,1}\right)x_1 + \left(\boldsymbol{a}_{*,1}b_{1,2} + \dots + \boldsymbol{a}_{*,n} b_{n,2}\right)x_2 + \dots + \left(\boldsymbol{a}_{*,1}b_{1,n} + \dots + \boldsymbol{a}_{*,n} b_{n,n}\right)x_n \\ &= \left(\boldsymbol{a}_{*,1}b_{1,1}x_1 + \dots + \boldsymbol{a}_{*,n}b_{n,1}x_1\right) + \left(\boldsymbol{a}_{*,1}b_{1,2}x_2 + \dots + \boldsymbol{a}_{*,n} b_{n,2}x_2\right) + \dots + \left(\boldsymbol{a}_{*,1}b_{1,n}x_n + \dots \boldsymbol{a}_{*,n} b_{n,n}x_n\right) \\ &= \boldsymbol{a}_{*,1}(b_{1,1}x_1 + \dots + b_{1,n}x_n) + \boldsymbol{a}_{*,2}(b_{2,1}x_1 + \dots + b_{2,n}x_n) + \dots + \boldsymbol{a}_{*,n}(b_{n,1}x_1 + \dots + b_{n,n}x_n)  \\ &= \boldsymbol{a}_{*,1}(\boldsymbol{Bx})_1 + \boldsymbol{a}_{*,2}(\boldsymbol{Bx})_2+ \dots \boldsymbol{a}_{*,n}(\boldsymbol{Bx})_n  \\ &= \boldsymbol{A}(\boldsymbol{Bx}) \end{align*}$$

$\square$