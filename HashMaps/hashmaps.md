<h1>hashmaps</h1>

Q) Extract Unique characters

#### Given a string, you need to remove all the duplicates. That means, the output string should contain each character only once. The respective order of characters should remain same.

```c++
#include<unordered_map>

char* uniqueChar(char *str){
    // Write your code here
    int i = 0;
    int j = 0;
    unordered_map<char,bool> hasOccured;
    while(str[j] != '\0'){
        
       if(hasOccured[str[j]]){
           j++;
       } 
       else{
           
           str[i] = str[j];
           hasOccured[str[j]] = true;
           i++;
           j++;
           
           
       }
        
        
        
        
    }
    str[i] = '\0';
    return str;
}
```



Q) Longest Consecutive Subsequence

#### You are given with an array of integers that contain numbers in random order. Write a program to find the longest possible sub sequence of consecutive numbers using the numbers from given array.

#### You need to return the output array which contains consecutive elements. Order of elements in the output is not important.

#### Best solution takes O(n) time.

#### If two arrays are of equal length return the array whose index of smallest element comes first.

```c++
#include<unordered_map>
vector<int> longestSubsequence(int *arr, int n){
	// Write your code here
    unordered_map<int,int> seq;
    for(int i = 0; i<n; i++){
        int num = arr[i];
        if(seq[num]){
            continue;
        }
        if(seq[num-1] || seq[num+1]){
            seq[num] = seq[num-1] + seq[num+1] + 1;
            int j = num-1;
            while(seq[j]!= 0){
                seq[j] = seq[num];
                j--;
            }
            
            j = num + 1;
            while(seq[j]!= 0){
                seq[j] = seq[num];
                j++;
            }
            
        }
        else{
            seq[num] = 1;
        }
    }
    int maxm = 0;
    
    for(int i = 0; i<n; i++){
        if(seq[arr[i]] > maxm){
            maxm = seq[arr[i]];
        }
    }
    
    unordered_map<int,bool> start_elem;
    for(int i = 0; i<n; i++){
        if(seq[arr[i]] == maxm){
            int j = arr[i];
            while(seq[j]){
                j-=1;
            }
            //j is a start of max sequence
            start_elem[j+1] = true;
            
        }
    }
    
    vector<int> v;
    int start_num = 0;
    for(int i = 0; i<n; i++){
        if(start_elem[arr[i]] == true){
            start_num = arr[i];
            break;
        }
    }
    
    for(int i = start_num; i<start_num + maxm; i++){
        v.push_back(i);
    }
    return v;
}
```



Q) 

