# Trees

## Binary Trees

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

