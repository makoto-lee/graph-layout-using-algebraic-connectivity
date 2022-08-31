---
tags: Graph Theory Layout
title: README
---

## Graph Layout using Algebraic Connectivity

This program is trying to layout a graph in graph theorem, by adding some 'spring' as the edges in this graph, and the repulsive force computed from [algebraic connectivity](https://en.wikipedia.org/wiki/Algebraic_connectivity).

---

### What is algebraic connectivity ?

The algebraic connectivity of a graph (also known as  Fiedler vector) is the 2nd smallest eigenvector of the [Laplacian matrix](https://en.wikipedia.org/wiki/Laplacian_matrix) of the graph.

Algebraic connectivity can be a method to find out a 'center' of a graph, by indicating the nodes with element in the Fiedler vector.

For example:

![](https://i.imgur.com/9YA4PoE.png =200x)
with its Fiedler vector : $\vec{v_f} =\begin{pmatrix}
-0.3717\\
-0.6015\\
2.7637\times 10^{-15}\\
0.6015\\
0.3717\\
-2.6990\times 10^{-15}
\end{pmatrix}$
 
 we denote node 0 ~ 5 with elements in $\vec{v_f}$ in its order then 1 of 2 cases below happens:
 
 $A: \text{One node with denoted value = 0 }$ 
 $B: \text{Two nodes with denoted value close to 0, and one of it is positive the another is negtive}$
 
 ![](https://i.imgur.com/0vqpUGv.png =250x)

The above example is case $B$.

In both case $A$ and $B$ the node(s) with value close (or equal) to 0 will approximately be a center of the graph.

By this we can layout a graph in some methods.

---

### How did this program use algebraic connectivity to layout ?

For each pair of nodes $a$ and $b$ we give a repulsive force between them, I design the power of the repulsive force by this following formula : 
$$ \text{power} = \frac{| \text{sigmoid}(\vec{v_f}(a)) - \text{sigmoid}(\vec{v_f}(b)) | }{\text{distance between a  and b}} \times k$$

Note that the $\vec{v_f}(a)$ is the denoted value of node $a$ in $\vec{v_f}$, and $k$ is a const value used to adjust the power according to the size of canvas.

Also, to make sure all the value of $\vec{v_f}(i)$ were in a controllable range so I put them in a $sigmoid$ function. Next divid it with the distance between $a$ and $b$, so that the edges will not be stretch over when their distance is far enough, meanwhile nodes will have larger repulsive force when they are too close.

---

### Some examples

| Without algebraic connectivity support | With algebraic connectivity support |
| -------- | -------- |
| ![](https://i.imgur.com/jkaYGnn.png =300x300)| ![](https://i.imgur.com/5K9evP6.gif =300x300)
  |
  |![](https://i.imgur.com/qgUL4mu.jpg =300x300)|![](https://i.imgur.com/XI23vDF.gif =300x300)
|
|![](https://i.imgur.com/NRiD4W1.jpg =300x300)|![](https://i.imgur.com/xWBzW35.gif =300x300)
|