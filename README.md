# codsoft_task2
```python
import math

board = [" " for _ in range(9)]

def print_board():
    print()
    for i in range(0, 9, 3):
        print(f" {board[i]} | {board[i+1]} | {board[i+2]} ")
        if i < 6:
            print("---+---+---")
    print()

def check_winner():
    combinations = [
        (0, 1, 2), (3, 4, 5), (6, 7, 8),
        (0, 3, 6), (1, 4, 7), (2, 5, 8),
        (0, 4, 8), (2, 4, 6)
    ]

    for a, b, c in combinations:
        if board[a] == board[b] == board[c] and board[a] != " ":
            return board[a]

    if " " not in board:
        return "Draw"

    return None

def minimax(is_maximizing):
    result = check_winner()

    if result == "O":
        return 1
    if result == "X":
        return -1
    if result == "Draw":
        return 0

    if is_maximizing:
        best_score = -math.inf

        for i in range(9):
            if board[i] == " ":
                board[i] = "O"
                score = minimax(False)
                board[i] = " "
                best_score = max(best_score, score)

        return best_score

    else:
        best_score = math.inf

        for i in range(9):
            if board[i] == " ":
                board[i] = "X"
                score = minimax(True)
                board[i] = " "
                best_score = min(best_score, score)

        return best_score

def ai_move():
    best_score = -math.inf
    best_move = None

    for i in range(9):
        if board[i] == " ":
            board[i] = "O"
            score = minimax(False)
            board[i] = " "

            if score > best_score:
                best_score = score
                best_move = i

    board[best_move] = "O"

def human_move():
    while True:
        try:
            position = int(input("Enter your position (1-9): ")) - 1

            if position < 0 or position > 8:
                print("Enter a number between 1 and 9.")
            elif board[position] != " ":
                print("That position is already occupied.")
            else:
                board[position] = "X"
                break
        except ValueError:
            print("Enter a valid number.")

def main():
    print("Tic-Tac-Toe")
    print("You are X. AI is O.")
    print("Positions:")
    print(" 1 | 2 | 3 ")
    print("---+---+---")
    print(" 4 | 5 | 6 ")
    print("---+---+---")
    print(" 7 | 8 | 9 ")

    while True:
        print_board()

        human_move()

        result = check_winner()

        if result:
            print_board()
            if result == "X":
                print("You win!")
            else:
                print("Draw!")
            break

        ai_move()

        result = check_winner()

        if result:
            print_board()
            if result == "O":
                print("AI wins!")
            else:
                print("Draw!")
            break

if __name__ == "__main__":
    main()
```
