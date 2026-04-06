## Activity 9.1: Insertion sort
```Java
import java.util.Scanner;

public class InsertionSort {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter size of an integer array, followed by the elements of the array (no duplicates)");

        if (!scanner.hasNextInt()) return;
        int n = scanner.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }

        printArray(arr);
        System.out.println();

        insertionSort(arr);
    }

    public static void insertionSort(int[] arr) {
        int comparisons = 0;
        int swaps = 0;

        for (int i = 1; i < arr.length; i++) {
            int key = arr[i];
            int j = i - 1;

            while (j >= 0) {
                comparisons++;
                if (arr[j] > key) {
                    arr[j + 1] = arr[j];
                    swaps++;
                    j--;
                } else {
                    break; 
                }
            }
            arr[j + 1] = key;
            
            printArray(arr);
        }

        System.out.println("\ncomparisons: " + comparisons);
        System.out.println("swaps: " + swaps);
    }

    public static void printArray(int[] arr) {
        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + (i == arr.length - 1 ? "" : " "));
        }
        System.out.println();
    }
}

```
