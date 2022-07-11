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

## 42. Print LIS

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
 
 ## 44. Largest Divisible Subset

#### Approach 1 : Recursion + Memoization (Same as LIS just change the if condition)

#### Approach 2 : Tabulation (Same as LIST just change the if condition)

#### Approach 3 : Space optimization (Same as LIS, just change the if condition)

#### Appraoch 4 : Another Way Tabulation

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
## 45. Longest String Chain

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
## 46. Longest Bitonic Subsequence LIS

- isme hme aage se and piche se LIS dhundna hai 2 array bnakr,
- and fr hmne dp1[i] + dp2[i] - common element (1) krna hai, isme se jo max aayega vo hmara ans

```cpp
int longestBitonicSequence(vector<int>& arr, int n) {
	// from aage se
    vector<int> dp1(n,1);
    for(int idx = 1; idx < n; idx++){
        for(int prev_idx = 0; prev_idx < idx; prev_idx++){
            if(arr[prev_idx] < arr[idx]){
                dp1[idx] = max(dp1[idx],dp1[prev_idx]+1);
            }
        }
    }
    
    // from piche se
    vector<int> dp2(n,1);
    for(int idx = n-2; idx >= 0; idx--){
        for(int prev_idx = n-1; prev_idx > idx; prev_idx--){
            if(arr[prev_idx] < arr[idx]){
                dp2[idx] = max(dp2[idx],dp2[prev_idx]+1);
            }
        }
    }
    
    int maxi = 1;
    for(int i = 0; i < n; i++){
        maxi = max(maxi,(dp1[i]+dp2[i]-1));
    }
    return maxi;
} 
```

## 47. Count/Number of Longest Increasing Subsequence

```cpp
int findNumberOfLIS(vector<int> &arr)
{
    int n = arr.size();
    vector<int> dp(n,1);
    vector<int> count(n,1);
    int maxi = 1;
    for(int idx = 0; idx < n; idx++){
        for(int prev_idx = 0; prev_idx < idx; prev_idx++){
            if(arr[prev_idx] < arr[idx] && dp[idx] < dp[prev_idx] + 1){
                dp[idx] = dp[prev_idx] + 1;
                count[idx] = count[prev_idx];
            }else if(arr[prev_idx] < arr[idx] && dp[idx] == dp[prev_idx]+1){
                count[idx] = count[idx] + count[prev_idx];
            }
        }
        maxi = max(dp[idx],maxi);
    }
    
    int cnt = 0;
    for(int i = 0; i < n; i++){
        if(dp[i] == maxi) cnt += count[i];
    }
    
    return cnt;
}
```

## 48. Matrix Chain Multiplication (MCM)

#### Appraoch 1 : Recursion + Memoization

```cpp
int f(int i,int j,vector<int>& arr,vector<vector<int>>& memo){
    if( i == j) return 0;
    if(memo[i][j] != -1) return memo[i][j];
    int mini = INT_MAX;
    for(int k = i; k <= j-1; k++){
        int steps = arr[i-1] * arr[k] * arr[j];
        steps += f(i,k,arr,memo);
        steps += f(k+1,j,arr,memo);
        mini = min(mini,steps);
    }
    return memo[i][j] = mini;
}

int matrixMultiplication(vector<int> &arr, int N)
{
    vector<vector<int>> memo(N+1,vector<int>(N+1,-1));
    return f(1,N-1,arr,memo);
}
```
## 49. Matrix Chain Multiplication (Tabular)

#### Approach 2 : Tabulation

```cpp
int matrixMultiplication(vector<int> &arr, int N)
{
    vector<vector<int>> dp(N+1,vector<int>(N+1,0));
    // Base Case
    for(int i = 0; i < N; i++){
        dp[i][i] = 0;
    }
    
    // Functional
    for(int i = N-1; i >= 0 ; i--){
        for(int j = i+1; j < N; j++){
            int mini = INT_MAX;
            for(int k = i; k <= j-1; k++){
                int steps = arr[i-1] * arr[k] * arr[j];
                steps += dp[i][k];
                steps += dp[k+1][j];
                mini = min(mini,steps);
            }
            dp[i][j] = mini;
        }
    }
    return dp[1][N-1];
}
```

## 50. Minimum cost to Cut the Stick

```cpp
int f(int i,int j,vector<int>& cuts,vector<vector<int>>& memo){
    if( i > j) return 0;
    if(memo[i][j] != -1) return memo[i][j];
    int mini = INT_MAX;
    for(int idx = i; idx <= j; idx++){
        int cost = cuts[j+1] - cuts[i-1] + f(i,idx-1,cuts,memo) + f(idx+1,j,cuts,memo);
        mini = min(mini,cost);
    }
    return memo[i][j] = mini;
}
int minCost(int n, vector<int>& cuts) {
    int N = cuts.size();
    cuts.push_back(n);
    cuts.insert(cuts.begin(),0);
    sort(cuts.begin(),cuts.end());
    
    vector<vector<int>> memo(N+1,vector<int>(N+1,-1));
    
    return f(1,N,cuts,memo);
}
```

## 51. Burst Ballons

#### Appraoch 1 : Recursion + Memoization

```cpp
class Solution {
public:
    
    int f(int i,int j,vector<int>& nums,vector<vector<int>>& memo){
        if( i > j ) return 0;
        if(memo[i][j] != -1) return memo[i][j];
        int maxi = INT_MIN;
        for(int idx = i; idx <= j; idx++){
            int cost = nums[i-1] * nums[idx] * nums[j+1]
                        + f(i,idx-1,nums,memo) + f(idx+1,j,nums,memo);
            maxi = max(maxi,cost);
        }
        return memo[i][j] = maxi;
    }
    
    int maxCoins(vector<int>& nums) {
        int n = nums.size();
        nums.push_back(1);
        nums.insert(nums.begin(),1);
        vector<vector<int>> memo(n+1,vector<int>(n+1,-1));
        return f(1,n,nums,memo);
    }
};
```

#### Appraoch 2 : Tabulation

```cpp
int maxCoins(vector<int>& nums) {
        int n = nums.size();
        nums.push_back(1);
        nums.insert(nums.begin(),1);
        vector<vector<int>> dp(n+2,vector<int>(n+2,0));
        
        for(int i = n; i >= 1; i--){
            for(int j = 1; j <= n; j++){
                if(i > j) continue;
                int maxi = INT_MIN;
                for(int idx = i; idx <= j; idx++){
                    int cost = nums[i-1] * nums[idx] * nums[j+1]
                                + dp[i][idx-1] + dp[idx+1][j];
                    maxi = max(maxi,cost);
                }
                dp[i][j] = maxi;
            }
        }
        
        return dp[1][n];
    }
```

## 52. Boolean Evaluation to True

```cpp
#define ll long long int
#define mod 1000000007
int f(int i,int j,int isTrue,string& str,vector<vector<vector<ll>>>& memo){
    if(i > j) return 0;
    if(i == j){
        if(isTrue){
            return (str[i] == 'T');
        }else{
            return (str[i] == 'F');
        }
    }
    
    if(memo[i][j][isTrue] != -1) return memo[i][j][isTrue];
    
    ll ways = 0;
    for(int idx = i+1; idx <= j-1; idx+=2){
        ll lT = f(i,idx-1,1,str,memo);
        ll lF = f(i,idx-1,0,str,memo);
        ll rT = f(idx+1,j,1,str,memo);
        ll rF = f(idx+1,j,0,str,memo);
        
        if(str[idx] == '&'){
            if(isTrue){
                ways =  (ways + (lT * rT)%mod)%mod;
            }
            else{
                ways =  (ways + (lF * rF)%mod + (lF * rT)%mod + (lT * rF)%mod)%mod;
            }
        }else if(str[idx] == '|'){
            if(isTrue){
                ways =  (ways + (lT * rF)%mod + (lF * rT)%mod + (lT * rT)%mod)%mod;
            }
            else{
                ways = (ways + (lF * rF)%mod)%mod;
            }
        }else if(str[idx] == '^'){
            if(isTrue){
                ways =  (ways + (lF * rT)%mod + (lT * rF)%mod)%mod;
            }
            else{
                ways = (ways + (lF * rF)%mod + (lT * rT)%mod)%mod;
            }
        }
    }
    return memo[i][j][isTrue] = ways;
}

int evaluateExp(string & exp) {
    int n = exp.size();
    vector<vector<vector<ll>>> memo(n,vector<vector<ll>>(n,vector<ll>(2,-1)));
    return f(0,n-1,1,exp,memo);
}
```
## 53. Palindrome Partitioning II

```cpp
class Solution {
public:
    
    bool isPali(string& str){
        int i = 0;
        int j = str.size()-1;
        while(i <= j){
            if(str[i] != str[j]) return false;
            i++;
            j--;
        }
        return true;
    }
    
    int f(int i,string& str,vector<int>& memo){
        if(i == str.size()) return 0;
        if(memo[i] != -1) return memo[i];
        int mini = INT_MAX;
        string temp = "";
        for(int idx = i; idx < str.size(); idx++){
            temp += str[idx];
            if(isPali(temp)){
                int cost = 1 + f(idx+1,str,memo);
                mini = min(mini,cost);
            }
        }
        return memo[i] = mini;
    }
    
    int minCut(string s) {
        int n = s.size();
        vector<int> memo(n,-1);
        return f(0,s,memo)-1 ;
    }
};
```

> we can also write ispali like that

```cpp
bool isPali(string& str,int i,int j){
    while(i <= j){
        if(str[i] != str[j]) return false;
        i++;
        j--;
    }
    return true;
}
// call : isPali(str,i,idx)
```

## 54. Partition Array for Max Sum

```cpp
class Solution {
public:
    
    int f(int i,int k,vector<int>& arr,vector<int>& memo){
        int n = arr.size();
        if(i == n) return 0;
        if(memo[i] != -1) return memo[i];
        int len = 0;
        int maxi = INT_MIN;
        int ans = INT_MIN;
        for(int idx = i; idx < min(i+k,n); idx++){
            len++;
            maxi = max(maxi,arr[idx]);
            int sum = maxi*len + f(idx+1,k,arr,memo);
            ans = max(sum,ans);
        }
        return memo[i] = ans;
    }
    
    int maxSumAfterPartitioning(vector<int>& arr, int k) {
        int n = arr.size();
        vector<int> memo(n,-1);
        return f(0,k,arr,memo);
    }
};
```

## 55. Largest Rectangle in a Matrix (histogram vale se jo solve hota hai)

## 56. Count Square Submatrices with all One's

```cpp
class Solution {
public:
    int countSquares(vector<vector<int>>& matrix) {
        int m = matrix.size();
        int n = matrix[0].size();
        
        vector<vector<int>> dp(m,vector<int>(n));
        
        for(int j = 0; j < n; j++){
            dp[0][j] = matrix[0][j];
        }
        
        for(int i = 0; i < m; i++){
            dp[i][0] = matrix[i][0];
        }
        
        for(int i = 1; i < m; i++){
            for(int j = 1; j < n; j++){
                if(matrix[i][j] == 1){
                    dp[i][j] = 1 + min({dp[i-1][j],dp[i][j-1],dp[i-1][j-1]});
                }else{
                    dp[i][j] = 0;
                }
            }
        }
        int sum = 0;
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                sum += dp[i][j];
            }
        }
        return sum;
    }
};
```


