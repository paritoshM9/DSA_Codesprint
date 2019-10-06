<h1>Linked List</h1>

A linked list is a linear data structure where each element is a separate object.
Linked list elements are not stored at contiguous location, the elements are linked using pointers.
Each node of a list is made up of two items - the data and a reference to the next node. The last node has a reference to null. The entry point into a linked list is called the head of the list.

Q) Find a node in LL

#### Given a linked list and an integer n you need to find and return index where n is present in the LL. Do this iteratively.

#### Return -1 if n is not present in the LL.

```c++
int indexOfNIter(Node *head, int n) {
    int i = 0;
    while(head!=NULL){
        if(head->data == n){
            return i;
        }
        i++;
        head = head->next;
    }
    return -1;
    
    
}
```



Q2) AppendLastNToFirst

#### Given a linked list and an integer n, append the last n elements of the LL to front.

##### Indexing starts from 0. You don't need to print the elements, just update the elements and return the head of updated LL.

##### Assume given n will be smaller than length of LL.

```c++
node* append_LinkedList(node* head,int n)
{
    node* temp = head;
    for(int i =0; i<n; i++){
        temp = temp->next;
    }
    
    node* temp_slow = head;
    while(temp->next){
        
        temp = temp->next;
        temp_slow = temp_slow->next;
    
    }
    
    temp->next = head;
    node* newhead = temp_slow->next;
    temp_slow->next = NULL;
    return newhead;
    
}

```

Q3) Eliminate duplicates from LL

#### Given a sorted linked list (elements are sorted in ascending order). Eliminate duplicates from the given LL, such that output LL contains only unique elements.

```c++
node* eliminate_duplicate(node* head)
{
    node* temp = head;
    while(temp->next){
        if(temp->next->data == temp->data){
            temp->next = temp->next->next;
        }
        else{
            temp = temp->next;
        }
        
    }
    return head;
}

```



Q4) Print reverse LinkedList

#### Print a given linked list in reverse order. You need to print the tail first and head last. You can’t change any pointer in the linked list, just print it in reverse order

```c++
void print_linkedlist_spl(node*head)
{
    if(head == NULL){
        return;
    }
    
    print_linkedlist_spl(head->next);
    cout<<head->data<<" ";
}

```

Q5) Palindrome LinkedList

#### Check if a given linked list is palindrome or not. Return true or false.

```c++


//head is the head of you linked list
// Following is the node structure
/**************
class node{
public:
    int data;
    node * next;
    node(int data){
        this->data=data;
        this->next=NULL;
    }
};
***************/
node* reverse(node* head){
    if(head == NULL){
        return NULL;
        
    }
    if(head->next == NULL){
        return head;
    }
    
    node* reverse_next = reverse(head->next);
    node* temp = reverse_next;
    while(temp && temp->next){
        temp = temp->next;
    }
    temp->next = head;
    head->next = NULL;
    return reverse_next;
    
    
}
bool check_palindrome(node* head)
{
    node* faster = head;
    node* slower = head;
    while(faster->next!= NULL && faster->next->next!= NULL){
        slower = slower->next;
        faster = faster->next->next;
    }
    //cout<<slower->next->data;
    slower->next = reverse(slower->next);
    //cout<<slower->next->data;
    node* i = head;
    node* j = slower->next;
    while(j!= NULL){
        if(i->data != j->data){
            return false;
        }
        i = i->next;
        j = j->next;
    }
    return true;
}


```

Q6) Find a node in LL (recursive)

#### Given a linked list and an integer n you need to find and return index where n is present in the LL. Do this recursively.

#### Return -1 if n is not present in the LL.

```c++
int helper(Node* head, int n, int i){
    if(head == NULL){
        return -1;
    }
    if(head->data == n){
        return i;
    }
    
    return helper(head->next, n, i+1);
    
    
    
    
}
int indexOfNRecursive(Node *head, int n) {
    int i = 0;
    return helper(head, n, i);
  
}
```

Q7) Even after Odd LinkedList

#### Arrange elements in a given Linked List such that, all even numbers are placed after odd numbers. Respective order of elements should remain same.

```c++


node* arrange_LinkedList(node* head)
{
    node* even_h = new node(-1);
    node* odd_h = new node(-1);
    node* temp_even = even_h;
    node* temp_odd = odd_h;
    
    node* temp = head;
    node* curr;
    while(temp){
        curr = temp;
        temp = temp->next;
        curr->next = NULL;
        if(curr->data%2 == 0){
            temp_even->next = curr;
            temp_even = temp_even->next;
        }
        else{
            temp_odd->next = curr;
            temp_odd = temp_odd->next;
        }
    }
    
    even_h = even_h->next;
    temp_odd->next = even_h;
    return odd_h->next;
    
}

```



Q8) Delete every N nodes

#### Given a linked list and two integers M and N. Traverse the linked list such that you retain M nodes then delete next N nodes, continue the same until end of the linked list. That is, in the given linked list you need to delete N nodes after every M nodes.

```c++
// Following is the node structure
/**************
class node{
public:
    int data;
    node * next;
    node(int data){
        this->data=data;
        this->next=NULL;
    }
};
***************/
void delete_m(node* head, int m, int n){
    if(head == NULL){
        return;
    }
    
    node* temp = head;
    node* prev;
    int i = 0;
    while(temp && i<m){
        prev = temp;
        temp = temp->next;
        i++;
    }
    int j = 0;
    while(temp && j<n){
        temp = temp->next;
        j++;
    }
    prev->next = temp;
    delete_m(temp, m, n);
    
}
node* skipMdeleteN(node  *head, int M, int N) {
    // Write your code here
    delete_m(head, M, N);
    return head;
}

```





