#include <iostream>
using namespace std;

char board[3][3] = {{' ', ' ', ' '}, {' ', ' ', ' '}, {' ', ' ', ' '}};
char currentPlayer = 'X';

void printBoard() {
    cout << "  0 1 2" << endl;
    for (int i = 0; i < 3; ++i) {
        cout << i << " ";
        for (int j = 0; j < 3; ++j) {
            cout << board[i][j] << "|";
        }
        cout << endl;
        if (i < 2) cout << "  -----" << endl;
    }
}

bool checkWin() {
    // Проверка строк
    for (int i = 0; i < 3; ++i) {
        if (board[i][0] == currentPlayer && board[i][1] == currentPlayer && board[i][2] == currentPlayer)
            return true;
    }
    // Проверка столбцов
    for (int j = 0; j < 3; ++j) {
        if (board[0][j] == currentPlayer && board[1][j] == currentPlayer && board[2][j] == currentPlayer)
            return true;
    }
    // Проверка диагоналей
    if (board[0][0] == currentPlayer && board[1][1] == currentPlayer && board[2][2] == currentPlayer)
        return true;
    if (board[0][2] == currentPlayer && board[1][1] == currentPlayer && board[2][0] == currentPlayer)
        return true;

    return false;
}

bool isBoardFull() {
    for (int i = 0; i < 3; ++i) {
        for (int j = 0; j < 3; ++j) {
            if (board[i][j] == ' ')
                return false;
        }
    }
    return true;
}

void switchPlayer() {
    currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
}

int main() {
    int row, col;

    while (true) {
        printBoard();
        cout << "Игрок " << currentPlayer << ", введите строку и столбец (0-2): ";
        cin >> row >> col;

        if (row < 0 || row > 2 || col < 0 || col > 2 || board[row][col] != ' ') {
            cout << "Некорректный ход, попробуйте снова." << endl;
            continue;
        }

        board[row][col] = currentPlayer;

        if (checkWin()) {
            printBoard();
            cout << "Игрок " << currentPlayer << " выиграл!" << endl;
            break;
        }

        if (isBoardFull()) {
            printBoard();
            cout << "Игра закончилась вничью!" << endl;
            break;
        }

        switchPlayer();
    }

    return 0;
}
