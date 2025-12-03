import java.util.Arrays;
public class CyclicSort{
    public static void main(String[] args)
    {   //T.C=O(n),used when array having ele in range from 1 to n is given or 0 to n - 1(for 0 to n - 1->change algo accordingly by replacing this part ->int correctIndexOfCurrentEle = arr[i] - 1; to int correctIndexOfCurrentEle = arr[i];
        //stable if elements are unique otherwise don't know
        //algo:-start from index 0->check whether ele is at its correct index->if yes move ahead_>i.e. do i++->else swap current ele with ele present at correct index of current ele...end at i = n
        int[] arr = {3, 4, 1, 2, 5};
        int n = arr.length;
        int i = 0;
        while(i < n){
            //index = correctValueAtThatIndex - 1
            int correctIndexOfCurrentEle = arr[i] - 1;
            //if current ele is not equal ele at its correct index swap it with ele present at its correct index
            if(arr[i] != arr[correctIndexOfCurrentEle]){
                int temp = arr[i];//current ele is stored
                arr[i] = arr[correctIndexOfCurrentEle];//current ele placed at its correct index as arr[currentIndexOfCurrEle]=arr[corrIndexOfCurrentEle = valueOfCurrentEle - 1]
                arr[correctIndexOfCurrentEle] = temp;//ele at correct index is swapped with current ele
            }
            else{//move ahead and do the above check for all next elements one by one
                i++;
            }
        }
        System.out.println(Arrays.toString(arr));
    }
}

o/p:-[1, 2, 3, 4, 5]
