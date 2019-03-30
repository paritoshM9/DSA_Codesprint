<h1>Trees</h1>



Q1) Given a generic tree and an integer x, check if x is present in the given tree or not. Return true if x is present, return false otherwise.

```c++
bool containsX(TreeNode<int>* root, int x) {
    
    if(root == NULL){
        return false;
    }
    
    if(root->data == x){
        return true;
    }
    
    for(int i = 0; i<root->children.size(); i++){
        bool ispresent = containsX(root->children[i], x);
        if(ispresent == true){
            return true;
        }
    }
    return false;
    

}
```



Q2) Count nodes

#### Given a tree and an integer x, find and return the number of Nodes which are greater than x.

```c++
int nodesGreaterThanX(TreeNode<int> *root, int x) {
    if(root == NULL){
        return 0;
    }
    
    int count = 0;
    if(root->data > x){
        count++;
    }
    
    for(int i = 0; i<root->children.size(); i++){
        int temp_count = nodesGreaterThanX(root->children[i], x);
        count += temp_count;
    }
    
    return count;
}
```



Q3) 

Node with maximum child sum

#### Given a tree, find and return the node for which sum of data of all children and the node itself is maximum. In the sum, data of node itself and data of immediate children is to be taken.

```c++
/**************

template <typename T>
class TreeNode {
public:
    T data;
    vector<TreeNode<T>*> children;
    
    TreeNode(T data) {
        this->data = data;
    }
    
    ~TreeNode() {
        for (int i = 0; i < children.size(); i++) {
            delete children[i];
        }
    }
};
***************/
class Pair{
    public:
        TreeNode<int> *node;
        int max_sum;
};

Pair helper(TreeNode<int>* root){
    
    if(root == NULL){
        Pair p;
        p.node = NULL;
        p.max_sum = 0;
        return p;
    }
    
    int my_sum = root->data;
    for(int i = 0; i<root->children.size(); i++){
        my_sum += root->children[i]->data;
    }
    Pair result;
    result.node = root;
    result.max_sum = my_sum; 
    
    for(int i = 0; i<root->children.size(); i++){
        Pair child_result = helper(root->children[i]);
        if(child_result.max_sum > result.max_sum){
            result = child_result;
        }
        
    }
    
    return result;
    
    
}

TreeNode<int>* maxSumNode(TreeNode<int> *root){
    Pair max_node_pair = helper(root);
    return max_node_pair.node;

}
```



Q4)

Structurally identical

#### Given two Generic trees, return true if they are structurally identical i.e. they are made of nodes with the same values arranged in the same way.

```c++
bool isIdentical(TreeNode<int> *root1, TreeNode<int> * root2) {
    
    if(root1 == NULL && root2 == NULL){
        return true;
    }
    
    if(root1 == NULL || root2 == NULL){
        return false;
    }
    
    
    if(root1->data != root2->data){
        return false;
    }
    
    if(root1->children.size() != root2->children.size()){
        return false;
    }
    for(int i = 0; i<root1->children.size(); i++){
        if(isIdentical(root1->children[i], root2->children[i]) == false){
            return false;
        }
    }
    return true;
}

```



Q5) Next larger

#### Given a generic tree and an integer n. Find and return the node with next larger element in the Tree i.e. find a node with value just greater than n

```c++
#include<climits>
class Pair{
    
  public:
    TreeNode<int>* node;
    int data;
    
};

Pair findNextLarger(TreeNode<int>* root, int n){
    if(root == NULL){
        Pair p;
        p.node = NULL;
        p.data = INT_MAX;
        return p;
    }
    
    Pair result;
    result.node = NULL;
    result.data = INT_MAX;
    
    if(root->data > n){
        result.node = root;
        result.data = root->data;
    }
    
    for(int i = 0; i<root->children.size(); i++){
        Pair child_result = findNextLarger(root->children[i], n);
        if(child_result.node != NULL){
            if(child_result.data < result.data){
                result.node = child_result.node;
                result.data = child_result.data;
            }
        }
        
    }
    
    return result;
    
    
}
TreeNode<int>* nextLargerElement(TreeNode<int> *root, int n) {
    
    Pair result = findNextLarger(root, n);
    return result.node;

}

```



Q6) Second Largest Element In Tree

#### Given a generic tree, find and return the node with second largest value in given tree. Return NULL if no node with required value is present.

```c++
#include<climits>
void helper(TreeNode<int> *root, TreeNode<int>*& max, TreeNode<int>*& second_max){
    
  if(root == NULL){
      return;
  }  
  if(max == NULL){
      max = root;
  }  
  if(root->data > max->data){
      second_max = max;
      max = root;
  }
  
  else if(second_max!= NULL && root->data >second_max->data){
      second_max = root;
  }
    
  for(int i = 0; i<root->children.size(); i++){
      helper(root->children[i], max, second_max);
  }
 
}
TreeNode <int>* secondLargest(TreeNode<int> *root) {
    TreeNode<int>* max = NULL;
    TreeNode<int>* second_max = NULL;
    helper(root, max, second_max);
    return second_max;

}

```



Q7)  Replace with depth

#### In a given Generic Tree, replace each node with its depth value. You need to just update the data of each node, no need to return or print anything.

```c++
#include<queue>

void replaceWithDepthValue(TreeNode<int> *root){    
    
    queue<TreeNode<int>*> q;
    int level = 0;
    q.push(root);
    q.push(NULL);
    
    while(q.size()>0){
        
        TreeNode<int>* node = q.front();
        q.pop();
        if(node == NULL ){
            if(q.size()!= 0){
               q.push(NULL); 
            }
            level++;
        }
        else{
            node->data = level;
            for(int i = 0; i<node->children.size(); i++){
                q.push(node->children[i]);
            }
        }
        
        
    }

}
```

Q ) Remove leaf nodes in Tree

#### Remove all leaf nodes from a given generic Tree. Leaf nodes are those nodes, which don't have any children.

##### Note : Root will also be a leaf node if it doesn't have any child. You don't need to print the tree, just remove all leaf nodes and return the updated root.

##### 

```c++
// Following is the given Tree node structure.
/**************
class TreeNode {
	TreeNode<T>** children;
	int childCount;

	public:
	T data;

	TreeNode(T data);	// Constructor
	int numChildren();
	void addChild(TreeNode<T>* child);
	TreeNode<T>* getChild(int index);
	void setChild(int index, TreeNode<T>* child);
    void removeChild(int index);
 
};
***************/
#include<vector>
TreeNode<int>* removeLeafNodes(TreeNode<int>* root) {
    // Write your code here
    if(root == NULL){
        return NULL;
    }
    int num_child = root->numChildren();
    if(num_child == 0){
        return NULL;
    }
    vector<int> indices;
    for(int i = 0; i<num_child; i++){
        
        TreeNode<int>* child = root->getChild(i);
        if(child->numChildren() == 0){
            indices.push_back(i);
        }
        
    }
    for(int i = indices.size() - 1; i>= 0; i--){
        root->removeChild(indices[i]);
    }
    
    for(int i = 0; i<root->numChildren(); i++){
        TreeNode<int>* temp = removeLeafNodes(root->getChild(i));
        if(temp == NULL){
            root->removeChild(i);
        }
        
    }
    return root;
}


```

