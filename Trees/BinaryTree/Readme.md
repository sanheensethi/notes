# Binary Tree

## 1. Termonologies

- Root
- Childrens
- Leaf Node
- SubTree - Node and it's benath (niche vale sare children) is subtree
- Ancestors - bche ke papa, uske dada, uske pardada , uske par par dada

![take U forward - L1  Introduction to Trees Types of Trees  _ANrF3FJm7I - 885x498 - 4m15s](https://user-images.githubusercontent.com/35686407/172037552-66cb469e-082a-43d7-a644-8d7c92e8b21b.png)


## 2. Types of Binary Tree
- Full : Either has 0 or 2 children
- Complete : 
        1. All levels are completly filled except last level
        2. The last level has nodes as left as possible
- Perfect : All leaf node are at same level
- Balanced : `Height of Tree` at `max log(N)`
- Degenerate : Skewed Trees either left or right , mtlb ek single line ki trh hai left ya right ki trf bdte ja rhe hai.

## 3. Representation

![take U forward - L2  Binary Tree Representation in C++  ctCpP0RFDFc - 885x498 - 2m19s](https://user-images.githubusercontent.com/35686407/172037416-1d7422c6-16a9-4d79-b665-965fb826ddf1.png)

![take U forward - L2  Binary Tree Representation in C++  ctCpP0RFDFc - 853x480 - 2m45s](https://user-images.githubusercontent.com/35686407/172037419-8679dec1-a74a-4653-b94d-180944a6020c.png)

## 4. Graph Traversals (BFS / DFS)

#### DFS : (Depth First Search)
- InOrder : Left Root Right
- PreOrder : Root Left Right
- PostOrder : Left Right Root

#### BFS : (Breadth First Search)
- Level Order

## 5. PreOrder - PostOrder - InOrder Traversal [Recursion]

- TC : O(n)

```cpp
void preOrder(TreeNode* root,vector<int>& ans){
        // Root Left Right
        if(root == NULL) return;
        ans.push_back(root->val);
        preOrder(root->left,ans);
        preOrder(root->right,ans);
}
```

```cpp
void postOrder(TreeNode* root,vector<int>& ans){
        // Left Right Root
        if(root == NULL) return;
        preOrder(root->left,ans);
        preOrder(root->right,ans);
        ans.push_back(root->val);
}
```

```cpp
void inOrder(TreeNode* root,vector<int>& ans){
        // Left Root Right
        if(root == NULL) return;
        preOrder(root->left,ans);
        ans.push_back(root->val);
        preOrder(root->right,ans);
}
```

## 6. Level Order Traversal (BFS): 

- Queue DS is used.

```cpp
vector<vector<int>> levelOrder(TreeNode* root) {
        if(root == NULL) return {};
        vector<vector<int>> ans;
        queue<TreeNode*> Q;
        Q.push(root);
        while(!Q.empty()){
            int size = Q.size();
            vector<int> levelNodes;
            while(size--){
                TreeNode* node = Q.front();Q.pop();
                levelNodes.push_back(node->val);
                if(node->left){
                    Q.push(node->left);
                }
                if(node->right){
                    Q.push(node->right);
                }
            }
            ans.push_back(levelNodes);
        }
        return ans;
    }
```

## 7. PreOrder - PostOrder - InOrder Iterative

- Stack DataStructure is Used.

1. PreOrder:
    1. Root Left Right (in recursion)
    2. Root Right Left (in Iterative) , it's reverse of recursion , Why ? we need Left First in PreOrder, so by that Left will be at top. as Stack : LIFO
```cpp
vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ans;
        if(root == NULL) return ans;
        stack<TreeNode*> st;
        st.push(root);
        // Put in stack Method for Preorder in iterative :  Right Left 
        while(!st.empty()){
            TreeNode* node = st.top();st.pop();
            ans.push_back(node->val);
            if(node->right){
                st.push(node->right);
            }
            if(node->left){
                st.push(node->left);
            }
        }
        return ans;
    }
```

2. PostOrder:
        
