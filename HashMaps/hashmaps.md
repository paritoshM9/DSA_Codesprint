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



Q) Pairs with difference K

#### You are given with an array of integers and an integer K. Write a program to find and print all pairs which have difference K.

#### Best solution takes O(n) time. And take difference as absolute.

```c++
#include<unordered_map>
void printPairs(int *arr, int n, int k) {
	// Write your code here
	unordered_map<int,int> count;
    for(int i = 0; i<n; i++){
        count[arr[i]] += 1;
    }
    
    if(k == 0){
        for(auto x:count){
            int key = x.first;

            int num_prints = (x.second*(x.second-1))/2;
            //cout<<num_prints<<endl;
            for(int i = 0; i<num_prints; i++){
                cout<<key<<" "<<key<<endl;
            }
            
            count[key] = 0;
            
        }
        
    }
    
    else{
        
        for(int i = 0; i<n; i++){
            
            int a = arr[i];
            if(count[a+k]){
                int times = count[a]*count[k+a];
                for(int i = 0; i<times; i++){
                    cout<<a<<" "<<a+k<<endl;
                    
                }
            }
            
            if(count[a-k]){
                int times = count[a]*count[a-k];
                for(int i = 0; i<times; i++){
                    cout<<min(a,a-k)<<" "<<max(a,a-k)<<endl;
                    
                }
            }
            
            count[a] = 0;
            
        }
        
        
        
    }
    
}



```

Q) Longest subset zero sum (Partial answer , 1 test case not working)

#### Given an array consisting of positive and negative integers, find the length of the longest continuous subset whose sum is zero.



```c++

#include<iostream>
#include<unordered_map>
using namespace std;

int lengthOfLongestSubsetWithZeroSum(int* arr, int size){
    
    unordered_map<int,int> sum_at;
    int max_len = 0;
    int running_sum = 0;
    sum_at[0] = -1;
    for(int i =0 ; i<size; i++){
        running_sum += arr[i];
        if(sum_at[running_sum]){
            int diff = i - sum_at[running_sum];
            if(diff>max_len){
                max_len = diff;
            }
           
        }
        if(running_sum!=0)
        {sum_at[running_sum] = i;}
    }
    
    
    return max_len;
    
}



```

