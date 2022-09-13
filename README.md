# Connect-4-AI
Connect 4 is a well known game where you drop peices into a board in hopes to connect 4 peices either diagonally, vertically, or horizontally, before the opponent.

In this project I coded from scratch a connect 4 algorithm which looks ahead at possible game states, evaluates each state based on a simple fitness function, then chooses the best move assuming the opponent is playing perfectly. The fitness function is quite simple, looking at the number of potential 4 in a row, i.e. if there is 3 in a row with a space or 2 in a row with a space.

This algorithm is called minimax and its main downside is that it the number of board states expotentially grows with each new layer of depth, which makes it impossible to calculate the best move using this algorithm as there is 4.5 trillion different board states. However, the greater the deapth of its search the greater it preforms, and so much work is done in optimizing it.

# How to play

When the program runs, it asks if you would like to play 'playerVscomputer' or 'computerVscomputer'
simply type into the terminal what you want to play

If you choose playerVscomputer, then when it is your turn you can type in the number corresponding to the slot where your peice will be dropped and press enter.
First to connect 4 in a row wins!

# Optimizers

**Alpha-beta pruning** is the first optimization I added. To explain it we can start by assuming we want to maximize our score, and the oponent wants to minimize our score. Suppose there are two different boardstates branching off of the main board, Board1 and Board2. Suppose it is the opponents move. If the opponent moves to Board1 then I will have a score of 6 with perfect play. When calculating my score at Board2, suppose there is two moves I can make, one move sets my score at 6, and the other move sets my score at 9. Since I want to maximize my score, I choose a score of 9, but since the opponent wants to minimize my score, they choose Board1, giving me a score of 6. Infact, we can replace the score of 9 with the score of 100 or any other number and come up with the same result. It follows that we don't have to look at what the last number is, which will save on computing time.

I also added **bitboards** which is a way of storing the gamedata by encoding it into binary. This made calculations such as checking for a winning board much easier and computationally faster through the use of binary operations, and since each boardstate has to check for a winning board, it greatly helped optimize the code.

Next was **changing the depth of the search**. At the start of the game it takes much more computation to get to the same depth since each turn there is 7 moves avaiable and not many winning moves, however, later on in the game the number of legal and plausable moves greatly decreases which means keeping the same time limit, much greater depth can be searched. Because of this I increased the depth of the search as the game progressed.

Lastly I added a checks for an **earlier deterination of a winning state** by checking if there was any 1 move wins first which slightly helped make it faster. I did also try to add a transposition table into my code, however,  I did not notice any tangible difference from before it was added and so decided to remove it.

