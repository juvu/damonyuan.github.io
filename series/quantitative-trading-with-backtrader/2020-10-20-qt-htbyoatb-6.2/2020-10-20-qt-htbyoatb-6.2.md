---
title:  "手动拆解《Quantitative Trading - How to Build Your Own Algorithmic Trading Business》（六.2）"
description: "手动拆解《Quantitative Trading - How to Build Your Own Algorithmic Trading Business》（六.2）"
date: 2020-11-01 15:04:23
hidden: true
categories: [Trading]
tags: [backtrader, quantitative, trading]
---

# 手动拆解《Quantitative Trading - How to Build Your Own Algorithmic Trading Business》（六.2）

上一章结尾我们提到股票投资中获利概率 P 不是一个常量，赔率（或者回报率）也不是常量，那我们必然需要用几个假设来界定适用范围。我们假设

1. 投资策略选中的投资组合中的股票回报是符合正态分布的。进一步说这意味着股票回报有固定的均值和方差，现在的均值和方差可以用于计算未来的参数。
2. 回报率指的是扣除了所有损耗的剩余回报。
3. 所有的利润都会被重新用于投资。

- The author initiated the practical application of the Kelly criterion by using it for card counting in blackjack.
  We will present some useful formulas and methods to answer various natural questions
  about it that arise in blackjack and other gambling games. 
- Then we illustrate its recentuse in a successful casino sports betting system. 
- Finally, we discuss its application to the securities markets where it has helped the author to make a thirty year total of 80 billion dollars worth of “bets”.

http://www.eecs.harvard.edu/cs286r/courses/fall12/papers/Thorpe_KellyCriterion2007.pdf

$$
f = W - (1 - W) / R
$$
$$
f = m / s^2
$$

assume that the return distribution of a strategy (or security) is Gaussian

https://www.quantstart.com/articles/Money-Management-via-the-Kelly-Criterion/

 “half-Kelly” betting.
 
 long-term compounded growth rate of your equity.
 
 $$ g = r + S^2/2 $$
 
 I would advise using a lookback period of six months.
 
 https://www.investopedia.com/articles/financial-theory/11/calculating-covariance.asp
 
 Dividing the maximum tolera- ble one-period drawdown on equity by the maximum historical loss will tell you whether even half-Kelly leverage is too large for your comfort. 
 
 * backtrader init orders
 * backtrader with kelly's formula
 
 [如何通俗易懂地解释「协方差」与「相关系数」的概念](https://www.zhihu.com/question/20852004)
 
 线性回归和协方差的关系 - 没有关系。
 
 https://github.com/kelly-direct/kelly-criterion/blob/master/kelly_criterion/kelly_criterion.py
 
 https://zhuanlan.zhihu.com/p/20869162
 
 1. if f is negative, remove the stock and wait it to turn positive; we don't want to sell when no leverage
 2. deal with the positive


