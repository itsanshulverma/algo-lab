# Radix Sort
*Written by Anshul Verma(19/78065)*
<br />

***Objective*** - Implement Radix Sort Algorithm. 

***Code*** -
<br />
***For full code, [please click here](https://github.com/itsanshulverma/algo-lab/blob/main/4_RadixSort/main.cpp).***

```cpp
...
// Counting Sort function on ith digit
void countingSort(int arr[], int size, int k)
{
	// 1) Let C be an array for storing counts of size 10
	// and output as sorted array of size 'size'
  int output[size];
  int C[10];

	// 2) Initialising each element of C to 0
  for (int i = 0; i < 10; ++i)
    C[i] = 0;

  // 3) Calculate number of elements equal to i 
	// for each element in arr
  for (int i = 0; i < size; i++)
    C[(arr[i] / k) % 10]++;

  // 3) Calculate number of elements less than or
	// equal to i for each element in arr
  for (int i = 1; i < 10; i++)
    C[i] += C[i - 1];

  // 4) Placing the elements in sorted order
  for (int i = size - 1; i >= 0; i--) {
    output[C[(arr[i]/k) % 10] - 1] = arr[i];
    C[(arr[i]/k) % 10]--;
  }

	// 5) Placing sorted elements to 'arr' from 'output'
  for (int i = 0; i < size; i++)
    arr[i] = output[i];
}

// Radix Sort Function
void radixSort(int arr[], int size)
{
	// 1) Get maximum element to determine maximum digits
  int max = arr[0];
  for (int i = 1; i < size; i++)
    if (arr[i] > max)
      max = arr[i];

  // 2) Applying a stable sorting algorithm (counting sort)
	// on ith digit 
  for (int i=1; max/i > 0; i *= 10)
	{
    countingSort(arr, size, i);
		cout << "  Array sorted on the basis of " << i 
			<< (i == 1 ? "st" : "th") << " digit from left:\n";
		print(arr, size, "    ");
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
		int *arr = new int[size];
		
		// Initializing array with random values
		// between 0 and 999
    for(int j = 0; j < size; j++)
    {
      arr[j] = rand()%999;
    }
    cout << "Iteration " << i+1 << ":";
		cout << "\n------------------------------------\n";
		print(arr, size, "\nUnsorted Array = ");
		cout << "\nApplying Radix Sort Algorithm:\n";
		radixSort(arr, size);
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

Unsorted Array = [700, 552, 391, 485, 774, 195, 872, 590, 84, 767, 882, 280, 144, 119, 494, 476]

Applying Radix Sort Algorithm:
  Array sorted on the basis of 1st digit from left:
    [700, 590, 280, 391, 552, 872, 882, 774, 84, 144, 494, 485, 195, 476, 767, 119]
  Array sorted on the basis of 10th digit from left:
    [700, 119, 144, 552, 767, 872, 774, 476, 280, 882, 84, 485, 590, 391, 494, 195]
  Array sorted on the basis of 100th digit from left:
    [84, 119, 144, 195, 280, 391, 476, 485, 494, 552, 590, 700, 767, 774, 872, 882]

Sorted Array = [84, 119, 144, 195, 280, 391, 476, 485, 494, 552, 590, 700, 767, 774, 872, 882]

Iteration 2:
------------------------------------

Unsorted Array = [765, 562, 402, 764, 106, 573, 142, 195, 352, 762, 992, 184, 982, 239, 388, 949, 165, 228]

Applying Radix Sort Algorithm:
  Array sorted on the basis of 1st digit from left:
    [562, 402, 142, 352, 762, 992, 982, 573, 764, 184, 765, 195, 165, 106, 388, 228, 239, 949]
  Array sorted on the basis of 10th digit from left:
    [402, 106, 228, 239, 142, 949, 352, 562, 762, 764, 765, 165, 573, 982, 184, 388, 992, 195]
  Array sorted on the basis of 100th digit from left:
    [106, 142, 165, 184, 195, 228, 239, 352, 388, 402, 562, 573, 762, 764, 765, 949, 982, 992]

Sorted Array = [106, 142, 165, 184, 195, 228, 239, 352, 388, 402, 562, 573, 762, 764, 765, 949, 982, 992]

Iteration 3:
------------------------------------

Unsorted Array = [652, 554, 777, 243, 887, 698, 429, 132]

Applying Radix Sort Algorithm:
  Array sorted on the basis of 1st digit from left:
    [652, 132, 243, 554, 777, 887, 698, 429]
  Array sorted on the basis of 10th digit from left:
    [429, 132, 243, 652, 554, 777, 887, 698]
  Array sorted on the basis of 100th digit from left:
    [132, 243, 429, 554, 652, 698, 777, 887]

Sorted Array = [132, 243, 429, 554, 652, 698, 777, 887]

Iteration 4:
------------------------------------

Unsorted Array = [683, 400, 67, 553, 830, 182, 604, 34, 674, 903, 558, 588, 656, 559, 398, 50, 542, 441, 649]

Applying Radix Sort Algorithm:
  Array sorted on the basis of 1st digit from left:
    [400, 830, 50, 441, 182, 542, 683, 553, 903, 604, 34, 674, 656, 67, 558, 588, 398, 559, 649]
  Array sorted on the basis of 10th digit from left:
    [400, 903, 604, 830, 34, 441, 542, 649, 50, 553, 656, 558, 559, 67, 674, 182, 683, 588, 398]
  Array sorted on the basis of 100th digit from left:
    [34, 50, 67, 182, 398, 400, 441, 542, 553, 558, 559, 588, 604, 649, 656, 674, 683, 830, 903]

Sorted Array = [34, 50, 67, 182, 398, 400, 441, 542, 553, 558, 559, 588, 604, 649, 656, 674, 683, 830, 903]

Iteration 5:
------------------------------------

Unsorted Array = [209, 906, 909, 907, 798, 784, 514, 848, 95, 765, 268, 0]

Applying Radix Sort Algorithm:
  Array sorted on the basis of 1st digit from left:
    [0, 784, 514, 95, 765, 906, 907, 798, 848, 268, 209, 909]
  Array sorted on the basis of 10th digit from left:
    [0, 906, 907, 209, 909, 514, 848, 765, 268, 784, 95, 798]
  Array sorted on the basis of 100th digit from left:
    [0, 95, 209, 268, 514, 765, 784, 798, 848, 906, 907, 909]

Sorted Array = [0, 95, 209, 268, 514, 765, 784, 798, 848, 906, 907, 909]

Iteration 6:
------------------------------------

Unsorted Array = [92, 473, 349, 216, 477, 683, 172, 750, 770, 193, 846, 204, 904, 305, 360]

Applying Radix Sort Algorithm:
  Array sorted on the basis of 1st digit from left:
    [750, 770, 360, 92, 172, 473, 683, 193, 204, 904, 305, 216, 846, 477, 349]
  Array sorted on the basis of 10th digit from left:
    [204, 904, 305, 216, 846, 349, 750, 360, 770, 172, 473, 477, 683, 92, 193]
  Array sorted on the basis of 100th digit from left:
    [92, 172, 193, 204, 216, 305, 349, 360, 473, 477, 683, 750, 770, 846, 904]

Sorted Array = [92, 172, 193, 204, 216, 305, 349, 360, 473, 477, 683, 750, 770, 846, 904]

Iteration 7:
------------------------------------

Unsorted Array = [443, 589, 622, 141, 850, 368, 529, 951, 20]

Applying Radix Sort Algorithm:
  Array sorted on the basis of 1st digit from left:
    [850, 20, 141, 951, 622, 443, 368, 589, 529]
  Array sorted on the basis of 10th digit from left:
    [20, 622, 529, 141, 443, 850, 951, 368, 589]
  Array sorted on the basis of 100th digit from left:
    [20, 141, 368, 443, 529, 589, 622, 850, 951]

Sorted Array = [20, 141, 368, 443, 529, 589, 622, 850, 951]

Iteration 8:
------------------------------------

Unsorted Array = [488, 595, 968, 653, 320, 742, 452, 54]

Applying Radix Sort Algorithm:
  Array sorted on the basis of 1st digit from left:
    [320, 742, 452, 653, 54, 595, 488, 968]
  Array sorted on the basis of 10th digit from left:
    [320, 742, 452, 653, 54, 968, 488, 595]
  Array sorted on the basis of 100th digit from left:
    [54, 320, 452, 488, 595, 653, 742, 968]

Sorted Array = [54, 320, 452, 488, 595, 653, 742, 968]

Iteration 9:
------------------------------------

Unsorted Array = [142, 580, 236, 383, 720, 809, 735, 104, 598, 191, 142, 622, 239, 637, 629, 496, 947]

Applying Radix Sort Algorithm:
  Array sorted on the basis of 1st digit from left:
    [580, 720, 191, 142, 142, 622, 383, 104, 735, 236, 496, 637, 947, 598, 809, 239, 629]
  Array sorted on the basis of 10th digit from left:
    [104, 809, 720, 622, 629, 735, 236, 637, 239, 142, 142, 947, 580, 383, 191, 496, 598]
  Array sorted on the basis of 100th digit from left:
    [104, 142, 142, 191, 236, 239, 383, 496, 580, 598, 622, 629, 637, 720, 735, 809, 947]

Sorted Array = [104, 142, 142, 191, 236, 239, 383, 496, 580, 598, 622, 629, 637, 720, 735, 809, 947]

Iteration 10:
------------------------------------

Unsorted Array = [696, 936, 967, 828, 552, 350, 766, 941, 981, 658, 973, 984, 889, 737, 356]

Applying Radix Sort Algorithm:
  Array sorted on the basis of 1st digit from left:
    [350, 941, 981, 552, 973, 984, 696, 936, 766, 356, 967, 737, 828, 658, 889]
  Array sorted on the basis of 10th digit from left:
    [828, 936, 737, 941, 350, 552, 356, 658, 766, 967, 973, 981, 984, 889, 696]
  Array sorted on the basis of 100th digit from left:
    [350, 356, 552, 658, 696, 737, 766, 828, 889, 936, 941, 967, 973, 981, 984]

Sorted Array = [350, 356, 552, 658, 696, 737, 766, 828, 889, 936, 941, 967, 973, 981, 984]

```