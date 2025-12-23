# 1)17. Letter Combinations of a Phone Number
## Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order. A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.
## Input: digits = "23" , Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
![r](images/Letter_Combinations_of_a_Phone_Number.jpg)
```java
import java.util.ArrayList;
public class Main {
    public static void main(String[] args) {
        String str = "23";
        System.out.println(possiblePermutations("", str));
    }

    public static ArrayList<String> possiblePermutations(String processed, String unprocessed){
        if(unprocessed.isEmpty()){
            ArrayList<String> list = new ArrayList<>();
            list.add(processed);
            return list;
        }
        int digit = unprocessed.charAt(0) - '0';/*to extract first character from gien string,e.g.String str = "23", digit = '2' - '0' = 2*/
        ArrayList<String> ans = new ArrayList<>();
        if(digit == 7){
            for(int i = (digit - 2) * 3; i <= (digit - 1) * 3; i++){
                char ch = (char)('a' + i);//to get all possible character from that digit
                ans.addAll(possiblePermutations(processed + ch, unprocessed.substring(1)));
            }
        }
        else if(digit == 8){
            for(int i = 19; i <= 21; i++){
                char ch = (char)('a' + i);//to get all possible character from that digit
                ans.addAll(possiblePermutations(processed + ch, unprocessed.substring(1)));
            }
        }
        else if(digit == 9){
            for(int i = 22; i <= 25; i++){
                char ch = (char)('a' + i);//to get all possible character from that digit
                ans.addAll(possiblePermutations(processed + ch, unprocessed.substring(1)));
            }
        }
        else{
            for(int i = (digit - 2) * 3; i < (digit - 1) * 3; i++){
                char ch = (char)('a' + i);//to get all possible character from that digit
                ans.addAll(possiblePermutations(processed + ch, unprocessed.substring(1)));
            }
        }
        return ans;
    }
}
o/p:-
[ad, ae, af, bd, be, bf, cd, ce, cf]
```


