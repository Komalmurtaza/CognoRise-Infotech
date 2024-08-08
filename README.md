
def print_board(board):
    print(f" {board[0]} | {board[1]} | {board[2]} ")
    print("---+---+---")
    print(f" {board[3]} | {board[4]} | {board[5]} ")
    print("---+---+---")
    print(f" {board[6]} | {board[7]} | {board[8]} ")

# Function to check for a win or tie
def check_winner(board, player):
    # Define winning combinations
    winning_combinations = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],  # Rows
        [0, 3, 6], [1, 4, 7], [2, 5, 8],  # Columns
        [0, 4, 8], [2, 4, 6]              # Diagonals
    ]
    for combo in winning_combinations:
        if board[combo[0]] == board[combo[1]] == board[combo[2]] == player:
            return True
    return False

# Function to check if the board is full
def is_board_full(board):
    return all([spot != ' ' for spot in board])

# Function to get a player's move
def player_move(board, player):
    while True:
        try:
            move = int(input(f"Player {player}, enter your move (1-9): ")) - 1
            if move < 0 or move >= 9:
                print("Invalid move. Please choose a number between 1 and 9.")
            elif board[move] != ' ':
                print("That spot is already taken. Try again.")
            else:
                board[move] = player
                break
        except ValueError:
            print("Invalid input. Please enter a number.")

# Function to switch player
def switch_player(player):
    return 'O' if player == 'X' else 'X'

# Main game function
def main():
    board = [' ' for _ in range(9)]  # Initialize an empty board
    current_player = 'X'  # Player X starts

    while True:
        print_board(board)
        player_move(board, current_player)

        if check_winner(board, current_player):
            print_board(board)
            print(f"Player {current_player} wins!")
            break
        elif is_board_full(board):
            print_board(board)
            print("It's a tie!")
            break

        current_player = switch_player(current_player)

if __name__ == "__main__":
    main()



