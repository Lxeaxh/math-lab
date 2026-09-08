# Order Statistics

This notebook investigates **order statistics** by connecting ranking, counting, probability, and simulation.

The main goal is to understand why an event involving the \(r\)-th smallest observation can be rewritten as a counting problem involving the original observations.

## Main Question

The central relationship is

$$
Y_{(r)} \le y
\quad\Longleftrightarrow\quad
\#\{X_i \le y\} \ge r.
$$

In words:

> The \(r\)-th smallest observation is less than or equal to \(y\) if and only if at least \(r\) observations are less than or equal to \(y\).

A major point of confusion was the difference between:

$$
Y_{(4)} \le 0.5
$$

and

$$
\text{exactly 4 observations are } \le 0.5.
$$

The first condition actually means

$$
\text{at least 4 observations are } \le 0.5.
$$

## What This Notebook Investigates

The notebook focuses on the following questions:

* What does the \(r\)-th order statistic represent?
* Why does \(Y_{(4)} \le 0.5\) include the case where all five observations are below \(0.5\)?
* Why is an order-statistic event an “at least” condition rather than an “exactly” condition?
* Why does the Binomial distribution appear in order-statistic probabilities?
* Why does the CDF \(F(y)\) become the Binomial success probability?
* How is a CDF obtained from a PDF?
* Why is the upper limit of the CDF integral the threshold rather than the end of the support?
* Can the theoretical relationship be verified with Python simulation?

## Example Distribution

The main example uses the probability density function

$$
f(x)=2x,\qquad 0<x<1.
$$

Its cumulative distribution function is

$$
F(x)=\int_0^x2t\,dt=x^2.
$$

Therefore,

$$
F\left(\frac12\right)=\frac14.
$$

This means that each independent observation has probability

$$
P\left(X_i\le\frac12\right)=\frac14
$$

of falling below the threshold.

## Connection to the Binomial Distribution

Define

$$
K=\#\{X_i\le y\}.
$$

If \(X_1,\ldots,X_n\) are independent and identically distributed, then

$$
K\sim\operatorname{Binomial}(n,F(y)).
$$

The order-statistic event can then be rewritten as

$$
Y_{(r)}\le y
\quad\Longleftrightarrow\quad
K\ge r.
$$

Therefore,

$$
P(Y_{(r)}\le y)
=
P(K\ge r).
$$

Using the Binomial distribution,

$$
P(Y_{(r)}\le y)
=
\sum_{k=r}^{n}
\binom{n}{k}
[F(y)]^k
[1-F(y)]^{n-k}.
$$

## Worked Example

For

$$
n=5,\qquad r=4,\qquad y=\frac12,
$$

we have

$$
F\left(\frac12\right)=\frac14.
$$

Therefore,

$$
K\sim\operatorname{Binomial}\left(5,\frac14\right).
$$

The target event becomes

$$
P\left(Y_{(4)}\le\frac12\right)
=
P(K\ge4).
$$

Thus,

$$
P(K\ge4)
=
P(K=4)+P(K=5).
$$

The theoretical result is

$$
P\left(Y_{(4)}\le\frac12\right)
=
\frac1{64}
=
0.015625.
$$

The \(K=5\) case must be included because having all five observations below the threshold still guarantees that the fourth smallest observation is below the threshold.

## Methods Used

This notebook uses several approaches to investigate the same idea:

* concrete examples;
* sorting observations;
* threshold counting;
* a number-line visualization;
* PDF and CDF visualization;
* hand calculation;
* a from-scratch Binomial calculation in Python;
* SciPy comparison;
* Monte Carlo simulation;
* theoretical vs. simulated validation.

The purpose of using multiple methods is not to make the notebook more complicated, but to verify the same mathematical idea from different perspectives.

## Validation

Two equivalent events are checked in the simulation:

$$
Y_{(4)}\le0.5
$$

and

$$
\#\{X_i\le0.5\}\ge4.
$$

The simulation verifies that these two conditions identify exactly the same samples.

The simulated probability is also compared with the theoretical value

$$
0.015625.
$$

Small differences between the simulated and theoretical probabilities are expected because simulation uses a finite number of random samples.

## Key Finding

The main insight from this notebook is:

> **Ranking and counting are two different ways of describing the same event.**

Order statistics describe observations through their **positions after sorting**.

The Binomial distribution describes the same situation by **counting how many observations cross a threshold**.

The conceptual chain is

$$
f(x)
\longrightarrow
F(y)
\longrightarrow
P(X_i\le y)
\longrightarrow
K
\longrightarrow
P(K\ge r)
\longrightarrow
P(Y_{(r)}\le y).
$$

Understanding each step in this chain makes the connection between order statistics, CDFs, and the Binomial distribution much clearer.

## What Changed in My Understanding

Before this investigation, I interpreted

$$
Y_{(4)}\le0.5
$$

as meaning that exactly four observations must be below \(0.5\).

After working through concrete examples and simulation, I understand that it means **at least four observations** must satisfy the threshold.

I also understand that:

* \(F(y)\) is the probability that one observation falls below the threshold;
* the Binomial distribution counts how many observations fall below that threshold;
* an order-statistic probability can therefore be converted into a Binomial tail probability;
* simulation can be used to validate the theoretical relationship.

## Remaining Question

A natural next step is to understand how the PDF of the \(r\)-th order statistic is obtained from its CDF.

The general PDF is

$$
g_r(y)
=
\frac{n!}{(r-1)!(n-r)!}
[F(y)]^{r-1}
[1-F(y)]^{n-r}
f(y).
$$

A detailed derivation of this result is left for a future investigation.
