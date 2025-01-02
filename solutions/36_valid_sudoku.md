# [36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku)

![Static Badge](https://img.shields.io/badge/Difficulty-Medium-yellow)

## Problem Statement

Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

- Each row must contain the digits 1-9 without repetition.
- Each column must contain the digits 1-9 without repetition.
- Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.

**Note**:  
- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

### Examples

> **Example 1**  
> Input:  
> board =  
> [["5","3",".",".","7",".",".",".","."]  
> ,["6",".",".","1","9","5",".",".","."]  
> ,[".","9","8",".",".",".",".","6","."]  
> ,["8",".",".",".","6",".",".",".","3"]  
> ,["4",".",".","8",".","3",".",".","1"]  
> ,["7",".",".",".","2",".",".",".","6"]  
> ,[".","6",".",".",".",".","2","8","."]  
> ,[".",".",".","4","1","9",".",".","5"]  
> ,[".",".",".",".","8",".",".","7","9"]]  
> Output: `true`

> **Example 2**  
> Input:  
> board =  
> [["8","3",".",".","7",".",".",".","."]  
> ,["6",".",".","1","9","5",".",".","."]  
> ,[".","9","8",".",".",".",".","6","."]  
> ,["8",".",".",".","6",".",".",".","3"]  
> ,["4",".",".","8",".","3",".",".","1"]  
> ,["7",".",".",".","2",".",".",".","6"]  
> ,[".","6",".",".",".",".","2","8","."]  
> ,[".",".",".","4","1","9",".",".","5"]  
> ,[".",".",".",".","8",".",".","7","9"]]  
> Output: `false`  
> **Explanation:** Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.

### Constraints:
- `board.length == 9`
- `board[i].length == 9`
- `board[i][j]` is a digit `'1'`-`'9'` or `'.'`.

## My Code

```python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        row = [0]*9
        col = [0]*9
        box = [0]*9
        for r in range(len(board)):
            for c in range(len(board)):
                if board[r][c] == '.':
                    continue
                num = ord(board[r][c]) - ord('1')
                bit_mask = 1 << num
                box_ind = r//3 * 3 + c//3
                if (row[r] & bit_mask) or (col[c] & bit_mask) or (box[box_ind] & bit_mask):
                    return False
                row[r] |= bit_mask
                col[c] |= bit_mask
                box[box_ind] |= bit_mask
        return True
```
## Explanation

This solution leverages bitwise operations and the concept of bitmasking to efficiently validate a partially filled Sudoku board. Here's a detailed explanation:

1. **Bitmasking Basics**:  
   A bitmask is a binary representation where each bit position can represent a specific state or value. In this solution:
   - Each row, column, and 3x3 sub-box is represented by a 9-bit integer (an element in the `row`, `col`, and `box` arrays).
   - Each bit in these integers corresponds to a specific digit from `1` to `9`. For example:
     - The least significant bit (rightmost) represents the digit `1`.
     - The second least significant bit represents the digit `2`, and so on.
   - If a bit is `1`, it indicates that the corresponding digit is present in the row, column, or sub-box. If it's `0`, the digit is absent.

2. **Processing Each Cell**:  
   - For every non-empty cell in the Sudoku board, the digit is converted to its corresponding bit position using `ord(board[r][c]) - ord('1')`. For example:
     - `'1'` results in bit position `0` (`1 << 0 = 1`).
     - `'9'` results in bit position `8` (`1 << 8 = 256`).
   - This bit is stored in a variable called `bit_mask` using the formula `1 << (digit - 1)`.

3. **Checking for Conflicts**:  
   - The board is invalid if the bit corresponding to the current digit is already set in:
     - The `row[r]` bitmask (indicating the digit is already in the row).
     - The `col[c]` bitmask (indicating the digit is already in the column).
     - The `box[box_ind]` bitmask (indicating the digit is already in the 3x3 sub-box).
   - The index for the 3x3 sub-box is computed as `r // 3 * 3 + c // 3`.

4. **Updating the Bitmask**:  
   - If no conflicts are detected, the bitmask for the corresponding row, column, and sub-box is updated using the `|=` operator:
     - `row[r] |= bit_mask`
     - `col[c] |= bit_mask`
     - `box[box_ind] |= bit_mask`
   - This operation "sets" the bit corresponding to the current digit in the respective bitmasks.

5. **Final Validation**:  
   - The function iterates through all cells of the board. If no conflicts are found during the checks, the board is valid, and the function returns `True`.

**Advantages of Using Bitmask**:
- Compact storage: Instead of using arrays or sets to track digits, a single integer efficiently encodes the presence of digits.
- Fast operations: Checking for conflicts (`&`) and updating bitmasks (`|=`) are constant-time operations, making the algorithm very efficient.

This approach ensures the solution is both space-efficient and time-efficient, particularly for the fixed size of a 9x9 Sudoku board.

