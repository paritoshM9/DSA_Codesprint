<h1>Binary Trees</h1>

Q1 ) Sum of all nodes

#### Given a binary tree, find and return the sum of all nodes.

```c++
int sumOfAllNodes(BinaryTreeNode<int>* root) {
    // Write your code here
    if(root == NULL){
        return 0;
    }
    
    int left_sum = sumOfAllNodes(root->left);
    int right_sum = sumOfAllNodes(root->right);
    return left_sum + right_sum + root->data;
}
```



Q2)  is Balanced

#### Given a binary tree, check if its balanced i.e. depth of left and right subtrees of every node differ by at max 1. Return true if given binary tree is balanced, false otherwise.

```c++
class Pair{
    public:
    
    int height;
    bool is_bal;
      
};

Pair helper(BinaryTreeNode<int> *root) {
    
    if(root == NULL){
        Pair p;
        p.height = 0; 
        p.is_bal = true;
        return p;
    }
    
    Pair left = helper(root->left);
    if(left.is_bal == false){
        return left;
    }
    
    Pair right = helper(root->right);
    if(right.is_bal == false){
        return right;
    }
    
    int diff = left.height - right.height;
    if(diff<-1 || diff>1){
        left.is_bal = false;
        return left;
    }
    
    Pair result;
    result.is_bal = true;
    result.height = max(left.height, right.height) + 1;
    return result;

}

bool isBalanced(BinaryTreeNode<int> *root) {
    return helper(root).is_bal;
    

}
```



Q3) Level order traversal

#### Given a binary tree, print the level order traversal. Make sure each level start in new line.

```c++
// Following is the Binary Tree node structure
/**************
class BinaryTreeNode {
    public : 
    T data;
    BinaryTreeNode<T> *left;
    BinaryTreeNode<T> *right;

    BinaryTreeNode(T data) {
        this -> data = data;
        left = NULL;
        right = NULL;
    }
};

***************/
#include<queue>
void printLevelATNewLine(BinaryTreeNode<int> *root) {
    queue<BinaryTreeNode<int>*> q;
    q.push(root);
    q.push(NULL);
    
    while(q.size()!=0){
        BinaryTreeNode<int>* node = q.front();
        q.pop();
        if(node == NULL){
            cout<<endl;
            if(q.size()!=0 ){
                q.push(NULL);
            }
        }
        else{
            cout<<node->data<<" ";
            if(node->left){
                q.push(node->left);
            }
            
            if(node->right){
                q.push(node->right);
            }
        }
        
    }
}

```

Q4) Remove Leaf nodes



#### Remove all leaf nodes from a given Binary Tree. Leaf nodes are those nodes, which don't have any children.

```c++
BinaryTreeNode<int>* removeLeafNodes(BinaryTreeNode<int> *root) {
    // Write your code here
    if(root == NULL){
        return NULL;
    }
    
    if(root->left == NULL && root->right == NULL){
        return NULL;//leaf node
    }
    
    root->left = removeLeafNodes(root->left);
    root->right = removeLeafNodes(root->right);
    
    return root;
}

```



Q5) Given a binary tree, write code to create a separate linked list for each level. You need to return the array which contains head of each level linked list.

```c++
// Following is the Node and Binary Tree node structure

/**************
class node{
public:
    T data;
    node<T> * next;
    node(T data){
        this->data=data;
        this->next=NULL;
    }
};

class BinaryTreeNode {
    public : 
    T data;
    BinaryTreeNode<T> *left;
    BinaryTreeNode<T> *right;

    BinaryTreeNode(T data) {
        this -> data = data;
        left = NULL;
        right = NULL;
    }
};

***************/
#include<queue>
vector<node<int>*> createLLForEachLevel(BinaryTreeNode<int> *root) {
    queue<BinaryTreeNode<int>*> q;
    vector<node<int>*> v;
    q.push(NULL);
    q.push(root);
    //q.push(NULL);
    
    node<int>* temp = new node<int>(-1);
    node<int>* next_node = new node<int>(-1);
    while(q.size()!=0){
        
        BinaryTreeNode<int>* tree_node = q.front();
        q.pop();
        
        if(tree_node == NULL){
            if(q.size() != 0){
                q.push(NULL);
                temp = new node<int>(q.front()->data);
                v.push_back(temp);
            }
            
        }
        else{
           if(q.size() == 0){
               next_node = NULL;
           }
           if(q.front() == NULL){
               next_node = NULL;
           }
           else{
               next_node = new node<int>(q.front()->data);
           }
           
           temp->next = next_node;
           temp = next_node;
           if(tree_node->left){
               q.push(tree_node->left);
           }
            
            
           if(tree_node->right){
               q.push(tree_node->right);
           }
        }
        
        
    }
    return v;

}
```

Q6) ZigZag tree

#### Given a binary tree, print the zig zag order i.e print level 1 from left to right, level 2 from right to left and so on. This means odd levels should get printed from left to right and even level right to left.



```c++
#include<stack>
void zigZagOrder(BinaryTreeNode<int> *root) {
    // Write your code here
    queue<BinaryTreeNode<int>*> q;
    q.push(root);
    q.push(NULL);
    int level = 1;
    
    stack<int> st;
    while(q.size()!=0){
        BinaryTreeNode<int>* node = q.front();
        q.pop();
        if(node == NULL){
            
            if(level%2 == 0){
                while(st.size()!= 0){
                    cout<<st.top()<<" ";
                    st.pop();
                }
            }
            cout<<endl;
            if(q.size()!=0 ){
                q.push(NULL);
            }
            level++;
        }
        else{
            
            if(level%2 == 0){
               st.push(node->data); 
                
            }
            
            else{
                //odd
                cout<<node->data<<" ";
                
                
            }
            if(node->left){
                q.push(node->left);
            }
            
            if(node->right){
                q.push(node->right);
            }
        }
        
    }
}

```

Q7) 

Nodes without sibling



#### Given a binary tree, print all nodes that don’t have a sibling.

#####  Print the elements in different lines. And order of elements doesn't matter.

##### 

```c++


void nodesWithoutSibling(BinaryTreeNode<int> *root) {
    // Write your code here
    if(root == NULL){
        return;
    }
    
    
    if(root->left && !root->right){
        cout<<root->left->data<<endl;
    }
    
    if(!root->left && root->right){
        cout<<root->right->data<<endl;
    }
    
    nodesWithoutSibling(root->left);
    nodesWithoutSibling(root->right);
    
}

```



