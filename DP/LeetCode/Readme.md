## Dynamic Programming

## 1. 1658. Minimum Operations to Reduce X to Zero [Question](https://leetcode.com/problems/minimum-operations-to-reduce-x-to-zero/)

![TECH DOSE - Minimum Operations to Reduce X to Zero Dynamic Programming Leetcode #1658  HddgLcq9Efs - 885x498 - 5m20s](https://user-images.githubusercontent.com/35686407/173192925-3525889e-d8a9-4e27-9b2b-03854086b8d0.png)

- Reducing x to 0, or finding sum of elements in sequence if min length = x , are same.
- we will find the min length sequence which allow us to make x ~ 0

![TECH DOSE - Minimum Operations to Reduce X to Zero Dynamic Programming Leetcode #1658  HddgLcq9Efs - 1536x864 - 10m36s](https://user-images.githubusercontent.com/35686407/173193265-8e787510-a26d-4d27-9374-6448e8c139f6.png)

- Length of the sequence is depth of the tree to leaf node, 
- so to make minimum moves to make x 0, we have to find minimum depth of the tree.

![TECH DOSE - Minimum Operations to Reduce X to Zero Dynamic Programming Leetcode #1658  HddgLcq9Efs - 1536x864 - 11m53s](https://user-images.githubusercontent.com/35686407/173193278-c9104050-ed09-4c69-9268-af89c7180ea9.png)

- Now , if we do the recursion , its exponention and gives the TLE
- So we will use memoization
- Now for memoization , what are the parameters changing, L,R,X where count is just the depth, so it need to be store as key's value. 
- So, for memoization in it we use HashMap
- in HashMap we use `key = L + "*" + R + "*" + x` and L,R,X will be in string
- and value corresponding is min(left,right);

![TECH DOSE - Minimum Operations to Reduce X to Zero Dynamic Programming Leetcode #1658  HddgLcq9Efs - 1536x864 - 17m24s](https://user-images.githubusercontent.com/35686407/173193739-f3d6388b-8e0f-4050-9691-45d972d4e7a8.png)

![TECH DOSE - Minimum Operations to Reduce X to Zero Dynamic Programming Leetcode #1658  HddgLcq9Efs - 1435x807 - 19m43s](https://user-images.githubusercontent.com/35686407/173193741-165178a6-ed66-4007-b504-2d64facc2015.png)

- But, memo gives TLE.

```cpp
unordered_map<string,int> memo;
    int operations(vector<int>& nums,int i,int j,int x,int depth){
        
        if(x == 0) return depth;
        if(i > j || x < 0) return INT_MAX;
        
        string key = to_string(i) + "*" + to_string(j) + "*" + to_string(x);
        if(memo.count(key)) return memo[key];
        
        int left = operations(nums,i+1,j,x-nums[i],depth+1);
        int right = operations(nums,i,j-1,x-nums[j],depth+1);
        
        return memo[key] = min(left,right);
    }
    
    int minOperations(vector<int>& nums, int x) {
        int ans = operations(nums,0,nums.size()-1,x,0)
        return ans == INT_MAX ? -1 : ans;
    }
```
