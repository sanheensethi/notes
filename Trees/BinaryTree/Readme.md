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

```cpp
int widthOfBinaryTree(TreeNode* root) {
        
        if(root == NULL) return 0;
        
        long long ans = 0;
        queue<pair<TreeNode*,long long>> Q;
        Q.push({root,0});
        
        while(!Q.empty()){
            long long min = Q.front().second;
            int size = Q.size();
            long long first,last;
            for(int i = 0; i < size ; i++){
                auto pr = Q.front();
                Q.pop();
                
                long long cur_idx = pr.second - min;
                TreeNode* node = pr.first;
                
                if(i == 0) first = cur_idx;
                if(i == size-1) last = cur_idx;
                
                if(node->left) Q.push({node->left,2*cur_idx+1});
                if(node->right) Q.push({node->right,2*cur_idx+2});
            }
            ans = max(ans,last-first+1);
        }
        
        return (int)ans;
    }
```

## 25. Children Sum Property

- left child + right child sum = node value
- is problem mae hum upar vali condition follow krte hai,
- if upar vali condition follow nhi hoti hai, to hme allow hia ki hum kisi bhi node ki value increase krde 1 se with any number of times but hum fr decrease ni kr skte.
- Examoke:

![take U forward - L29  Children Sum Property in Binary Tree O(N) Approach C++ Java  fnmisPM6cVo - 1536x864 - 3m24s](https://user-images.githubusercontent.com/35686407/172502461-a469a8ae-6177-4448-9001-3911f4074b3f.png)

> you might think in this problem that what's the big deal, add 35 and 10 then update the node value to 45, pr ye problem dikhne mae jitni aasan lgti hai , utni hai nhi. niche vala testcase dekho

![take U forward - L29  Children Sum Property in Binary Tree O(N) Approach C++ Java  fnmisPM6cVo - 1536x864 - 4m47s](https://user-images.githubusercontent.com/35686407/172502786-eeed2689-bc45-41e1-b00c-af3197b21296.png)

> is testcase mae agar leaf se increment kre to nodes ki value change hui 8 and 31 mae, but but, root ki value 50 hai lekin, 31+8 = 40 , and 50 ko hum decrement nhi kr skte srf increment kr skte hai,

- Question is convert binary tree to `any binary tree which follow children sum property` , we have to take advantage of that.

- use recursive traversal, go left, go right and come back

Steps:
   - niche jate hue sum kro `left child + right child` if, `< node value` then 
   - `update` `left child` and `right child` with `node value`
   - if `left child + right child > node value` then
   - `update the node value`
   - iske baad go to left and then right
   - ab upar aate wkt values ko fr se update kro, `left value + right value = node value`,
   - kyuki ho skta hai child change ho gye ho.

- Intuation:
   - while going down, hum make sure kr rhe hai, ki sum ki shortage na pde, to hum unko bda kr rhe hai niche jate hue taki jb upar vapis aaye to shortage na ho. 
   - while going down, increase the values as max possible so not be short in sum, tbhi hum root ki value se change kr rhe hai, if hmara left child + right child < sum
   - while comming back, add and update the value.
 
- This algorithm, does not gurantee that values are less incremented, 
- but this guranted that, you will get children sum property value.

```cpp
void childrenSum(Node* root){
    if(root == NULL) return;

    int child = 0;

    if(root->left) child += root->left->val;
    if(root->right) child += root->right->val;

    if(child >= root->val){
        root->val = child;
    }else{
        if(root->left) root->left->val = root->val;
        if(root->right) root->right->val = root->val;
    }

    childrenSum(root->left);
    childrenSum(root->right);

    int total = 0;

    if(root->left) total += root->left->val;
    if(root->right) total+= root->right->val;

    if(root->left or root->right) root->val = total;

}
```

## 26.Check childern sum Property [Question](https://practice.geeksforgeeks.org/problems/children-sum-parent/1#)

```cpp
int isSumProperty(Node *root)
    {
     if(root == NULL) return 1;
     if(!root->left and !root->right) return 1;
     int child = 0;
     if(root->left) child += root->left->data;
     if(root->right) child += root->right->data;
     
     if(root->data != child) return 0;
     
     int left = isSumProperty(root->left);
     
     if(left == 0) return 0;
     
     int right = isSumProperty(root->right);
     
     if(right == 0) return 0;
     
     return 1;
    }
```
## 27. All Nodes Distance K in Binary Tree [Question](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/)

#### Approach 1:

![take U forward - L30  Print all the Nodes at a distance of K in Binary Tree C++ Java  i9ORlEy6EsI - 885x498 - 10m52s](https://user-images.githubusercontent.com/35686407/172534812-ba179ba2-7a93-4fbd-852e-6301e67a5342.png)

- isme hmare paas niche ki trf jane ka to rasta hai lekin vapis parent ke paas jane ka nhi, 
- to hum isme pehle nodes ke parent ko ek Map mae store kr lenge, level order ke through
- and after that, hum level order se chlenge by maintainning int distance = 0 
- ek visited node ka map bhi rkhna hoga, jo ye btayega , ki hum node pr already visit kr chuke hai ya nhi.
- agar distance == k to break;
- now, in level order , starting from given target (starting node)and visited[target] = true, hum uske `left, right and parent` pr `traverse krenge`, and jo visited nhi hoga, usko queue mae dalkr visited mark kr denge.
- jese hi distance = k aauya we break;
- ab jo queue mae pda hai vo hmara ans hai.

```cpp
class Solution {
public:
    void makeParent(TreeNode* root,unordered_map<TreeNode*,TreeNode*>& parent){
        queue<TreeNode*> Q;
        Q.push(root);
        while(!Q.empty()){
            int size = Q.size();
            while(size--){
                TreeNode* node = Q.front();Q.pop();
                if(node->left){
                    Q.push(node->left);
                    parent[node->left] = node;
                }
                if(node->right){
                    Q.push(node->right);
                    parent[node->right] = node;
                }
            }
        }
    }
    
    vector<int> distanceK(TreeNode* root, TreeNode* target, int k) {
        vector<int> ans;
        if(root == NULL) return ans;
        
        unordered_map<TreeNode*,TreeNode*> parent;
        
        makeParent(root,parent);
        
        unordered_map<TreeNode*,bool> visited;
        
        int dis = 0;
        queue<TreeNode*> Q;
        
        Q.push(target);
        visited[target] = true;

        while(!Q.empty()){
            int size = Q.size();
            if(dis == k) break;
            dis++;
            while(size--){
                TreeNode* node = Q.front();Q.pop();
                
                if(node->left && visited[node->left] == false){
                    Q.push(node->left);
                    visited[node->left] = true;
                }
                if(node->right && visited[node->right] == false){
                    Q.push(node->right);
                    visited[node->right] = true;
                }
                if(parent.find(node) != parent.end() && visited[parent[node]] == false){
                    Q.push(parent[node]);
                    visited[parent[node]] = true;
                }
            }
        }
        
        while(!Q.empty()){
            ans.push_back(Q.front()->val);
            Q.pop();
        }
        return ans;
    }
};
```
#### Approach 2:

- hum `node to root` tk ka path find krenge
- fr `node to root` tk ke path mae ek ek traverse krke print k level down nodes ko print krenge
- jisme k 1 se decrement hota rhega
- example : print 5 distance nodes from node 7 in given finure example,
- path = [7 2 5 3] , 
    - ab 7 se 5 distance/level niche ki node ans mae dalenge, 
    - 2 se 4 level down ke nodes ans mae dalenge, 
    - 5 se 3 level down ke nodes ans mae dalenge, 
    - 3 se 2 level down niche ke nodes ans mae dalenge
 - ye hmara ans nhi aaya abhi , kyuki, 3 se agar 2 level niche dekhe to 6 and 2 is also nodes , jo ans mae aa skte hai, 
 - to hme vo ans mae nhi chahiye, iske liye jb hum k level down bna rhe honge uske ek node pass krenge jo ek side ko block kr dega
 - path[i-1] is blocker, example : 2 se jb 4 level niche print krenge to hme 7 ki trf nhi jana, kyuki 7 apna kaam kr chuka hai
 - simmilarly 3 se jb 2 level niche ki trf print krnnge to hme 5 ki trf nhi jana kyuki 5 apna kaam already kr chuka hai.
 - blocker node for i = 1 to n-1 is path[i-1]
 - and for i == 0 is NULL
 
 ```cpp
 bool nodeToRootPath(TreeNode* root,TreeNode* target,vector<TreeNode*>& path){
        if(root == NULL) return false;
        
        if(root == target){
            path.push_back(target);
            return true;
        }
        
        bool left = nodeToRootPath(root->left,target,path);
        if(left == true){
            path.push_back(root);
            return true;
        }
        bool right = nodeToRootPath(root->right,target,path);
        if(right == true){
            path.push_back(root);
            return true;
        }
        return false;
    }
    
    void saveKLevelDown(TreeNode* root,int k,TreeNode* blocker,vector<int>& ans){
        if(root == NULL || root == blocker) return;
        if(k == 0){
            ans.push_back(root->val);
            return;
        }
        saveKLevelDown(root->left,k-1,blocker,ans);
        saveKLevelDown(root->right,k-1,blocker,ans);
    }
    
    vector<int> distanceK(TreeNode* root, TreeNode* target, int k) {
        vector<TreeNode*> path;
        nodeToRootPath(root,target,path);
        int n = path.size();
        vector<int> ans;
        for(int i = 0;i < n; i++){
            TreeNode* blocker = i == 0 ? NULL : path[i-1];
            saveKLevelDown(path[i],k-i,blocker,ans);
        }
        return ans;
    }
 ```
#### Approach 3: (More Optimized above code)

- concept same hai, bs frk itna hia ki hum save nhi krenge path,
- kyuki stack se jb return krenge to path vhi aayega jo vector mae save hai, to kyu na usi recursion call mae hum printKLevelDown ko call kr le
- ab ye hoga kese ? , to
- jb ROOT == NULL return -1, jo ye darshata hai ki hme node nhi mila
- ab jb node mil jata hai, tb hm vha se printKLevelDown call kr denge, jisme niche ke k levels ke print kr denge
- ab jb pichle ke paas jayenge jese 7 se 5 pr gya, ab 5 ko print krna hoga 4 level down, but hme pta kese chlega 4 level krna hai ?
- to jb hum target found hone pr ans save kr kenge tb, hum return mae 1 bhejenge jo ye btayega ki ab jo pichli stack trace ka node hai vo 1 distance apart hai mujse
- ese hi left+1 return krte rhenge, and k-left levels print krte rhenge
- ab blocker node ki baat kre to vo vhi hoga jha se 1 aayega, either left or right.

```cpp
void saveKLevelDown(TreeNode* root,int k,TreeNode* blocker,vector<int>& ans){
        if(root == NULL || root == blocker) return;
        
        if(k == 0){
            ans.push_back(root->val);
            return;
        }
        
        saveKLevelDown(root->left,k-1,blocker,ans);
        saveKLevelDown(root->right,k-1,blocker,ans);
        
    }
    
    int nodeToRootPath(TreeNode* root,TreeNode* target,int k,vector<int>& ans){
        if(root == NULL) return -1;
        
        if(root == target){
            saveKLevelDown(root,k,NULL,ans); // NULL is blocker
            return 1;
        }
        
        int left = nodeToRootPath(root->left,target,k,ans);
        if(left != -1){
            saveKLevelDown(root,k-left,root->left,ans); // root->left is blocker
            return left+1;
        }
        int right = nodeToRootPath(root->right,target,k,ans);
        if(right != -1){
            saveKLevelDown(root,k-right,root->right,ans); // root->right is blocker
            return right+1;
        }
        return -1;
    }
    
    vector<int> distanceK(TreeNode* root, TreeNode* target, int k) {
        vector<int> ans;
        if(root == NULL) return ans;
        
        nodeToRootPath(root,target,k,ans);
        
        return ans;
    }
```

## 28. Burning Tree [Question](https://practice.geeksforgeeks.org/problems/burning-tree/1#)

- Same as nodes at k distance apart from given node, 
- just difference is that, we complete the while loop not breaking it , 
- because we have to burn all nodes.
- A node will burn its left child, right child and parent,
- now to go to the parent we need pointer to the parent, so for that we put that in hashmap, because there is no upward pointer
- then starting from the node, we burn all the tree.

```cpp
class Solution {
  public:
  
    Node* makeParent(Node* root,int target,unordered_map<Node*,Node*>& parent){
        Node* res = NULL;
        queue<Node*> Q;
        Q.push(root);
        while(!Q.empty()){
            int size = Q.size();
            while(size--){
                Node* node = Q.front();
                Q.pop();
                if(node->data == target) res = node;
                if(node->left){
                    parent[node->left] = node;
                    Q.push(node->left);
                }
                if(node->right){
                    parent[node->right] = node;
                    Q.push(node->right);
                }
            }
        }
        return res;
    }
  
    int minTime(Node* root, int target) 
    {
        unordered_map<Node*,Node*> parent;
        Node* targetAd = makeParent(root,target,parent);
        
        unordered_map<Node*,bool> visited;
        
        queue<Node*> Q;
        Q.push(targetAd);
        visited[targetAd] = true;
        
        int t = 0;
        
        while(!Q.empty()){
            int size = Q.size();
            bool flag = false;
            while(size--){
                Node* node = Q.front();
                Q.pop();
                if(node->left && !visited[node->left]){
                    flag = true;
                    Q.push(node->left);
                    visited[node->left] = true;
                }
                if(node->right && !visited[node->right]){
                    flag = true;
                    Q.push(node->right);
                    visited[node->right] = true;
                }
                if(parent.find(node) != parent.end() && !visited[parent[node]]){
                    flag = true;
                    Q.push(parent[node]);
                    visited[parent[node]] = true;
                }
            }
            if(flag) t++;
        }
        return t;
    }
};
```
## 29. Count total number of nodes in `Complete Binary Tree`

#### Approach 1:

- Brute Force:
        
![take U forward - L32  Count total Nodes in a COMPLETE Binary Tree O(Log^2 N) Approach C++ Java  u-yWemKGWO0 - 885x498 - 3m10s](https://user-images.githubusercontent.com/35686407/172674823-438f2c38-edeb-4619-a6d0-124aba6e8003.png)

#### Approach 2:
- Optimized:
    - In completer binary tree, hme ye pta hai ki total number of nodes is 2^(height) - 1 ,
    - but problem ye hai ki, ho skta hai right side mae last level mae right vali node exists hi na krti ho,
    - to hum smartly use krenge height of binary tree ke logic ko,
    - if leftHeight == rightHeight , it means we have complete binary tree then nodes = 2^(height) - 1.
    - but if leftHeight != rightHeight , it means we have to consider left subtree seperate and right subtree seperate and count nodes by doing same procedure again.
    - now if leftHeight != righHeight ~ return 1 + leftNodes + rightNodes
    - if leftHeight == rightHeight ~ return 2^(height) - 1
    - ab question ye aata hai ki height kese calculate kre ? vhi recursion vale method se ?
    - nhi, as hme complete binary tree given hai, to left vali nodes sari hogi , to height of left binary tree is node = node->left (mtlb left left left left jate rho) and count++ while node != null
    - same ese hi right side ki height ke liye node = node->right (right right right right jate rho) and count++ while node != null
    
![take U forward - L32  Count total Nodes in a COMPLETE Binary Tree O(Log^2 N) Approach C++ Java  u-yWemKGWO0 - 853x480 - 6m24s](https://user-images.githubusercontent.com/35686407/172676242-a3be9f7c-ff58-4f18-8287-a0c412b40cb1.png)

![take U forward - L32  Count total Nodes in a COMPLETE Binary Tree O(Log^2 N) Approach C++ Java  u-yWemKGWO0 - 853x480 - 10m23s](https://user-images.githubusercontent.com/35686407/172676318-c95c3f8d-52d1-4b9f-988f-91a2891677b4.png)


TC : O((logN)^2) ~ finding height is logN = Height, and at max we traverse logN nodes
SC : O(logN) ~ Auxillary Stack Space

![take U forward - L32  Count total Nodes in a COMPLETE Binary Tree O(Log^2 N) Approach C++ Java  u-yWemKGWO0 - 853x480 - 15m34s](https://user-images.githubusercontent.com/35686407/172678853-db8941c4-7100-4f2b-b212-1583f659b7b3.png)


```cpp
class Solution {
public:
    int countNodes(TreeNode* root) {
        if(root == NULL) return 0;
        
        int lHeight = findLeftHeight(root);
        int rHeight = findRightHeight(root);
        
        if(lHeight == rHeight){
            return (1<<lHeight) - 1; // pow(2,lHeight)-1
        }else{
            return 1 + countNodes(root->left) + countNodes(root->right);
        }
    }
    
    int findLeftHeight(TreeNode* node){
        int height = 0;
        while(node){
            node = node->left;
            height++;
        }
        return height;
    }
    
    int findRightHeight(TreeNode* node){
        int height = 0;
        while(node){
            node = node->right;
            height++;
        }
        return height;
    }
    
};
```

## 30. What kind of Traversels required to construct a Unique binary tree ?

a) PreOrder and PostOrder - We can't construct a unique binary tree.

![take U forward - L33  Requirements needed to construct a Unique Binary Tree Theory  9GMECGQgWrQ - 885x498 - 4m15s](https://user-images.githubusercontent.com/35686407/172679878-49b6a9a5-e27f-415b-8c78-e73f73ed7ca5.png)

b) InOrder and PreOrder - Yes
    - In PreOrder root is at first position
    - by Inorder we can figure out who is in left and who is in right of root.
    - InOrder is more important, as we have to know what is on the left of root and right of root, after seeing root in Prerder

![take U forward - L33  Requirements needed to construct a Unique Binary Tree Theory  9GMECGQgWrQ - 1536x864 - 5m30s](https://user-images.githubusercontent.com/35686407/172680132-862b936f-e9be-4afe-9126-eac05d6fab4d.png)

![take U forward - L33  Requirements needed to construct a Unique Binary Tree Theory  9GMECGQgWrQ - 1536x864 - 6m35s](https://user-images.githubusercontent.com/35686407/172680315-e75dbada-987d-457c-b1d5-2c320e303555.png)

c) InOrder and PostOrder - Yes, because Root is at last

## 31. Construct Binary Tree From PreOrder and InOrder

![take U forward - L34  Construct a Binary Tree from Preorder and Inorder Traversal C++ Java  aZNaLrVebKQ - 1536x864 - 6m41s](https://user-images.githubusercontent.com/35686407/172686750-2cf7e12b-76d8-4a50-9387-858529ea5227.png)
![take U forward - L34  Construct a Binary Tree from Preorder and Inorder Traversal C++ Java  aZNaLrVebKQ - 1435x807 - 8m16s](https://user-images.githubusercontent.com/35686407/172686774-f26d06c5-f703-417a-8426-85d16441ba58.png)
![take U forward - L34  Construct a Binary Tree from Preorder and Inorder Traversal C++ Java  aZNaLrVebKQ - 1435x807 - 9m42s](https://user-images.githubusercontent.com/35686407/172686788-ee24e424-bf10-47d6-9fbc-c85e94de68b0.png)
![take U forward - L34  Construct a Binary Tree from Preorder and Inorder Traversal C++ Java  aZNaLrVebKQ - 885x498 - 10m52s](https://user-images.githubusercontent.com/35686407/172687024-c503a119-75d8-4df2-b7d2-db40a21bacdc.png)
![take U forward - L34  Construct a Binary Tree from Preorder and Inorder Traversal C++ Java  aZNaLrVebKQ - 1536x864 - 12m37s](https://user-images.githubusercontent.com/35686407/172687231-de0ae290-8c1b-4259-8640-a0d4e64d5ae0.png)

```cpp
class Solution {
public:
    
    TreeNode* buildTree(vector<int>& preorder,vector<int>& inorder,int preStart,int preEnd,int inStart,int inEnd,unordered_map<int,int>& umap){
        if(preStart > preEnd || inStart > inEnd) return NULL;
        
        TreeNode* root = new TreeNode(preorder[preStart]);
        int idx = umap[preorder[preStart]];
        int num_ele = idx - inStart;
        
        root->left = buildTree(preorder,inorder,preStart + 1,preStart + num_ele,inStart,idx-1,umap);
            
        root->right = buildTree(preorder,inorder,preStart + num_ele + 1,preEnd,idx+1,inEnd,umap);
        
        return root;
        
    }
    
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        unordered_map<int,int> umap;
        int n = inorder.size();
        for(int i = 0;i < n; i++){
            umap[inorder[i]] = i;
        }
        
        int preStart = 0;
        int inStart = 0;
        int preEnd = n-1;
        int inEnd = n-1;
            
        TreeNode* root = buildTree(preorder,inorder,preStart,preEnd,inStart,inEnd,umap);
        return root;
    }
};
```
## 32. Construct Binary Tree from PostOrder and InOrder

![take U forward - L35  Construct the Binary Tree from Postorder and Inorder Traversal C++ Java  LgLRTaEMRVc - 1536x864 - 4m37s](https://user-images.githubusercontent.com/35686407/172761892-ed5acdb7-d2ca-4062-99ac-14e433af5b8c.png)

![take U forward - L35  Construct the Binary Tree from Postorder and Inorder Traversal C++ Java  LgLRTaEMRVc - 885x498 - 7m26s](https://user-images.githubusercontent.com/35686407/172763657-501e678f-bc0b-47e8-9fe5-997514a61c09.png)

![take U forward - L35  Construct the Binary Tree from Postorder and Inorder Traversal C++ Java  LgLRTaEMRVc - 853x480 - 9m46s](https://user-images.githubusercontent.com/35686407/172763690-aca7d819-25c9-4481-94f5-282dab636b07.png)

- TC: O(n) * O(1) ~ HashMap
- SC: O(n) + O(n) ~ Tree + Hashmap

```cpp
class Solution {
public:
    TreeNode* buildTree(vector<int>& inorder,int inStart,int inEnd,vector<int>& postorder,int postStart,int postEnd,unordered_map<int,int>& umap){
        if(postStart > postEnd || inStart > inEnd){
            return NULL;
        }
        
        TreeNode* root = new TreeNode(postorder[postEnd]);
        
        int idx = umap[postorder[postEnd]];
        int num_ele = idx - inStart;
        
        root->left = buildTree(inorder,inStart,idx-1,postorder,postStart,postStart + num_ele - 1,umap);
        root->right = buildTree(inorder,idx+1,inEnd,postorder,postStart + num_ele,postEnd-1,umap);
        
        return root;
    }
    
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        int n = inorder.size();
        
        unordered_map<int,int> umap;
        
        for(int i = 0;i < n;i++){
            umap[inorder[i]] = i;
        }
        
        return buildTree(inorder,0,n-1,postorder,0,n-1,umap);
    }
};
```
## 33. Serialize and De-Serialize a Binary Tree

- Searialize : hme binary tree ko string mae convert krna hai
- De-Searialize : hme string ko binary tree mae bnakr return krna hai
- Serialize : isme hum Level Order Traversal use kr rhe hai, NULL -> # and node ki val ko string mae convert krke str mae add kr dia with ',' seperated.
- De-Serialize : isme hum stringstream le rhe hai, jisse jariya hum input as cin jesa le payenge and input hum getline mae le rhe hai with ',' seperated, jese hi hum koi node bnate hai agar # nhi hai to usko queue mae push kr denge kyuki hum level order traversal jesa hi kaam kr rhe hai Serialize mae bhi level order hi kia tha.

- `stringstream s(data)` : create string stream object s
- `getline(s,str,',');` : s mae se str read kr rhe hai with ',' seperated
- if str == '#' aaya to NULL join kr rhe hai
- if str != '#' then , node bna rhe hai , join kr rhe hai, even queue mae bhi push kr rhe hai.

```cpp
class Codec {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        if(root == NULL) return "";
        queue<TreeNode*> Q;
        string str = "";
        Q.push(root);
        while(!Q.empty()){
            TreeNode* node = Q.front();
            Q.pop();
            if(node == NULL){
                str += "#,";
            }else{
                str += to_string(node->val) + ",";
                Q.push(node->left);
                Q.push(node->right);
            }
        }
        str.pop_back();
        cout<<str<<endl;
        return str;
    }
#define debug(x) cout<<#x<<":"<<x<<endl;
    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        if(data == "") return NULL;
        
        stringstream s(data); // stringstream object , it behave as we take input as cin
        string str = "";
        getline(s,str,','); // s mae se str read kro, and ',' mera seperator hai
        
        TreeNode* root = new TreeNode(stoi(str));
        
        queue<TreeNode*> Q;
        Q.push(root);
        
        while(!Q.empty()){
            TreeNode* node = Q.front();
            Q.pop();
            
            getline(s,str,','); // this is my left
            
            if(str == "#"){
                node->left = NULL;
            }else{
                node->left = new TreeNode(stoi(str));
                Q.push(node->left);
            }
            
            getline(s,str,','); // this is my right
            
            if(str == "#"){
                node->right = NULL;
            }else{
                node->right = new TreeNode(stoi(str));
                Q.push(node->right);
            }
        }
        
        return root;
    }
};
```

## 34. Morris Traversal (InOrder and PreOrder)

- TC ~ O(N)
- SC ~ O(1)

- Morris Traversal work krta hai Threaded Binary Tree pr.
- Tree mae parent ke paas jane ka rasta nhi hota, to hm parent ke paas jane ke liye ek thread jodte hai 

![take U forward - L37  Morris Traversal Preorder Inorder C++ Java  80Zug6D1_r4 - 885x498 - 4m45s](https://user-images.githubusercontent.com/35686407/172776081-010efbd6-89a6-46a4-b244-73ae355469a5.png)

- Now, how to traverse ?
- InOrder : LEFT ROOT RIGHT
- isme hmare paas 3 case arise hote hai:
    1. `Case 1`: agar left null hai sirf right hai, suppose kro esa root, jiska left null hai right mae srf ek element hai, ~ to hum print krke right mae move krenge
    2. `Case 2`: agar left mera null nhi hai, to uske extreme right mae jayenge
        - agar extremeRight -> right == NULL : add thread to cur (parent)
        - agar extrementRight -> right == cur : break thread, add cur val in ans, move right
    3. do this untill cur != NULL

- InOrder and PreOrder mae bs 1 line ka frk hai baki pura code same hai

```cpp
TreeNode* rightMostGuy(TreeNode* node,TreeNode* cur){
        while(node->right != NULL && node->right != cur){
            node = node->right;
        }
        return node;
    }
    
    // Morris Traversal
    #define debug(x) cout<<#x<<":"<<x<<endl;
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;
        if(root == NULL) return {};
        TreeNode* cur = root;
        while(cur != NULL){
            if(cur->left == NULL){
                ans.push_back(cur->val);
                cur = cur->right;
            }else if(cur->left != NULL){
                TreeNode* rightMost = rightMostGuy(cur->left,cur);
                if(rightMost->right == NULL){
                    rightMost->right = cur;
                    cur = cur->left;
                }else if(rightMost->right == cur){
                    rightMost->right = NULL;
                    ans.push_back(cur->val);
                    cur = cur->right;
                }
            }
        }
        return ans;
    }
```

- In PreOrder, change only one line and add onle same line
    - As we know preorder is Root Left Right
    - so, we go to root first, therefore before moving to the left we have to push value in ans, therefore after rightMost-> right = cur type ans.push_back(cur->val) in rightMost->right == NULL
    - and in rightMost->right == cur, remove the line ans.push_back(cur->val) , because that is for inorder traversal.

## 35. Flatten a Binary Tree

#### Approach 1: Brute Force (Create new TreeNodes, by traversing the Tree.)

#### Approach 2: (Changing Pointers)

![take U forward - L38  Flatten a Binary Tree to Linked List 3 Approaches C++ Java  sWf7k1x9XR4 - 885x498 - 9m12s](https://user-images.githubusercontent.com/35686407/172799605-04c5e557-8ec6-4007-a4d5-a88a8b82ca5c.png)

- In this we move like `Right Left Root` (reverse postorder)
- dry run krne se hi clear ho jayega logic or either watch [Youtube](https://youtu.be/sWf7k1x9XR4)
- TC : O(n)
- SC : ~ O(n) Auxillary Stack Space or O(H)

```cpp
TreeNode* prev = NULL;
    void flat(TreeNode* node){
        if(node == NULL) return;
        
        flat(node->right);
        flat(node->left);
        
        node->right = prev;
        node->left = NULL;
        prev = node;
    }
    void flatten(TreeNode* root) {
        flat(root);
        root = prev;
    }
```

#### Approach 3: (using stack) - dont tell to interviewer.

```cpp
void flatten(TreeNode* root) {
        if(root == NULL) return;
        
        stack<TreeNode*> st;
        st.push(root);
        TreeNode* node = NULL;
        
        while(!st.empty()){
            node = st.top();
            st.pop();
            
            if(node->right){
                st.push(node->right);
            }
            
            if(node->left){
                st.push(node->left);
            }
            
            node->left = NULL;
            if(!st.empty()){
                node->right = st.top();
            }
        }
        
    }
```
