# 1)Q1 : N-Queens Problem
![r](images/N_queens_1.jpg)
![y](images/N_queens_2.jpg)
```java
import java.util.Arrays;
public class Main {
    public static void main(String[] args) {
        boolean[][] board = new boolean[4][4];
        System.out.println(queens(board, 0));
    }

    public static int queens(boolean[][] board, int row){
        if(row == board.length){
            display(board);
            System.out.println();
            return 1;//to count number of possible ways to place N queens
            }
        int count = 0;
        //Placing queen and checking for every row and column
        for(int col = 0; col < board[0].length; col++){
            //place queen if it is safe
            if(isSafe(board, row, col)){
                board[row][col] = true;
                count += queens(board, row + 1);
                board[row][col] = false;//backtrack
            }
        }
        return count;
        }
        public static boolean isSafe(boolean[][] board, int row, int col){
        //check vertical col
            for(int i = 0; i < row; i++){
                if(board[i][col]){
                    return false;
                }
            }
        //check diagonal left
        for(int i = 1; i <= Math.min(row, col); i++){
            if(board[row - i][col - i]){
                return false;
            }
        }
        //check diagonal right
        for(int i = 0; i <= Math.min(row, board.length - col - 1); i++){
            if(board[row - i][col + i]){
                return false;
            }
        }
        return true;
        }
        public static void display(boolean[][] board){
        for(boolean[] arr: board){
            for(boolean element: arr){
                if(element){
                    System.out.print("Q ");
                }
                else{
                    System.out.print("X ");
                }
            }
            System.out.println();
        }
    }
}
o/p:-
X Q X X 
X X X Q 
Q X X X 
X X Q X 

X X Q X 
Q X X X 
X X X Q 
X Q X X 

2
```
---
