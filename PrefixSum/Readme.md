# Prefix Sum


## 1. Range Sum Query 2D

![image](https://user-images.githubusercontent.com/35686407/176986721-2cf91149-ef31-4b81-be01-d3edcf39271d.png)

- Step 1: Make prefix sum Row Wise
- Step 2: Make Prefix sum Col Wise
- 
![image](https://user-images.githubusercontent.com/35686407/176986755-2986aaf4-dca8-4dee-9586-b36dab436c8d.png)

![image](https://user-images.githubusercontent.com/35686407/176986765-90a97bbb-4952-4eb7-a7f7-56ccd039078a.png)

Now, we have to find the range sum from [2,1] to [4,3]

![image](https://user-images.githubusercontent.com/35686407/176986796-1f88f0b9-e6b3-47b5-b378-86866231955a.png)

- At [4,3] , as is 38, but this 38 is from [0,0] to [4,3] , so we have to reduce blue portion from the matrix which is extra sum , How ?
- we have to find the extra and subtract it,
![image](https://user-images.githubusercontent.com/35686407/176986854-9a837723-ad7f-4487-9bf4-4aebbc09859b.png)
- so, we have extra sum 24 [row1-1,col2], we have extra sum 14 , [row2,col-1] , but due to this we subtract 3 and 8, 2 times, so we have to add it once ~ [row-1,col-1] we have to add

![image](https://user-images.githubusercontent.com/35686407/176987067-08145b46-8f51-4c71-b8f9-89e386c08fec.png)

```cpp
class NumMatrix {
public:
    vector<vector<int>> matrix;
    NumMatrix(vector<vector<int>>& mat) {
        this->matrix = mat;
        int n = matrix.size();
        int m = matrix[0].size();
        
        for(int i = 0; i < n; i++){
            for(int j = 1; j < m; j++){
                matrix[i][j] = matrix[i][j] + matrix[i][j-1];
            }
        }
        
        for(int j = 0; j < m; j++){
            for(int i = 1; i < n; i++){
                matrix[i][j] = matrix[i][j] + matrix[i-1][j];
            }
        }
        
    }
    
    int sumRegion(int row1, int col1, int row2, int col2) {
        int sum = matrix[row2][col2];
        if(row1-1 >= 0){
            sum -= matrix[row1-1][col2];
        }
        if(col1-1 >= 0){
            sum -= matrix[row2][col1-1];
        }
        
        if(row1-1 >= 0 && col1-1 >= 0){
            sum += matrix[row1-1][col1-1];
        }
        
        return sum;
        
    }
};
```

## 2. Max Sum of Rectangle No Larger Than K

#### Approach 1: Brute Force

- using range sum method in matrix, we calculate the prefix sum, and call for all possible [row1 col1 row2 col2] range sums.
- there will be 4 loops.

```cpp
class Solution {
public:
    int maxSumSubmatrix(vector<vector<int>>& matrix, int k) {
        
        RangeSumMatrix obj(matrix);
        
        int n = matrix.size();
        int m = matrix[0].size();
        
        int maxi = INT_MIN;
        
        for(int row1 = 0; row1 < n; row1++){
            for(int col1 = 0; col1 < m; col1++){
                for(int row2 = row1; row2 < n; row2++){
                    for(int col2 = col1; col2 < m; col2++){
                        int x = obj.rangeSum(row1,col1,row2,col2);
                        if(x <= k){
                            maxi = max(maxi,x);
                        }
                    }
                }
            }
        }
        return maxi;
    }
};
```

#### Approach 2 : TODO Question Before This:
- Find max subarray with sum < k

## 3. Subarray Sum equals to K

- yha pr prefix sum ke count store krenge because suppose hme sum = k chhaiye
- to piche hum find krenge hashmap se ki sum-k aa rha hai ?
- agar haan aa rha hai to kitni baar aa rha ahi, kyuki vo sbhi subarary bnayenge for sum = k
[\[Link\]](https://github.com/sanheensethi/notes/tree/main/Array#brute-force--generate-all-subarray-and-find-the-given-condition)

```cpp
int subarraySum(vector<int>& nums, int k) {
    unordered_map<int,int> umap;
    
    int prSum = 0;
    umap[0] = 1;
    int ans = 0;
    
    for(auto&val : nums){
        prSum += val;
        
        if(umap.count(prSum - k)){
            ans += umap[prSum-k];
        }
        
        umap[prSum]++;
        
    }
    return ans;
}
```

## 4.


## 5. Path Sum III

![image](https://user-images.githubusercontent.com/35686407/176989541-fbbe1fdf-a6a9-41ff-a300-b28255094ea9.png)

- In this, we have to find the number of paths having given target sum, in above case target sum = 8

#### Approach 1: Brute Force [O(n^2)]

- Calculate the total path having target Sum from each node, by taking prev sum aage
- and if agar hme target sum mil jata hai to hum apne ans mae +1 kr denge
- pehle 10 pr aaye, prev sum 0 hai , sara ghum kr aaye and dekha ki kitna baar targetsum aa rha hai
- fr hum 5 pr aaye, vha se bhi targetsum ki searching lga di and so on.

```cpp
class Solution {
public:
    int total = 0;
    
    void findSum(TreeNode* root,long long int sum,long long int targetSum){
        if(root == NULL) return;
        
        sum += root->val;
        
        if(targetSum == sum){
            total++;
        }
        
        findSum(root->left,sum,targetSum);
        findSum(root->right,sum,targetSum);
        
    }
    
    
    int pathSum(TreeNode* root, int targetSum) {
        
        if(root == NULL) return 0;
        
        findSum(root,0,targetSum); // hr node se start kro
        pathSum(root->left,targetSum);
        pathSum(root->right,targetSum);
        
        return total;
    }
};
```
> Another way to write :

```cpp
int calc(TreeNode* root,long long int targetSum,long long int sum){
    if(root == NULL) return 0;
    
    sum += root->val;
    int x = 0;
    if(sum == targetSum){
        x++;
    }
    
    x += calc(root->left,targetSum,sum);
    x += calc(root->right,targetSum,sum);
    
    return x;
}

int pathSum(TreeNode* root, int targetSum) {
    if(root == NULL) return 0;
    int x = calc(root,targetSum,0);
    x += pathSum(root->left,targetSum) + pathSum(root->right,targetSum);
    return x;
}
```

#### Approach 2: Optimized [O(n)]

![image](https://user-images.githubusercontent.com/35686407/176989541-fbbe1fdf-a6a9-41ff-a300-b28255094ea9.png)

- - Now, for this question we have to know the question `count maximum subarray sum = k`, in array portion
- usme hum, ek unordered map lete the, hr moment pr check krte the ki (prefixsum - targetSum) , if this is in array then, we found the targetSum.
- ese hi tree ke case mae krna hai, niche jate time prefix sum niaklte jao, and umap mae dalte jao , if kisi bhi moment pr prefixSum - targetSum mil rha hai to, total+= jitne bhi times prefixSum - targetSum repeat hua
- or umap mae current sum ki freq bhada do.
- ab jb vapis aa rhe hai , yha pr hme freq of sum ki km krni hogi, kuki uska kaam khtm hua
- suppose when you found 8 standing at 3 (2nd last from root node, extreme left side), jb uske niche jayenge to or jayeda add krenge prefix sum mae
- but jb vapis aa rhe hai 3 pr, to jo 3 add kra tha prefix sum mae, to vo vala 3 added vala prefix sum bhi to htana hai.

```cpp
class Solution {
public:
    
    // same as subarray sum equal to k
    #define debug(x) cout<<#x<<":"<<x<<endl;
    unordered_map<long long int,int> umap;
    
    void find(TreeNode* root,long long int targetSum,long long int sum,int& total){
        if(root == NULL) return;
        
        sum += root->val;
        
        if(umap.count(sum-targetSum)){
            total += umap[sum-targetSum];
        }
        
        umap[sum]++;
        
        find(root->left,targetSum,sum,total);
        find(root->right,targetSum,sum,total);
        
        umap[sum]--;
        if(umap[sum] == 0){
            umap.erase(sum);   
        }
        
    }
    
    int calc(TreeNode* root,int targetSum){
        int total = 0;
        long long int sum = 0;
        umap[0] = 1;
        find(root,targetSum,sum,total);
        return total;
    }
    
    int pathSum(TreeNode* root, int targetSum) {
        if(root == NULL) return 0;
        return calc(root,targetSum);
    }
};
```














