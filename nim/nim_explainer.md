The following explanation is adapted from Tom Ferguson's note's, <https://www.math.ucla.edu/~tom/Game_Theory/comb.pdf>. 

Nim is an example of a <b>take-away game</b>, and of the larger class of combinatorial games. This game clearly has perfect information, and no stochastic elements, so we know who wins based on the initial position. It is solved, which explains why you can't win if the computer plays second. 
  
<b> P-positions:<b> A P-position is simply any position that is winning for the previous player. 
<b> N-positions:<b> Unsuprisingly, N-positions are positions that are winning for the next player
Say we are playing a very boring version of Nim with one pile with 4 pennies. A pile with 1 pennies, means the next player who plays next is definetly going to lose. If the next player loses, the previous player must be a winner. Thus we have a P-position! If 1 is a p-position, and a player can move from 2,3,4 to 1 (by taking 1,2, or 3 pennies respectively), 2,3, and 4 must be N-positions.
Ferguson shows how to generalize this using a recursive procedure for a broad class of games.
1. Terminal nodes are P-positions (this can be changed for misere rules, in which the last player to take a penny wins)
2. Positions that can reach P-positions in one turn are N-positions.
3. Positions that can only reach N-positions in one turn are P-positions.
4. Repeat 2 and 3 until no unlabeled positions.
