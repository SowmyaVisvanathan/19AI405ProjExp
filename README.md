# Implement a Sudoku Solver From Scratch
### Name: Sowmya V
### Reg no: 212222110045

## Aim:
To implement a Sudoku solver using the backtracking algorithm to find the solution for the given Sudoku puzzle.
## Steps to solve the Sudoku Puzzle in Python
- In this method for solving the sudoku puzzle, first, we assign the size of the 2D matrix to a variable M (M*M).
- Then we assign the utility function (puzzle) to print the grid.
- Later it will assign num to the row and col.
- If we find the same num in the same row or same column or in the specific 3*3 matrix, ‘false’ will be returned.
- Then we will check if we have reached the 8th row and 9th column and return true for stopping further backtracking.
- Next, we will check if the column value becomes 9 then we move to the next row and column.
- Further now we see if the current position of the grid has a value greater than 0, then we iterate for the next column.
- After checking if it is a safe place, we move to the next column and then assign the num in the current (row, col) position of the grid. Later we check for the next possibility with the next column.
- As our assumption was wrong, we discard the assigned num and then we go for the next assumption with a different num value

## Program:
```
def is_valid(board, row, col, num):
    # Check row
    for x in range(9):
        if board[row][x] == num:
            return False

    # Check column
    for x in range(9):
        if board[x][col] == num:
            return False

    # Check 3x3 subgrid
    start_row, start_col = 3 * (row // 3), 3 * (col // 3)
    for x in range(3):
        for y in range(3):
            if board[start_row + x][start_col + y] == num:
                return False

    return True

def solve_sudoku(board):
    for row in range(9):
        for col in range(9):
            if board[row][col] == 0:  # Empty cell
                for num in range(1, 10):
                    if is_valid(board, row, col, num):
                        board[row][col] = num
                        if solve_sudoku(board):
                            return True
                        board[row][col] = 0  # Backtrack
                return False
    return True

def print_board(board):
    for row in board:
        print(" ".join(str(num) if num != 0 else "." for num in row))

# Example board (0 = empty)
sudoku_board = [
    [5, 3, 0, 0, 7, 0, 0, 0, 0],
    [6, 0, 0, 1, 9, 5, 0, 0, 0],
    [0, 9, 8, 0, 0, 0, 0, 6, 0],

    [8, 0, 0, 0, 6, 0, 0, 0, 3],
    [4, 0, 0, 8, 0, 3, 0, 0, 1],
    [7, 0, 0, 0, 2, 0, 0, 0, 6],

    [0, 6, 0, 0, 0, 0, 2, 8, 0],
    [0, 0, 0, 4, 1, 9, 0, 0, 5],
    [0, 0, 0, 0, 8, 0, 0, 7, 9]
]

if solve_sudoku(sudoku_board):
    print("Solved Sudoku:")
    print_board(sudoku_board)
else:
    print("No solution exists.")

```
## Output:
![image](https://github.com/user-attachments/assets/a56e5ddb-5b87-4a74-8d0e-aac41e1d3151)

## Result:
Thus, a Sudoku solver using the backtracking algorithm is implemented for the given Sudoku puzzle.

