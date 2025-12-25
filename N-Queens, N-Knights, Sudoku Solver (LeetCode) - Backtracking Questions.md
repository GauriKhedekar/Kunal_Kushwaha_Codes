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
# Time and Space complexity
# ⬛ N-Queens Problem — Time & Space Complexity Analysis

This document analyzes the **time and space complexity** of a **backtracking-based N-Queens solution in Java**.

---

## 🔁 Recurrence Relation

Let **N** be the number of queens (size of the board).

$$
T(N) = N \cdot T(N-1) + O(N^2)
$$

---

## 📌 Meaning of Each Term

### **T(N)**
Time required to place queens in **N remaining rows**.

---

### **N · T(N−1)**

- At a given row, the algorithm tries **all N columns**
- For each safe placement, it recursively solves the remaining **N−1 rows**
- Hence, in the worst case, **N recursive calls** are made

---

### **O(N²)** — Non-Recursive Work

### **O(N)** — Safety Check Cost

For each queen placement, `isSafe()` performs:

| Check | Time |
|----|----|
| Vertical column | O(N) |
| Left diagonal | O(N) |
| Right diagonal | O(N) |

Total safety check per placement:

\[
O(N)
\]

- i.e each queen requires N checks for isSafe(),(total queens to be placed) N * Total checks N reuired for each queen placement(as given above - total checks per placement)
  
Total work per level:

$$
O(N \times N) = O(N^2)
$$

---

## 🔄 Manual Unrolling (Step-by-Step)

Starting recurrence:

$$
T(N) = N \cdot T(N-1) + O(N^2)
$$

---

### 🔹 Step 1: Expand `T(N−1)`

At row **N−1**, the algorithm tries **(N−1) columns**:

$$
T(N-1) = (N-1) \cdot T(N-2) + O(N^2)
$$

---

### 🔹 Step 2: Substitute into `T(N)`

$$
T(N) = N \cdot (N-1) \cdot T(N-2) + O(N^3)
$$

---

### 🔹 Step 3: Expand Further

$$
T(N-2) = (N-2) \cdot T(N-3) + O(N^2)
$$

$$
T(N) = N \cdot (N-1) \cdot (N-2) \cdot T(N-3) + O(N^4)
$$

---

### 🔹 Step 4: Continue Until Base Case

$$
T(N) = N \cdot (N-1) \cdot (N-2) \cdots 1 \cdot T(0)
$$

$$
T(N) = N!
$$

Polynomial terms are dominated by factorial growth.

---

## 📐 Akra–Bazzi Interpretation

Although the recurrence is **not divide-and-conquer**, it exhibits:

- Linearly increasing branching factor
- Recursion depth of **N**
- Multiplicative expansion across recursion levels

This results in **factorial time complexity**:

$$
T(N) = O(N!)
$$

---

## ⏱ Time Complexity

| Case | Complexity |
|------|-----------|
| Worst Case | O(N!) |
| Average Case | O(N!) |
| Best Case | O(N!) |

(Backtracking explores permutations of queen placements)

---

## 🧠 Space Complexity

### 1️⃣ Board Storage

```java
boolean[][] board = new boolean[N][N];
```
---
# 2)N-Knights problem:-​
