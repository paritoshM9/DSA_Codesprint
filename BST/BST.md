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



Q)  LCA of BST

#### Given a binary search tree and two nodes, find LCA(Lowest Common Ancestor) of the given two nodes in the BST. Read about LCA if you are having doubts about the definition.

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

int lcaInBST(BinaryTreeNode<int>* root , int val1 , int val2){
    // Write your code here
	if(root == NULL){
      return NULL;
    }
  
  
  if(root->data == val1 || root->data == val2){
    return root->data;
  }
  
  
  if(val1<root->data && val2>root->data){
    
	return root->data;
  }
  
  if(val1<root->data && val2 < root->data){
    return lcaInBST(root->left, val1, val2);
  }
  if(val1>root->data && val2 > root->data){
    return lcaInBST(root->right, val1, val2);
  }
  
  
  
}

```



Q) Largest BST

#### Given a Binary tree, find the largest BST subtree. That is, you need to find the BST with maximum height in the given binary tree.

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
class Pair{
    
  public:
    int max_height;
    bool isBST;
    int root;
    
};
bool isBST_node(BinaryTreeNode<int> *root){
    if(root == NULL){
        return true;
    }
    if(root->left && root->left->data > root->data){
           return false; 
    }
    else if(root->right && root->right->data<root->data){
          return false;  
    }
    return true;
}
Pair helper(BinaryTreeNode<int> *root){
    
    
    Pair result;
    if(root == NULL){
        result.isBST = true;
        result.max_height = 0;
        result.root = -1;
        return result;
    }
    
    Pair left = helper(root->left);
    Pair right = helper(root->right);
    
    if(left.isBST == true && right.isBST == true){
        if(isBST_node(root) == false){
            result.isBST = false;
            if(left.max_height > right.max_height){
                result.max_height = left.max_height;
                result.root = left.root;
                return result;
            }
            else{
                result.max_height = right.max_height;
                result.root = right.root;
                return result;
            }
        }
        
        else{
            
            result.isBST = true;
            result.max_height = max(left.max_height, right.max_height) + 1;
            result.root = root->data;
            return result;
            
        }
    }
    //right -> false
    else if(left.isBST == true){
        result = left;
        result.isBST = false;
        return result;
    }
    else if(right.isBST == true){
        result = right;
        result.isBST = false;
        return result;
    }
    else{
        result = left;
        if(right.max_height > left.max_height){
            result.max_height = right.max_height;
            result.root = right.root;
        }
        return result;
    }
    
}
int largestBSTSubtree(BinaryTreeNode<int> *root) {
    Pair result = helper(root);
    return result.max_height;

}

```



Q) Replace with Sum of greater nodes

#### Given a binary search tree, replace each nodes' data with the sum of all nodes' which are greater or equal than it. You need to include the current node's data also.

#### That is, if in given BST there is a node with data 5, you need to replace it with sum of its data (i.e. 5) and all nodes whose data is greater than or equal to 5.

```c++
int helper(BinaryTreeNode<int> *root, int sum){
    
    if(root == NULL){
        return 0;
    }
    
    //right
    int right_compl = helper(root->right, sum);
    int prev_root = root->data + right_compl;
    root->data += right_compl;
    root->data += sum;
    
    return helper(root->left, root->data) + prev_root;
    
    
    
}
void replaceWithLargerNodesSum(BinaryTreeNode<int> *root) {
    // Write your code here
    int a = helper(root, 0);
}

```



Q)  Path Sum Root to Leaf

#### Given a binary tree and a number k, print out all root to leaf paths where the sum of all nodes value is same as the given number k.

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
#include<vector>

void display(vector<BinaryTreeNode<int> *> v){
    
    for(int i = 0; i<v.size(); i++){
        cout<<v[i]->data<<" ";
    }
    cout<<endl;
    
    
}
void helper(BinaryTreeNode<int> *root, int k, vector<BinaryTreeNode<int> *> v ) {
    if(root == NULL){
        return;
    }
    if(root->left == NULL && root->right == NULL){
        v.push_back(root);
        k -= root->data;
        if(k == 0){
            display(v);
        }
        
        return;
    }
    
    k -= root->data;
    v.push_back(root);
    helper(root->left,k, v);
    
    helper(root->right,k, v);
    
}

void rootToLeafPathsSumToK(BinaryTreeNode<int> *root, int k) {
    // Write your code here
    vector<BinaryTreeNode<int> *> v;
    helper(root, k, v);

}

```





