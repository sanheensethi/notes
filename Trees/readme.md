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
  
  vector<int> pathRight = nodeToRootPath(root->right,data);
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

## Trees are special types of Graph.
- Graph can be stored with adjacency matrix and adjacency list.
- Adjacency is not memory sufficient so we use mostly adjacency list.
- we can perform DFS and BFS in Trees also, they are same as graph {BFS - Level order traversal in  trees}

```cpp
#include<bits/stdc++.h>
const int N = 1e5+10;

vector<int> g[N]; // in this we are declaring N vectors i.e. 2D vector, i.e. there are N vectors inside a `g` vector.
bool visited[N]; // whenever we enter into any vertex , we visit it.

int main(){
  int n,m;
  cin>>m>>m; // n vertices and m edges
  for(int i=0; i<m; ++i){
    int v1,v2;
    cin>>v1>>v2;
    g[v1].push_back(v2);
    g[v2].push_back(v1);
  }
}
```

### DFS (Depth-First-Search)
- In this we go deeply into a single child untill we reach last leaf node, before moving to other childs. 

```cpp
void dfs(int vertex){
  /* Section 1:Take action on vertex after entering the vertex. */
    visited[vertex] = true;
    for(int child:g[vertex]){
      /* Section 2: Take action on child before entering child node. */
      if(visited[child] == true) continue;
      dfs(child);
      /* Section 3: Take action on child after exiting the child node */
    }
  /* Section 4: Take action on vertex before exiting the vertex. */
}
```
