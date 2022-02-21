# Chess-AI
A work in progress. I am writing a program to run a heuristic-minimax algorithm with alpha-beta pruning to play chess. I am using the chess library in python, but writing the code for the AI myself, and making it so a user can interactively play against the computer.

I currently have it working. It can play either first or second, the user gets to choose. The user also can choose a depth for the minimax, although I've only tested with a depth of up to 4. Before, it could only handle a depth of 2, and would otherwise crash midgame, but I think that my alpha-beta pruning is effective at allowing the program to go to a deeper depth. 


