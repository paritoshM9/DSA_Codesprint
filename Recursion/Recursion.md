<h1>Recursion</h1>

Recursion is the process which comes into existence when a function calls a copy of itself to work on a smaller problem. Any function 
which calls itself is called recursive function, and such function calls are called recursive calls. Recursion involves several numbers 
of recursive calls. However, it is important to impose a termination condition of recursion.

Q. 1) Generating all possible Subsequences using Recursion

###Given an array. The task is to generate and print all of the possible subsequences of the given array using recursion.

```c
// C++ code to print all possible 
// subsequences for given array using 
// recursion 
#include <bits/stdc++.h> 
using namespace std; 

void printArray(vector<int> arr, int n) 
{ 
	for (int i = 0; i < n; i++) 
		cout << arr[i] << " "; 
	cout << endl; 
} 

// Recursive function to print all 
// possible subsequences for given array 
void printSubsequences(vector<int> arr, int index, 
					vector<int> subarr) 
{ 
	// Print the subsequence when reach 
	// the leaf of recursion tree 
	if (index == arr.size()) 
	{ 
		int l = subarr.size(); 

		// Condition to avoid printing 
		// empty subsequence 
		if (l != 0) 
			printArray(subarr, l); 
	} 
	else
	{ 
		// Subsequence without including 
		// the element at current index 
		printSubsequences(arr, index + 1, subarr); 

		subarr.push_back(arr[index]); 

		// Subsequence including the element 
		// at current index 
		printSubsequences(arr, index + 1, subarr); 
	} 
	return; 
} 

// Driver Code 
int main() 
{ 
	vector<int> arr{1, 2, 3}; 
	vector<int> b; 

	printSubsequences(arr, 0, b); 

	return 0; 
} 

```

Q2) Find All Permutations of String using Recursion

```c
#include <bits/stdc++.h>
using namespace std;


// Function to print permutations of string  
// This function takes three parameters:  
// 1. String  
// 2. Starting index of the string  
// 3. Ending index of the string.  
void permute(string a, int l, int r)  
{  
    // Base case  
    if (l == r)  
        cout<<a<<endl;  
    else
    {  
        // Permutations made  
        for (int i = l; i <= r; i++)  
        {  

            // Swapping done  
            swap(a[l], a[i]);  

            // Recursion called  
            permute(a, l+1, r);  

            //backtrack  
            swap(a[l], a[i]);  
        }  
    }  
}  

// Driver Code  
int main()  
{  
  //example string as an input
    string str = "ABC";  
    int n = str.size();  
    permute(str, 0, n-1);  
    return 0;  
}  
```
