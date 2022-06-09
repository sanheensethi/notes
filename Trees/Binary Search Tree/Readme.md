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

