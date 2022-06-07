# Binary Tree

[Lowest Common Ancestor](#LCA)

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

## 9. Depth/Height of Binary Tree

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

# Variations of Height of Binary Tree : From 10 to 12

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

## 11. Diameter of Binary Tree

- Longest Path between 2 Nodes.
- Path doesn't need to pass via root.

![take U forward - L16  Diameter of Binary Tree C++ Java  Rezetez59Nk - 885x498 - 2m41s](https://user-images.githubusercontent.com/35686407/172090414-27868b91-1aab-4695-9a43-0ec481e4fd24.png)

- `LeftHeight+RightHeight` for every node, max number is diameter of binary tree.
-  We have to find max(leftHeight+rightHeight) for every node.

1. Brute Force:

- Calculate Left Height and Right Height from each node, and find diameter and compare it with max value
- Do above step for all nodes.
- TC : O(n^2) , for a skewed tree.

```cpp
int height(TreeNode* root){
        if(root == NULL){
            return 0;
        }
        int lh = height(root->left);
        int rh = height(root->right);
        return 1+max(lh,rh);
        
    }
    
    void solve(TreeNode* root,int& diameter){
        if(root == NULL) return;
        
        int leftHeight = height(root->left);
        int rightHeight = height(root->right);
        
        diameter = max(diameter,leftHeight+rightHeight);
        
        solve(root->left,diameter);
        solve(root->right,diameter);
        
    }
    
    int diameterOfBinaryTree(TreeNode* root) {
        int diameter = 0;
        solve(root,diameter);
        return diameter;
    }
```
2. Optimized Solution:

- We know how to find height of tree in O(n),
- now while `finding height` from every node, `we have left height and right height` at that time, just `calculate the diameter at that time` `in height code`.
- we don't need to seperately code for the diameter.

```cpp
int height(TreeNode* root,int& diameter){
        if(root == NULL) return 0;
        
        int leftHeight = height(root->left,diameter);
        int rightHeight = height(root->right,diameter);
        
        diameter = max(diameter,leftHeight + rightHeight);
        
        return 1 + max(leftHeight,rightHeight);
    }
    
    int diameterOfBinaryTree(TreeNode* root) {
        int diameter = 0;
        int hgt = height(root,diameter);
        return diameter;
    }
```
## 12. Maximum Path Sum

- hum `maxi = max(maxi,node->val+leftSum+rightSum)` isliye le rhe hai, ho skta hai path 20 se start ho max vala, na ki root se.
- `return node->val + max(leftSum,rightSum)` -> isse hum root ko bta rhe hai, tumhe konsi side mae jana chahiye left ya right side jga se max sum aara ho.
- ho skta hai andar child node se start krke andar khi max sum aara hai to uske liye hmne `maxi = max(maxi,node->val+leftSum+rightSum)` vala rkha hai. umbrealla shape curve andar bhi bnkr max sum deri ho maybe.
- Children node act as root, and say ki max path sum mujse hoke jayega,
- return mae hum upar direction bta rhe hai ki aap kis trf ja skte hai max sum pane ke liye
 
![take U forward - L17  Maximum Path Sum in Binary Tree C++ Java  WszrfSwMz58 - 853x480 - 5m29s](https://user-images.githubusercontent.com/35686407/172124299-159da4cd-7b60-46b0-8c23-5c67a38cf1d8.png)

![take U forward - L17  Maximum Path Sum in Binary Tree C++ Java  WszrfSwMz58 - 1536x864 - 13m40s](https://user-images.githubusercontent.com/35686407/172124242-ee6bb6f2-78a7-458d-addf-a5d7a19d2441.png)

- Now , also we have to ignore the negative Path Sums, because it will lead more negative to ans, so we ignore negative path sums. and instead negative take 0.

![take U forward - L17  Maximum Path Sum in Binary Tree C++ Java  WszrfSwMz58 - 853x480 - 15m04s](https://user-images.githubusercontent.com/35686407/172125253-7a8f06b0-7fe4-47cb-8b2b-21a62dfe354c.png)

```cpp
int pathSum(TreeNode* root,int& ans){
        if(root == NULL) return 0;
        
        int lSum = pathSum(root->left,ans);
        int rSum = pathSum(root->right,ans);
    
        lSum = max(0,lSum); // discarding if left sum is negative;
        rSum = max(0,rSum); // discarding if right sum is negative;
        
        ans = max(ans,lSum + rSum + root->val); // khud ans bnna chah rha hai node
        
        return root->val + max(lSum,rSum);
    }
    int maxPathSum(TreeNode* root) {
        int ans = INT_MIN;
        int a = pathSum(root,ans);
        return ans;
    }
```
## 13. Identical Trees/Same Trees [Question](https://leetcode.com/problems/same-tree/)

- move both simultaneouly.
- if p == NULL || q == NULL , check both are same or not and return

```cpp
bool isSameTree(TreeNode* p, TreeNode* q) {
        if(p == NULL || q == NULL){
            return p == q;
        }
        
        return (p->val == q->val) 
            && isSameTree(p->left,q->left)
            && isSameTree(p->right,q->right);
    }
```
## 14. Zig-Zag Traversal [Question](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

- Same as Level Order
- Just put flag true false, true for left to right and false for right to left;

![take U forward - L19  Zig-Zag or Spiral Traversal in Binary Tree C++ Java  3OXWEdlIGl4 - 1536x864 - 5m20s](https://user-images.githubusercontent.com/35686407/172138051-882a7b09-1056-4006-9858-431b13ab3e48.png)


- 1st Way:
    - if right to left then we reverse the vec and push it
    - other wise not reverse it

```cpp
vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        if(root == NULL) return {};
        vector<vector<int>> ans;
        
        queue<TreeNode*> Q;
        Q.push(root);
        bool leftToRight = true;
        
        while(!Q.empty()){
            int size = Q.size();
            vector<int> vec;
            while(size--){
                TreeNode* node = Q.front();Q.pop();
                if(node->left) Q.push(node->left);
                if(node->right) Q.push(node->right);
                vec.push_back(node->val);
            }
            if(leftToRight == false){
                // it means right to left
                reverse(vec.begin(),vec.end());
                leftToRight = true;
            }else{
                leftToRight = false;
            }
            ans.push_back(vec);
        }
        return ans;
    }
```

- 2nd Way
    - Saving the Reverse Time
    - Initialze the vector of size
    - then `index = i` if `left to right is true`, `otherwise` it's stored in last index so `index = size - 1 - i`

```cpp
vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> ans;
        if(root == NULL) return ans;
        
        queue<TreeNode*> Q;
        Q.push(root);
        bool leftToRight = true;
        
        while(!Q.empty()){
            int size = Q.size();
            vector<int> vec(size);
            
            // level start
            for(int i = 0 ; i < size ; i++){
                TreeNode* node = Q.front();
                Q.pop();
                
                // if LR is true -> we put from front in vector
                // if LR is false -> we put from back in vector
                int index = leftToRight ? i : size - 1 - i;
                
                vec[index] = node->val;
                
                if(node->left) Q.push(node->left);
                
                if(node->right) Q.push(node->right);
                
            }
            // level end
            leftToRight = !leftToRight;
            ans.push_back(vec);
        }
        return ans;
    }
```

## 15. Boundary Traversal [Question](https://practice.geeksforgeeks.org/problems/boundary-traversal-of-binary-tree/1#)

1. Anti-Clock Wise

- 3 Steps:
    - Take Left Boundary, excluding leaf nodes
    - TakeLeaf Nodes from left to right
    - Take Right Boundary, in reverse Direction, exclusing leaf nodes

- Take Left Boundary:
    - From Root , go to Left , Left , Left , Left 
    - if Left not exists go to right
    - then again Left Left Left

- Take Leaf Nodes:
    - It's Left and Right both are NULL.
    - Use InOrder Traversal, not preorder or levelorder because, maybe some leafs are on upper level.
    - Left ki trf jao, right ki trf jao, jb end pr pocho leaf node pr add krte jao.
 
 - Take Right Boundary in Reverse:
     - From Root, Take Right Right Right
     - if Right not exists go to Left 
     - then again Right Right Right
     - put all in stack, so when you pop, it's in reverse direction.
     
![take U forward - L20  Boundary Traversal in Binary Tree C++ Java  0ca1nvR0be4 - 885x498 - 6m41s](https://user-images.githubusercontent.com/35686407/172161626-54c287d0-9638-4353-a3b8-ab14cad4e2fe.png)

```cpp
    bool isLeaf(Node* root){
        return (!root->left && !root->right);
    }
    
    void addLeftBoundary(Node* root,vector<int>& ans){
        Node* cur = root->left;
        while(cur){
            if(!isLeaf(cur)) ans.push_back(cur->data);
            if(cur->left) cur = cur->left;
            else cur = cur->right;
        }
    }
    
    void addLeaf(Node* root,vector<int>& ans){
        if(isLeaf(root)){
            ans.push_back(root->data);
            return;
        }
        if(root->left) addLeaf(root->left,ans);
        if(root->right) addLeaf(root->right,ans);
    }
    
    void addRightBoundary(Node* root,vector<int>& ans){
        Node* cur = root->right;
        stack<int> st;
        while(cur){
            if(!isLeaf(cur)) st.push(cur->data);
            if(cur->right) cur = cur->right;
            else cur = cur->left;
        }
        while(!st.empty()){
            ans.push_back(st.top());st.pop();
        }
    }
    
    vector <int> boundary(Node *root)
    {
        vector<int> ans;
        if(root == NULL) return ans;
        if(!isLeaf(root)) ans.push_back(root->data);
        addLeftBoundary(root,ans);
        addLeaf(root,ans);
        addRightBoundary(root,ans);
        return ans;
    }
```

2. Clockwise

- 3 Steps:
    - Take Right Boundary, excluding leaf nodes , right right right if not left then right right right
    - TakeLeaf Nodes from right to left , recursive, go to right then left
    - Take Left Boundary, in reverse Direction, exclusing leaf nodes , left left left if not right then left left left, reverse and then add in ans.


## 16. Vertical Order Traversal:

- `map<int,map<int,multiset<int>>> mp` , it represents vertical , level , node value (sorted order, having same value therefore multiset)
- `class cluster` , store [ vertical, level, node ] as single box/entity.
- Do, level order, and if left then vertical - 1, and if right then vertical + 1

![take U forward - L21  Vertical Order Traversal of Binary Tree C++ Java  q_a6lpbKJdw - 885x498 - 5m33s](https://user-images.githubusercontent.com/35686407/172165987-d5312ed9-ca55-4d73-a9d9-d081be147eae.png)


![take U forward - L21  Vertical Order Traversal of Binary Tree C++ Java  q_a6lpbKJdw - 1435x807 - 7m40s](https://user-images.githubusercontent.com/35686407/172165854-7fe468f7-fc9a-4bea-9bcb-989fef44cd92.png)

```cpp
class Solution {
    
    class cluster{
        public:
            int vertical;
            int level;
            TreeNode* node;
            cluster(int _v,int _l,TreeNode* _n){
                this->vertical = _v;
                this->level = _l;
                this->node = _n;
            }
    };
    
public:
    vector<vector<int>> verticalTraversal(TreeNode* root) {
        if(root == NULL) return {};
        vector<vector<int>> ans;
        
        map<int,map<int,multiset<int>>> mp;
        queue<cluster> Q;
        Q.push(cluster(0,0,root));
        
        while(!Q.empty()){
            int size = Q.size();
            while(size--){
                auto cl = Q.front();
                Q.pop();
                int v = cl.vertical;
                int lvl = cl.level;
                TreeNode* node = cl.node;
                
                mp[v][lvl].insert(node->val);
                
                if(node->left){
                    Q.push(cluster(v-1,lvl+1,node->left));
                }
                
                if(node->right){
                    Q.push(cluster(v+1,lvl+1,node->right));
                }
            
            }
        }
        
        for(auto& vertical:mp){
            vector<int> vec;
            for(auto& level:vertical.second){
                for(auto& val:level.second){
                    vec.push_back(val);
                }
            }
            ans.push_back(vec);
        }
        
        return ans;
    }
};
```

- we can also use for loop as

```cpp
for(auto& vertical:ds){
            vector<int> smallAns;
            for(auto& level:vertical.second){
                smallAns.insert(smallAns.end(),level.second.begin(),level.second.end());
            }
            ans.push_back(smallAns);
        }
```

## 17. Top View of Binary Tree (Vertical Order Traversal Line Concept)

![take U forward - L22  Top View of Binary Tree C++ Java  Et9OCDNvJ78 - 853x480 - 2m50s](https://user-images.githubusercontent.com/35686407/172295920-7b53b66e-86b3-42e2-9345-98dcbdd11aab.png)

![take U forward - L22  Top View of Binary Tree C++ Java  Et9OCDNvJ78 - 885x498 - 7m16s](https://user-images.githubusercontent.com/35686407/172296433-377c437b-1b62-4a4d-94d5-bf470b1c5715.png)


- First Node in every line is my Top View
- Using Level Order
- Not recursion because : Suppose we do inorder traversal, when you reach node 6, it's not the first node in that line, 3 is the first node, so we have to write the seperate logic for the height of the tree, so in that line, min height node is taken, so it's not more intuative, this vertical order is intuative.
- First time visit on line and find node is my top view node, (didn't update when you find line already in map)
- Map of Line and Node . Queue of Line and Node

```cpp
vector<int> topView(Node *root)
    {
        queue<pair<int,Node*>> Q; // vertical,node
        map<int,int> mp; // vertical,node val
        
        Q.push({0,root});
        
        while(!Q.empty()){
            int size = Q.size();
            while(size--){
                auto pr = Q.front();
                Q.pop();
                int v = pr.first;
                Node* node = pr.second;
                
                if(mp.find(v) == mp.end()){
                    // if v is not found in map, put, if found dont do anything,
                    // because already first node is present
                    mp[v] = node->data;
                }
                
                if(node->left) Q.push({v-1,node->left});
                if(node->right) Q.push({v+1,node->right});
                
            }
        }
        
        vector<int> ans;
        for(auto& pr:mp){
            ans.push_back(pr.second);
        }
        
        return ans;
    }
```

## 18. Bottom View of Binary Tree

![take U forward - L23  Bottom View of Binary Tree C++ Java  0FtVY6I4pB8 - 885x498 - 3m32s](https://user-images.githubusercontent.com/35686407/172299268-11a73f60-41b8-4425-95df-b313f93dcedc.png)


- Similar as Top view, 
- difference is only that , in top view , node is first node of vertical line
- in this node is last node of vertical line
- so , we have to update the value in map, again and again,
- therefore we remove the if condition of mp.find in top view, which only allow us to put value only once.
- So, in while loop just write: 
- `mp[v] = node->data` , there will be no if condition.

## 19. Right/Left Side of Binary Tree.

> Note : Tell Interview the Recursive Case, very important.

#### Right View:

![take U forward - L24  RightLeft View of Binary Tree C++ Java  KV4mRzTjlAk - 1536x864 - 11m12s](https://user-images.githubusercontent.com/35686407/172302565-1ad48c4f-1604-4053-bb76-1b28f386cf53.png)

> Worst Cast of Level Order: TC : O(n) and SC : O(n) , for full binary tree, stores level all nodes

> In Recursive: Since we are moving recursve , TC : O(n) and SC : O(H) , Height of the tree, in skew , O(N). Recursive will used when we have less space provided.

> Recursive : Code is short and crisp.

- Recurson Method : `Reverse PreOrder Traversal`
    - In PreOrder : Root , Left, Right
    - In Reverse PreOrder : Root , Right , Left
    - So, storing is the way, as vec.size() == level then vec.push_back(val) ,
    - this works as , vec.size() == level tells, wheather you came to that level for the first time or not, if you came at that level for the first time,
    - then add the value.

```cpp
    vector<int> ans;
    
    void rightView(Node* root,int level){
        if(root == NULL) return;
        if(ans.size() == level){
            // it tells you came to that level for the first time or not,
            // if yes, then push.
            ans.push_back(root->data);
        }
        rightView(root->right,level+1);
        rightView(root->left,level+1);
    }
    
    vector<int> rightView(Node *root)
    {
        rightView(root,0);
        return ans;
    }
```

- Itreative Method : Level Order
    - Last node of every level.

```cpp
vector<int> rightView(Node *root)
    {
       // Your Code here
       queue<Node*> Q;
       vector<int> ans;
       
       Q.push(root);
       
       while(!Q.empty()){
           int size = Q.size();
           for(int i = 0; i < size ; i++){
               Node* node = Q.front();Q.pop();
               
               if(i == size-1) ans.push_back(node->data);
               
               if(node->left) Q.push(node->left);
               if(node->right) Q.push(node->right);
               
           }
       }
       
       return ans;
    }
```

#### Left View of Binary Tree
- Recursive: 
    - Do PreOrder Traversal
    - Root Left Right
    - Push in ans vector, when you came to that level for the firs time.

- Iterative
    - Level Order Traversal
    - First Node of Every level.

## 20. Check for Symmetrical Binary Tree

![take U forward - L25  Check for Symmetrical Binary Trees C++ Java  nKggNAiEpBE - 1536x864 - 1m11s](https://user-images.githubusercontent.com/35686407/172306383-1f32bf20-5fca-439a-9539-3f686335ad53.png)

![take U forward - L25  Check for Symmetrical Binary Trees C++ Java  nKggNAiEpBE - 1536x864 - 5m27s](https://user-images.githubusercontent.com/35686407/172306398-8eb87e07-1bc0-4188-9a04-b8c1cd8079df.png)

1. TC : O(n)
2. SC : in worst ~ O(n)

- if we draw mirror on root,
- hme pta hai mirror ki property, left ~ right dekhega
- right ~ left dekhega,
- to hum kuch ese traverse krenge, ki mirror ke left mae jb left mae jaye, to mirror ke right mae hum right ko jaye
- means left ke corresponding right
- right ke correspoinding left
- Root->left : ROOT LEFT RIGHT
- Root->right : ROOT RIGHT LEFT
- and now same as identical check of binary tree

```cpp
bool isSymmetric(TreeNode* p,TreeNode* q){
        if(p == NULL || q == NULL){
            return p == q;
        }

        return (p->val == q->val) &&
               isSymmetric(p->left,q->right) &&
               isSymmetric(p->right,q->left);
}
    
bool isSymmetric(TreeNode* root) {
        if(root == NULL) return true;
        return isSymmetric(root->left,root->right);
}
```
## 21. Node to Root Path:

![take U forward - L26  Print Root to Node Path in Binary Tree C++ Java  fmflMqVOC7k - 1536x864 - 7m12s](https://user-images.githubusercontent.com/35686407/172312209-95f5237e-f7ed-4c34-9256-5b0e76aa7ca4.png)

- We will use inOrder Traversal,
- The simple you use, the simple explanation will be and its simple to tell to interviewer
- niche jate wkt add krte jao nodes ko
- if node left and right dono jagah na mile to current val ko ans mae se remove kr do
- if ek bhi jgh mil jaye either left or right , just return ans
- ye pta lgane ke liye node mila ya nhi, hum bool ~ true,false ka use kr rhe hai.

```cpp
bool rootToNode(TreeNode* root,int target,vector<int>& ans){
        if(root == NULL) return false;
        
        if(root->val == target){
            ans.push_back(target);
            return true;
        }else{
            ans.push_back(root->val);
        }
        
        bool left = rootToNode(root->left,target,ans);
        if(left == true) return true;
        
        bool right = rootToNode(root->right,target,ans);
        if(right == true) return true;
        
        // if both false, pop back
        
        ans.pop_back();
        
        return false;
        
    }
    
    vector<int> rootToNodePath(TreeNode* root,int target){
        vector<int> ans;
        bool res = rootToNode(root,target,ans);
        return ans;
    }
```
## 22. Root to Leaf Path

- Just same as Root to Node Path,
- Just difference is, we will go to the leaf.
- we wi

```cpp
void Paths(Node* root,vector<int>& ds,vector<vector<int>>& ans){
    if(root->left == NULL && root->right == NULL){
        //leaf node , left and right both not exists
        ds.push_back(root->data); // add data to ds
        
        ans.push_back(ds); // push ds to ans , as we are in leaf
        
        ds.pop_back(); // pop current data from ds
        
        return;
    }
    
    ds.push_back(root->data); // push data to ds
    
    if(root->left) Paths(root->left,ds,ans); // call when left exists
    if(root->right) Paths(root->right,ds,ans); // call when right exists
    
    ds.pop_back(); // added current data will be popped
    
} 

vector<vector<int>> Paths(Node* root)
{
    vector<vector<int>> ans;
    vector<int> ds;
    Paths(root,ds,ans);
    return ans;
}
```
## 23. LCA

- Lowest Common Ancestor

#### Brute Force

![take U forward - L27  Lowest Common Ancestor in Binary Tree LCA C++ Java  _-QHfMDde90 - 1435x807 - 4m05s](https://user-images.githubusercontent.com/35686407/172331398-6e0d4d82-54b0-4b3e-aad4-6546ab550eee.png)

Steps:
    - Node to Root Path of each node,
    - traverse from front of both path,
    - if they are same, go head
    - moment when two nodes didn't match , the LCA is just uske pichle wala
    - TC : O(2n)
    - SC : O(2n)

```cpp
bool RootToNodePath(TreeNode* root,TreeNode* target,vector<TreeNode*>& path){
        if(root == NULL) return false;
        
        if(root == target){
            path.push_back(root);
            return true;
        }
        
        path.push_back(root);
        
        bool left = RootToNodePath(root->left,target,path);
        if(left == true) return true;
        
        bool right = RootToNodePath(root->right,target,path);
        if(right == true) return true;
        
        path.pop_back();
        return false;
    }
    
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        vector<TreeNode*> path1,path2;
        
        RootToNodePath(root,p,path1);
        RootToNodePath(root,q,path2);
        
        TreeNode* prev = NULL;
        
        int n = path1.size();
        int m = path2.size();
        
        int i,j;
        i = j = 0;
        
        while(i < n && j < m){
            if(path1[i] == path2[j]){
                prev = path1[i];
                i++;
                j++;
            }else{
                break;
            }
        }
        
        return prev;
    }
```

#### Optimized (DFS Traversal) , Left Right Work
- Move Left
- Move Right
- then work
- Moment when you find one of the node from both
- instead of going aage return that number , in this case 4
- left and right both return null then return null,
- from left null , from right its 7
- return 7 not null,
- when going to 2 , we found from left 4 and from right 7
- that signify, what 2 is lca of both nodes.
- TC : O(n)
- SC : O(n) in worst cast, skewed tree, otherwise O(H)

![take U forward - L27  Lowest Common Ancestor in Binary Tree LCA C++ Java  _-QHfMDde90 - 853x480 - 9m10s](https://user-images.githubusercontent.com/35686407/172333456-9ed3260e-a3a0-4355-b318-2119555dd7eb.png)

```cpp
TreeNode* lca(TreeNode* root,TreeNode* p,TreeNode* q){
        if(root == NULL) return NULL;
        if(root == p) return p;
        if(root == q) return q;
        
        TreeNode* left = lca(root->left,p,q);
        TreeNode* right = lca(root->right,p,q);
        
        if(left == NULL){
            return right;
        }else if(right == NULL){
            return left;
        }else{
            return root;
        }
        
    }
```

## 24. Max Width of Binary Tree

![take U forward - L28  Maximum Width of Binary Tree C++ Java  ZbybYvcVLks - 1435x807 - 7m17s](https://user-images.githubusercontent.com/35686407/172383962-925331dc-ee01-4024-b5b1-426cc4cda9ec.png)


![take U forward - L28  Maximum Width of Binary Tree C++ Java  ZbybYvcVLks - 1435x807 - 9m04s](https://user-images.githubusercontent.com/35686407/172383934-cca99e15-feae-48eb-a123-dc18447ccdcb.png)


![take U forward - L28  Maximum Width of Binary Tree C++ Java  ZbybYvcVLks - 1435x807 - 9m35s](https://user-images.githubusercontent.com/35686407/172383908-59d5b71d-266a-4ce5-a773-169e36ecde82.png)


![take U forward - L28  Maximum Width of Binary Tree C++ Java  ZbybYvcVLks - 1435x807 - 11m40s](https://user-images.githubusercontent.com/35686407/172383859-014d6322-019b-484f-ace6-cf59e9cbd161.png)


![take U forward - L28  Maximum Width of Binary Tree C++ Java  ZbybYvcVLks - 1435x807 - 14m33s](https://user-images.githubusercontent.com/35686407/172383822-d922d12b-0bac-476a-b2b6-e028bc782bbc.png)


![take U forward - L28  Maximum Width of Binary Tree C++ Java  ZbybYvcVLks - 1435x807 - 15m29s](https://user-images.githubusercontent.com/35686407/172383795-38aed705-28a1-4382-8c56-ba3e5fb50503.png)
