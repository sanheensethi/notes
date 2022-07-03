## Striver DP Series

## DP : Those who cannot remember the past are condemned to repeat it.

## Couple of ways to solve
1. Memoization (Top Down)
2. Tabulation (Bottom Up)

## 1. Fibonacci Number

#### Approach 1: Recursion

- Recurrance Relation : f(n) = f(n-1) + f(n-2)
```cpp
int fib(int n){
    if(n == 0 ) return 0;
    if(n == 1) return 1;
    return fib(n-1) + fib(n-2);
}
```

![image](https://user-images.githubusercontent.com/35686407/176879672-8bfa1d4d-385d-4bc3-aea5-e8cacbc70f40.png)

> Note : Whenever we are approaching the same problem again , again , again then it's `overlapping subproblem` , so, there is no need to calculate it again, you can see f(2) and f(3) , in recursive tree. So, here comes Memoization / Tabulation i.e. Dynamic Programming. We tend to store the values of subproblems in some map/table.Over here we have f(2) , how many parameters are there which are changing in recusive function ? it's 1, so we make 1-D array.

#### Approach 2 : Memoization

- Storing the subproblems in recursion while returning is memoization, when we go to same type of subproblem, we directly return it in O(1).
- TC : O(N)
- SC : O(N) + O(N) ~ stack space and memo array

```cpp
int fib(int n,vector<int>& memo){
    if(n == 0 ) return 0;
    if(n == 1) return 1;
    if(memo[n] != -1) return memo[n];
    return memo[n] = fib(n-1,memo) + fib(n-2,memo);
}

int fib(int n) {
    vector<int> memo(n+1,-1);
    return fib(n,memo);
}
```

> How to convert Memoization into Tabulation(Bottom Up) ? Try to go from base case to the required answer.

Steps to convert:
1. In Recrusion, whatever dp array you used, initialize the same thing.
2. write base cases of recursion , dp[0] = 0, dp[1] = 1
3. look for recursion relationship f(n-1) + f(n-2) ~ these lines are executed from n = 2, so we write
```cpp
for(int i = 2; i <= n; i++){
    // memo[i] = f(n-1) + f(n-2); // change f to dp and n to i
    dp[i] = dp[i-1] + dp[i-2]; \
}
```

#### Approach 3 : Tabulation

```cpp
int fib(int n) {
    if(n <= 1) return n;
    vector<int> dp(n+1,-1);
    dp[0] = 0;
    dp[1] = 1;
    for(int i = 2; i <= n; i++){
        dp[i] = dp[i-1] + dp[i-2];
    }
    return dp[n];
}
```

#### Approach 4 : More Optimize the space Complexity of Tabulation

- what i require for dp[i], dp[i-1] and dp[i-2] only two values.
![image](https://user-images.githubusercontent.com/35686407/176883862-3d84a3cf-e10a-4ec6-8090-94599a1c9019.png)
- say i-1 as prev and i-2 as prev2
- in Next Step where will i go ?
![image](https://user-images.githubusercontent.com/35686407/176884006-1586ca4d-1886-41d0-a63e-3a15bfbfda65.png)
- from here what we observe, i become i-1 and i-1 become i-2, i.e., simply, i become prev and i-1 become prev2
- so there is a pattern i become prev and prev2 become prev
![image](https://user-images.githubusercontent.com/35686407/176884311-d0fadf25-3ee7-428f-93fb-d418b925aedf.png)

> So :

- Now , dp[0] is prev2 and dp[1] is prev
- curi = prev + perv2 in loop , where curi is the dp[i], prev = dp[i-1] and prev2 is dp[i-2]
- before next step , prev2 = prev and prev = curi
- TC : O(n)
- SC : O(1)

```cpp
int fib(int n) {
    if(n <= 1) return n;
    int prev2 = 0;
    int prev1 = 1;
    for(int i = 2; i <= n; i++){
        int curi = prev2 + prev1;
        prev2 = prev1;
        prev1 = curi;
    }
    return prev1;
}
```

## Remember in 1-D DP

> Understand DP Problem :

- Count Number of Ways
- there are multiple ways to do it ,  minimal output/maximal output

 > Note : Concept of Try All Possible ways comes in : Count , Best Way ~ then try to do recursion
 
## Shortcut - write any recurrence , then memoization then tabulation then space optimization
1. Try to represent the problem in terms of index
2. Do all possible stuffs on that index according to the problem statement
3. Count All Ways , then do sum(all stuffs)
4. Find Minimum , then do min(all stuffs)
5. Find Maximum , then do max(all stuffs)

## 2. Climbing Stairs

- Either take 1 Jump or 2 Jump to reach at the top.
- Step 1 : Here , you are at `0` , you have to reach `n`, so assume 0 , 1 , 2 , 3 , ... n index
- Step 2 : what recursion job is ? f(n) = number of ways to reach 0 to n
- Step 3 : write recurrance , jump 1 or jump 2 ~ f(n) = f(n-1) + f(n-2) , sum is because we have to find total ways.

#### Appraoch 1: Recursion

```cpp
int reachTop(int n){
        if(n == 0) return 1;
        if( n < 0) return 0;
        return reachTop(n-1) + reachTop(n-2); // fibonacci
    }
    int climbStairs(int n) {
        return reachTop(n);
    }
```

#### Approach 2: Memoization

- See which parameters are changing , just make that dimension array
- Here only n is chainging, so we make 1D array

```
int reachTop(int n,vector<int>& memo){
    if(n == 0) return 1;
    if( n < 0) return 0;
    if(memo[n] != -1) return memo[n];
    return memo[n] = reachTop(n-1,memo) + reachTop(n-2,memo); // fibonacci
}
int climbStairs(int n) {
    vector<int> memo(n+1,-1);
    return reachTop(n,memo);
}
```

#### Approach 3: Tabulation

- change reachTop() , to dp[] and n to i

```cpp
int climbStairs(int n) {
    vector<int> dp(n+1,-1);
    dp[0] = 1;
    for(int i = 1; i <= n; i++){
        int count = 0;
        count += dp[i-1];
        if(i > 1) count += dp[i-2];
        dp[i] = count;
    }
    return dp[n];
}
```

#### Approach 4: Space Optimization 

```cpp
int climbStairs(int n) {
    int prev = 1;
    int prev2 = 0;
    for(int i = 1; i <= n; i++){
        int cur = prev + prev2;
        prev2 = prev;
        prev = cur;
    }

    return prev;
}
```
## 3. Frog Jump

> Why Greedy not Work ?

- You may lost out the actual path when trying greedy
![image](https://user-images.githubusercontent.com/35686407/176993836-cdfd158a-0cf2-4d0b-9a71-0212c2184ca2.png)
- cost = 60 in above, Now :
- ![image](https://user-images.githubusercontent.com/35686407/176993840-99fb64f2-77b9-4fa2-8204-600867649cee.png)
- but got another path cost = 40, which is minimum, hence, greedy may give you wrong ans.

> Steps to build Recursion

1. Make everything in terms of index
2. do all stuffs on that index
3. take min(all stuffs)

> f(n-1) : min energy required to reach from n-1 to 0

- if I'm jumping from idx to idx-1, then enery consume is abs(arr[idx] - arr[idx-1])

| Overlapping Subproblems : 

![image](https://user-images.githubusercontent.com/35686407/176994372-846ac1ce-11e4-48f2-bf3b-8514c5a996f2.png)

#### Approach 1 : Recursion

```cpp
int solve(int idx,vector<int>& heights){
    if(idx == 0) return 0; // goal pr poch gya.
    
    int v1 = solve(idx-1,heights) + abs(heights[idx] - heights[idx-1]);
    
    int v2 = INT_MAX;
    if(idx-2 >= 0){
        v2 = solve(idx-2,heights) + abs(heights[idx] - heights[idx-2]);
    } 
    return min(v1,v2);
}

int frogJump(int n, vector<int> &heights)
{
    return solve(n-1,heights);
} 
```

#### Approach 2 : Memoization

```cpp
int solve(int idx,vector<int>& heights,vector<int>& memo){
    if(idx == 0) return 0; // goal pr poch gya.
   
    if(memo[idx] != -1) return memo[idx];
    
    int v1 = solve(idx-1,heights,memo) + abs(heights[idx] - heights[idx-1]);
    int v2 = INT_MAX;
    if(idx-2 >= 0){
        v2 = solve(idx-2,heights,memo) + abs(heights[idx] - heights[idx-2]);
    } 
    return memo[idx] = min(v1,v2);
}

int frogJump(int n, vector<int> &heights)
{    
    vector<int> memo(n,-1);
    return solve(n-1,heights,memo);
}
```

#### Approach 3 : Tabulation

```cpp
int frogJump(int n, vector<int> &height)
{    
    vector<int> dp(n,-1);
    dp[0] = 0;
    for(int i = 1; i < n; i++){
        int v1 = dp[i-1] + abs(height[i] - height[i-1]);
        int v2 = INT_MAX;
        if(i-2 >= 0){
            v2 = dp[i-2] + abs(height[i] - height[i-2]);
        }
        dp[i] = min(v1,v2);
    }
    return dp[n-1];
}
```

#### Approach 4: Space Optimization

> Note : Whenever you find idx-1 and idx-2 , then there will always be a space optimization.

```cpp
int frogJump(int n, vector<int> &height)
{    
    int prev2 = 0;
    int prev = 0;
    for(int i = 1; i < n; i++){
        int v1 = prev + abs(height[i] - height[i-1]);
        int v2 = INT_MAX;
        if(i-2 >= 0){
            v2 = prev2 + abs(height[i] - height[i-2]);
        }
        int curr = min(v1,v2);
        prev2 = prev;
        prev = curr;
    }
    return prev;
}
```

## 4. Frog jump with K Distance

- isme bs k jumps hai, pehle 1 ya 2 hi jump thi

#### Approach 1: Recursion

```cpp
int solve(int idx,int k,vector<int>& heights){
    if(idx == 0) return 0;
    int ans = INT_MAX;
    for(int i = 1; i<= k; i++){
        if(idx-i >= 0){
            int u = solve(idx-i,k,heights) + abs(heights[idx] - heights[idx-i]);
            ans = min(ans,u);
        }
    }
    return ans;
}

int frogWithKJumps(int n,int k,vector<int>& heights){
    return solve(n-1,k,heights);
}
```

#### Approach 2: Memoization
- TC : O(n*k)
- SC : O(n) stack space + O(n)

```cpp
int solve(int idx,int k,vector<int>& heights,vector<int>& memo){
        if(idx == 0) return 0;
        if(memo[idx] != -1) return memo[idx];
        int ans = INT_MAX;
        for(int i = 1; i<= k; i++){
            if(idx-i >= 0){
                int u = solve(idx-i,k,heights,memo) + abs(heights[idx] - heights[idx-i]);
                ans = min(ans,u);
            }
        }
        return memo[idx] = ans;
    }

    int frogWithKJumps(int n,int k,vector<int>& heights){
        vector<int> memo(n,-1);
        return solve(n-1,k,heights,memo);
    }
```

#### Approach 3: Tabulation
- TC : O(n*k)
- SC : O(n)

```cpp
int frogWithKJumps(int n,int k,vector<int>& heights){
    vector<int> dp(n,-1);
    
    dp[0] = 0;
    for(int idx = 1; idx < n; idx++){
        int ans = INT_MAX;
        for(int i = 1; i <= k; i++){
            if(idx - i >= 0){
                int u = dp[idx-i] + abs(heights[idx] - heights[idx-i]);
                ans = min(ans,u);
            }
        }
        dp[idx] = ans;
    }
    
    return dp[n-1];
}
```

#### Approach 4: Space Optimization

- In worst case k = n, so we have to take atleast k elements array i.e., n , so there is no need to make space optimization as it cannot be done
- because in worst case k = n.
- if k is very less then n, we can create a list of k elements and use that, list is because we dont need then assigning k-4 = k-3 , k-3 = k-2 like that.

## 5. House Robber II (Circular Array, 1st index and nth index are joined)

- 1st and Last element didn't occur together.
- so ans1 = leave 1st element, and perform the house robber problem
- ans2 = leave last element and perform the house robber problem
- `ans = max(ans1,ans2)`

![image](https://user-images.githubusercontent.com/35686407/177028154-7af41528-d4de-44c5-8eb1-0fde5d4c34f5.png)

```cpp
class Solution {
public:
    int solve(int idx,vector<int>& nums,vector<int>& memo){
        if(idx == 0) return nums[idx];
        if(idx < 0) return 0;
        if(memo[idx] != -1) return memo[idx];
        
        int pick = nums[idx] + solve(idx-2,nums,memo);
        int notpick = 0 + solve(idx-1,nums,memo);
        
        return memo[idx] = max(pick,notpick);
    }
    
    int robLinear(vector<int>& nums){
        int n = nums.size();
        vector<int> memo(n,-1);
        return solve(n-1,nums,memo);
    }
    
    int rob(vector<int>& nums) {
        int n = nums.size();
        if(n == 1) return nums[0];
        vector<int> temp1(nums.begin(),nums.end());
        vector<int> temp2(nums.begin(),nums.end());
        temp1.erase(temp1.begin()); // pop first
        temp2.pop_back(); // pop last element
        int ans1 = robLinear(temp1);
        int ans2 = robLinear(temp2);
        return max(ans1,ans2);
    }
};
```
## 6. Ninja Training

#### Appraoch 1 : Recursion and Memoization

```cpp
#include<climits>
int solve(int idx,int last,vector<vector<int>>& points,vector<vector<int>>& memo){
    
    if(idx == 0){
    // when we are at last day , we have to take the maximum from all 3 such that whatever you are picking up the task , that is not performed on the last day from where you are coming.
        int maxi = INT_MIN;
        for(int i = 0; i < 3; i++){
            if(i != last){
                maxi = max(maxi,points[0][i]);
            }
        }
        return maxi;
    }
    
    if(memo[idx][last] != -1) return memo[idx][last];
    
    int maxi = INT_MIN;
    for(int i = 0; i < 3; i++){
        if(i != last){
            // do not perform the task, whatever you did in the last day therefore we write i != last
            int val = points[idx][i] + solve(idx-1,i,points,memo);
            maxi = max(maxi,val);
        }
    }
    return memo[idx][last] = maxi;
}

int ninjaTraining(int n, vector<vector<int>> &points)
{
    vector<vector<int>> memo(n,vector<int>(4,-1));
    return solve(n-1,3,points,memo);
}
```
#### Appraoch 2 : Tabulation
```cpp
int ninjaTraining(int n, vector<vector<int>> &points)
{
    vector<vector<int>> dp(n,vector<int>(4,-1));
    
    // base case
//     dp[0][0] = max(points[0][1],points[0][2]);
//     dp[0][1] = max(points[0][0],points[0][2]);
//     dp[0][2] = max(points[0][0],points[0][1]);
//     dp[0][3] = max(points[0][0],max(points[0][1],points[0][2]));
    for(int last = 0; last < 4; last++){
        // options : 0,1,2,3
        int maxi = INT_MIN;
        for(int i = 0; i < 3; i++){
            // pick max such that not equal to the last
            if(i != last){
                maxi = max(maxi,points[0][i]);
            }
        }
        dp[0][last] = maxi;
    }
    
    for(int idx = 1; idx < n; idx++){
        for(int last = 0; last < 4; last++){
            int maxi = INT_MIN;
            for(int i = 0 ; i < 3; i++){
                if(i != last){
                    int val = points[idx][i] + dp[idx-1][i];
                    maxi = max(maxi,val);
                }
            }
            dp[idx][last] = maxi;
        }
    }
    
    return dp[n-1][3];
}
```
