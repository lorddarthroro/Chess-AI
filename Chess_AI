import chess.svg

winner = False
score = 0


class Algorithms():
    global bestmove

    def __init__(self, board1):
        self.boardx = board1

    def minimax(self, board, isMax, depth, bestmove, alpha, beta):
        if (winner == True):
            return bestmove
        if (depth == 0):
            return bestmove

        if isMax:
            bestscore = -10000
            Holder = False

            for move in board.legal_moves:

                currentMove = chess.Move.from_uci(str(move))
                if bestmove == None:
                    bestmove == currentMove
                game = chessGame(board)
                if (currentMove in board.legal_moves):
                    board.push(currentMove)

                    nextMove = Algorithms(board).minimax(board, False, depth - 1, bestmove, alpha, beta)
                    if(nextMove in board.legal_moves):
                        board.push(nextMove)
                        Holder = True
                    if evaluateBoard(board) > bestscore:
                        bestscore = evaluateBoard(board)
                        bestmoveWhite = currentMove
                        bestmove = currentMove


                    if Holder == True:
                        board.pop()
                        Holder = False
                    else:
                        Holder = False
                    board.pop()
                if bestscore > alpha:
                    alpha = bestscore
                if beta <= alpha:
                    break

            return bestmove


        else:
            bestscore = 10000
            holder = False
            for move in board.legal_moves:
                currentMove = chess.Move.from_uci(str(move))
                if bestmove == None:
                    bestmove == currentMove
                game = chessGame(board)
                if (currentMove in board.legal_moves):
                    board.push(currentMove)
                    nextMove = Algorithms(board).minimax(board, True, depth - 1, bestmove, alpha, beta)
                    if (nextMove in board.legal_moves):
                        board.push(nextMove)
                        holder = True
                    else:
                        holder = False
                    if evaluateBoard(board) < bestscore:
                        bestscore = evaluateBoard(board)
                        bestmoveBlack = currentMove
                        bestmove = currentMove
                    if holder == True:
                        board.pop()
                        holder = False
                    board.pop()
                if bestscore < beta:
                    beta = bestscore
                if beta <= alpha:
                    break
            return bestmove


class chessGame():
    def __init__(self, board):
        self.board = board
        self = self

    # might remove, doesn't do anything rn
    def is_valid(self, move):
        legal_moves = list(boardx.legal_moves)  # creates list of legal moves
        for moves in legal_moves:  # checks if move is legal
            if moves == Nf3:
                return True
        return False


def evaluateBoard(board):
    count = 0
    # can't move your own king into checkmate, so this will return 1000 for a winning move for whoevers turn it is
    if board.is_checkmate():
        global winner
        winner = True
        if board.turn == False:  # return 1000 if white went last
            count += 1000
        else:  # return -1000 if black went last
            count -= 1000

    for s in range(64):
        # capital letters = white, lowercase = black
        piece = board.piece_at(getattr(chess, all_squares[s]))
        if str(piece) == 'P':
            count += 10
        elif str(piece) == 'p':
            count -= 10
        elif str(piece) == 'B' or str(piece) == 'N':
            count += 30
        elif str(piece) == 'b' or str(piece) == 'n':
            count -= 30
        elif str(piece) == 'R':
            count += 50
        elif str(piece) == 'r':
            count -= 50
        elif str(piece) == 'Q':
            count += 100
        elif str(piece) == 'q':
            count -= 100
        elif str(piece) == 'K':
            if s == 16:
                count += 5
            elif s == 48:
                count += 5
        if str(piece) == 'k':
            if s == 23:
                count -= 5
            elif s == 55:
                count -= 5

        if s in (
        18, 19, 20, 21, 26, 27, 28, 29, 34, 35, 36, 37, 42, 43, 44, 45):  # checks center squares (center control good)
            if str(piece) == 'P':
                count += 1
            elif str(piece) == 'p':
                count -= 1
            elif str(piece) == 'B':
                count += 2
            elif str(piece) == 'b':
                count -= 2
            elif str(piece) == 'N':
                count += 5
            elif str(piece) == 'n':
                count -= 5
            elif str(piece) == 'Q':
                count += 4
            elif str(piece) == 'q':
                count -= 4

    # TO DO: add hueristics for rook placement, castling, and fiencetto bishop
    return count


boardx = chess.Board()

Nf3 = chess.Move.from_uci("b1c3")
game = chessGame(boardx)
# if (game.is_valid(Nf3)):
#   board.push(Nf3)  # Make the move
# board.pop()  # Unmake the last move
squares = (chess.A1, chess.A2)  # oh lord
# print(chess.RANK_NAMES + chess.FILE_NAMES)
# all_squares holds all squares
all_squares = []
for i in range(8):
    for j in range(8):
        all_squares.append((chess.FILE_NAMES[i].upper() + chess.RANK_NAMES[j]))
# for i in all_squares:
# print(i)
piece = boardx.piece_at(getattr(chess, all_squares[1]))
# print(list(board.legal_moves))
AI = Algorithms(boardx)
# print(evaluateBoard(boardx))
print('Would you like to go FIRST (enter 1) or SECOND (enter 2)')
first_or_second = input()
print('Please choose a depth')
depth = int(input())
alp = -1000000
bet = 1000000
if int(first_or_second) == 1:
    while not boardx.is_game_over():

        print('Please enter your move (in format of current location of piece + desired location ex. a2a4')
        x = input()
        move = chess.Move.from_uci(str(x))
        if move in boardx.legal_moves:
            boardx.push(move)
        print(boardx)
        print()
        best_move = (AI.minimax(boardx, False, depth, None, alp, bet))
        print(best_move)
        move = chess.Move.from_uci(str(best_move))
        boardx.push(move)  # Make the move
        print(boardx)
        print()

        # displays gui in svg file
        board_svg = chess.svg.board(boardx, size=350)
        output_file = open('test.svg', "w")
        output_file.write(board_svg)
        output_file.close()
else:
    while not boardx.is_game_over():
        best_move = (AI.minimax(boardx, True, depth, None, alp, bet))
        move = chess.Move.from_uci(str(best_move))
        boardx.push(move)  # Make the move
        print(boardx)
        print()

        # displays gui in svg file
        board_svg = chess.svg.board(boardx, size=350)
        output_file = open('test.svg', "w")
        output_file.write(board_svg)
        output_file.close()

        print('Please enter your move (in format of current location of piece + desired location ex. a2a4')
        x = input()
        move = chess.Move.from_uci(str(x))
        boardx.push(move)
        print(boardx)
        print()

# displays gui in svg file
board_svg = chess.svg.board(boardx, size=350)
output_file = open('test.svg', "w")
output_file.write(board_svg)
output_file.close()
