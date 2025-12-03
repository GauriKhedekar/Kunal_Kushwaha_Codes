import java.util.Arrays;
public class SelectionSort{
    public static void main(String[] args)
    {   //Best and Worst Case T.C = O(n^2),unstable,performs well on small arrays/lists
        int[] arr = {1, 9, 7, 5, 0};
        int n = arr.length;
        //outer for loop to count number of passes = n - 1(required in SelectionSort(i.e.0 n - 2)
        for(int i = 0; i < n - 1; i++){
            int j;
            int maxEleIndex = 0;
            int max = arr[0];//hence start j from 1 as we are taking arr[0] here as max everytime
            //inner for loop to find max in only unsorted part of an array,can find min ele and put it at its correct index in selection sort
            for(j = 1; j < n - i; j++){
                if(max < arr[j]){
                    max = arr[j];
                    maxEleIndex = j;
                }

            }
            //swap current largest element with element present at its correct last position
            //j - 1 due to j++ at the end of the loop
            int currentMaxEleCorrectIndex = j - 1;
            int temp = arr[maxEleIndex];
            arr[maxEleIndex] = arr[currentMaxEleCorrectIndex];
            arr[currentMaxEleCorrectIndex] = temp;
        }
        System.out.println(Arrays.toString(arr));
    }
}

o/p:-[0, 1, 5, 7, 9]
