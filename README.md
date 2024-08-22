# TIC-TAC-TOE-GAME
#include <iostream>
#include <vector>

using namespace std;

void printBoard(const vector<vector<char>>& board) {
    for (const auto& row : board) {
        for (char cell : row) {
            cout << cell << ' ';
        }
        cout << endl;
    }
}

bool checkWin(const vector<vector<char>>& board, char player) {
    // Check rows and columns
    for (int i = 0; i < 3; ++i) {
        if ((board[i][0] == player && board[i][1] == player && board[i][2] == player) ||
            (board[0][i] == player && board[1][i] == player && board[2][i] == player)) {
            return true;
        }
    }
    // Check diagonals
    if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
        (board[0][2] == player && board[1][1] == player && board[2][0] == player)) {
        return true;
    }
    return false;
}

bool checkDraw(const vector<vector<char>>& board) {
    for (const auto& row : board) {
        for (char cell : row) {
            if (cell == ' ') return false;
        }
    }
    return true;
}

bool updateBoard(vector<vector<char>>& board, int move, char player) {
    int row = (move - 1) / 3;
    int col = (move - 1) % 3;
    if (board[row][col] == ' ') {
        board[row][col] = player;
        return true;
    } else {
        cout << "Cell already taken. Try again." << endl;
        return false;
    }
}

int getMove() {
    int move;
    while (true) {
        cout << "Enter your move (1-9): ";
        cin >> move;
        if (move >= 1 && move <= 9) return move;
        cout << "Invalid input. Please enter a number between 1 and 9." << endl;
    }
}

void playGame() {
    while (true) {
        vector<vector<char>> board(3, vector<char>(3, ' '));
        char currentPlayer = 'X';
        while (true) {
            printBoard(board);
            int move = getMove();
            if (!updateBoard(board, move, currentPlayer)) continue;
            if (checkWin(board, currentPlayer)) {
                printBoard(board);
                cout << "Player " << currentPlayer << " wins!" << endl;
                break;
            }
            if (checkDraw(board)) {
                printBoard(board);
                cout << "It's a draw!" << endl;
                break;
            }
            currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
        }
        char playAgain;
        cout << "Play again? (y/n): ";
        cin >> playAgain;
        if (playAgain != 'y' && playAgain != 'Y') break;
    }
}

int main() {
    playGame();
    return 0;
}

