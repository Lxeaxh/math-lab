<h1>Order Statistics: From Ranking to Counting</h1>

This notebook explores **order statistics** through mathematical reasoning, visualization, hand calculation, and Python simulation.

The main goal is to understand why a statement about the position of an observation after sorting can be rewritten as a counting problem.

<h2>Notebook</h2>

[Open the Order Statistics notebook](./order_statistics.ipynb)

<h2>Main Question</h2>

Suppose the original observations are

```math
X_1, X_2, \ldots, X_n
```

and the sorted observations are

```math
Y_{(1)} \le Y_{(2)} \le \cdots \le Y_{(n)}.
```

The central question of this notebook is:

> Why does the event \(Y_{(r)} \le y\) mean that **at least** \(r\) observations must be less than or equal to \(y\)?

Define the counting variable

```math
K=\sum_{i=1}^{n} I(X_i\le y),
```

where \(I(X_i\le y)\) equals 1 when \(X_i\le y\) and 0 otherwise.

Therefore, \(K\) represents the number of observations that are less than or equal to \(y\).

The key relationship is

```math
Y_{(r)}\le y
\quad\Longleftrightarrow\quad
K\ge r.
```

<h2>Initial Confusion</h2>

At first, I understood that \(Y_{(4)}\) represents the fourth smallest observation.

However, I incorrectly interpreted

```math
Y_{(4)}\le0.5
```

as meaning:

> Exactly four observations are less than or equal to \(0.5\).

The main confusion was why a case in which **all five observations** are less than or equal to \(0.5\) must also be included.

This notebook investigates why the correct interpretation is:

> At least four observations are less than or equal to \(0.5\).

<h2>Investigation 1: Ranking vs. Counting</h2>

Consider the sorted sample

```math
0.10,\ 0.20,\ 0.30,\ 0.40,\ 0.45.
```

The fourth order statistic is

```math
Y_{(4)}=0.40.
```

Therefore,

```math
Y_{(4)}\le0.5.
```

At the same time, all five observations satisfy the threshold, so

```math
K=5.
```

This shows that the condition is not

```math
K=4,
```

but rather

```math
K\ge4.
```

The fifth observation is also allowed to fall below the threshold.

Therefore,

```math
Y_{(4)}\le0.5
\quad\Longleftrightarrow\quad
K\ge4.
```

More generally,

```math
Y_{(r)}\le y
\quad\Longleftrightarrow\quad
K\ge r.
```

The notebook uses a number-line visualization to make the difference between **exactly** and **at least** easier to see.

<h2>Investigation 2: Why the Binomial Distribution Appears</h2>

For each original observation, define a success as

```math
X_i\le y.
```

The probability of success is

```math
P(X_i\le y)=F(y),
```

where \(F(y)\) is the CDF of the original distribution.

The counting variable is

```math
K=\sum_{i=1}^{n} I(X_i\le y).
```

If the observations are independent and identically distributed, then

```math
K\sim \mathrm{Binomial}(n,F(y)).
```

Since

```math
Y_{(r)}\le y
\quad\Longleftrightarrow\quad
K\ge r,
```

the order-statistic probability can be rewritten as

```math
P(Y_{(r)}\le y)=P(K\ge r).
```

A Binomial PMF gives the probability of exactly \(k\) successes:

```math
P(K=k)
=
\binom{n}{k}
p^k
(1-p)^{n-k}.
```

Therefore, an "at least" probability requires adding all possible values from \(r\) to \(n\):

```math
P(Y_{(r)}\le y)
=
\sum_{k=r}^{n}
\binom{n}{k}
[F(y)]^k
[1-F(y)]^{n-k}.
```

<h2>Investigation 3: From PDF to CDF</h2>

The example distribution used in this notebook is

```math
f(x)=2x,
\qquad
0<x<1.
```

To calculate an order-statistic probability, I first need the probability that one observation falls below a given threshold.

The CDF is

```math
F(x)=P(X\le x).
```

For this distribution,

```math
F(x)=\int_0^x 2t\,dt.
```

Evaluating the integral gives

```math
F(x)=x^2,
\qquad
0<x<1.
```

The upper limit is \(x\) rather than \(1\) because the CDF asks for the accumulated probability only up to the chosen value \(x\).

The notebook also visualizes both the PDF and CDF to connect the integral with accumulated probability.

<h2>Worked Example</h2>

Consider

```math
n=5,
\qquad
r=4,
\qquad
y=\frac{1}{2}.
```

Since

```math
F(x)=x^2,
```

we have

```math
F\left(\frac{1}{2}\right)
=
\left(\frac{1}{2}\right)^2
=
\frac{1}{4}.
```

Therefore,

```math
K\sim
\mathrm{Binomial}
\left(5,\frac{1}{4}\right).
```

The target probability is

```math
P\left(Y_{(4)}\le\frac{1}{2}\right).
```

Using the counting interpretation,

```math
P\left(Y_{(4)}\le\frac{1}{2}\right)
=
P(K\ge4).
```

Therefore,

```math
P(K\ge4)
=
P(K=4)+P(K=5).
```

For exactly four observations,

```math
P(K=4)
=
\binom{5}{4}
\left(\frac{1}{4}\right)^4
\left(\frac{3}{4}\right).
```

For exactly five observations,

```math
P(K=5)
=
\binom{5}{5}
\left(\frac{1}{4}\right)^5.
```

Combining the two cases gives

```math
P\left(Y_{(4)}\le\frac{1}{2}\right)
=
\frac{1}{64}.
```

Therefore,

```math
P\left(Y_{(4)}\le\frac{1}{2}\right)
=
0.015625.
```

The \(K=5\) case must be included because all five observations being below the threshold still guarantees that the fourth smallest observation is below the threshold.

<h2>Python Validation</h2>

The theoretical calculation is checked in three ways:

1. A Binomial probability is implemented directly in Python.
2. The result is compared with SciPy.
3. A Monte Carlo simulation estimates the probability empirically.

The simulation independently constructs two events.

<strong>Order-statistic condition</strong>

```math
Y_{(4)}\le0.5
```

<strong>Counting condition</strong>

```math
K\ge4
```

where

```math
K=\sum_{i=1}^{5} I(X_i\le0.5).
```

The simulation verifies that these two conditions identify exactly the same samples.

The simulated probability is also close to the theoretical value

```math
0.015625.
```

Small differences between the theoretical and simulated probabilities are expected because Monte Carlo simulation uses a finite number of random samples.

<h2>Methods Used</h2>

This notebook uses:

- mathematical reasoning
- concrete examples
- sorting and counting
- number-line visualization
- PDF and CDF visualization
- hand calculation
- NumPy
- from-scratch Binomial calculation
- SciPy validation
- Monte Carlo simulation
- theoretical vs. empirical comparison

Each method is used to answer a specific question rather than simply adding technical complexity.

<h2>Key Finding</h2>

The central insight from this investigation is:

> **Ranking and counting are two different ways of describing the same event.**

Order statistics describe observations through their **positions after sorting**.

The Binomial distribution describes the same event by **counting how many observations cross a threshold**.

The reasoning process can be summarized as

```math
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
```

<h2>What Changed in My Understanding</h2>

Before this investigation:

- I thought \(Y_{(4)}\le0.5\) meant exactly four observations were below \(0.5\).
- I did not understand why the case with all five observations below \(0.5\) had to be included.
- I understood the Binomial distribution separately but did not see its connection to order statistics.
- I was unsure why \(F(y)\) appeared as the Binomial success probability.
- I confused calculating a CDF with integrating across the full support.

After this investigation:

- I understand that \(Y_{(4)}\le0.5\) means **at least four** observations are below the threshold.
- I understand that later-ranked observations can also lie below the threshold.
- I see the Binomial distribution as a way to count how many observations cross the threshold.
- I understand that \(F(y)\) is the probability that one observation satisfies \(X_i\le y\).
- I understand why the CDF integrates only up to the chosen threshold.
- I can connect the mathematical result with a Python simulation.

<h2>Remaining Question</h2>

This notebook focuses mainly on understanding the CDF of an order statistic.

A natural next question is:

> How can the PDF of the \(r\)-th order statistic be derived from its CDF?

The general PDF is

```math
g_r(y)
=
\frac{n!}{(r-1)!(n-r)!}
[F(y)]^{r-1}
[1-F(y)]^{n-r}
f(y).
```

A detailed derivation is left for a future investigation.
