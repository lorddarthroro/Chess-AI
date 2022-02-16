# Chess-AI
A work in progress. I am writing a program to run a heuristic-minimax algorithm with alpha-beta pruning to play chess. I am using the chess library in python, but writing the code for the AI myself, and making it so a user can interactively play against the computer.

I currently have it working. It can play either first or second, the user gets to choose. The user also can choose a depth for the minimax, although anything above 2 seems to cause a crash after a few moves (I'm working on debugging but it might just be a memory problem, since chess gets exponentially more complex as pieces are developed. I might try to prune the search tree). I'm gonna work on adding heuristics to improve it.


