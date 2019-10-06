<h1>Priority Queue</h1>

Priority Queue is an extension of queue with following properties:
1)Every item has a priority associated with it.
2)An element with high priority is dequeued before an element with low priority.
3)If two elements have the same priority, they are served according to their order in the queue.

Q1) Check Max-Heap

#### Given an array of integers, check whether it represents max-heap or not.

#### Return true or false.

```c++
#include<iostream>
#include<queue>

using namespace std;
bool checkMaxHeap(int arr[], int n){
    
    int curr = 0;
    int child1 = 1;
    int child2 = 2;
    queue<int> q;
    q.push(curr);
    
    while(curr<n && q.size()!= 0){
        
        curr = q.front();
        q.pop();
        child1 = 2*curr + 1;
        child2 = 2*curr + 2;
        if(child1 < n){
            q.push(child1);
            if(arr[curr] < arr[child1]){
                return false;
            }
        }
        if(child2 < n){
            q.push(child2);
            if(arr[curr] < arr[child2]){
                return false;
            }
        }        
        
        
    }
    return true;
}

```



Q2) 

Kth largest element

#### Given an array A of random integers and an integer k, find and return the kth largest element in the array.

#### Try to do this question in less than O(nlogn) time.

```c++
#include<iostream>
#include<queue>
using namespace std;

int kthLargest (vector<int> arr, int n, int k){
    
    priority_queue<int, vector<int>, greater<int>> pq;
    for(int i = 0; i<k; i++){
        pq.push(arr[i]);
    }
    for(int i = k; i<n; i++){
        if(pq.top() < arr[i]){
            pq.pop();
            pq.push(arr[i]);
        }
    }
    return pq.top();
}

```

Q3) Running median

#### You are given a stream of n integers. For every ith integer, add it to the running list of integers and print the resulting median (of the list till now).

#### Print the only integer part of median.

```c++
#include<iostream>
#include<queue>
using namespace std;

void heapify(priority_queue<int, vector<int>, less<int>>& left_heap, priority_queue<int, vector<int>, greater<int>>& right_heap, int& left_num, int& right_num ){
    
    if(left_num - right_num >1){
        right_heap.push(left_heap.top());
        left_heap.pop();
        left_num--;
        right_num++;
    }
    
    else if(right_num > left_num){
        left_heap.push(right_heap.top());
        right_heap.pop();
        right_num--;
        left_num++;
    }
    
    
}
int findMedian(priority_queue<int, vector<int>, less<int>>& left_heap, priority_queue<int, vector<int>, greater<int>>& right_heap, int& left_num, int& right_num ){
    
   if(left_num == right_num){
       return (left_heap.top() + right_heap.top())/2;
   }
   return left_heap.top();
    
    
}


void findMedian(int arr[], int n){
    
    
    priority_queue<int, vector<int>, less<int>> left_heap;
    priority_queue<int, vector<int>, greater<int>> right_heap;
    
    int left_num = 0;
    int right_num = 0;
    
    
    //right heap -> min heap
    //left heap ->max heap
    //left num >= right num by 1

    //new elem comes if both heap empty ->insert to left 
    
    // if elem < left top ->left heap  , else ->right heap
    
    // heapify - adjusting the number of elem in left and right
    
    //if right num>left num , push right.top into left 
    
    //if num left + right num is even , median is avg of left top and right top
    
    //else return left top
    
    for(int i = 0; i<n; i++){
        if(i == 0){
            left_heap.push(arr[i]);
            left_num++;
            cout<<arr[i]<<endl;
        }
        else{
            if(arr[i] < left_heap.top()){
                left_heap.push(arr[i]);
                left_num++;
            }
            else{
                right_heap.push(arr[i]);
                right_num++;
            }
            heapify(left_heap, right_heap, left_num, right_num);
            cout<<findMedian(left_heap, right_heap, left_num, right_num)<<endl;
            
        }
    }
}

```

Q) Buy the ticket

Send Feedback

#### You want to buy a ticket for a well-known concert which is happening in your city. But the number of tickets available is limited. Hence the sponsors of the concert decided to sell tickets to customers based on some priority.

#### A queue is maintained for buying the tickets and every person has attached with a priority (an integer, 1 being the lowest priority). The tickets are sold in the following manner -

#### 1. The first person (pi) in the queue asked to comes out.

#### 2. If there is another person present in the queue who has higher priority than pi, then ask pi to move at end of the queue without giving him the ticket.

#### 3. Otherwise, give him the ticket (and don't make him stand in queue again).

##### Giving a ticket to a person takes exactly 1 minutes and it takes no time for removing and adding a person to the queue. And you can assume that no new person joins the queue.

#### Given a list of priorities of N persons standing in the queue and the index of your priority (indexing starts from 0). Find and return the time it will take until you get the ticket.

```c++
#include<iostream>
#include<queue>
using namespace std;

class Pair{
    
  public:
    int priority;
    int queue_num;
    Pair(int p, int n){
        priority = p;
        queue_num = n;
    }
};

class Comp{
  public:
    bool operator()(Pair a, Pair b){
        return a.priority<b.priority;
    }    
};

int buyTicket (int *arr, int n, int k){
    priority_queue<Pair, vector<Pair>, Comp> pq;
    for(int i = 0; i<n; i++){
        Pair temp(arr[i], i);
        pq.push(temp);
    }
    int count = 1;
    Pair front = pq.top();
    pq.pop();
    while(front.queue_num != k){
        count++;
        front = pq.top();
        pq.pop();
    }
    return count;
}

```

