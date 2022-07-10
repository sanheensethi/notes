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

## Print LIS

```cpp
int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<int> dp(n,1);
        vector<int> hash(n);
        iota(hash.begin(),hash.end(),0); // fill with consecutive numbers
        
        int maxi = 1;
        int lastIdx = 0;
        for(int idx = 1; idx < n; idx++){
            for(int prev_idx = 0; prev_idx < idx; prev_idx++){
                if(nums[idx] > nums[prev_idx] && dp[idx] < dp[prev_idx]+1){
                    dp[idx] = dp[prev_idx]+1;
                    hash[idx] = prev_idx;
                }
            }
            if(maxi < dp[idx]){
                maxi = dp[idx];
                lastIdx = idx;
            }
        }
        
        cout<<nums[lastIdx]<<" ";
        while(hash[lastIdx] != lastIdx){
            lastIdx = hash[lastIdx];
            cout<<nums[lastIdx]<<" ";
        }
        
        return maxi;
 ```
 
 ## 42. Largest Divisible Subset

```cpp
class Solution {
public:
    vector<int> largestDivisibleSubset(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(),nums.end());
        vector<int> dp(n,1);
        vector<int> hash(n);
        iota(hash.begin(),hash.end(),0);
        
        int maxi = 1;
        int lastIdx = 0;
        
        for(int idx = 1; idx < n; idx++){
            for(int prev_idx = 0; prev_idx < idx; prev_idx++){
                if(nums[idx]%nums[prev_idx] == 0 && dp[idx] < dp[prev_idx] + 1){
                    dp[idx] = dp[prev_idx] + 1;
                    hash[idx] = prev_idx;
                }
            }
            if(dp[idx] > maxi){
                maxi = dp[idx];
                lastIdx = idx;
            }
        }
        
        vector<int> ans;
        ans.push_back(nums[lastIdx]);
        
        while(hash[lastIdx] != lastIdx){
            lastIdx = hash[lastIdx];
            ans.push_back(nums[lastIdx]);
        }
        reverse(ans.begin(),ans.end());
        return ans;
    }
};
```
## 43. Longest String Chain

#### Approach 1 : Recursion + Memoization

```cpp
class Solution {
public:
    
    bool compare(string& s1,string& s2){
        if(s1.size() != s2.size()+1) return false;
        // s2 is smaller and s1 is larger
        
        int first = 0;
        int second = 0;
        
        while(first < s1.size()){
            if(second < s2.size() && s1[first] == s2[second]){
                first++;
                second++;
            }else{
                first++;
            }
        }
        
        if(first == s1.size() && second == s2.size()) return true;
        return false;
    }
    
    int solve(int cur_idx,int prev_idx,vector<string>& words,vector<vector<int>>& memo){
        if(cur_idx == words.size()) return 0;
        
        if(memo[cur_idx][prev_idx+1] != -1) return memo[cur_idx][prev_idx+1];
        
        // not take
        int len = 0 + solve(cur_idx+1,prev_idx,words,memo);
        
        // take
        if(prev_idx == -1 || compare(words[cur_idx],words[prev_idx])){
            len = max(len,1+solve(cur_idx+1,cur_idx,words,memo));
        }
        return memo[cur_idx][prev_idx+1] = len;
    }
    
    static bool cmp(string& s1,string& s2){
        return s1.size() < s2.size();
    }
    
    int longestStrChain(vector<string>& words) {
        sort(words.begin(),words.end(),cmp);
        // for(auto& word:words){
        //     cout<<word<<endl;
        // }
        int cur_idx = 0;
        int prev_idx = -1;
        int n = words.size();
        vector<vector<int>> memo(n,vector<int>(n+1,-1));
        return solve(cur_idx,prev_idx,words,memo);
    }
};
```

#### Approach 2 : Tabulation (Same as LIS, just we have to do comapre string in if condition)

#### Approach 3 : Space Optimization (Same as LIS, just we have to compare stirng in if condition)

#### Approach 2 : Another Way Tabulation
```cpp
class Solution {
public:
    
    static bool compare(const string& s1,const string& s2){
        return s1.size() < s2.size();
    }
    
    bool compareWords(const string& s1,const string& s2){
        int first = 0;
        int second = 0;
        int n = s1.size();
        int m = s2.size();
        
        if(n != m+1) return false;
        
        while(first < n){
            if(second < m && s1[first] == s2[second]){
                first++;
                second++;
            }else{
                first++;
            }
        }
        if(first == n && second == m) return true;
        return false;
    }
    
    int longestStrChain(vector<string>& words) {
        int n = words.size();
        sort(words.begin(),words.end(),compare);
        vector<int> dp(n,1);
        int maxi = 1;
        for(int idx = 1; idx < n; idx++){
            for(int prev_idx = 0; prev_idx < idx; prev_idx++){
                if(compareWords(words[idx],words[prev_idx]) && dp[idx] < dp[prev_idx]+1){
                    dp[idx] = dp[prev_idx]+1;
                }
            }
            maxi = max(maxi,dp[idx]);
        }
        return maxi;
    }
};
```
