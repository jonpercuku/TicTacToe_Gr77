Tic-Tac-Toe (C++) Console Game

Ky projekt është një implementim në C++ i lojës klasike Tic-Tac-Toe për console. Dy lojtarë luajnë me radhë në një fushë 3×3, duke synuar të vendosin tre shenja rresht (horizontalisht, vertikalisht ose diagonalisht). Loja mbështet disa raunde rresht, emra të personalizuar dhe mbajtje rezultatesh.

Features

Lojë me dy lojtarë (pa AI)

Emra të personalizuar për Player X dhe Player O

Scoreboard që ruan fitoret dhe barazimet

Mundësi për të luajtur disa raunde rresht

Gameplay me radhë (turn-based)

Validim i inputit (kontroll kufijsh dhe qelizash të zëna)

Zbulim fitoreje (rreshta, kolona, diagonale)

Zbulim barazimi

Shfaqje e pastër e tabelës në console pas çdo lëvizjeje

How to Compile and Run

Për ta kompiluar programin duke përdorur g++:
To compile the code using `g++`, run:

g++ -std=c++11 -o TicTacToe_Gr77 MainTicTacToe.cpp
./TicTacToe_Gr77

How to Play

Loja fillon automatikisht pas ekzekutimit.

Në fillim, përdoruesi fut emrat për Player X dhe Player O.

Tabela është një grid 3×3 me indekse nga 0 deri në 2 për rreshta dhe kolona.

Player X fillon gjithmonë i pari.

Kur të kërkohet, fut dy numra: rreshti dhe kolona ku dëshiron të vendosësh shenjën.

Shembull: 1 2 → rreshti 1, kolona 2

Nëse lëvizja është jashtë kufijve ose qeliza është e zënë, lëvizja refuzohet dhe i njëjti lojtar provon përsëri.

Loja përfundon kur:

Një lojtar fiton

Tabela mbushet pa fitues (barazim)

Pas çdo raundi shfaqet scoreboard-i dhe pyetja nëse dëshironi të luani përsëri.

Game Layout Example

Tabela bosh:

 | | 
-----
 | | 
-----
 | |
 
Pas disa lëvizjeve:

X|O| 
-----
 |X| 
-----
 | |O
 
Shembull rezultati:
John (X) wins!
Scoreboard:
John (X): 2
Anna (O): 1
Draws: 1
Code Overview

Class: TicTacToe

Private Members

vector<vector<char>> board – përfaqëson fushën 3×3

char currentPlayer – lojtari aktual ('X' ose 'O')

string playerXName, playerOName – emrat e lojtarëve

int scoreX, scoreO, draws – rezultatet

Public Methods

TicTacToe() – inicializon tabelën dhe rezultatet

getPlayerNames() – merr emrat e lojtarëve

displayBoard() – shfaq tabelën

placeMark(int row, int col) – vendos shenjën me validim

checkWin() – kontrollon fitore

switchPlayer() – ndërron lojtarin

updateScore(char winner) – përditëson scoreboard-in

displayScores() – shfaq rezultatet

resetBoard() – rifillon tabelën për raund të ri

playGame() – logjika kryesore e lojës

Customization Ideas

Shtimi i një AI (minimax)

Ruajtja e rezultateve në file

Ndryshimi i madhësisë së tabelës (NxN)

Interface grafike (SFML / SDL)

## License

This code is open source and free to use for educational or personal projects :) 
