---
title       : Fair football odds
subtitle    : Yes, that's how bookies do it (at least in principle)
author      : The guy from
job         : BYOBookie.com
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Basic considerations

1. In reasonably good approximation, football goals are 
  - independent of each other
  - scarce

2. Such independent and scarce events can be described by Poisson distributions
  - To describe a Poisson distributed random variable, we only need its expectation value $\lambda$, i.e. <span style="color:blue">its average</span>
  - If we know $\lambda$, we can calculate the whole distribution
  
3. This means for football teams: Once we know how many <span style="color:blue">goals to expect for a team on average</span>, we can calculate the probability for this team to score exactly 0, 1, 2... goals

4. We can then easily compute the probabilitiy of each final result

5. From the final results we can get the odds for a <span style="color:blue">home win / draw / away win</span> bet

---

## The necessary maths

Assume we expect $\lambda_h$ as the average number of goals for the home team. The home team's probability $P_k(\lambda_h)$ to score exactly k goals then is:

<center>
$P_k(\lambda_h) = \frac{\lambda_h^k}{k!} e^{-\lambda_h}$, with k = 0,1,2... 
</center>

Simliarly, we get for the away team's probability to score exactly j goals, if its expected average is $\lambda_a$:<center>
$P_j(\lambda_a) = \frac{\lambda_a^j}{j!} e^{-\lambda_a}$, with j = 0,1,2... 
</center>

Let's see an example for $\lambda_h$ = 1.3 and k=2:

```r
lambda_h = 1.3; k = 2; p_k <- exp(-lambda_h) * lambda_h^k / factorial(k); p_k
```

```
## [1] 0.2303
```

---

## The necessary maths (cont'd)

Since we treat the goals as being independent from each other, the probility $P_{kj}(\lambda_h,\lambda_a)$ of a final score of k:j (0:0, 1:0, 0:1, 2:0, 1:1, etc) simply is the product of the home team scoring exactly k goals and the away team scoring exactly j goals:

<center>
$P_{kj}(\lambda_h,\lambda_a) = P_k(\lambda_h) * P_j(\lambda_a)$, with k,j = 0,1,2... 
</center>

The rest is easy:
- Get the probability $P_{Home}$ of a home win by adding the probabilites of all scores in which the home team wins
- Do the same for $P_{Draw}$ and $P_{Away}$
- The fair betting odds are $1/P_{Home}$, $1/P_{Draw}$ and $1/P_{Away}$
- Done!

---

## Does it work?

1) In general, it's a very good approximation

2) Main problems 

- Usually underestimates the probability of a draw
- Especially underestimates the probability of a 0:0

3) Reason and solution

- Numbers of goals of home and away team are not completely independent of each other
- Can be remedied by using a bivariate Poisson distribution

4) More information

- Find a discussion with example here: 
http://www.byobookie.com/modelling-football/

