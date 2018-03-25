---
title: MUSCL-Hancock Method
date: 2018-03-21 12:38:03
tags: Conservation_laws
mathjax: true
---
# Summary of the MUSCL-Hancock Method
For a give domain $[0,L]$ and a mesh size $\Delta x$, determined by the choice of the number $M$ of computing cells, one first sets the initial conditions $U^0 \equiv U(x,0)$ at time $t = 0$. Then, for each time step $n$ one performs the following operations
<!-- more --> 
### Operation (I): **Boundary condition.**
This is carried out according to these boundary condition:
- ***Transmissive boudary conditions***

$$
W_0^n=W_1^n;\\\
W_{-1}^n=W_2^n;\\\ 
W_{M+1}^n=W_M^n;\\\
W_{M+2}^n=W_{M-1}^n
$$
where $W$ may be the vector of conserved variables or some other variables, such as the primitive variables.
- ***Reflective boundary condidtions***

$$
\rho_{M+1}^n=\rho_{M}^n;u_{M+1}^n=-u_M^n+2u_{wall};p_{M+1}^n=p_M^n,\\\
\rho_{M+2}^n=\rho_{M-1}^n;u_{M+2}^n=-u_{M-1}^n+2u_{wall};p_{M+2}^n=p_{M-1}^n.
$$
where $u_{wall}$ is the speed of a reflective solid boundary at $x=L$.
### Operation (II): **Computation of time step.**
This is carried out according to
$$
\Delta t=C_{CFL}\frac{\Delta x}{S_{max}^{(n)}}
$$
where $\Delta x$ is the mesh spacing, $S_{max}^{(n)}$ is the maximum wave speed present at time level $n$ and $C_{CFL}$ coefficient, with $C_{CFL}\in (0,1]$. A practical choice is 
$$
S_{max}^{(n)}=max_i\{|u_{i}^n|+a_i^n\}
$$
where the range of $i$ must include data arising from boundary from boundary conditions.
A choice of $C_{CLF}$ must be made at the beginning of the computations. One usually takes $C_{CLF}=0.9$. Recall however that the choice of $S_{max}^{(n)}$ is crucial and given that the practical choice above produces somewhat unreliable estimates for the true speeds we recommend that when solving problems with shock-tube like data, the CFL coefficient $C_{CLF}$ be set to small number, e.g. 0.2, for a few time steps.
### Operation (III): **Boundary extrapolated values.**
This involves **Step (I)** and **Step (II)**
- **Step (I): Data Reconstruction.**
In the following, we assume a choice of variables $W$ has been made. One possibility is the conserved variables $W = U$ of course; another choice is offered by the *primitive or physical* variables. For the Euler equations, these are $W=(\rho,u,p)^T$. Here we present the scheme in terms of the conserved variables $U$. In the data reconstruction step, data cell everage values $U_i^n$ are locally replaced by pievewise linear functions in each call $I_i=[x_{i-\frac{1}{2}},x_{i+\frac{1}{2}}]$, namely
$$
U_i(x)=U_i^n+\frac{(x-x_i)}{\Delta x} \Delta_i,~~x \in [0,\Delta x]
$$
where $\Delta_i$ is a suitably chosen *slope* vector (actually a difference) of $U_i(x)$ in cell $I_i$. The extreme points $x = 0$ and $x = \Delta x$, in local co-ordinates, correspond to the intercell houndaries $x_{i-\frac{1}{2}}$ and $x_{i+\frac{1}{2}}$, in global co-ordinates, respectively. The values of $U_i(x)$ at the exteme points are
$$
U_i^L=U_i^n-\frac{1}{2}\Delta_i;\\\
U_i^R=U_i^n+\frac{1}{2}\Delta_i
$$
and are usually called *boundary extrapolated values*. Note that $U$ and $\Delta_i$ are vectors of three components for the Euler equations and thus there six scalar extrapolated values in above fomulae.
- **Step (II): Evolution.**
For each cell $I_i$, the boundary extrapolated values $U_i^L$, $U_i^R$ are *evolved* by a time $\frac{1}{2} \Delta t$, according to

$$
\overline{U}_i^L=U_i^L+\frac{1}{2}\frac{\Delta t}{\Delta x}[F(U_i^L) - F(U_i^R)],\\\
\overline{U}_i^R=U_i^R+\frac{1}{2}\frac{\Delta t}{\Delta x}[F(U_i^L) - F(U_i^R)]
$$
Note that this evolution step is entriely contained in each cell $I_i$, as the *intercell* fluxes are evaluated at the boundary extrapolated values of each cell. At each intercell position $i + \frac{1}{2}$ there are two fluxes, namely $F(U_i^R)$ and $F(U_{i+1}^L)$, which are in general distinct. This does not really affect the *conservative* character of the overall method, as this step is only an intermediate step; the intercell flux $F_{i+\frac{1}{2}}$ to be used in the conservative formula is yet to be evaluated;
In Step (I) and Step (II), the slopes $\Delta_i$ are replaced by the limited slopes $\overline{\Delta}_i$, which are to operation results in TVD, evolved boundary extrapolated values $\overline{U}_i^{L,R}$, for each cell $i$.
### Operation (IV): **Solution of Riemann problem.**
At each intercell position $i + \frac{1}{2}$ one finds the solution of Riemann problem with data   $(\overline{U}\_i^R,\overline{U}\_{i+1}^L)$ and computes the intercell flux according to 
$$
F_{i + \frac{1}{2}}=F(U_{i + \frac{1}{2}}(0))
$$
The intercell flux $F_{i + \frac{1}{2}}$ is now computed in *exactly the same way as in the Godunov first order upwind method*. 
### Operation (V): **Updating of solution.**
Proceed to update the conserved variables according to conservative formula.
$$
U_i^{n+1}=U_i^n+\frac{\Delta t}{\Delta x}[F_{i-\frac{1}{2}} - F_{i + \frac{1}{2}}]
$$
### Operation (VI): **Next time level.**
Go to (I).

