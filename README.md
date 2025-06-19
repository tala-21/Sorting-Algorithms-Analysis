import java.util.*;

public class SortingComparison {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("اختر طريقة إدخال المصفوفة:");
        System.out.println("1. توليد عشوائي");
        System.out.println("2. إدخال يدوي");
        System.out.print("الخيار: ");
        int choice = scanner.nextInt();

        System.out.print("أدخل حجم المصفوفة: ");
        int size = scanner.nextInt();

        int[] original = new int[size];
        Random rand = new Random();

        if (choice == 1) {
            for (int i = 0; i < size; i++) {
                original[i] = rand.nextInt(100000); // عناصر عشوائية
            }
        } else {
            System.out.println("أدخل عناصر المصفوفة:");
            for (int i = 0; i < size; i++) {
                System.out.print("عنصر " + (i + 1) + ": ");
                original[i] = scanner.nextInt();
            }
        }

        int[] arr1 = Arrays.copyOf(original, size);
        int[] arr2 = Arrays.copyOf(original, size);
        int[] arr3 = Arrays.copyOf(original, size);

        System.out.println("\nالمصفوفة الأصلية:");
        System.out.println(Arrays.toString(original));

        // Bubble Sort
        long start = System.nanoTime();
        bubbleSort(arr1);
        long end = System.nanoTime();
        System.out.println("\nBubble Sort:");
        System.out.println(Arrays.toString(arr1));
        System.out.printf("الزمن: %.6f ثانية\n", (end - start) / 1e9);

        // Merge Sort
        start = System.nanoTime();
        mergeSort(arr2);
        end = System.nanoTime();
        System.out.println("\nMerge Sort:");
        System.out.println(Arrays.toString(arr2));
        System.out.printf("الزمن: %.6f ثانية\n", (end - start) / 1e9);

        // Quick Sort
        start = System.nanoTime();
        quickSort(arr3, 0, size - 1);
        end = System.nanoTime();
        System.out.println("\nQuick Sort:");
        System.out.println(Arrays.toString(arr3));
        System.out.printf("الزمن: %.6f ثانية\n", (end - start) / 1e9);
    }

    public static void bubbleSort(int[] arr) {
        for (int i = 0; i < arr.length - 1; i++) {
            for (int j = 0; j < arr.length - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }

    public static void mergeSort(int[] arr) {
        if (arr.length < 2) return;
        int mid = arr.length / 2;
        int[] left = Arrays.copyOfRange(arr, 0, mid);
        int[] right = Arrays.copyOfRange(arr, mid, arr.length);
        mergeSort(left);
        mergeSort(right);
        merge(arr, left, right);
    }

    public static void merge(int[] arr, int[] left, int[] right) {
        int i = 0, j = 0, k = 0;
        while (i < left.length && j < right.length) {
            if (left[i] <= right[j]) arr[k++] = left[i++];
            else arr[k++] = right[j++];
        }
        while (i < left.length) arr[k++] = left[i++];
        while (j < right.length) arr[k++] = right[j++];
    }

    public static void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            int pi = partition(arr, low, high);
            quickSort(arr, low, pi - 1);
            quickSort(arr, pi + 1, high);
        }
    }

    public static int partition(int[] arr, int low, int high) {
        int pivot = arr[high];
        int i = low - 1;
        for (int j = low; j < high; j++) {
            if (arr[j] < pivot) {
                i++;
                int temp = arr[i]; arr[i] = arr[j]; arr[j] = temp;
            }
        }
        int temp = arr[i + 1]; arr[i + 1] = arr[high]; arr[high] = temp;
        return i + 1;
    }
}
