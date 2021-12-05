# Trees

## Binary Trees

### Node of Tree
```cpp
class Node{
public:
  int data;
  Node *left,*right;
  Node(int data){
    this->data = data;
    this->left = NULL;
    this->right = NULL;
  }
};
```
### Sample Tree for Testing
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/lca.png)
```cpp
Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
```

### Find Node in Tree
- Idea is to use tree traversal.
- If current node has same data then return with that node
- otherwise, find in left subtree and right subtree.

```cpp
bool findNode(Node* root,int data){
  if(root == NULL) return false;
  
  if(root->data == data){ // check if current node data is the data we are finding
    return true;
  }
  
  bool findLeft = findNode(root->left,data); // find in left subtree
  if(findLeft) return true;
  
  bool findRight = findNode(root->right,data); // find in right subtree
  if(findRight) return true;
  
  return false; // if not found in left and right return false
}
```
### Find Node to Root Path
- First Find the Node
- While going back to root -> add the nodes to a ;ist while returning.

> Note: we can reduce the time if we pass the vector by reference in a function.

```cpp
vector<int> nodeToRootPath(Node* root,int data){
  if(root == NULL){
    vector<int> ans;
    return ans;
  }
  
  if(root->data == data){
    vector<int> path;
    path.emplace_back(root->data); // emplace_back is similar to push_back , difference in speed, push_back is bit slower then emplace back
    return path;
  }
  
  vector<int> pathLeft = nodeToRootPath(root->left,data);
  if(pathLeft.size() != 0){
    pathLeft.emplace_back(root->data);
    return pathLeft;
  }
  
  vector<int> pathRight = nodeToRootPath(root->left,data);
  if(pathRight.size() != 0){
    pathRight.emplace_back(root->data);
    return pathRight;
  }
  
  vector<int> ans;
  return ans; // empty path if not found.
  
}
```

### LCA (Lowest Common Ancestor)

- The lowest common ancestor (LCA) of two nodes x and y in a binary tree is the lowest (i.e., deepest) node that has both x and y as descendants, where each node can be a descendant of itself (so if x is reachable from w, w is the LCA). 
- In other words, the LCA of x and y is the shared ancestor of x and y that is located farthest from the root.
- For example, consider the following binary tree. Let x = 6 and y = 7. The common ancestors of nodes x and y are 1 and 3. Out of nodes 1 and 3, the LCA is 3 as it is farthest from the root.

![](https://www.techiedelight.com/wp-content/uploads/LCA.png)

**How To Find ?**

- A simple solution would be to store the path from root to x and the path from the root to y in two auxiliary arrays. 
- Then traverse both arrays simultaneously till the values in the arrays match. 
- The last matched value will be the LCA. 
- If the end of one array is reached, then the last seen value is LCA. 
- The time complexity of this solution is O(n), where n is the total number of nodes in the binary tree. 
- But the auxiliary space used by it is O(n) required for storing two arrays.

