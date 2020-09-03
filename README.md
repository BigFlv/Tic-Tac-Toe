# Tic-Tac-Toe
Tic - TAC Toe -  02. 09.2020

package tictactoe;
import java.util.*;

public class Main {

    static Scanner scanner = new Scanner(System.in);
    public static void main(String[] args) {
        char[][] newGame = readField();
        printBoard(newGame);
        play(newGame);
    }

    static char[][] readField(){
        char[][] cells = new char[4][4];
        for (int i = 1; i <= 3; i++) {
            for (int j = 1; j <= 3; j++) {
                cells[i][j] = '_';
            }
        }
        return cells;
    }

    static void printBoard(char[][] cells) {
        System.out.println("---------");
        for (int i = 1; i <= 3; i++) {
            System.out.print("| ");
            for(int j = 1; j <= 3; j++) {
                System.out.print(cells[i][j] + " ");
            }
            System.out.println("|");
        }
        System.out.println("---------");
    }

    static void play(char[][] cells) {
        boolean stopped = false;
        int countX = 1;
        int countO = 0;
        while (!stopped) {
            System.out.print("Enter the coordinates: ");
            String input = scanner.nextLine().replaceAll(" ", "");

            try {
                int x = Integer.parseInt(input.substring(0, 1));
                int y = Integer.parseInt(input.substring(1, 2));
                if (x < 1 || x > 3 || y < 1 || y > 3) {
                    System.out.println("Coordinates should be from 1 to 3! ");
                } else if (cells[x][y] == 'O' || cells[x][y] == 'X') {
                    System.out.println("This cell is occupied! Choose another one!");
                } else {
                        if (countX > countO) {
                            cells[x][y] = 'X';
                            countO++;
                        } else {
                            cells[x][y] = 'O';
                            countX++;
                        }
                        printBoard(cells);
                        for (int row = 1; row <= 3; row++) {
                            for (int col = 1; col <= 3; col++) {
                                if (cells[row][1] == cells[row][2] && cells[row][1] == cells[row][3] && cells[row][1] != '_') {
                                    System.out.println(cells[row][1] + " wins");
                                    stopped = true;
                                } else if (cells[1][row] == cells[2][row] && cells[1][row] == cells[3][row] && cells[1][row] != '_') {
                                    System.out.println(cells[1][row] + " wins");
                                    stopped = true;
                                } else if (cells[1][1] == cells[2][2] && cells[1][1] == cells[3][3] && cells[1][1] != '_') {
                                    System.out.println(cells[1][1] + " wins");
                                    stopped = true;
                                } else if (cells[3][1] == cells[2][2] && cells[3][1] == cells[1][3] && cells[3][1] != '_') {
                                    System.out.println(cells[3][1] + " wins");
                                    stopped = true;
                                }
                                if (stopped) {
                                    break;
                                }
                            }
                            if (stopped) {
                                break;
                            }
                    }
                    if (countO + countX - 10 == 0 && !stopped) {
                        System.out.println("Draw");
                        stopped = true;
                    }
                }
            } catch (NumberFormatException e) {
                System.out.println("You should enter numbers!");
            }
        }
    }
}
