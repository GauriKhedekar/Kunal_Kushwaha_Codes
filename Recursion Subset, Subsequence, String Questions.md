# 1) Return a String with all 'a's removed
---
## Approach 1: Modify `ans` string in arguments (No return)
- Pass an extra `ans` string
- Do not return anything
- Print result at base case

```java
public class Main {
    public static void main(String[] args) {
        String str = "bccedafg";
        removea(str,""); // removea(mainString, answerString)
    }

    // Recursive function to remove 'a'
    public static void removea(String str, String ans){
        if(str.isEmpty()){
            System.out.println(ans);
            return;
        }
        char ch = str.charAt(0);
        if(ch == 'a'){
            removea(str.substring(1), ans); // skip 'a'
        } else {
            removea(str.substring(1), ans + ch); // add non-'a'
        }
    }
}
---
## Approach 2: Return answer string to main
- No extra argument needed
- Build answer while returning

```java
public class Main {
    public static void main(String[] args) {
        String str = "bccedafg";
        System.out.println(removea(str)); // call recursive function
    }

    // Recursive function to remove 'a'
    public static String removea(String str){
        if(str.isEmpty()){
            return ""; // base case
        }
        char ch = str.charAt(0);
        if(ch == 'a'){
            return removea(str.substring(1)); // skip 'a'
        } else {
            return ch + removea(str.substring(1)); // add non-'a'
        }
    }
}


![Recursion Tree of Subsets](images/recursion_tree_of_subsets_question.png)


