# Merge Sort
*Written by Anshul Verma(19/78065)*
<br />

***Objective*** - Implement Merge Sort(The program should report the number of comparisons). 
<br />
Test run the algorithm on 100 different inputs of sizes varying
from 30 to 1000. Count the number of comparisons and draw the graph. Compare it with a graph
of nlogn.
<br />

***Code*** -
<br />
*This is only the Merge and Merge Sort function.* ***For full code, [please click here](https://github.com/itsanshulverma/algo-lab/blob/main/1_InsertionNMergeSort/b_MergeSort/main.cpp).***
```cpp
...
// Comarison counter
int comps;

// Merge function to merge two subarrays into arr
void merge(int arr[], int left, int mid, int right) {
 
  // Create L <- arr[left:mid] and M <- arr[mid+1:right]
  int n1 = mid - left + 1;
  int n2 = right - mid;

  int L[n1], M[n2];

  for (int i = 0; i < n1; i++)
      L[i] = arr[left + i];
  for (int j = 0; j < n2; j++)
      M[j] = arr[mid + 1 + j];

  // Current indices of subarrays and arr
  int i = 0, j = 0, k = left;

  /**
    Iterate over elements of L and M and pick larger element from L and M
    until we reach end of either array, add the elements to correct position in arr
  **/
  while (i < n1 && j < n2) {
      if (L[i] <= M[j]) {
          arr[k] = L[i];
          i++;
      } else {
          arr[k] = M[j];
          j++;
      }
      comps++;
      k++;
  }

  // Put remaining elements in arr
  while (i < n1) {
      arr[k] = L[i];
      i++;
      k++;
  }
  while (j < n2) {
      arr[k] = M[j];
      j++;
      k++;
  }
}

// Merge Sort function
void mergeSort(int arr[], int left, int right) {
  if (left < right) {
    // Finding mid of array
    int mid = left + (right - left) / 2;

    mergeSort(arr, left, mid);
    mergeSort(arr, mid + 1, right);

    // Merge the sorted subarrays
    merge(arr, left, mid, right);
  }
}
...
```

***Sample Output*** -
```

------------------------------------
Array 1:
No. of elements: 260
No. of comparisons: 1759

------------------------------------
Array 2:
No. of elements: 806
No. of comparisons: 6781

------------------------------------
Array 3:
No. of elements: 323
No. of comparisons: 2314

------------------------------------
...
...
...

------------------------------------
Array 97:
No. of elements: 83
No. of comparisons: 432

------------------------------------
Array 98:
No. of elements: 128
No. of comparisons: 745

------------------------------------
Array 99:
No. of elements: 993
No. of comparisons: 8680

------------------------------------
Array 100:
No. of elements: 465
No. of comparisons: 3542

```

***Plots*** -

- **Plot of Merge Sort**

<img alt="Plot of Merge Sort (Size vs #Comparisons)" src="https://github.com/itsanshulverma/algo-lab/blob/main/1_InsertionNMergeSort/b_MergeSort/plot.png" width="720px" />

- **Plot of Merge Sort compared with plot of nlogn**

<img alt="Plot of Merge Sort and nlogn" src="https://github.com/itsanshulverma/algo-lab/blob/main/1_InsertionNMergeSort/b_MergeSort/plot_compare_nlogn.png" width="720px" />