---
title: Conservation laws
date: 2017-08-23 11:29:54
tags: Conservation_laws
mathjax: true
---
# Linearization of nonlinear systems
Consider a nonlinear system of conservation laws
$$
u_t+f(u)_x=0,
$$
where $u:R \times R \rightarrow R^m$ and $f:R^m \rightarrow R^m$. This can be written in the quasilinear form 
$$
u_t+A(u)u_x=0
$$
where $A(u)=f'(u)$ is the $m \times m$ Jacobian matrix. Again the system is **hyperbolic** if $A(u)$ is diagonalizable with real eigenvalues for all values of $u $, at least in some range where the solution is known to lie, and strictly hyperoblic if the eigenvalues are distinct for all $u $.