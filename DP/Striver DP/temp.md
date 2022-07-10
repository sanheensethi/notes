## 41. Longest Increasing Subsequence

#### Appraoch 1 : Recurison + Memoization

```cpp
class Solution {
public:
    int f(int idx,int prev_idx,vector<int>& nums,vector<vector<int>>& memo){
        if(idx == nums.size()) return 0;
        if(memo[idx][prev_idx+1] != -1) return memo[idx][prev_idx+1];
        int take = 0;
        if(prev_idx== -1 || nums[prev_idx] < nums[idx]){
            take = 1 + f(idx+1,idx,nums,memo);
        }
        int nottake = f(idx+1,prev_idx,nums,memo);
        return memo[idx][prev_idx+1] = max(take,nottake);
        
    }
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<vector<int>> memo(n,vector<int>(n+1,-1));
        return f(0,-1,nums,memo);
    }
};
```

#### Appraoch 2 : Tabulation
```cpp
int lengthOfLIS(vector<int>& nums) {
    int n = nums.size();
    vector<vector<int>> dp(n+1,vector<int>(n+1,0));
    
    for(int idx = n-1; idx >= 0; idx--){
        for(int prev_idx = idx-1; prev_idx >= -1; prev_idx--){
            int take = 0;
            if(prev_idx== -1 || nums[prev_idx] < nums[idx]){
                take = 1 + dp[idx+1][idx+1];
            }
            int nottake = dp[idx+1][prev_idx+1];
            dp[idx][prev_idx+1] = max(take,nottake);
        }
    }
    
    return dp[0][-1+1];
}
```

#### Appraoch 3 : Space Optimization

```cpp
int lengthOfLIS(vector<int>& nums) {
    int n = nums.size();
    vector<int> ahead(n+1,0),cur(n+1,0);
    
    for(int idx = n-1; idx >= 0; idx--){
        for(int prev_idx = idx-1; prev_idx >= -1; prev_idx--){
            int take = 0;
            if(prev_idx== -1 || nums[prev_idx] < nums[idx]){
                take = 1 + ahead[idx+1];
            }
            int nottake = ahead[prev_idx+1];
            cur[prev_idx+1] = max(take,nottake);
        }
        ahead = cur;
    }
    
    return ahead[-1+1];
}
```

#### Appraoch 4 : (Different Way of Tabulation)

```cpp
int lengthOfLIS(vector<int>& nums) {
    int n = nums.size();
    vector<int> dp(n,1);
    int maxi = 1;
    for(int idx = 0; idx < n; idx++){
        for(int prev = 0; prev < idx; prev++){
            if(nums[prev] < nums[idx]){
                dp[idx] = max(1 + dp[prev],dp[idx]);
            }
        }
        maxi = max(dp[idx],maxi);
    }
    return maxi;
}
```

#### Approach 5 : (Binary Search) Optimized Appraoch
- Concerned about only Length

```cpp
int lengthOfLIS(vector<int>& nums) {
    int n = nums.size();
    vector<int> temp;
    temp.push_back(nums[0]);
    int size = 1;
    for(int i = 1; i < n; i++){
        if(temp.back() < nums[i]){
            temp.push_back(nums[i]);
            size++;
        }else{
            int idx = lower_bound(temp.begin(),temp.end(),nums[i]) - temp.begin();
            temp[idx] = nums[i];
        }
    }
    return size;
}
```
