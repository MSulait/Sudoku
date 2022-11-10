# Sudoku
package com.company;
import java.util.*;
public class Main {

    public static void main(String[] args) {
        // write your code here
        Scanner input = new Scanner(System.in);

        int[][] board =
                {
                        {5, 3, 0, 0, 7, 0, 0, 0, 0},
                        {6, 0, 0, 1, 9, 5, 0, 0, 0},
                        {0, 9, 8, 0, 0, 0, 0, 6, 0},
                        {8, 0, 0, 0, 6, 0, 0, 0, 3},
                        {4, 0, 0, 8, 0, 3, 0, 0, 1},
                        {7, 0, 0, 0, 2, 0, 0, 0, 6},
                        {0, 6, 0, 0, 0, 0, 0, 0, 0},
                        {0, 0, 0, 4, 1, 9, 0, 0, 5},
                        {0, 0, 0, 0, 8, 0, 0, 7, 9}
                };

        do {
            printBoard(board); // Display Board

            // Ask Coordinates
            System.out.println("Enter the row to change: ");
            int row = input.nextInt();
            System.out.println("Enter the column to change: ");
            int column = input.nextInt();

            // Make Changes
            do {
                System.out.println("Enter a number between 1 and 9: ");
                board[row][column] = input.nextInt();
            }

            // Check if number is between 1 and 9
            while (board[row][column] < 1 || board[row][column] > 9);

            // Check rows columns and small boxes and set number to 0 in case of invalid input
            if (!row(board, row, column) || !column(board, row, column) || !smallbox(board, row, column)) {
                board[row][column] = 0;
                System.out.println("Sorry! Invalid number");
            }
        }

        while (!solution(board));
        System.out.println("Congratulations!");

        printBoard(board);
    }


    public static boolean row(int[][] arr, int row, int column) {
        int count = 0;
        for (int i = 0; i < 9; i++) {
            if (arr[row][column] == arr[i][column]) {
                count++;
            }
            if (count > 1) {
                return false;
            }
        }
        return true;
    }

    // Check if number already exists in column
    public static boolean column(int[][] arr, int row, int column) {
        int count = 0;
        for (int i = 0; i < 9; i++) {
            if (arr[row][column] == arr[row][i]) {
                count++;
            }
            if (count > 1) {
                return false;
            }
        }
        return true;
    }

    // Check if number already exists in smallbox
    public static boolean smallbox(int[][] arr, int row, int col) {
        int count = 0;
        for (int i = ((row / 3) * 3); i <= (((row / 3) * 3) + 2); i++) {
            for (int j = ((col / 3) * 3); j <= (((col / 3) * 3) + 2); j++) {
                if (arr[row][col] == arr[i][j]) {
                    count++;
                }
                if (count > 1) {
                    return false;
                }
            }
        }
        return true;
    }

    // Check rows
    public static boolean rowcheck(int[][] arr) {
        for (int i = 1; i <= 9; i++) {
            for (int row = 0; row <= 8; row++) {
                int count = 0;
                for (int col = 0; col <= 8; col++) {
                    if (arr[row][col] == i) {
                        count++;
                    }
                }
                if (count != 1)
                    return false;
            }
        }
        return true;
    }

    // Check columns
    public static boolean columncheck(int[][] arr) {

        for (int i = 1; i <= 9; i++) {
            for (int col = 0; col <= 8; col++) {
                int count = 0;
                for (int row = 0; row <= 8; row++) {
                    if (arr[row][col] == i) {
                        count++;
                    }
                }
                if (count != 1)
                    return false;
            }
        }
        return true;
    }

    // Checks small box
    public static boolean smallboxcheck(int[][] arr) {
        for (int k = 1; k <= 9; k++) {
            for (int l = 0; l < 2; l++) {
                int count = 0;

                for (int i = (l * 3); i <= ((l * 3) + 2); i++) {
                    for (int j = (l * 3); j <= ((l * 3) + 2); j++) {
                        if (arr[i][j] == k) {
                            count++;
                        }
                    }
                }
                if (count != 1) {
                    return false;
                }
            }
        }
        return true;
    }

    // Calls all checking methods
    public static boolean solution(int[][] arr)
    {
        return (rowcheck(arr) && columncheck(arr) && smallboxcheck(arr));
    }

    // Display board method
    public static void printBoard(int[][] arr)
    {
        for (int i = 0; i < 9; i++)
        {
            if (i % 3 == 0 && i != 0)
            {
                System.out.println("--------------------");
            }
            for (int j = 0; j < 9; j++)
            {
                if (j % 3 == 0 && j != 0)
                {
                    System.out.print("|");
                }
                System.out.print(arr[i][j] + " ");
            }
            System.out.println();
        }
    }
}

//help for making methods taken from coding with john
