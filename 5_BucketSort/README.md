# Bucket Sort
*Written by Anshul Verma(19/78065)*
<br />

***Objective*** - Implement Bucket Sort Algorithm. 

***Code*** -
<br />
***For full code, [please click here](https://github.com/itsanshulverma/algo-lab/blob/main/5_BucketSort/main.cpp).***

```cpp
...
// Declaration of required functions
template <typename T> void insertionSort(T[], int);
void print(float[], int, string);

// Bucket stuct
struct bucket 
{
  int ptr;
  float* value;
};

// Bucket Sort Function
void bucketSort(float ar[], int n)
{
	// 1) let B[0..n-1] be a new array of buckets
	struct bucket B[n];

	// 2) Create n empty buckets of size n
	for (int i=0; i < n; i++)
	{
		B[i].ptr = -1;
		B[i].value = new float[n];
	}

	// 3) Put ar elements in suitable buckets
	for (int i=0; i<n; i++) 
	{
		int idx = n * ar[i];
		B[idx].value[++B[idx].ptr] = ar[i];
	}

	// 4) Sort and print each bucket using insertion sort
	for (int i=0; i<n; i++)
	{
		insertionSort<float>(B[i].value, B[i].ptr+1);
		cout << "  Bucket " << i;
		print(B[i].value, B[i].ptr+1, " = ");
	}

	// 5) Concatenate all buckets together to ar in order
	int idx = 0;
  for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < B[i].ptr+1; j++)
    	ar[idx++] = B[i].value[j];
		delete[] B[i].value; // and free the memory
	}
}
...
```
*Main Driver Function*
```cpp

int main(){
	// Initialize srand 
  srand(time(0));

	// Number of iterations
  int N = 10;

	for(int i = 0; i < N; i++)
  {
		// Taking a random size ranging from 5 to 20
		int size = rand()%15 + 5;
		float *arr = new float[size];
		
		// Initializing array with random values
		// between 0 and 1 with 2 digits after decimal
    for(int j = 0; j < size; j++)
    {
      arr[j] = (float) (rand()%100)/100;
    }
    cout << "Iteration " << i+1 << ":";
		cout << "\n------------------------------------\n";
		print(arr, size, "\nUnsorted Array = ");
		cout << "\nApplying Bucket Sort Algorithm:\n\n";
		bucketSort(arr, size);
		print(arr, size, "\nSorted Array = ");
		cout << endl;
	}

	return 0;
}
```

***Sample Output*** -
```
Iteration 1:
------------------------------------

Unsorted Array = [0.23, 0.3, 0.39, 0.74, 0.2, 0.54, 0.9, 0.09, 0.24, 0.21, 0.24, 0.94, 0.91, 0.11, 0.36, 0.03, 0.29, 0.52, 0.05]       

Applying Bucket Sort Algorithm:

  Bucket 0 = [0.03, 0.05]
  Bucket 1 = [0.09]
  Bucket 2 = [0.11]
  Bucket 3 = [0.2, 0.21]
  Bucket 4 = [0.23, 0.24, 0.24]
  Bucket 5 = [0.29, 0.3]
  Bucket 6 = [0.36]
  Bucket 7 = [0.39]
  Bucket 8 = []
  Bucket 9 = [0.52]
  Bucket 10 = [0.54]
  Bucket 11 = []
  Bucket 12 = []
  Bucket 13 = []
  Bucket 14 = [0.74]
  Bucket 15 = []
  Bucket 16 = []
  Bucket 17 = [0.9, 0.91, 0.94]
  Bucket 18 = []

Sorted Array = [0.03, 0.05, 0.09, 0.11, 0.2, 0.21, 0.23, 0.24, 0.24, 0.29, 0.3, 0.36, 0.39, 0.52, 0.54, 0.74, 0.9, 0.91, 0.94]

Iteration 2:
------------------------------------

Unsorted Array = [0.26, 0.66, 0.99, 0.28, 0.49, 0.25, 0.61, 0.61, 0.06, 0.39, 0.6, 0.51, 0.88, 0.26, 0.42, 0.36]

Applying Bucket Sort Algorithm:

  Bucket 0 = [0.06]
  Bucket 1 = []
  Bucket 2 = []
  Bucket 3 = []
  Bucket 4 = [0.25, 0.26, 0.26, 0.28]
  Bucket 5 = [0.36]
  Bucket 6 = [0.39, 0.42]
  Bucket 7 = [0.49]
  Bucket 8 = [0.51]
  Bucket 9 = [0.6, 0.61, 0.61]
  Bucket 10 = [0.66]
  Bucket 11 = []
  Bucket 12 = []
  Bucket 13 = []
  Bucket 14 = [0.88]
  Bucket 15 = [0.99]

Sorted Array = [0.06, 0.25, 0.26, 0.26, 0.28, 0.36, 0.39, 0.42, 0.49, 0.51, 0.6, 0.61, 0.61, 0.66, 0.88, 0.99]

Iteration 3:
------------------------------------

Unsorted Array = [0.22, 0.96, 0.9, 0.62, 0.67, 0.17, 0.69, 0.08, 0.26, 0.64, 0.44, 0.77, 0.95, 0.23, 0.41, 0.71]

Applying Bucket Sort Algorithm:

  Bucket 0 = []
  Bucket 1 = [0.08]
  Bucket 2 = [0.17]
  Bucket 3 = [0.22, 0.23]
  Bucket 4 = [0.26]
  Bucket 5 = []
  Bucket 6 = [0.41]
  Bucket 7 = [0.44]
  Bucket 8 = []
  Bucket 9 = [0.62]
  Bucket 10 = [0.64, 0.67]
  Bucket 11 = [0.69, 0.71]
  Bucket 12 = [0.77]
  Bucket 13 = []
  Bucket 14 = [0.9]
  Bucket 15 = [0.95, 0.96]

Sorted Array = [0.08, 0.17, 0.22, 0.23, 0.26, 0.41, 0.44, 0.62, 0.64, 0.67, 0.69, 0.71, 0.77, 0.9, 0.95, 0.96]

Iteration 4:
------------------------------------

Unsorted Array = [0.89, 0.11, 0.66, 0.19, 0.97, 0.76, 0.95, 0.37, 0.76, 0.43]

Applying Bucket Sort Algorithm:

  Bucket 0 = []
  Bucket 1 = [0.11, 0.19]
  Bucket 2 = []
  Bucket 3 = [0.37]
  Bucket 4 = [0.43]
  Bucket 5 = []
  Bucket 6 = [0.66]
  Bucket 7 = [0.76, 0.76]
  Bucket 8 = [0.89]
  Bucket 9 = [0.95, 0.97]

Sorted Array = [0.11, 0.19, 0.37, 0.43, 0.66, 0.76, 0.76, 0.89, 0.95, 0.97]

Iteration 5:
------------------------------------

Unsorted Array = [0.09, 0.21, 0.39, 0.04, 0.87, 0.19, 0.21, 0.24, 0.23, 0.15, 0.7, 0.34, 0.93, 0.71, 0.73]

Applying Bucket Sort Algorithm:

  Bucket 0 = [0.04]
  Bucket 1 = [0.09]
  Bucket 2 = [0.15, 0.19]
  Bucket 3 = [0.21, 0.21, 0.23, 0.24]
  Bucket 4 = []
  Bucket 5 = [0.34, 0.39]
  Bucket 6 = []
  Bucket 7 = []
  Bucket 8 = []
  Bucket 9 = []
  Bucket 10 = [0.7, 0.71, 0.73]
  Bucket 11 = []
  Bucket 12 = []
  Bucket 13 = [0.87, 0.93]
  Bucket 14 = []

Sorted Array = [0.04, 0.09, 0.15, 0.19, 0.21, 0.21, 0.23, 0.24, 0.34, 0.39, 0.7, 0.71, 0.73, 0.87, 0.93]

Iteration 6:
------------------------------------

Unsorted Array = [0.26, 0.01, 0.36, 0.34, 0.7, 0.84, 0.4]

Applying Bucket Sort Algorithm:

  Bucket 0 = [0.01]
  Bucket 1 = [0.26]
  Bucket 2 = [0.34, 0.36, 0.4]
  Bucket 3 = []
  Bucket 4 = [0.7]
  Bucket 5 = [0.84]
  Bucket 6 = []

Sorted Array = [0.01, 0.26, 0.34, 0.36, 0.4, 0.7, 0.84]

Iteration 7:
------------------------------------

Unsorted Array = [0.75, 0.59, 0.86, 0.96, 0.06]

Applying Bucket Sort Algorithm:

  Bucket 0 = [0.06]
  Bucket 1 = []
  Bucket 2 = [0.59]
  Bucket 3 = [0.75]
  Bucket 4 = [0.86, 0.96]

Sorted Array = [0.06, 0.59, 0.75, 0.86, 0.96]

Iteration 8:
------------------------------------

Unsorted Array = [0.79, 0.76, 0.65, 0.48, 0.03]

Applying Bucket Sort Algorithm:

  Bucket 0 = [0.03]
  Bucket 1 = []
  Bucket 2 = [0.48]
  Bucket 3 = [0.65, 0.76, 0.79]
  Bucket 4 = []

Sorted Array = [0.03, 0.48, 0.65, 0.76, 0.79]

Iteration 9:
------------------------------------

Unsorted Array = [0.33, 0.03, 0.26, 0.33, 0.05, 0.87, 0.46, 0.13, 0.38, 0, 0.25, 0.03]

Applying Bucket Sort Algorithm:

  Bucket 0 = [0, 0.03, 0.03, 0.05]
  Bucket 1 = [0.13]
  Bucket 2 = []
  Bucket 3 = [0.25, 0.26, 0.33, 0.33]
  Bucket 4 = [0.38]
  Bucket 5 = [0.46]
  Bucket 6 = []
  Bucket 7 = []
  Bucket 8 = []
  Bucket 9 = []
  Bucket 10 = [0.87]
  Bucket 11 = []

Sorted Array = [0, 0.03, 0.03, 0.05, 0.13, 0.25, 0.26, 0.33, 0.33, 0.38, 0.46, 0.87]

Iteration 10:
------------------------------------

Unsorted Array = [0.67, 0.27, 0.56, 0.98, 0.79, 0.82, 0.65, 0.53, 0.23, 0.1, 0.41, 0.38, 0.97]

Applying Bucket Sort Algorithm:

  Bucket 0 = []
  Bucket 1 = [0.1]
  Bucket 2 = [0.23]
  Bucket 3 = [0.27]
  Bucket 4 = [0.38]
  Bucket 5 = [0.41]
  Bucket 6 = [0.53]
  Bucket 7 = [0.56]
  Bucket 8 = [0.65, 0.67]
  Bucket 9 = []
  Bucket 10 = [0.79, 0.82]
  Bucket 11 = []
  Bucket 12 = [0.97, 0.98]

Sorted Array = [0.1, 0.23, 0.27, 0.38, 0.41, 0.53, 0.56, 0.65, 0.67, 0.79, 0.82, 0.97, 0.98]

```