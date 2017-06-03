---
layout: post
title: "FiveThirtyEight Riddler - Auctions"
date: 2017-06-02
---

In this post I rewrite some notes from my game theory course to solve the ["how much should you bid" Riddler.](https://fivethirtyeight.com/features/how-much-should-you-bid-for-that-painting/)

## Problem set-up
The premise for the problem is you are bidding against your arch-rival for a painting. You each have a valuation for the painting drawn from a uniform distribution between 0 and 100,000,000. You each submit a sealed bid (private valuation), with a winner pay format, first price format.

### Defining what we want to solve for
What is the object we are looking for? Well, for this sort of game we want a Bayesian Nash Equilibrium. For completeness, I'll briefly mention what a Nash EQ is before defining a BNE. The core principle behind a NE (despite what [a certain movie](https://www.youtube.com/watch?v=2d_dtTZQyUM) might have you believe...) is that all players are playing strategies that are best responses to the strategies played by all of the other players. That is there is no profitable unilateral deviation (i.e. no one player can do better by playing a different strategy unless the other players were to also change their strategies). 

The Bayesian version of this concept isn't so different, but since we're being all Bayesian about things know we've got beliefs floating around. These beliefs will be driven by Nature (Harsanyi 1967), which is basically a short-hand way of modeling randomness in the game. The important thing for these Bayesian games is that there is some sort of incomplete information. Being lazy and taking the definition from wikipdia... "A Bayesian Nash equilibrium is defined as a strategy profile and beliefs specified for each player about the types of the other players that maximizes the expected payoff for each player given their beliefs about the other players' types and given the strategies played by the other players."

But since I'm studying for prelims... let's practice making this a bit more formal. I'm going to follow Mas Collel, Whinston, & Green for this, but there are plenty of similar notes online. A Baysian game has the following elements:
* players \{ 1, ... , i , ... , N \}
* payoff function: $$u_i(s_i, s_{-i}, \theta_i) $$
* player type: $$ \theta_i \in \Theta_i $$ player type for player i chosen by nature (private information to i)
* Joint pdf of $$ \theta_i$$'s governed by a (commonly) known $$ F(\theta_i,...,\theta_N) $$
* strategies (read: decision rule), $$s_i(\theta_i)\in S_i $$, importantly a function of player type.

We can thus summarize the game as  $$ [N, \{S_i\}, \{ u_i(\cdot) \}, \Theta, F(\cdot)] $$. With this in mind, it is easy to formulate the definition of an equilibrium as: the set of decision rules $$(s_1(\cdot),...,s_N(\cdot))$$ s.t.
$$ \mathbb{E}[u_i(s(\theta),\theta)]\geq \mathbb{E}[u_i(s'_i(\theta_i),s_{-i}(\theta_{-i}),\theta) $$.
Another way of framing this is to say a profile of decision rules is a BNE iff $$ \mathbb{E}_{\theta-1}[u_i(s_i(\tilde{\theta}_i),s_{-i}(\theta_{-i},\tilde{\theta}_i)|\tilde{\theta_i}]\geq \mathbb{E}_{\theta-1}[u_i(s'_i,s_{-i}(\theta_{-i},\tilde{\theta}_i)|\tilde{\theta_i}] \forall s'_i \in S_i. $$ This definition tells us that we can basically treat each type of player seperately, with each rying to max her payoff given the conditional pd over her rivals choices.


