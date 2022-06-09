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
