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

#### 1. `PreOrder`:
    1. `Root Left Right` (in `recursion`)
    2. `Root Right Left` (in `Iterative`) , it's reverse of recursion , Why ? we need Left First in PreOrder, so by that Left will be at top. as Stack : LIFO
    3. TC : O(N)
    4. SC : O(N) ~ O(H) (Worse Case : Skewed Binary Tree)
 
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

#### 2. InOrder:
    1. In this, we push the node if it is not null, and move node to left
    2. after that if node is null then pop the node and print and move to right
    3. Simple Steps:
        - Node != NULL , Push in Stack , Node = Node->left
        - Node == NULL , Pop from Stack , Print , Node = Node->right
        - If st.empty() then break;
    4. TC : O(n)
    5. SC : O(n) ~ O(H) (Worst Case : Skewed Binary Tree)

```cpp
vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;
        if(root == NULL) return {};
        
        stack<TreeNode*> st;
        TreeNode* node = root;
        
        while(true){
            if(node != NULL){
                st.push(node);
                node = node->left;
            }else{
                if(st.empty()) break;
                node = st.top();st.pop();
                ans.push_back(node->val);
                node = node->right;
            }
        }
        
        return ans;
    }
```
        
#### 3. PostOrder:

`3.1 Using 2 Stack` -

- Create 2 Stacks. st1,st2
- Push Root in St1
- in loop : Pop from St1 and Push in st2
- Push Left Right in st1 of node in loop
- When loops end, empty st2 , its postOrder Traversal
- TC : O(n)
- SC : O(2n)

```cpp
vector<int> postorderTraversal(TreeNode* root) {
        vector<int> ans;
        if(root == NULL) return ans;
        
        stack<TreeNode*> st1,st2;
        st1.push(root);
        
        while(!st1.empty()){
            TreeNode* node = st1.top();st1.pop();
            st2.push(node);
            if(node->left) st1.push(node->left);
            if(node->right) st1.push(node->right);
        }
        
        while(!st2.empty()){
            ans.push_back(st2.top()->val);
            st2.pop();
        }
        
        return ans;
    }
```

`3.2 Using 1 Stack` -

![take U forward - L12  Iterative Postorder Traversal using 1 Stack C++ Java Binary Trees  NzIGLLwZBS8 - 1536x864 - 9m14s](https://user-images.githubusercontent.com/35686407/172042915-678e58ee-39f2-47a8-ad01-c14f2d9cc774.png)

- As we do in Recursion
- Go to left left left left
- if left null , go to last left's right
- then go again to left left left
- if left is null and also , last left's right is also null,
- then we print and in returning, we print the values.

- Same thing is doing in this iterative
- Simple Steps:
    1. curr = root
    2. while curr != NULL OR stack is not empty
    3. if curr != NULL , then push curr to stack , Curr = Curr->left
    4. if Curr == NULL , i.e., we got left as NULL , trying to move in right
    5. then temp = stack top's right
    6. if temp != NULL , it means right exists , then we again go to left left left => curr = temp;
    7. if temp == NULL , it means right is also NULL, 
    8. then , temp = top of stack , pop the element from stack, print the element
    9. while loop again, untill stack is empty and temp == stack top right, it means we are going to print parent while returning to the parent then temp = stack top, pop from stack and print the element

```cpp
vector<int> postorderTraversal(TreeNode* root) {
        
        if(root == NULL) return {};
        
        TreeNode* curr = root;
        stack<TreeNode*> st;
        vector<int> ans;
        
        while(curr != NULL || !st.empty()){
            if(curr != NULL){
                st.push(curr);
                curr = curr->left;
            }else{
                TreeNode* temp = st.top()->right;
                
                if(temp != NULL){
                    curr = temp;
                }else{
                    temp = st.top();
                    st.pop();
                    ans.push_back(temp->val);
                    
                    while(!st.empty() && temp == st.top()->right){
                        temp = st.top();
                        st.pop();
                        ans.push_back(temp->val);
                    }
                    
                }
            }
        }
        
        return ans;
    }
```
## 8. PreOrder - PostOrder - InOrder in One Traversal

![take U forward - L13  Preorder Inorder Postorder Traversals in One Traversal C++ Java Stack Binary Trees  ySp2epYvgTE - 1536x864 - 8m36s](https://user-images.githubusercontent.com/35686407/172045217-0d85cb6e-dfb2-4afa-bbb6-36bc5d684f83.png)


- if num == 1 , preorder, num++ , push node again with new num , if left push it with num = 1
- if num == 2 , inorder, num++, push node again with new num, if right push it with num = 1
- if num == 3, postorder, we don't need to push it again

```cpp
vector<int> preorderTraversal(TreeNode* root) {
        if(root == NULL) return {};
        vector<int> pre;
        stack<pair<TreeNode*,int>> st;
        st.push({root,1});
        while(!st.empty()){
            auto pr = st.top();
            st.pop();
            
            if(pr.second == 1){
                // part of pre
                pre.push_back(pr.first->val);
                st.push({pr.first,pr.second+1});
                if(pr.first->left){
                    st.push({pr.first->left,1});
                }
            }else if(pr.second == 2){
                // part of in
                // in.push_back(pr.first->val);
                st.push({pr.first,pr.second+1});
                if(pr.first->right){
                    st.push({pr.first->right,1});
                }
            }else{
                // post.push_back(pr.first->val);
            }
        }
        return pre;
    }
```

## 9. Depth of Binary Tree

- ROOT == NULL : return 0
- return max(leftCall,rightCall) + 1;

```cpp
int maxDepth(TreeNode* root) {
        if(root == NULL) return 0;
        
        int leftHeight = maxDepth(root->left);
        int rightHeight = maxDepth(root->right);
        
        return max(leftHeight,rightHeight) + 1;
    }
```
## 10. Balaced Binary Tree

- Balaced Tree : abs(leftHeight - rightHeght) <= 1 for every node.

```cpp
int depth(TreeNode* root){
        if(root == NULL) return 0;
        
        int leftHeight = depth(root->left);
        if(leftHeight == -1) return -1;
        
        int rightHeight = depth(root->right);
        if(rightHeight == -1) return -1;
        
        if(abs(leftHeight - rightHeight) > 1) return -1; // to send it is not balanced -1 is marker
        
        return max(leftHeight,rightHeight) + 1;
    }
    bool isBalanced(TreeNode* root) {
        if(depth(root) == -1){
            return false;
        }
        return true;
    }
```
