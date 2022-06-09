# Binary Search Tree (BST)
 
## 1. Introduction

- L < N < R
- left nodes are smaller then root
- right nodes are greater then root
- Left Subtree is also BST
- Right Subtree is also BST

- Duplicates are not allowed in BST , but in some books it is given it's allowed in MIT's, but you want to insert dublicates, then
- L <= N < R
- or for dublicates , we can store (node,frequencey) in node.

> Inorder of BST is increasing order ~ non-decreasing order.

## 2. Why BST ?

- Generally not in worst, Height of Binary Search Tree log_2 (N)
- Search in BT its worst is O(N)
- Search in BST its O(logN)

![take U forward - L39  Introduction to Binary Search Tree BST  p7-9UvDQZ3w - 885x498 - 6m56s](https://user-images.githubusercontent.com/35686407/172829386-b2d600cf-c218-4b7a-b560-965082126648.png)

## 3. Search in a BST 

- TC : O(log_2 N) , where in BT : O(N)
- if target < root->val, we move to left
- if target > root->val, we move to right
- if target == root->val, we return node
- if not found return NULL
- either moving right or left, therefore TC : O(log_2 (N))

![take U forward - L40  Search in a Binary Search Tree BST C++ Java  KcNt6v_56cc - 885x498 - 3m50s](https://user-images.githubusercontent.com/35686407/172830428-e35142a1-b8b2-4bfd-bd59-f8a2fd2b8f92.png)

> Recursive:

```cpp
TreeNode* searchBST(TreeNode* root, int val) {
        if(root == NULL) return NULL;
        if(root->val == val) return root;
        if(val < root->val){
            return searchBST(root->left,val);
        }else{
            return searchBST(root->right,val);
        }
    }
```
> Iterative:

```cpp
TreeNode* searchBST(TreeNode* root, int val) {
        while(root != NULL && root->val != val){
            root = val < root->val ? root->left : root->right;
        }
        return root;
    }
```
## 4. Ceil in BST [Question](https://www.codingninjas.com/codestudio/problems/ceil-from-bst_920464?leftPanelTab=0)

- find lowest value in tree , such that `val <= key`

![take U forward - L41  Ceil in a Binary Search Tree BST C++ Java  KSsk8AhdOZA - 853x480 - 1m28s](https://user-images.githubusercontent.com/35686407/172831356-8dcbe8bf-90e7-4e0b-8fb6-7dd54ca20ee9.png)

- if key = 8, Answer = 9
- if key = 11, Answer = 11
- if key = 12, Answer = 13

> Ceil : Smallest Value >= key

- we will solve this question by taking variable ceil,
- if `key <= root->val` ceil = root->data , move left ~ agar root ki value bdi hai key se, to ho skta hai ki vo ceil ho.
- else move right
- if key == root->val ceil = root->data

```cpp
int findCeil(BinaryTreeNode<int> *node, int x){
    int ceil = -1;
    while(node){
        if(node->data == x){
            ceil = node->data;
            return ceil;
        }
        
        if(x <= node->data){
            ceil = node->data;
            node = node->left;
        }else{
            node = node->right;
        }
    }
    return ceil;
}
```
## 5. Floor in BST [Question](https://www.codingninjas.com/codestudio/problems/floor-from-bst_920457)

- which value is the `greatest value` which is `smaller then or equal` to 7 if key is 7 Answer : 6
- which is the greatest value which is smaller then or equal to 14 if key is 14 Answer : 10

![take U forward - L42  Floor in a Binary Search Tree BST C++ Java  xm_W1ub-K-w - 885x498 - 1m48s](https://user-images.githubusercontent.com/35686407/172833376-19e492b5-bfbf-4dba-bfeb-f9f97fd8e4e7.png)

> Floor =  Greatest Value <= key

- Create a variable floor as ans
- if key < root->val , move left
- if key >= root->val , 5 is smaller then 9 here, and if we want to increase 5 we have to move right. (in above figure).
- so , if key >= root->val : `floor = root->val` and move right;

```cpp
int floorInBST(TreeNode<int> * root, int x)
{
    int floor = -1;
    while(root){
        if(root->val == x){
            floor = x;
            return floor;
        }
        
        if(x < root->val){
            root = root->left;
        }else{
            floor = root->val;
            root = root->right;
        }
    }
    return floor;
}
```
## 6. Insert Given Node in BST

- Insert in such a way that leftSubtree remains BST and rightSubtree remains BST.

![take U forward - L43  Insert a given Node in Binary Search Tree BST C++ Java  FiFiNvM29ps - 885x498 - 2m09s](https://user-images.githubusercontent.com/35686407/172835534-f067707c-2658-4565-88fc-5178189dcabc.png)

- Create any one Binary Tree.
- Find Where node can be ? and insert it
- Where is leaf position.
- TC : log_2 (N)

> Recursive: 

- if val < root->val, left mae jao
- else right mae jao
- jb null pr pohcho, new node bnao us value ki and return krdo node;

```cpp
TreeNode* insertIntoBST(TreeNode* root, int val) {
        if(root == NULL) return new TreeNode(val);
        if(val < root->val){
            root->left = insertIntoBST(root->left,val);
        }else{
            root->right = insertIntoBST(root->right,val);
        }
        return root;
    }
```

> Iterative:

- take previous pointer because you will stop when you reach null,
- and we have to attach the new node to prev node from where we came to null

```cpp
TreeNode* insertIntoBST(TreeNode* root, int val) {
        TreeNode* newNode = new TreeNode(val);
        
        if(root == NULL) return newNode;
        
        TreeNode* prev = NULL;
        TreeNode* node = root;
        
        while(node){
            prev = node;
            if(val < node->val){
                node = node->left;
            }else{
                node = node->right;
            }
        }
        
        if(val < prev->val){
            prev->left = newNode;
        }else{
            prev->right = newNode;
        }
        
        return root;
    }
```
## 7. Delete Node in BST

> Method:

1. Search Node
2. Delete Node

- Node = 3 delele (Multiple answer exists)

![take U forward - L44  Delete a Node in Binary Search Tree BST C++ Java  kouxiP_H5WE - 885x498 - 2m08s](https://user-images.githubusercontent.com/35686407/172838701-4597d1a9-17df-478b-84ca-b0f0ffb197de.png)

![take U forward - L44  Delete a Node in Binary Search Tree BST C++ Java  kouxiP_H5WE - 853x480 - 3m17s](https://user-images.githubusercontent.com/35686407/172838906-fb86d290-f293-4629-bef8-5e3985ef2e7f.png)

- Everything jo bhi left subtree mae hai, vo sare smaller hai right subtree se . We will use this stuff.
- when delete 5,
- 4 is the greatest element in the left subtree ? right, so 
- take the right subtree,and attach it to extreme right of left subtree

![take U forward - L44  Delete a Node in Binary Search Tree BST C++ Java  kouxiP_H5WE - 853x480 - 5m01s](https://user-images.githubusercontent.com/35686407/172839242-bb6589c5-364d-4147-9409-57ccb6a84075.png)

> Edge Cases ? Yes.

> Another way ? Yes.

![take U forward - L44  Delete a Node in Binary Search Tree BST C++ Java  kouxiP_H5WE - 885x498 - 6m07s](https://user-images.githubusercontent.com/35686407/172839399-d55bbf62-d556-41b0-bb91-268155728f0b.png)

- Everyting on the right subtree is greater then left subtree after deleting 5, so we take 2 and attach it to `right smallest guy's left side`

![take U forward - L44  Delete a Node in Binary Search Tree BST C++ Java  kouxiP_H5WE - 853x480 - 6m33s](https://user-images.githubusercontent.com/35686407/172839625-53746848-0548-415c-9952-aaa8bfb2f33b.png)

2 Ways : 
- Either cut link of right portion or left portion.

> Edge Cases :

delete node = 2

![take U forward - L44  Delete a Node in Binary Search Tree BST C++ Java  kouxiP_H5WE - 885x498 - 7m33s](https://user-images.githubusercontent.com/35686407/172839888-85426e4d-7213-4d5c-9fb5-733924558d63.png)

- if there exists left , then reattach right part to the most right of left subtree
- if there is no left , then reattach right part to deleted node's parent.

![take U forward - L44  Delete a Node in Binary Search Tree BST C++ Java  kouxiP_H5WE - 885x498 - 8m55s](https://user-images.githubusercontent.com/35686407/172840435-d5a42f44-b728-4c20-9e5d-3fa827c8d350.png)

![take U forward - L44  Delete a Node in Binary Search Tree BST C++ Java  kouxiP_H5WE - 885x498 - 14m51s](https://user-images.githubusercontent.com/35686407/172841619-793a3b68-cb7a-47ac-aee6-9af38018bdf1.png)

> jis node ko delete krna hai, uska left dekha if null hai to right ko bhej do, if right null hai to left ko bhej do, if dono hai to left ke rightmost portion mae rightsubtree ko lga do and return krdo, jisse node attach ho jaye jha se call aai.

- TC : O(Height of Tree)

```cpp
TreeNode* deleteNode(TreeNode* root, int key) {
        if(root == NULL) return NULL;
        if(root->val == key) return helper(root);
        
        TreeNode* dummy = root;
        
        while(root != NULL){
            if(key < root->val){
                if(root->left && root->left->val == key){
                    root->left = helper(root->left);
                    break;
                }else{
                    root = root->left;
                }
            }else if(key > root->val){
                if(root->right && root->right->val == key){
                    root->right = helper(root->right);
                    break;
                }else{
                    root = root->right;
                }
            }
        }
        return dummy;
    }
    
    TreeNode* helper(TreeNode* root){
        TreeNode* left = root->left;
        TreeNode* right = root->right;
        
        delete root;
        
        if(left == NULL) return right;
        if(right == NULL) return left;
        
        TreeNode* extRight = extremeRight(left);
        extRight->right = right;
        
        return left; 
    }
    
    TreeNode* extremeRight(TreeNode* root){
        while(root->right != NULL){
            root = root->right;
        }
        return root;
    }
```

## 8. Kth Smallest Element in BST

#### Brute Force :
- Do any traversal
- Store in vector
- Sort the vector
- Find kth smallest and return
- TC : O(n) for traversal + O(nlogn) for sorting
- SC : O(n) to store in vector and O(n) ~ Auxillary Stack Space for Recursive Traversal

#### Optimized : 
- Property: Inorder Traversal give Sorted Numbers of Binary Search Tree
- Do Inorder Traversal
- Store in vector
- find kth smallest and return
- TC : O(n)
- SC : O(n) to store in vector and O(n) ~ Auxillary Stack Space for Recursive Traversal

#### Further Optimzed:
- don't need to store the nodes
- just maintain count variable
- if count == k return node->val
- TC : O(n)
- SC : O(n) ~ Auxillary Stack Space ~ O(1)

```cpp
int inorder(TreeNode* root,int& count,int k){
    if(root == NULL) return -1;
    int v = inorder(root->left,count,k);
    if(v!=-1) return v;
    count++;
    if(count == k){
        return root->val;
    }
    int w = inorder(root->right,count,k);
    return w;
}
int kthSmallest(TreeNode* root, int k) {
    int count = 0;
    return inorder(root,count,k);
}
```

### More Further Optimized (Morris Traversal)

- But in this, we have to traverse entire tree, we can't leave it within traversing , because some of the links are updated and not reseted.
- TC: O(n)
- SC : O(1)

```cpp
TreeNode* rightMostGuy(TreeNode* node,TreeNode* cur){
        while(node->right != NULL && node->right != cur){
            node = node->right;
        }
        return node;
    }
    
    int kthSmallest(TreeNode* root, int k) {
        if(root == NULL) return -1;
        
        TreeNode* cur = root;
        int count = 0;
        int ans;
        
        while(cur != NULL){
            if(cur->left == NULL){
                count++;
                if(count == k) ans = cur->val;
                cur = cur->right;
            }else if(cur->left != NULL){
                TreeNode* rightMost = rightMostGuy(cur->left,cur);
                if(rightMost->right == NULL){
                    rightMost->right = cur;
                    cur = cur->left;
                }else if(rightMost->right == cur){
                    rightMost->right = NULL;
                    count++;
                    if(count == k) ans = cur->val;
                    cur = cur->right;
                }
            }
        }
        return ans;
    }
```
## 9. Validate BST

- I provide range to each node, and check if it lies in it or not, if not lies then return false it's not valid BST
- in left - everyone should be lesser then node val
- in right - everyone should be greater then node val
- Left and Right Subtree Should be valid to make whole tree valid BST.

![take U forward - L46  Check if a tree is a BST or BT Validate a BST  f-sj7I5oXEI - 885x498 - 7m12s](https://user-images.githubusercontent.com/35686407/172859876-8d26f289-7fe6-48ff-91e5-c20b925964a0.png)


```cpp
bool isValidBST(TreeNode* root) {
        return isValidBST(root,LONG_MIN,LONG_MAX);
    }
    
bool isValidBST(TreeNode* root,long long minRange,long long maxRange){
    if(root == NULL) return true;

    if(root->val <= minRange || root->val >= maxRange) return false;

    return isValidBST(root->left,minRange,root->val)
        && isValidBST(root->right,root->val,maxRange);
}
```
## 10. LCA of BST 

> lca vo hota hai jb hm path nikale node to root mtlb niche se dekh rhe hai ki konsa first intersection point hoga, and agar upar se dekhe to vo last intersection point hota hai. to jo last intersection point hota hai, vhi mera lca hai.

Condition:
  1. both lie on left ~ move left
  2. both lie on right ~ move right
  3. one in left and one in right ~ that node is LCA
  4. root is one of p and q ~ that node is LCA

```cpp
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if(root == NULL) return NULL;
    if(p->val < root->val && q->val < root->val){
        return lowestCommonAncestor(root->left,p,q);
    }else if(p->val > root->val && q->val > root->val){
        return lowestCommonAncestor(root->right,p,q);
    }else{
        return root;
    }
}
```
## 11. Contruct BST from PreOrder Traversal

#### Approach 1: (Naive)

> vector ko traverse krte jao, and node ko insert krte jao, INSERT NODE IN BST

- TC : o(N x N) first N is, traversing vector array and 2nd N is, searhing for the position and N is because in worst case, maybe a skewed tree.
- SC : O(N), to store the tree and if not using auxillary stack

#### Approach 2: (Better Appraoch from before)

> hme ye hai ki, BST ka inorder sorted way mae aata hai, to hum, preorder ko sort kr denge jisse inorder mil jayega. or ab CREATE BT FROM PREORDER AND INORDER chlayenge jo ultimately hme BST dega

- TC : O(NlogN) + O(N) ~ NlogN to sort and N to travese in tree
- SC : O(n) to store tree

### Approach 3: (Optimized Approach)

> hme pta hai hm hr node ki upper bound and nikal skte hai, IS VALID BST question mae vhi kra hai, agar hum usi concept ka use krke BST bnaye to vhi hmari optimized approach hogi

- vector ko traverse krte jao, and lower bound and upper bound pass krte jao
- if lower and upper bound mae lie nhi krta to vo return NULL krega, 
- even if hmare paas agar elements nhi bche to bhi vo return NULL krega.

```cpp
TreeNode* buildTree(vector<int>& preorder,int& idx,int minRange,int maxRange){
    if(idx == preorder.size() || preorder[idx] < minRange || preorder[idx] > maxRange) return NULL;
    TreeNode* root = new TreeNode(preorder[idx++]);
    root->left = buildTree(preorder,idx,minRange,root->val);
    root->right = buildTree(preorder,idx,root->val,maxRange);
    return root;
}

TreeNode* bstFromPreorder(vector<int>& preorder) {
    int idx = 0;
    return buildTree(preorder,idx,INT_MIN,INT_MAX);
}
```

#### Appraoch 3 Improvement

- imprvement ye hai ki, hm srf upper bound se kaam chla skte hai
- we dont need to give lower bound
- left mae jb bna rhe hai to root->val bhejo as upper bound
- and right mae jb bna rhe hai to maxRange bhejo as upper bound.

```cpp
TreeNode* buildTree(vector<int>& preorder,int& idx,int maxRange){
    if(idx == preorder.size() ||  preorder[idx] > maxRange) return NULL;
    TreeNode* root = new TreeNode(preorder[idx++]);
    root->left = buildTree(preorder,idx,root->val);
    root->right = buildTree(preorder,idx,maxRange);
    return root;
}

TreeNode* bstFromPreorder(vector<int>& preorder) {
    int idx = 0;
    return buildTree(preorder,idx,INT_MAX);
}
```

![take U forward - L48  Construct a BST from a preorder traversal 3 Methods  UmJT3j26t1I - 1536x864 - 13m01s](https://user-images.githubusercontent.com/35686407/172865465-e51a6329-4e0d-47f3-a72f-5896280509eb.png)

![take U forward - L48  Construct a BST from a preorder traversal 3 Methods  UmJT3j26t1I - 1435x807 - 14m42s](https://user-images.githubusercontent.com/35686407/172865449-74517bf2-4a29-4a3d-bcc4-562e5679ee29.png)

## 12. Inorder Successor/Predecessor in BSTof given node val

![take U forward - L49  Inorder SuccessorPredecessor in BST 3 Methods  SXKAD2svfmI - 1536x864 - 7m47s](https://user-images.githubusercontent.com/35686407/172880960-5a46bf58-cecc-4eb7-b8c3-a0aabd52bfd7.png)

![take U forward - L49  Inorder SuccessorPredecessor in BST 3 Methods  SXKAD2svfmI - 1435x807 - 9m18s](https://user-images.githubusercontent.com/35686407/172880972-0797c187-34d1-4220-a15a-ddee078c1d10.png)

> Inorder Successor: node whose value is just/immediate greater then the given node value.

- agar root ki value bdi hai, to possibility hai vo successor ho skta hai [its like searching first occurance of element in BS, as usme hum index ko update krte rehte hai]
- isme hum successor ko update krte rhenge
- if we found our first successor
- next successor is jiski value just immediate greater hai given node val se and successor se km hai jo abhi tk tha

```cpp
Node * inOrderSuccessor(Node *root, Node *x){
    Node* successor = NULL;
    while(root){
        if(x->data < root->data){
            successor = root;
            root = root->left;
        }else{
            root = root->right;
        }
    }

    return successor;
}
```

> Predecessor : vo node jiski value mere given node ki value se immediate choti hogi

```cpp
void findPre(Node* root, Node*& pre, int key){
    pre = NULL;
    node = root;
    while(node){
        if(key <= node->key){
            node = node->left;
        }else{
            pre = node;
            node = node->right;
        }
    }
}
```
## 13. Binary Search Tree Iterator

- Isme hum INORDER TRAVERSAL ITERATIVE STACK APPROACH , use kre rhe hai, BINARY TREE vala
- Inorder stack iterative traversal mae hum, kya krte then left left left left if left null, then right again left left left left
- isme bhi yhi method lgana hai but 1 bari mae sara nhi bhrna hai stack.
- stack lo, if node ka left hai to put left left left left left sare left daal do
- if next() puche, to top ka element uthao, check kro uska right hai, if right hai to sare left left left left daal do, and return krdo stack ke top mae se jo uthaya tha uski value.
- hasnext() puche, to true if stack is not empty otherwise `false if st.empty`

```cpp
class BSTIterator {
public:
    stack<TreeNode*> st;
    BSTIterator(TreeNode* root) {
        pushAll(root);
    }
    
    int next() {
        TreeNode* node = st.top();st.pop();
        if(node->right){
            pushAll(node->right);
        }
        return node->val;
    }
    
    bool hasNext() {
        return !st.empty();
    }
    
private:
    void pushAll(TreeNode* node){
        // for(;node!=NULL,st.push(root),root = root->right)
        while(node != NULL){
            st.push(node);
            node = node->left;
        }
    }
};
```
## 14. Binary Search Iterator Reverse Direction (Decreasing Order)

- This is similar to Binary Search Tree Iterator from Increasing Direction,
- Just difference is that in normal BSTIteratpr, we push left left left left left if not left right then again left left left
- here we push like right right right right if not right left then again right right right right [`Reverse InOrder`]
- All Logic is same as above after that.
- Implemented in next question Two Sum IV


## 15. Two Sum IV (BST is given)

- In this we have to find , v1 + v2 == value if yes return true elsse return false;

#### Approach 1:

- use inorder traversal in BST and store inorder traversal nodes
- now use two sum question method 2 pointer to solve
- TC : O(N) + O(N) ~ Traversing + 2 Pointer
- SC : O(N) ~ storing inorder nodes

#### Approach 2:

- what if, hum iterator ka use kre, 
- ek aage se chle ek piche se
- to hum use krenge BinarySearchIterator
- we set a flag reverse = true, so that we have not to code seperate for reverse order.
- now simply use it as two pointer in Two Sum.

```cpp
class BSTIterator{
private:
    stack<TreeNode*> st;
    bool reverse;
public:
    BSTIterator(TreeNode* root,bool rev){
        this->reverse = rev;
        putAll(root);
    }
    
    int next(){
        TreeNode* node = st.top();st.pop();
        if(reverse != true){
            if(node->right){
                putAll(node->right);
            }
        }else{
            if(node->left){
                putAll(node->left);
            }
        }
        return node->val;
    }
    
    bool hasNext(){
        return !st.empty();
    }

private:
    void putAll(TreeNode* node){
        while(node != NULL){
            if(reverse != true){
                st.push(node);
                node = node->left;
            }else{
                st.push(node);
                node = node->right;
            }
        }
    }
    
};

class Solution {
public:
    bool findTarget(TreeNode* root, int k) {
        BSTIterator p(root,false);
        BSTIterator q(root,true);
        
        int i = p.next();
        int j = q.next();
        
        while(i < j){
            if(i + j == k) return true;
            else if(i + j < k){
                i = p.next();
            }else if(i + j > k){
                j = q.next();
            }
        }
        return false;
    }
};
```
