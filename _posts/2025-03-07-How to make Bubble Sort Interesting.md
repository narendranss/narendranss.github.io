---
layout: post
section-type: post
title: How to make Bubble Sort Interesting?
category: tech, algorithms
tags: [ 'Algorithms', 'Bubble Sort']
---

# How to make bubble sort interesting?

Bubble sort is a simple sorting algorithm that works by repeatedly swapping adjacent elements if they are in the wrong order.

If we stop learning with how bubble sort works and learning only the time and space complexity, we can never improve up on it. 
Asking **"how to improve bubble sort is an interesting question and an interesting challenge?"** to embark on an interesting journey.

Many of us don't ask, as we have many performing sort algorithms, which are useful in various applications. 
This exercise to ask simple questions and embarking on scientific investigation journey improves our acumen as well as our understanding.

Let us get started.

## How to improve bubble sort?

Is it possible to improve bubble sort? In best case, `Bubble sort` time complexity is O(n^2). 
Despite bubble sort is not most efficient sorting algorithm, It is interesting to find ways to improve its performance.

In `bubble sort` we traverse an array from left to right comparing 2 elements at a time and swap them when they are not
in order.

Here is an example program in java.
### General Bubble Sort
```java
public class BubbleSort {

    /**
     * Sorts an array of integers using the bubble sort algorithm.
     *
     * @param arr The array to be sorted.
     */
    public static void bubbleSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    // Swap elements
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }

    /**
     * Prints the contents of an array.
     *
     * @param arr The array to be printed.
     */
    public static void printArray(int[] arr) {
        for (int i : arr) {
            System.out.print(i + " ");
        }
    }

    public static void main(String[] args) {
        int[] arr = {64, 34, 25, 12, 22, 11, 90};
        System.out.println("Original array:");
        printArray(arr);
        bubbleSort(arr);
        System.out.println("Sorted array:");
        printArray(arr);
    }
}
```
We do N-1 comparison for N elements, at the end of first iteration, the largest element is at the end of the array.
We do N-2 comparison for N-1 elements, at the end of second iteration, the 2nd largest element is at the end of the array.
Totally we perform (N-1) + (N-2) + (N-3) + (N-4) + ... + 1 comparison. Sum of N numbers is N*(N+1)/2. 
Here it is (N-1)*(N)/2. Which makes the time complexity O(n^2).

---

By any change can we reduce the number of comparisons?

Fortunately, yes. when no swapping happens in an iteration, the array has converged to become a sorted array`. 

## How to reduce no. of comparison in bubble sort?

A simple flag to check `no` swap happened in an iteration can act as a stop signal, 
thus reducing the no. of comparisons.

Here is an example program in java.
### Optimized Bubble Sort - Early Termination with No Swap Flag
```java
public class ImprovedBubbleSort {

    /**
     * Sorts an array of integers using the improved bubble sort algorithm.
     *
     * @param arr The array to be sorted.
     */
    public static void improvedBubbleSort(int[] arr) {
        int n = arr.length;
        boolean swapped;

        do {
            swapped = false;
            for (int i = 0; i < n - 1; i++) {
                if (arr[i] > arr[i + 1]) {
                    // Swap elements
                    int temp = arr[i];
                    arr[i] = arr[i + 1];
                    arr[i + 1] = temp;
                    swapped = true;
                }
            }
        } while (swapped);
    }

    /**
     * Prints the contents of an array.
     *
     * @param arr The array to be printed.
     */
    public static void printArray(int[] arr) {
        for (int i : arr) {
            System.out.print(i + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        int[] arr = {64, 34, 25, 12, 22, 11, 90};
        System.out.println("Original array:");
        printArray(arr);
        improvedBubbleSort(arr);
        System.out.println("Sorted array:");
        printArray(arr);
    }
}
```
The time complexity and space complexity is same as the original bubble sort. While still the improved sort can be performing.

| Algorithm                                | Time Complexity                                           | Space Complexity |
|------------------------------------------|-----------------------------------------------------------|------------------| 
| Traditional Bubble Sort                  | Best-case: O(n), Average-case: O(n^2), Worst-case: O(n^2) | O(1)             | 
| Improved Bubble Sort (Early Termination) | Best-case: O(n), Average-case: O(n^2), Worst-case: O(n^2) | O(1)             | 

## Is it possible to Improve further?
Is it is a pure luck to find the fact that no swapping means the array is sorted?
We can rely on scientific means based on data distribution or based on data convergence or precipitation. 
Any given array can be already sorted array or partially sorted array or completely unsorted array.
We did not analyze and take advantage of the entropy and data distribution, but there are cases where algorithms performs
worst for a given data distribution.

Let us analyze where and how bubble sort performs,

1. Bubble sort perform better in `small data set`.
2. Bubble sort can perform better on `nearly sorted` or `partially sorted` array.
3. Bubble sort does not work well in `large data set` due to it time complexity O(n^2).
4. Bubble sort does not perform better when the data is `completely not sorted` or `randomly sorted` array.
5. Bubble sort's worst nightmare is `reverse sorted data`, as it does max number of swaps in this case. Data convergence takes place by moving large elements to last.
6. Bubble sort is `unstable sort` as it can swap elements that are not supposed to be swapped when the elements are duplicates or equal (ideally stable when swap is allowed when elements are equal).

Given these facts and understanding how data convergence takes place, 
we can improve the performance of bubble sort further in best cases such as `smaller data set` or `nearly sorted` or `partially sorted` array.
Let us leave other worst distribution to other sorting algorithms.

In reality data convergence is taking on one side of the array, pushing a large numbers to the right.
can we converge the data on both sides? can we improve the performance of bubble sort by `bi-directional` convergence?
This improvement on bubble sort is also called as "rinsing sort", "cocktail sort" or "shaker sort".

Here is an example program in java.
### Optimized Bidirectional Bubble Sort - Early Termination with No Swap Flag and reduced iteration with faster convergence
```java
public class CocktailShakerSort {
    
    // Function to perform Cocktail Shaker Sort
    public static void cocktailShakerSort(int[] arr) {
        boolean swapped = true;
        int start = 0;
        int end = arr.length - 1;

        while (swapped) {
            swapped = false;
            
            // Traverse from left to right, similar to bubble sort
            for (int i = start; i < end; i++) {
                if (arr[i] > arr[i + 1]) {
                    // Swap if the element is greater than the next element
                    int temp = arr[i];
                    arr[i] = arr[i + 1];
                    arr[i + 1] = temp;
                    swapped = true;
                }
            }
            
            // If no elements were swapped, the array is sorted
            if (!swapped) break;
            
            // Decrease the end index since the largest element is now at the end
            end--;
            
            // Traverse from right to left
            for (int i = end - 1; i >= start; i--) {
                if (arr[i] > arr[i + 1]) {
                    // Swap if the element is greater than the next element
                    int temp = arr[i];
                    arr[i] = arr[i + 1];
                    arr[i + 1] = temp;
                    swapped = true;
                }
            }
            
            // Increase the start index since the smallest element is now at the start
            start++;
        }
    }
    
    // Utility function to print an array
    public static void printArray(int[] arr) {
        for (int i : arr) {
            System.out.print(i + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        int[] arr = {5, 3, 8, 4, 2, 7, 1, 6};
        
        System.out.println("Original Array:");
        printArray(arr);
        
        cocktailShakerSort(arr);
        
        System.out.println("Sorted Array:");
        printArray(arr);
    }
}
```
We get the following advantages by using cocktail shaker sort.
1. Now the iterations have reduced by half and convergence to sorted array is faster.
2. We converge both smaller and larger number on either side.
3. Best suited for cases where smaller elements are on the left and larger elements are on the right yet unsorted.

## Is it possible to Improve further?
Have you ever wondered why only consequent elements are compared and swapped? why not compare elements with a gap?
What is the advantage of having a gap? My guess is bubble sort works better with partially sorted array, which means consequent elements are sorted, leaving a gap could converge faster.

Someone did come up with something called Comb sort.

## Untangling the tangled hair with comb. 
Imagine using a comb to untangle hair. we start by combing through larger sections of the hair (larger gaps) and gradually move to finer teeth (smaller gaps) as we get closer to the scalp.
Comb sort is an improvement on bubble sort with gap reduction from larger gap to smaller gap as we move closer to sorted array.

Hey, our hairs are mostly sorted at the roots, seems my guess was right.

Here is an example program in java.
```java
public class CombSort {

    // Function to perform Comb Sort
    public static void combSort(int[] arr) {
        int n = arr.length;
        int gap = n;
        boolean swapped = true;
        
        // Continue sorting until the gap is 1 and no swaps are made
        while (gap != 1 || swapped) {
            // Update the gap value for the next iteration
            gap = (int) (gap / 1.3);
            if (gap < 1) {
                gap = 1;
            }
            
            swapped = false;
            
            // Compare elements at current gap distance
            for (int i = 0; i < n - gap; i++) {
                if (arr[i] > arr[i + gap]) {
                    // Swap if elements are in the wrong order
                    int temp = arr[i];
                    arr[i] = arr[i + gap];
                    arr[i + gap] = temp;
                    swapped = true;
                }
            }
        }
    }

    // Utility function to print an array
    public static void printArray(int[] arr) {
        for (int i : arr) {
            System.out.print(i + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        int[] arr = {5, 3, 8, 4, 2, 7, 1, 6};
        
        System.out.println("Original Array:");
        printArray(arr);
        
        combSort(arr);
        
        System.out.println("Sorted Array:");
        printArray(arr);
    }
}
```
You may ask about the magic number 1.3, The gap reducing factor. 
It is an empirical number obtained by experimenting with many unsorted arrays to improve bubble sort performance.
If gap reducing factor is 1.5, gap reduces faster but could miss out to swap few distant elements.
If gap reducing factor is 1.2, gap reduces slower and algorithm will end up doing too many comparisons.
The gap reducing factor 1.3 is a sweet spot for the algorithm to balance between speed and accuracy.

We get the following advantages by using comb sort.
1. Partially sorted array gets sorted faster.
2. We converge distant elements first before closer elements. 
3. When elements are 'strandardly' distributed, comb sort performs faster reducing the standard deviations. i.e., it can perform better in roughly uniform data.

Now we have 3 improvements.
1. With no swap flag
2. Bidirectional convergence
3. Gap reducing factor 1.3

We can build a hybrid with all three.

Here is an example program in java.
```java
public class CombCocktailSort {

    // Function to perform Hybrid Comb-Cocktail Shaker Sort
    public static void hybridCombCocktailSort(int[] arr) {
        int n = arr.length;
        int gap = n;
        boolean swapped = true;
        
        // Continue sorting until the gap reduces to 1 and no swaps are made
        while (gap > 1 || swapped) {
            // Update the gap value for the next iteration (based on Comb Sort)
            gap = (int) (gap / 1.3);
            if (gap < 1) {
                gap = 1;  // Ensure gap is at least 1
            }

            swapped = false;

            // Perform bidirectional pass (like Cocktail Shaker Sort) for current gap
            // Left-to-right pass (using current gap)
            for (int i = 0; i < n - gap; i++) {
                if (arr[i] > arr[i + gap]) {
                    // Swap if elements are in the wrong order
                    int temp = arr[i];
                    arr[i] = arr[i + gap];
                    arr[i + gap] = temp;
                    swapped = true;
                }
            }

            // Right-to-left pass (using current gap)
            for (int i = n - gap - 1; i >= 0; i--) {
                if (arr[i] > arr[i + gap]) {
                    // Swap if elements are in the wrong order
                    int temp = arr[i];
                    arr[i] = arr[i + gap];
                    arr[i + gap] = temp;
                    swapped = true;
                }
            }
        }
    }

    // Utility function to print an array
    public static void printArray(int[] arr) {
        for (int i : arr) {
            System.out.print(i + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        int[] arr = {5, 3, 8, 4, 2, 7, 1, 6};
        
        System.out.println("Original Array:");
        printArray(arr);
        
        hybridCombCocktailSort(arr);
        
        System.out.println("Sorted Array:");
        printArray(arr);
    }
}
```
Does the hybrid has any advantage? Does it have more quick convergence than cocktail shaker sort and comb sort? I will leave that for you to experiment.

On a high level, it can perform convergence in both directions and converge distant element first and then closer elements.

# Summary
In this post, we make the boring bubble sort interesting by asking simple questions 
and conducting scientific investigation on how and where bubble sort work best and how to improve further.
These lil improvement are going to be of no use, but the investigation procedure will keep sharpening us.
When we find partially sorted data, smaller numbers mostly on left and larger numbers mostly on right, 
we can improve the performance of bubble sort by bidirectional convergence.
When we find many standards of sorted data grouped together, we can make use of comb sort to improve the performance of 
bubble sort.

| Algorithm                                | Short Description                                                                                              | Time Complexity                                           | Space Complexity | When to Use?                                                                              |
|------------------------------------------|----------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------|------------------|-------------------------------------------------------------------------------------------| 
| Traditional Bubble Sort                  | compare and swap                                                                                               | Best-case: O(n), Average-case: O(n^2), Worst-case: O(n^2) | O(1)             | nearly sorted small dataset                                                               |
| Improved Bubble Sort (Early Termination) | early Termination with "no swap" flag                                                                          | Best-case: O(n), Average-case: O(n^2), Worst-case: O(n^2) | O(1)             | nearly sorted sort dataset                                                                |
| Cocktail Shaker Sort                     | bidirectional convergence, on each iteration move large element to one side and smaller elements to other side | Best-case: O(n), Average-case: O(n^2), Worst-case: O(n^2) | O(1)             | nearly sorted small dataset with more smaller numbers on left and larger numbers on right |
| Comb Sort                                | sort with larger gap and then reduce the gap with gap reducing factor                                          | Best-case: O(n), Average-case: O(n^2), Worst-case: O(n^2) | O(1)             | nearly sorted small dataset with standards of sorted data grouped together                |                                                              

While there is no change in time complexity and space complexity, there can be a good difference in performance based on data distribution.

Happy Learning!