# Stochastic Modelling

This course notes only contain the first half of the half-module. 

The instructor had well written notes for second half on Martingale model, which is sufficient for me to depend on.

* auto-gen TOC:
{:toc}

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script type="text/javascript" id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
<script>window.MathJax = {tex: {inlineMath: [['$', '$'], ['\\(', '\\)']]}};</script>


Prerequisites

- Manufacturing and Service Operations

  - https://tonghuikang.github.io/notes/sutd-manufacturing-and-service-operations/
  - Kendall's notation $A/S/c$
    - $A$ denotes the time between arrivals to the queue
      - $M$ - memoryless or exponential interarrival time
      - $G$ - general distribution
      - $D$ - deterministic
    - $S$ the service time distribution
      - $M$ - memoryless or exponential service time
      - $G$ - general distribution
      - $D$ - deterministic
    - $c$ is the number of servers

- Simulation Modelling and Analysis
  - https://raw.githubusercontent.com/tonghuikang/notes_ESD_term10/master/SMA/finals-cheatsheet-front.png
  - https://raw.githubusercontent.com/tonghuikang/notes_ESD_term10/master/SMA/finals-cheatsheet-front.png



## Renewal process

- $N(t)$ is the number of renewals before time $t$
  - "renewal" - as good as new. The state of the memory (if there is) should be the same at every renewal
- $S_n$ is the time of n-th renewal
- $X_n$ is the time between the n-th renewal and the (n-1)-th renewal
- $R_n$ is the reward from the n-th arrival
- Identities
  - $S_n = X_n - X_{n-1}$
  - $S_{N(t)} \leq t$
  - $\{ N(t) \geq n \} = \{ S_n \leq t \}$
  - $P\{N(t) = n)\} \\ = P\{N(t) \geq n)\} - P\{N(t) \geq n+1)\} \\ = P(S_n \leq t) - P(S_{n+1} \leq t)$

Inventory depletion

  - $N(u) = \max\{n: X_1 + ... + X_n \leq u \}$
  - $X_1 + ... + X_{N(u)} \leq u$
  - $X_1 + ... + X_{N(u+1)} > u$
  - Number of weeks taken to deplete the inventory, afterwards you need to refill the inventory such that it is good as new?




### Renewal-Reward theorem

For a renewal process, if $E[X]$ is the mean time between renewals, we have

$\lim_\limits{t \to \infty} \dfrac{N(t)}{t} = \dfrac{1}{E[X]}$

The number of renewals per unit time is the inverse of the mean time between renewals. (Idea of proof - sample mean converges to true mean, sandwich theorem)

Renewal-Reward theoerm

$\lim_\limits{t \to \infty} \dfrac{R(t)}{t} = \dfrac{E[R]}{E[X]}$

The Renewal theorem is a special case Renewal-Reward theoerm where the reward is one. The rate of reward is the expected reward per arrival multiplied by the rate of arrival.

Optimal machine repair policy

- Problem statement
  - Machine failure time has a density of $f(t) = 2t/900$ for $0 \leq t \leq 30$
  - If the machine fails prior to replacement it costs $1200
  - If you replace the machine prior to failure it costs $300
  - Consider a replacement policy in which the tools is replaced after $c$ months or when it fails. Find the optimal $c$.
- Approach
  - Find cost as a function of $c$
  - $X_i = \min(c,T_i)$, where $T_i \sim f(t)$ 
  - $R_i = 1200$ if $T_i \leq c$, or $300$ if $T_i > c$
  - $E[X] = c \cdot P(T > c) + E[T|T\leq C] \cdot P(T \leq c)$
  - $E[R] = 1200 \cdot P(T \leq c) + 300 \cdot P(T \leq c)$
  - $\dfrac{E[R]}{E[X]} = \dfrac{c^2 + 300}{c - c^3/2700}$
  - Minimise w.r.t. $c$

Alternative renewal process

- $X_i$ are independent copies of $U+D$
- $R_i$ are independent copies of $U$
- Fraction of time the machine is in the up state = $\dfrac{E[R]}{E[X]}$ = $\dfrac{E[U]}{E[U] + E[D]}$

Possion janitor

- $X_i = F + P(\lambda)$
- $R_i = F$
- $E[X] = E[F] + E[P(\lambda)] = \mu_F + \dfrac{1}{\lambda}$
- $E[R] = \mu_F$
- Fraction of time that the light bulb works = $\dfrac{\mu_F}{\mu_F + 1/\lambda}$
- Idea - the does not matter when the janitor visits the bulb when the bulb is up, because the visits are more emoryless.
- The fraction of visits of which the bulb is off = $\dfrac{\text{rate of bulb going off}}{\text{rate of janitor visits}} = \dfrac{1/E[X]}{\lambda} = \dfrac{\dfrac{1}{\mu_F + 1/\lambda}}{\lambda} = \dfrac{1}{\lambda \mu_F + 1}$
- The rate of replacement is the rate of bulb malfunctioning.
- We can consider the expected number of times the visits made by the janitor during the uptime = $\lambda\mu_F$ and expected number of times the visits made by the janitor during the downtime = 1s



### Poisson processes

If the interarrival times is exponentially distributed with parameter $\lambda$, the renewal process is a Poisson process.

- The number of events in two disjoint intervals are independent
- The number of events in any interval is Poisson
- The merging of two Poisson processes is a Poisson process
- The splitting of two Poisson processes in a Poisson process



### Little's Law

Long run average of number of customers in the system = arrival rate $\times$ the long run average time spent by each customer in the system

$\overline{N} = \lambda \overline{T}$

Proof of Little's Theorem (assuming long run averages exist, i.e. queue does not explode infinity)

- Refer to slides on how it is a consequence of renewal reward theorem - the average number of customers in the system is squeezed by ... (no idea)
- Rate of departure is the minimum of arrival rate and service rate

Queuing

- Relationship between $N_Q$ and $N$ - one if the system is busy, otherwise zero
- Time spent in the system is the time spent queuing and the service time $T_Q + S_i = T$
- Fraction of time the system is busy = $\overline{N} - \overline{N}_Q = \lambda \overline{T} - \lambda \overline{T}_Q = \lambda (\overline{T} - \overline{T}_Q) = \lambda S_i = \lambda /\mu$




## Regenerative Processes

A stochastic process $X(t), t \in T$ with time-index $T$ is said to be regenerative if there exists a random epoch $S_1$ such that

- $X(t+S_1), t \in T$ Is independent of $X(t), 0 \leq t \leq S_1$
  - The stochasitc process rengerate itself at certain (potentially random) points in time so that ...
- $X(t+S_1), t \in T$ has the same distribution as $X(t), t \in T$
  - The behaviour after regeneration is independent of the behaviour before the regeneration

Examples

- (s,S) inventory model

  - Immediately refill to $S$ when the stock falls under $s$.
  - The regenerative point is when the stock is refilled

- Single server queue

  - The regenerative point is when the queue is emptied, or when there is an arrival to an empty system.

### Long run average cost

$\lim_\limits{t \to \infty} \dfrac{1}{t} \int_0^t f(X(s)) ds = \dfrac{E[R_1]}{E[C_1]}$

The long run average cost is the expected reward from each cycle divided by the length of each cycle.



## Simulation

### Steady-state average

$\lim_\limits{t \to \infty} E[f(X(t))]$

Long run average = steady-state average

- For processes with aperiodic regenerative structure
- There there is periodicity, the long run steady-state aveage does not exist.

$\lim_\limits{t \to \infty} P\{X(t) \in B \} = \dfrac{E[T_B]}{E[C_1]}$

The probability of state being at $B$ is equal to the expected time spent in state $B$ over the expected time of the cycle.

Example

- Reliability problem with redundancies

  - Statement

    - Choose the number of redundant components $r$ and inspection interval $K$
    - Minimise the depreciation cost ($I$ per time unit), reparation cost ($R$ per unit) and inspection cost ($K$ per inspection)
      - (Reparation cost and depreciation cost has to be considered separately because the component could have failed twice in the interval)
    - Subject to constraint that the probability of system failure between two inspection is at most $\alpha$, which more than $m$ components are working

  - Solution

    - The regenerative time is after every inspection.
    - $E(C) = T$
    - Probability of failure of component in the time interval = $1-e^{-\mu T}$
    - $E(R)$ = cost of one cycle 
      = inspection cost + depreciation cost + reparation cost 
      = $K + (m+r)IT + (m+r)(1-e^{-\mu T})R$
    - Long run average cost = $E(R)/E(C)$
- Probability of system failure = $P(\text{Binomial}(m+r,  p) \geq m) \leq \alpha$
    - Minimise objective subject to constraint



### Steady State Simulation

- (We conduct simulations because we cannot find a simple expression for the numerator or denominator)
- Replication/Deletion
  - Run $n$ additional independent simulations (replication)
  - Discard the first $l$ observations in each run (deletion)
  - Compute average of each simulation
  - Compute mean and sample deviation of simulation averages
  - Compute confidence interval
  - Downsides
    - Difficult to estimate burn-in period
    - Computationally expensive because we throw away multiple burn-in periods
- Batch-means method
  - Obtain one long simulation run of length $T$
  - Determine burn-in $l$
  - Divide observations after burn-in into $R$ batches
  - Compute the sample mean $\bar{Y}$ for each of the batches
  - Downsides
    - Difficult to estimate burn-in period
    - Samples across batches are potentially correlated

- Regenerative simulation
  - Choose the number of cycles $N$
  - Identify regeneration times
    - For $G/G/1$, the regeneration times are the times of customer arrivals to an empty queue
    - A typical regeneration point is a point at which an event has just occured and no future event had yet been schduled just before
  - Compute reward for each cycle $R$
  - Computer average cycle length $C$
  - Output $\dfrac{\bar{R}}{\bar{C}}$ as the estimate for steady state average.
  - Compute sample variances
    - $s_{11} = \dfrac{1}{N-1} \sum_{i=1}^N (R_i - \bar{R})^2$
    - $s_{22} = \dfrac{1}{N-1} \sum_{i=1}^N (C_i - \bar{C})^2$
    - $s_{12} = \dfrac{1}{N-1} \sum_{i=1}^N (R_i - \bar{R})(C_i - \bar{C})$
      - The reward and cycle length is likely to be correlated (the longer the cycle, the more likely the queue is long)
    - $s^2 = s_{11}^2 - 2\dfrac{\bar{R}}{\bar{C}} s_{12}^2 + \left(\dfrac{\bar{R}}{\bar{C}}\right)^2 s_{22}^2$
  - Output the confidence interval $(1-\alpha)\times100\%$
    - $\left(\dfrac{\bar{R}}{\bar{C}} - \dfrac{sz_{\alpha/2}}{\bar{C}\sqrt{N}}, \dfrac{\bar{R}}{\bar{C}} + \dfrac{sz_{\alpha/2}}{\bar{C}\sqrt{N}} \right)$
    - Outline of proof (refer to prof) - Taylor expansion of $f(x,y)=x/y$, the error term has a factorisable coefficient of $1/\bar{C}\sqrt{N}$, and show the calculation for $s^2$
  - Upsides
    - Batches are not guaranteed to be uncorrelated (unlike batch means)
    - Burn-in period is not longer needed to be decided and discarded
  - Downsides
    - Not every system posesses regeneration points, this method require regeneration points



## Simulation Theorems

### Possion Arrival See Time Average (PASTA)

- Suppose that the arrival process is a Poisson process. The long-run fraction of arrivals who find the system in the set $B$ of states equals the long-run fraction of time the system is in the set $B$ of states.
  - $I_B(t)$  - how the system view, 1 if state is $B$
  - $I_n(B$ - how the customer view, 1 if state if $B$
  - Interesting because the customer's point of view (discrete) is consistent with the system's point of view (continuous)
  - The Possion arrivals are assumed to be exogenous (are all Possion arrivals exogenous?)
  - $\lim\limits_{n \to \infty} \dfrac{1}{n} \sum_{t=1}^n I_k(B) = \lim\limits_{n \to \infty} \dfrac{1}{t}  \int_0^t I_B(u) du$
- Arrivals do not see time averages generally (it is possible for customers to never see another customer
  - Do exogenous arrivals still see time averages? No. Exogenous Poisson arrivals yes.
- Server utilization $\rho = \lambda/\mu$



### Inspection paradox

- The sum of expectation of age and the expectation of excess can be more than the expected time to complete a job
  -  $2 \cdot \dfrac{E[X^2]}{2E[X]} \geq E[X]$
  - It is more likely for a Poisson arrival to land in the large inter-renewal duration rather than in a smaller window
  - $E[S_e] = \dfrac{E[X^2]}{2E[X]} = \dfrac{1}{2} E[X] \dfrac{E[X^2]}{(E[X])^2} = \dfrac{1}{2} E[X] (C_X^2 + 1)$
  - Squared coefficient of variance $C_X^2$
    - $C_X^2 = \dfrac{\text{Var}[X]}{E[X]^2} = \dfrac{E[X^2]}{E[X]^2} - 1$
- To improve customer experience by decreasing $E[S_e]$, either decrease $E[X]$ by deploying more buses (which may be costly) or decrease $C_X$ which can be done without deploying more buses.



The long-run average waiting time in the M/G/1 queue $E[T_Q]$  

- = unfinished work that an arrival witnesses in the system
- = unfinished work in the queue + unfinished work at the server
- = expected number of jobs in the queue $\times$ expected time to serve a job + probability that there is some job in service $\times$ expected remaining service time of job in service
- = $E[N_Q] \cdot E[S] + \rho \cdot E[S_e]$
- = $E[T_Q] \cdot \lambda / \mu + \rho \cdot E[S_e]$
- = $\rho \cdot E[T_Q] + \rho \cdot E[S_e]$
- $= \dfrac{\rho}{1 - \rho}E[S_e]$
- $= \dfrac{\rho}{1 - \rho} \dfrac{E[S^2]}{2 E[S]}$
- $= \dfrac{\rho}{1 - \rho} \dfrac{E[S]}{2} (C_S^2 + 1)$
- $= \dfrac{\lambda E[S^2]}{2(1 - \rho)}$
- (This is the Pollaczek-Khinchin PK-formula)

PASTA is invoked twice here

- $E[N_Q^A] = E[N_Q]$ the average state the arrivals see is the average of the state of the system
- Probability that there is some job in service seen by the arrival is the server ultilisation rate $\rho$ 

Sensitivity analysis

- Differentiate w.r.t. the variable and subsitute the variable with the reference value
- $C_X = C_{nX}$ and does not change with scaling



## 1-server queues

### M/G/1 single queue

Excess and Age

- Age is a linearly growing random variable that increases and reset to zero when it resets
- Excess is a linearly decreasing random variable that decreases to zero when the next renewal cycle starts
- Time-average age = time-average excess = $\dfrac{E[X^2]}{2E[X]}$
  - Intuition - average area per unit x-axis, which is the average area of the triangle divided by the average size of the base
  - (Please understand the integral expression)



M/G/1 with different job types

- Red job with possion arrival time 0.25/sec arrival, 1s mean processing with variance 1s
- Blue job with possion arrival time 0.5/sec arrival, 0.5s mean processing with variance 1s
- E[Response_R] = E[W] + E[Service_R]
- E[Response_B] = E[W] + E[Service_B]
- The wait time is the same because they enter the same queue
- $\lambda = 0.5 + 0.25 = 0.75$
- $E[S] = \mu = 1 \times 1/3 + 0.5 \times 2/3 = 2/3$
- $\rho = \lambda/\mu = 1/2$
- $E[S_A^2] = \text{Var}[S_A] + (E[S_A])^2 = 1 + 1 = 2$ 
- $E[S_B^2] = \text{Var}[S_B] + (E[S_B])^2 = 1 + 0.25 = 1.25$ 
- $E[S^2] = 2 \times 1/3 + 5/4 \times 2/3 = 1.5$
- $E[\text{wait}] = \dfrac{\lambda E[S^2]}{2(1 - \rho)} = 9/8$



### M/G/1 priority queue

- Non-preemptive - once a job starts running, it cannot be preempted even if a higher priority job comes along
- Relevant identities
  - The overall rate is the sum of rates
  - The expected service time is the sum of probabilities of service time
  - The expected square of service time is the sum of probabilities of square of service time
  - (You cannot calculate variance directly this way)

The class $k$ customer needs to wait for

- The job currently in service, if there is one
- All jobs of priority 1...k in queue when the job arrives
- All jobs of priority 1...k-1 that arrive when the new job is waiting

Refer to slides and work them out



## Martingales Model

I have mostly referred an annotated

Takeaways

- A Martingales is a process where the expected value of the next step is always the same as the current value. This is used to derive other insights, which may not be exactly related to the Martingale process.
- We assume that markets are efficient, and all prices reflected are in equilibrium. This includes the initial stock price and the price of the option.




## Finals Cheatsheet

We are allowed a one page cheatsheet. 

![finals-cheatsheet](./finals-cheatsheet.png)





