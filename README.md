# leetcode----37
Sudoku Solver
//code in java
class Solution {
    public void solveSudoku(char[][] board) {
        solve(board);
    }

    private boolean solve(char[][] board) {
        for (int row = 0; row < 9; row++) {
            for (int col = 0; col < 9; col++) {
                if (board[row][col] == '.') { // Find an empty cell
                    for (char num = '1'; num <= '9'; num++) {
                        if (isValid(board, row, col, num)) {
                            board[row][col] = num; // Try placing the number
                            if (solve(board)) {    // Recur to solve the next cells
                                return true;
                            }
                            board[row][col] = '.'; // Undo if the solution doesn't work
                        }
                    }
                    return false; // No valid number can be placed in this cell
                }
            }
        }
        return true; // Solved successfully
    }

    private boolean isValid(char[][] board, int row, int col, char num) {
        for (int i = 0; i < 9; i++) {
            // Check the row
            if (board[row][i] == num) {
                return false;
            }
            // Check the column
            if (board[i][col] == num) {
                return false;
            }
            // Check the 3x3 subgrid
            if (board[row / 3 * 3 + i / 3][col / 3 * 3 + i % 3] == num) {
                return false;
            }
        }
        return true;
    }
}
