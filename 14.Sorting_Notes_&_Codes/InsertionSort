import java.util.Arrays;
public class InsertionSort{
    public static void main(String[] args)
    {   //adaptive:-steps get reduced if array is sorted,stable,used for partially sorted array and takes part in hybrid sorting algorithms
        //best case T.C = O(n - 1) as inner loop will run only once for every i as it will break for every i(which goes from 0 to n - 2 = n - 1 comparisons
        //worst case T.C = 0(n^2) -> first(1 comparison) + 2 + 3 + ... + (n - 1) comparisons = n^2 comparisons
        //in this algo we will sort array in parts i.e. in left halfs
        int[] arr = {1, 9, 7, 5, 0};
        int n = arr.length;
        //outer loop is used to count no. of passes
        for(int i = 0; i < n - 1; i++){
            //inner loop is used to iterate over left halfs (each half will range from 0 to i + 1),to avoid IOBE for j = 0 we avoided j .= 0 and took only j > 0 as termination condition in inner for loop
            for(int j = i + 1; j > 0; j--){
                if(arr[j] < arr[j - 1]){
                    //swap
                    int temp = arr[j];
                    arr[j] = arr[j - 1];
                    arr[j - 1 ] = temp;
                }
                else{
                    break;//as if arr[j] > arr[j - 1] then left half  is already sorted hence why to check more on the left
                }
            }
        }

        System.out.println(Arrays.toString(arr));
    }
}

o/p:- [0, 1, 5, 7, 9]
