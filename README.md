# Tic-Tac-Toe (C++) Console Game

A two-player Tic-Tac-Toe console game with additional quality-of-life features: play vs the computer, undo moves, persistent scoreboard across rounds, player names, and a simple random AI.

---

## Features 

- Play vs Computer  
  At startup you can choose to play against a basic computer opponent named "Computer". When enabled, the computer plays as O and chooses an empty cell at random.

- Player names  
  Players can enter display names. Names are shown in prompts and on the scoreboard so the game feels more personal and easier to follow.

- Undo last move  
  If you make a mistake, enter `-1` for the row when prompted to undo the most recent move. Undo restores the last cell to empty and switches the turn back to the other player. Multiple undos are supported until there are no moves left.

- Persistent scoreboard and rounds  
  Wins for X, wins for O, and draws are counted across rounds. After a round finishes the scoreboard is displayed and you are asked if you want to play another round; the `round` counter increments each time.

- Simple AI (random)  
  The computer player selects random empty cells. This provides a lightweight single-player option; the AI is intentionally simple and can be replaced with a stronger algorithm later.

- Input validation and retry behavior  
  Attempts to play out-of-bounds (row/col not in 0..2) or on an occupied cell are rejected and the player is prompted to try again without losing their turn.

- Clear console board display  
  The board is printed each turn with `|` and `-----` separators so every move is easy to read.

- Colored win message (where supported)  
  The program uses ANSI color codes to print a green win message on terminals that support ANSI sequences.

---

## Files

- `MainTicTacToe.cpp` — the C++ source implementing the `TicTacToe` class and game loop  
- `README.md` — this documentation

---

## How to Compile and Run

Save the source as `MainTicTacToe.cpp` and compile with a C++11 (or newer) compiler:

```bash
g++ -std=c++11 -o tic_tac_toe MainTicTacToe.cpp
./tic_tac_toe
```

If your file has a different name, replace `MainTicTacToe.cpp` with that filename.

---

## Board Layouts

Indexes for rows and columns are 0..2. The board is shown with separators; each cell contains a space `' '` (empty), `X`, or `O`.

Visual layout (empty):

```
   0   1   2
0  _ | _ | _
  ---+---+---
1  _ | _ | _
  ---+---+---
2  _ | _ | _
```

When printed by the program it appears like:

```
Current Board:
  |   |  
-----
  |   |  
-----
  |   |  
```

Example with coordinates for clarity:

```
   Col 0  Col 1  Col 2
Row 0   0,0 | 0,1 | 0,2
       -----+-----+-----
Row 1   1,0 | 1,1 | 1,2
       -----+-----+-----
Row 2   2,0 | 2,1 | 2,2
```

Use row then column when making a move.

---

## How to Play

1. Run the program.
2. When asked "Do you want to play vs Computer? (y/n):" enter `y` to play vs the built-in Computer or `n` to play two humans.
3. If playing vs Computer you will be prompted for your name and the other player will be "Computer". If playing two humans, enter both player names.
4. The board uses indices 0..2 for rows and columns. On your turn enter:
   - `<row> <column>` (each 0..2), for example `1 2`, to place your mark.
   - `-1` (for the row) to undo the last move; the column value is ignored in this case.
5. Invalid moves are rejected and you will be asked to retry without losing the turn.
6. The game ends when a player gets three in a row (win) or the board is full (draw).
7. After the round the scoreboard is shown and you can choose to play again.

---

## Detailed Gameplay Example (with boards)

Below is a step-by-step example of a short game between two human players (Alice = X, Bob = O). Each line shows the board after the move.

Start (empty):

```
Current Board:
  |   |  
-----
  |   |  
-----
  |   |  
```

1) Alice (X) plays 0 0

```
Current Board:
X |   |  
-----
  |   |  
-----
  |   |  
```

2) Bob (O) plays 1 1

```
Current Board:
X |   |  
-----
  | O |  
-----
  |   |  
```

3) Alice (X) plays 0 1

```
Current Board:
X | X |  
-----
  | O |  
-----
  |   |  
```

4) Bob (O) plays 2 2

```
Current Board:
X | X |  
-----
  | O |  
-----
  |   | O
```

5) Alice (X) plays 0 2 — this completes a row and X wins:

```
Current Board:
X | X | X
-----
  | O |  
-----
  |   | O

Player Alice (X) wins!
```

After the win, the program updates the scoreboard and asks whether to play again.

---

## Example Showing Undo and Computer Move

1) At start choose to play vs Computer: `y`  
   Enter name: `Charlie` (Charlie will be X, Computer will be O)

2) Round begins. Charlie plays 0 0:

```
Current Board:
X |   |  
-----
  |   |  
-----
  |   |  
```

3) Computer chooses (random) 1 1 — program prints:

```
Computer chooses: 1 1

Current Board:
X |   |  
-----
  | O |  
-----
  |   |  
```

4) Charlie accidentally types a wrong move, wants to undo — when prompted for row enter `-1`:

```
Enter your move (row[0-2] and col[0-2], -1 to undo): -1
Last move undone.
```

After undo, the board reverts to previous state (the last move removed and the turn switched back). If the last move was the computer's, the computer's move is undone; if the last move was the player’s, their move is undone.

---

## Implementation Overview

Class: `TicTacToe` (implemented in `MainTicTacToe.cpp`)

- Private members:
  - `std::vector<std::vector<char>> board` — 3×3 board (cells initialized with `' '`)
  - `char currentPlayer` — `'X'` or `'O'`
  - `std::string playerXName, playerOName` — player display names
  - `int scoreX, scoreO, draws` — scoreboard across rounds
  - `int round` — current round number
  - `std::stack<std::pair<int,int>> lastMoves` — history of moves for undo
  - `bool vsComputer` — whether O is played by the computer

- Key methods:
  - `getPlayerNames()` — asks whether to play vs computer and collects names
  - `resetBoard()` — clears the board and move history for a new round
  - `displayBoard()` — prints the board to the console
  - `placeMark(int row, int col)` — validates and places a mark; returns `false` for invalid move
  - `undoMove()` — reverts the most recent move and switches the player
  - `checkWin()` — checks rows, columns, and diagonals for a win
  - `getComputerMove()` — returns a random empty cell (simple AI)
  - `updateScore(char winner)` and `displayScores()` — update and print scoreboard
  - `playGame()` — main loop that handles rounds, input, undo, AI moves, and replay prompts

---

## Input Notes & Behavior

- Valid row/column values: 0, 1, 2.
- Enter `-1` for the row to undo the last move. Multiple undos are possible until no moves remain.
- Invalid moves do not consume a turn; you'll be asked to try again.
- The computer chooses moves randomly; randomness is seeded by the current time.
- ANSI color sequences are used for a colored win message; not all consoles may render the color.

---

## Suggestions for Further Improvement

- Implement a stronger AI (e.g., Minimax) to make the computer a challenging opponent.
- Add input sanitization for non-integer input.
- Save scoreboard to disk so scores persist between program runs.
- Make the board size configurable (NxN) and support variable win lengths.

---

## License

This project is open source and free to use for educational or personal projects.
