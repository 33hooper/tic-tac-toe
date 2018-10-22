# tic-tac-toe
basic tic tac toe game created via Python


from IPython.display import clear_output

def display_board(board):
    # clear the output to show an empty board
    clear_output()
    print(board[7] + " | " + board[8] + " | " + board[9])
    print("- | - | -")
    print(board[4] + " | " + board[5] + " | " + board[6])
    print("- | - | -")
    print(board[1] + " | " + board[2] + " | " + board[3])
    

def player_input():
    marker = ""
    # keep asking player 1 to choose "X" or "O"
    while marker != "X" and marker != "O":
        marker = input("Player 1 chooses(X or O): ").upper()
    # set player1 equals to the first valid input 
    # if player1 chooses "X" then player2 is "O", vice versa
    ''' output = (player1 marker, player2 marker) '''
    if marker == "X":
        return("X","O")

    else: 
        return ("O", "X")

   
 
def place_marker(board, marker, position):
    board[position] = marker
    
    
def win_check(board, mark):
        return (board[1] == mark and board[2] == mark and board[3] == mark) or (board[4] == mark and board[5] == mark and board[6] == mark) or (board[7] == mark and board[8] == mark and board[9] == mark) or (board[1] == mark and board[5] == mark and board[9] == mark) or (board[7] == mark and board[5] == mark and board[3] == mark) or (board[9] == mark and board[6] == mark and board[3] == mark) or (board[8] == mark and board[5] == mark and board[2] == mark) or (board[7] == mark and board[4] == mark and board[1] == mark)


import random

def choose_first():
    return f"player{random.randint(1,2)}"
    

def space_check(board, position):
    return (board[position] != "X" and board[position] != "O")
    
    
def full_board_check(board):
#     marks_count = []
#     for marks in board:
#         if marks == "X" or marks == "O":
#             marks_count.append(marks)
#     return len(marks_count) == 9
    for i in range(1,10):
        if space_check(board,i):
            return False
    # board is full
    return True
    
    
    
def player_choice(board):
    position = 0
    while position not in [1,2,3,4,5,6,7,8,9] or not space_check(board, position):
    # use position to take the input of option
        position = int(input("choice of position(1-9): "))
    # check the availability of that position
    return position
    
    
def replay():
    check_for_rematch = input("do you want to play the game again(yes or no)? ")
    return check_for_rematch == "yes"


def tic_tac_toe():
    # use a while loop to keep the game going
    print('Welcome to Tic Tac Toe!')

    while True:

    # set up
    # board, who chooses first, marker choice, 
        game_board = ["0","1","2","3","4","5","6","7","8","9"]
        player1_marker,player2_marker = player_input()
        turn = choose_first()
        print(turn + " will go first")

        play_game = input("Ready to play? yes or no ")
        if play_game == "yes":
            game_on = True
        else:
            game_on = False

        while game_on:
            if turn == "player1":
                # show the board
                display_board(game_board)
                # choose a position
                position = player_choice(game_board)
                # place the marker on the position if it is available
                place_marker(game_board, player1_marker, position)
                # check if they won
                if win_check(game_board, player1_marker):
                    display_board(game_board)
                    print("player1 has won")
                    game_on = False
                # check if there is a tie
                else:
                    if full_board_check(game_board):
                        display_board(game_board)
                        print("Tie game!!!")
                        break
                    else: 
                        turn = "player2"  # no tie, no win, then next player's turn
            else:
                display_board(game_board)
                # choose a position
                position = player_choice(game_board)
                # place the marker on the position if it is available
                place_marker(game_board, player2_marker, position)
                # check if they won
                if win_check(game_board, player2_marker):
                    display_board(game_board)
                    print("player2 has won")
                    game_on = False
                # check if there is a tie
                else:
                    if full_board_check(game_board):
                        display_board(game_board)
                        print("Tie game!!!")
                        break
                    else: 
                         turn = "player1"  # no tie, no win, then next player's turn

        if not replay():
            break
