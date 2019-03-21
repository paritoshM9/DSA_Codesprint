<h1>BST</h1>

Q1) Create & Insert Duplicate Node

#### Given a Binary Tree with N number of nodes, for each node create a new duplicate node, and insert that duplicate as left child of the original node.

```c++
void insertDuplicateNode(BinaryTreeNode<int> *root) {
    // Write your code here
    if(root == NULL){
        return;
    }
    
    BinaryTreeNode<int> *duplicate = new BinaryTreeNode<int>(root->data);
    duplicate->left = root->left;
    root->left = duplicate;
    
    insertDuplicateNode(duplicate->left);
    insertDuplicateNode(root->right);

}
```



Q2)Pair sum BInary Tree



#### Given a binary tree and an integer S, print all the pair of nodes whose sum equals S.

##### Assume binary tree contains all unique elements.

##### Note : In a pair, print the smaller element first. Order of different pair doesn't matter.

```c++
#include<unordered_map>
void helper(BinaryTreeNode<int> *root, int sum, unordered_map<int,int>& isPresent){
    if(root == NULL){
        return;
    }
    
    int diff = sum - root->data;
    if(isPresent[diff]){
        cout<<min(diff, root->data)<<" "<<max(diff, root->data)<<endl;
        
    }
    
    isPresent[root->data] = 1;
    helper(root->left, sum, isPresent);
    
    helper(root->right, sum, isPresent);
    
    
    
}
void nodesSumToS(BinaryTreeNode<int> *root, int sum) {
    // Write your code here
    unordered_map<int,int> isPresent;
    helper(root, sum, isPresent);
}

```



Q) LCA of Binary Tree

#### Given a binary tree and two nodes, find LCA (Lowest Common Ancestor) of the given two nodes in Binary Tree. 

##### If out of 2 nodes only one node is present, return that node.

##### If both are not present, return -1.



```c++

int lcaBinaryTree(BinaryTreeNode <int>* root , int val1, int val2){
    // Write your code here
    if(root == NULL){
        return -1;
    }
    
    int left = lcaBinaryTree(root->left, val1, val2);
    int right = lcaBinaryTree(root->right, val1, val2);
    int ans = -1;
    
    if(root->data == val1){
        ans = val1;
    }
    else if(root->data == val2){
        ans = val2;
    }
    
    if(left != -1 && right != -1){
        return root->data;
    }
    
    
    
    if(left!=-1){
        if(ans != -1){
            return ans;
        }
        return left;
    }
    else if(right!= -1){
        if(ans != -1){
            return ans;
        }
        return right;
    }
    
    return ans;

    
    
    
}

```



Q) 

