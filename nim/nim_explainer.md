<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

The following explanation is adapted and borrows heavily from Tom Ferguson's notes, <https://www.math.ucla.edu/~tom/Game_Theory/comb.pdf>. 

Nim is an example of a <b>take-away game</b>, and of the larger class of combinatorial games. This game clearly has perfect information and no stochastic elements, so we know who wins based on the initial position. It is solved, which explains why you can't win if the computer plays second. 
  
<b> P-positions:</b> A P-position is simply any position that is winning for the previous player. 

<b> N-positions:</b> Unsuprisingly, N-positions are positions that are winning for the next player

Say we are playing a very boring version of Nim with one pile with 4 pennies. A pile with 1 pennies, means the next player who plays next is definetly going to lose. If the next player loses, the previous player must be a winner. Thus we have a P-position! If 1 is a P-position, and a player can move from 2, 3, 4 to 1 (by taking 1, 2, or 3 pennies respectively), 2, 3, and 4 must be N-positions. Note that the rules of Nim we have been considering are actually the misère rules, in which the player who takes the last coin loses. "Normal play" is defined as the player who takes the last coin wins. This doesn't make a huge difference for our analysis for Nim, but can complicate other games.

Ferguson shows how to generalize this using a recursive procedure for a broad class of games.
1. Terminal nodes are P-positions (this can be changed for misère rules, in which the last player to take a penny wins)
2. Positions that can reach P-positions in one turn are N-positions.
3. Positions that can only reach N-positions in one turn are P-positions.
4. Repeat 2 and 3 until no unlabeled positions.

Let's build some intuition, by looking at a few positions. We have a good sense of how one pile Nim works, but what about two? For convenience I will represent the number of pennies in each row seperated by a column, so (1,0) is one penny in the first row (a P-position). So what is (1,1)? The next player can move to a P-position (1,0) by taking one from the second row, so this is an N-position. What about (1,2)? This is an N-position as well, as are any of the form (1,n)! Let's think about adding a row next. (1,1,1) turns out to be an P-position, because any possible move collapses to (1,1) which is an N-position. 

<details> 
  <summary>Q1: Test your intuition. What is (1,3,1)?  </summary>
   N-Position, removing two from the second stack gets to a P-position. A single turn to an P-position means it is a P-position.
</details>

Ok, that example wasn't so bad, but what if we get something more complicated, like (4,3,15)?

<b>Don't be a dumb-dumb, learn how to Nim-sum:</b>

It turns out that Nim is really all about the exclusive or operator (xor). We will express the xor operator as $$\oplus$$. Nim-sum is thus about adding in base 2. Here is a quick review of conversion between a binary representation (base 2), and decimal.

| Decimal | Base two |
| --- | --- |
| 4 | $$(0100)_2 $$ |
| 3 | $$(0011)_2 $$ |
|15 | $$(1111)_2 $$ |

The idea here is that each digit in the base two representation represents a power of 2, i.e. $$(2^n,...,2^3,2^2,2^1,2^0)$$. "Summing up" a base two representation if there is a 1 gets you back to decimal (i.e. $$(0100)_2= 0*2^3+1*2^2+0*2^1+0*2^0)=4$$). But this isn't so different from what we do in base 10, $$(015)_{10}=0*10^2+1*10^1+5*10^0=15$$.

Nim-sum works by adding in base two and ignoring any carries from one digit to another. This is mostly easily seen with an example. 

|var  |     |decimal    |Base 2 |
| --- | --- | --- | ---            |
|x    |=    |4    |=$$(0100)_2 $$ |
|y    |=    |5    |=$$(0101)_2 $$ |
|x$$\oplus$$y  |=    |1    |=$$(0001)_2 $$ |

Note we "canceled" out the 1 in the $$2^2$$ position. Note that nim-sum has a lot of the same properties as our standard operators, it is assosciated, has an identity with 0, and has a negative (itself).

<details> 
  <summary> Q2: \(22 \oplus 15 \oplus 13 \) ?  </summary>
         $$ 22= 10110  $$
         $$ \oplus$$
         $$ 15= 01111 $$
         $$ \oplus$$
         $$ \underline{13= 01101} $$
         $$ \textbf{20= 10100} $$           
</details>

So what does Nim-sum have to do with Nim? 

<b>Bouton's Theorem:<\b> In Nim, under "normal play" rules, a position \(  (x_1, x_2, ..., x_n) \) is a P-position iff the nim-sum over all piles, \(  x_1 \oplus x_2 \oplus ... \oplus x_n) \) is 0. 

<b> Proof: <b> Let's check this is true. Under normal play, we will consider the last position as 0 coins remaining (note I was loose in my definition of this earlier, and called one coin left the terminal position, this is technically incorrect, but makes the analysis under misere simpler) \(  0 \oplus 0 \oplus ... \oplus 0) \) is 0. This condition is satisfied. 

Every move from a P-position is to an N-position. We can show this by contradiction. We are in P-position \( (x_1, x_2,...,x_n) \), so \(  x_1 \oplus x_2 \oplus ... \oplus x_n) \) = 0. Claim, there is some \( x'_i \lt x_i \) s.t. \(  x'_1 \oplus x_2 \oplus ...\oplus  x_i \oplus ... \oplus x_n) \) = 0. But for this to be true, by the negation property established earlier, \( x'_i = x_i \), which is a contradiction to our assumption. So any move must lead to an N-position.

Every N-position can move to a P-position: To move from N to P, find the leftmost column with an odd number of 1's. Remove the leading 1 from one of the rows with a 1 in the leftmost colum with an odd number, and change the entries in this row such that all trailing columns have an even number of 1's. This will always be possible since every column is clearly at most one 1 away from having an even number of 1's. This move will always be legal because removing the leading 1 will shrink the total of the row regardless of what happens to the following columns. QED

Note that this proof is constructive and tells you the next move you want to make. Note that the above proof is for the normal version of Nim. However, most of our discussion and the game on this site are in the more common misère version of the game. In order to adapt the proof for misère, play as if the game was under the normal rules until there are less than 2 rows only 1 remaining. Eventually your opponent will eventually be forced to move so that there is exactly one pile greater than 1 (or two rows each with 1). You can then win by leaving only 1 left in 1 row, forcing the other play to lose! It turns out a lot of combinatorial games are actually just Nim in disguise. You can test your understanding by winning the game here: <https://benpyle.github.io/nim/>

