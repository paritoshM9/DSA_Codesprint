<h1>Sorting</h1>

Sorting refers to arranging data in a particular format. Sorting algorithm specifies the way to arrange data in a particular order. 

Q. 1) Sort an Array of 0s, 1s and 2s

###Given an array A[] consisting 0s, 1s and 2s. The task is to write a function that sorts the given array. The functions should put all 0s first, then all 1s and all 2s in last.

```c
// C program to sort an array with 0, 1 and 2 
#include <stdio.h> 

/* Function to swap *a and *b */
void swap(int* a, int* b); 

// Sort the input array, the array is assumed to 
// have values in {0, 1, 2} 
void sort012(int a[], int arr_size) 
{ 
	int lo = 0; 
	int hi = arr_size - 1; 
	int mid = 0; 

	while (mid <= hi) { 
		switch (a[mid]) { 
		case 0: 
			swap(&a[lo++], &a[mid++]); 
			break; 
		case 1: 
			mid++; 
			break; 
		case 2: 
			swap(&a[mid], &a[hi--]); 
			break; 
		} 
	} 
} 

void swap(int* a, int* b) 
{ 
	int temp = *a; 
	*a = *b; 
	*b = temp; 
} 

/* function to print array arr[] */
void printArray(int arr[], int arr_size) 
{ 
	int i; 
	for (i = 0; i < arr_size; i++) 
		printf("%d ", arr[i]); 
	printf("n"); 
} 

int main() 
{ 
	int arr[] = { 0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1 }; 
	int arr_size = sizeof(arr) / sizeof(arr[0]); 
	int i; 

	sort012(arr, arr_size); 

	printf("array after segregation "); 
	printArray(arr, arr_size); 

	getchar(); 
	return 0; 
} 

```
Q. 2 ) C Program to Sort an array of names or strings

###Given an array of strings in which all characters are of the same case, write a C function to sort them alphabetically.

```c
#include <stdio.h> 
#include <stdlib.h> 
#include <string.h> 

static int myCompare(const void* a, const void* b) 
{ 

	// setting up rules for comparison 
	return strcmp(*(const char**)a, *(const char**)b); 
} 

// Function to sort the array 
void sort(const char* arr[], int n) 
{ 
	// calling qsort function to sort the array 
	// with the help of Comparator 
	qsort(arr, n, sizeof(const char*), myCompare); 
} 

int main() 
{ 

	// Get the array of names to be sorted 
	const char* arr[] 
		= { "pythonlanguage", "javascript", "clanguage" }; 

	int n = sizeof(arr) / sizeof(arr[0]); 
	int i; 

	// Print the given names 
	printf("Given array is\n"); 
	for (i = 0; i < n; i++) 
		printf("%d: %s \n", i, arr[i]); 

	// Sort the given names 
	sort(arr, n); 

	// Print the sorted names 
	printf("\nSorted array is\n"); 
	for (i = 0; i < n; i++) 
		printf("%d: %s \n", i, arr[i]); 

	return 0; 
} 
```


