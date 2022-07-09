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

- isme hm jo task on 1st day perform kr rhe hai usko agle din perform nhi kr skte and baki 2 mae se koi ek task perform krna hai, lekin jo task aaj hmne kra haii vo hum paro kr skte hai, consecutive 2 days mae nhi kr skte hai.
- hme maximum points ko gain krna hai.
- isme greedy fail ho rha hai
    - as choose 50 from day0 and now choose 11 from day 1 because we cant able to choose task 2, therefore we got profit 61
    - but if we choose 10 in day 0 therefore because of that we choose 100 from day 1 , then we get profit of 110, therefore here greedy fails
![image](https://user-images.githubusercontent.com/35686407/177037308-b7fe767c-2806-4bcf-bcc0-106f2abc7fc0.png)
- so, whenever greedy fails, we have to `Try ALL POSSIBLE WAYS` to get out the maximum

> How to develop recursion ?

Step 1: Treat as index, here what will be the index ? DAY ! as 0th day we are going to do something, day 1 we are going to do something
Step 2: Do Stuffs on that index
Step 3: Maximize
- so, as we see, from the day if we choose task 0 then on next day we cann't able to choose task 0, so we need to know which task is performed on the prev day, so we have to add extra perameter to the recursion i.e., last by which we got to know which task i should not consider current day.


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
#### Approach 4: Space Optimization

- As you can see in the tabulation code, only the prev array index in used. dp[idx-1] rest, current array is used.
- So, what if we create an array of size 4, only.
- we use it as prev array, and create a temp array as current array then, after process we make temp array as prev array and new temp array as current array.

![image](https://user-images.githubusercontent.com/35686407/177037040-1021a69b-2ffe-49ff-a6ca-04ce7443789d.png)

```cpp
#include<climits>
int ninjaTraining(int n, vector<vector<int>> &points)
{
    vector<int> prev(4,-1);
    
    for(int last = 0; last < 4; last++){
        // options : 0,1,2,3
        int maxi = INT_MIN;
        for(int i = 0; i < 3; i++){
            // pick max such that not equal to the last
            if(i != last){
                maxi = max(maxi,points[0][i]);
            }
        }
        prev[last] = maxi;
    }
    
    for(int idx = 1; idx < n; idx++){
        vector<int> temp(4,-1);
        for(int last = 0; last < 4; last++){
            int maxi = INT_MIN;
            for(int i = 0 ; i < 3; i++){
                if(i != last){
                    int val = points[idx][i] + prev[i];
                    maxi = max(maxi,val);
                }
            }
            temp[last] = maxi;
        }
        prev = temp;
    }
    
    return prev[3];
}
```
## 1. Unique Paths (DP on Grids)

> Count Ways : return 0 , if you are not on destination and return 1 if you are at destination

- we have to find number of ways to reach start to end, we can only move right and down
- so, we are trying all possible ways to go to end ~ Apply Recursion

![image](https://user-images.githubusercontent.com/35686407/177037767-26cd3570-2e54-4f03-a873-ec814647990c.png)

> In 2D Dp

1. Express everything in terms of (i,j)
2. do stuff on that
3. for count add all or min/max for min/max cost/moves question

> Note : As i m wrinting recursion in top down approach , so if we are trying to move from (m-1,n-1) to (0,0) we have to move up and left, because from (0,0) to (m-1,n-1) its, right and down.

#### Approach 1: Recursion and Memoization

- TC of rec : every cell have 2 paths up and left : therefore in total 2 x 2 x 2 x ... (mxn) times = O(2^(m x n))
- SC of rec : O(path length) = O(m-1 + n-1)

![image](https://user-images.githubusercontent.com/35686407/177038242-f63aa1eb-c82b-4cde-ada8-fb4e2844f904.png)

> Memoization : Only when there are overlapping subproblems.

- Changing Parameters : i and j 
    - i max value : m-1
    - j max value : n-1
    - therefore if i need m-1 index we have to make vector of size m
    - vector<vector<int>> memo(m,vector<int>(n,-1);

```cpp
int ways(int i,int j,vector<vector<int>>& memo){
    if(i == 0 && j == 0) return 1;
    if(i < 0 || j < 0) return 0;
    
    if(memo[i][j] != -1) return memo[i][j];
    
    int up = ways(i-1,j,memo);
    int left = ways(i,j-1,memo);
    return memo[i][j] = up + left;
    
}

int uniquePaths(int m, int n) {
    vector<vector<int>> memo(m,vector<int>(n,-1));
    return ways(m-1,n-1,memo);
}
```

#### Approach 2 : Tabulation

- write the base case , i == 0 && j == 0 , dp[i][j] = 0
- now, for i = 0, there are multiple values
    - i = 0 , j = 0,1,2,3,...n-1
    - i = 1 , j = 0,1,2,3,...n-1
    - i = 2 , j = 0,1,2,3,...n-1
    - ans so on.
- So, for each state of i from 0 to m-1 we have j from 0 to n-1
- TC : O(NxM)
- SC : O(NxM)

| Outer Loop     | Inside Loop       |
| -------------- | -------------- |
| ![image](https://user-images.githubusercontent.com/35686407/177042202-08132e6d-bb5f-4b29-a8c8-12e430ba44d7.png)    | ![image](https://user-images.githubusercontent.com/35686407/177042317-09e54785-21d2-4d55-a52c-ce7058212b83.png)|

> Memoization _to_ Tabulation :

```cpp
# Step 1: Declare Base Case
# Step 2: compress all states in for loop
# Step 3 : Copy the reccurance and write
```

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m,vector<int>(n,-1));
        dp[0][0] = 1;
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(i == 0 && j == 0) dp[i][j] = 1;
                else{
                    int up = 0, left = 0;
                    if(i-1 >= 0) up = dp[i-1][j];
                    if(j-1 >= 0) left = dp[i][j-1];
                    dp[i][j] = up + left;
                }
            }
        }
        
        
        return dp[m-1][n-1];
    }
};
```

#### Approach 3: Space Optimization

- `Golden Rule` : if you see at any moment we are using the prev row(dp[i-1][j]), if there is a case iof prev row and prev col(dp[i][j-1]), so there is always a case of space optimization
- dp[i-1] is always prev row
- dp[i] is always curr row
- we initialize prev row as prev
- and cur row as temp

|Image 1|Image 2|
|----|----|
|![image](https://user-images.githubusercontent.com/35686407/177042725-dcd58a94-8e49-408a-abbd-57e43f16bbfe.png)|![image](https://user-images.githubusercontent.com/35686407/177042732-297ec558-84f0-4985-8eec-1f0866e33cc5.png)|

```cpp
int uniquePaths(int m, int n) {
    vector<int> prev(n,0); // prev row
    for(int i = 0; i < m; i++){
        vector<int> temp(n); // current row
        for(int j = 0; j < n; j++){
            if(i == 0 && j == 0) temp[j] = 1;
            else{
                int up = 0, left = 0;
                if(i-1 >= 0) up = prev[j];
                if(j-1 >= 0) left = temp[j-1];
                temp[j] = up + left;
            }
        }
        prev = temp;
    }
    return prev[n-1];
}
```

## 8. Unique Paths 2

- Similar as Unique Path, just a small difference is that there is a blockage of cell, when mat[i][j] == -1, then there is a blockage we can't move there. so, we have to return 0
- extra base case : if(i >= 0 && j >= 0 && mat[i][j] == -1) return 0;

#### Appraoch 1 : Recursion + Memoization

```cpp
int mod = (int)(1e9+7);
int f(int i,int j,vector<vector<int>>& mat,vector<vector<int>>& memo){
    // base case
    if(i >= 0 && j >=0 && mat[i][j] == -1) return 0;
    if(i == 0 && j == 0) return 1;
    if(i < 0 || j < 0) return 0;
    
    if(memo[i][j] != -1) return memo[i][j];
    
   // functional
    int up = f(i-1,j,mat,memo);
    int left = f(i,j-1,mat,memo);
    
    return memo[i][j] = (up + left)%mod;
}

int mazeObstacles(int n, int m, vector< vector< int> > &mat) {
    vector<vector<int>> memo(n,vector<int>(m,-1));
    return f(n-1,m-1,mat,memo);
}
```

#### Approach 2 : Tabulation

```cpp
int mod = (int)(1e9+7);
int mazeObstacles(int n, int m, vector< vector< int> > &mat) {
    vector<vector<int>> dp(n,vector<int>(m,-1));
    
    if(mat[0][0] == -1) return 0;
    
    dp[0][0] = 1;
    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++){
            if(mat[i][j] == -1){
                dp[i][j] = 0;
            }else if(i == 0 && j == 0){
                dp[i][j] = 1;
            }else{
                int up = 0,left = 0;
                if(i-1 >= 0) up += dp[i-1][j];
                if(j-1 >= 0) left += dp[i][j-1];
                dp[i][j] = (up + left)%mod;
            }
        }
    }
    return dp[n-1][m-1];
}
```

#### Appraoch 3: Space Optimization

```cpp
int mod = (int)(1e9+7);
int mazeObstacles(int n, int m, vector< vector< int> > &mat) {
   
    vector<int> prev(m,0);
    
    if(mat[0][0] == -1) return 0;
    
    prev[0] = 1;
    for(int i = 0; i < n; i++){
        vector<int> temp(m);
        for(int j = 0; j < m; j++){
            if(mat[i][j] == -1){
                temp[j] = 0;
            }else if(i == 0 && j == 0){
                temp[j] = 1;
            }else{
                int up = 0,left = 0;
                if(i-1 >= 0) up += prev[j];
                if(j-1 >= 0) left += temp[j-1];
                temp[j] = (up + left)%mod;
            }
        }
        prev = temp;
    }
    return prev[m-1];
}
```
## 9. Minimum Path Sum
- isme hum INT_MAX isliye return kr rhe hai kyuki hum (0,0) pr nhi poche to hme compare krne ke liye bhtt badi value chahiye taki agar koi minimum value la rha ahi to vo hum return kr sake.

#### Approach 1 : Recursion + Memoization

```cpp
#include<climits>
int f(int i,int j,vector<vector<int>>& grid,vector<vector<int>>& memo){
    // BASE CASE
    if(i == 0 && j == 0) return grid[0][0];
    if(i < 0 || j < 0) return INT_MAX;
    
    if(memo[i][j] != -1) return memo[i][j];
    
    // FUNCTIONALITY
    int up = f(i-1,j,grid,memo);
    
    if(up != INT_MAX){
        up += grid[i][j];
    }
    
    int left = f(i,j-1,grid,memo);
    
    if(left != INT_MAX){
        left += grid[i][j];
    }
       
    return memo[i][j] = min(up,left);
}

int minSumPath(vector<vector<int>> &grid) {
    int n = grid.size();
    int m = grid[0].size();
    vector<vector<int>> memo(n,vector<int>(m,-1));
    return f(n-1,m-1,grid,memo);
}
```

#### Appraoch 2 : Tabulation

```cpp
#include<climits>
int minSumPath(vector<vector<int>> &grid) {
    int n = grid.size();
    int m = grid[0].size();
    vector<vector<int>> dp(n,vector<int>(m,-1));
    
    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++){
            if(i == 0 && j == 0) dp[i][j] = grid[i][j];
            else{
                int up = INT_MAX;
                int left = INT_MAX;
                if(i-1 >= 0) up = grid[i][j] + dp[i-1][j];
                if(j-1 >= 0) left = grid[i][j] + dp[i][j-1];
                dp[i][j] = min(up,left);
            }
        }
    }
    
    return dp[n-1][m-1];
}
```

#### Approach 3 : Space Optimization

```cpp
#include<climits>
int minSumPath(vector<vector<int>> &grid) {
    int n = grid.size();
    int m = grid[0].size();
    vector<int> prev(m);
    
    for(int i = 0; i < n; i++){
        vector<int> temp(m);
        for(int j = 0; j < m; j++){
            if(i == 0 && j == 0) temp[j] = grid[i][j];
            else{
                int up = INT_MAX;
                int left = INT_MAX;
                if(i-1 >= 0) up = grid[i][j] + prev[j];
                if(j-1 >= 0) left = grid[i][j] + temp[j-1];
                temp[j] = min(up,left);
            }
        }
        prev = temp;
    }
    
    return prev[m-1];
}
```
## Variable Starting and Variable Ending

## 10. Triangle (Fixed Start and Variable Ending)

![image](https://user-images.githubusercontent.com/35686407/177080595-85f8e021-4c2d-4777-8912-dc00099d94f3.png)|
- Staring Point is fixed. Ending point might vary,
- in ending row, you can eiter reach index 0 or 1 or 2 or 3
- You can move downward in next row, or downward in aage in next row.
    - from (i,j) to (i+1,j) or (i+1,j+1)
- Find the minimum cost to reach to the row.
- There is no uniformity/greedy solution, therefore we try out all the paths.
- Try all ways ~ Recursion , find the minimum sum

> Steps

1. Represent everything in numbers (i,j)
2. Explore all the paths , down or diagonally
3. Minimum(all paths)

> In prev questions, we know ending point is something like n-1,m-1 from where we write recursion,
bur here we didn;'t know where to end.

|Point|Image|
|---|---|
|Logically it make no sense if i write the recurrence i.e., you write recurrence from the last , you have many options to write the recurrance, now all the 4 reccurance which give you best ans is your ans.|![image](https://user-images.githubusercontent.com/35686407/177080991-95237886-0209-4f85-8304-0ccc97693b32.png)|

> Preferable logic : we know there is single fixed point from the start , so we start from there  Logically it is preferraable that you start from top and do recursion, if we start from bottom then we have to write recursion for 4 different cols

- f(0,0) ~ minimum path sum from 0,0 to the last row


```cpp
Base Case: destination is (n-1)th row, so we have to stop at (n-1)th row, 
return whatever is there on jth columns
```

#### Approach 1 : Recursion + Memoization
- 2 Moves, Move down and Move diagonal
- TC of recursion :
    - 1st row 1 col
    - 2nd row 2 cols
    - 3 row 3 cols
    - for every column we have 2 options down/diagonal
    - n row has n cols
    - So, 2^(1+2+3+....n)
- SC : Stack Space O(n)
- Found overlapping subproblems, so we apply memoization
- TC of memoization :

```cpp
int solve(int i,int j,vector<vector<int>>& triangle,vector<vector<int>>& memo){
    if(i == triangle.size()-1){
        return triangle[i][j];
    }
    
    if(memo[i][j] != -1) return memo[i][j];
    
    int move1 = triangle[i][j] + solve(i+1,j,triangle,memo);
    int move2 = triangle[i][j] + solve(i+1,j+1,triangle,memo);
    
    return memo[i][j] = min(move1,move2);
}

int minimumTotal(vector<vector<int>>& triangle) {
    int n = triangle.size();
    int m = traiangle[n-1].size();
    vector<vector<int>> memo(n,vector<int>(m,-1));
    return solve(0,0,triangle,memo);
}
```

#### Approach 2 : Tabulation

- it is different from the last questions
- here the tabulation is slight different
- `Golden Rule : ` Whaterever you write in the recursion , tabulation is just opposite to that.
- In recursion its 0 to n-1,
- now for tabulation its from n-1 to 0

> Now :

- How many base cases we have ?
- if i == n-1, possible values of j :
    - j = 0, 1, 2, 3

```cpp
// Base Case
for (int i = 0 ; i < n; i++){
    dp[n-1][j] = triangle[n-1][j];
}
```

![image](https://user-images.githubusercontent.com/35686407/177083425-e39072b2-c789-4c02-91ca-5cfa36cd0333.png)

- we know, for each row there are uthne hi cols
- i.e., for i = 0 , j = 0
- for i = 1, j = 0,1
- for i = 2, j = 0,1,2
- for i = 3, j = 0,1,2,3
- therefore first write the loop for i then write the loop for j
- create nested loop
- TC : O(NxM)
- SC : O(NxM)

```cpp
for(int i = n-2; i >= 0; i--){
    for(int j = i; j >= 0; j--){
        // copy paste reccuranec
    }
}
```

> Code

```cpp
int minimumTotal(vector<vector<int>>& triangle) {
        
    int n = triangle.size();
    int m = triangle[n-1].size();
    
    vector<vector<int>> dp(n,vector<int>(m,-1));
    
    // Base Case
    for(int j = m-1; j>= 0; j--){
        dp[n-1][j] = triangle[n-1][j];
    }
    
    // functional
    for(int i = n-2; i>= 0; i--){
        for(int j = i; j>= 0; j--){
            int move1 = triangle[i][j] + dp[i+1][j];
            int move2 = triangle[i][j] + dp[i+1][j+1];
            dp[i][j] = min(move1,move2);
        }
    }
    return dp[0][0];
}
```


#### Approach 3 : Space Optimization

- There is i+1 and i only, so we need only the next row,
- so i just need to store the 2 rows
- current row and next row (dp)
- thus these 2 are needed.

```cpp
int minimumTotal(vector<vector<int>>& triangle) {
    int n = triangle.size();
    int m = triangle[n-1].size();
    
    vector<int> nextRow(m,-1);
    
    // Base Case
    for(int j = m-1; j>= 0; j--){
        nextRow[j] = triangle[n-1][j];
    }
    
    // functional
    for(int i = n-2; i>= 0; i--){
        vector<int> temp(m);
        for(int j = i; j>= 0; j--){
            int move1 = triangle[i][j] + nextRow[j];
            int move2 = triangle[i][j] + nextRow[j+1];
            temp[j] = min(move1,move2);
        }
        nextRow = temp;
    }
    return nextRow[0];
}
```

## 11. Minimum Maximim Falling Path Sum (Variable Starting Point and Variable Ending Point)

|Points|Image|
|---|---|
|This question has variable starting and variable ending point.|![image](https://user-images.githubusercontent.com/35686407/177093241-6e91a5e8-7600-4fde-b5aa-a01a8bd608bf.png)|
you can start anywhere from the first row and and you can end anywhere in the ending row||

- Uniformity is not there, we can not apply greedy
- Start from any cell in the first row and end in any cell in the last row
- Try out all the paths ~ Recursion

> Steps

![image](https://user-images.githubusercontent.com/35686407/177097338-a86187b5-f8ee-454a-a74f-5b9e458049aa.png)

#### Approach 1: Recursion + Memoization
- TC for rec : from each cell 3 options : 3^n
- SC for rec : O(n) , n rows
- TC for memo : O(NxM)
- SC for memo : O(NxM)

```cpp
class Solution {
public:
    int f(int i,int j,vector<vector<int>>& matrix,vector<vector<int>>& memo){
        // niche se upar aa rhe hai, top down approach
        if(j < 0 || j >= matrix[0].size()) return INT_MAX;
        if(i == 0) return matrix[0][j];
        
        if(memo[i][j] != -1) return memo[i][j];
        
        int up = INT_MAX,left = INT_MAX,right = INT_MAX;
        
        up = f(i-1,j,matrix,memo);
        left = f(i-1,j-1,matrix,memo);
        right = f(i-1,j+1,matrix,memo);
        
        if(up != INT_MAX) up += matrix[i][j];
        if(left != INT_MAX) left += matrix[i][j];
        if(right != INT_MAX) right += matrix[i][j];
        
        return memo[i][j] = min({up,left,right});
    }
    
    int minFallingPathSum(vector<vector<int>>& matrix) {
        int n = matrix.size();
        int m = matrix[0].size();
        vector<vector<int>> memo(n,vector<int>(m,-1));
        int mini = INT_MAX;
        for(int j = 0; j < m; j++){
            int val = f(n-1,j,matrix,memo);
            mini = min(mini,val);
        }
        return mini;
    }
};
```

#### Appraoach 2 : Tabulation

- TC : O(N x M)
- SC : O(N x M)

```cpp
int minFallingPathSum(vector<vector<int>>& matrix) {
    int n = matrix.size();
    int m = matrix[0].size();
    vector<vector<int>> dp(n,vector<int>(m,-1));
    
    // Base Case
    for(int j = 0; j < m; j++){
        dp[0][j] = matrix[0][j];
    }
    
    // functional
    for(int i = 1; i < n; i++){
        for(int j = 0; j < m; j++){
            
            int up = INT_MAX,left = INT_MAX,right = INT_MAX;
            
            up = matrix[i][j] + dp[i-1][j];
            if(j-1 >= 0) left = matrix[i][j] + dp[i-1][j-1];
            if(j+1 < m) right = matrix[i][j] + dp[i-1][j+1];
            
            dp[i][j] = min({up,left,right});
            
        }
    }
    
    int ans = INT_MAX;
    for(int j = 0; j < m; j++){
        ans = min(ans,dp[n-1][j]);
    }
    return ans;
}
```

#### Approach 3 : Space Optimization

- TC : O(N x M)
- SC : O(M)

```cpp
class Solution {
public:
    int minFallingPathSum(vector<vector<int>>& matrix) {
        int n = matrix.size();
        int m = matrix[0].size();
        vector<int> prev(m,-1);
        
        // Base Case
        for(int j = 0; j < m; j++){
            prev[j] = matrix[0][j];
        }
        
        // functional
        for(int i = 1; i < n; i++){
            vector<int> cur(m);
            for(int j = 0; j < m; j++){
                
                int up = INT_MAX,left = INT_MAX,right = INT_MAX;
                
                up = matrix[i][j] + prev[j];
                if(j-1 >= 0) left = matrix[i][j] + prev[j-1];
                if(j+1 < m) right = matrix[i][j] + prev[j+1];
                
                cur[j] = min({up,left,right});
                
            }
            prev = cur;
        }
        
        int ans = INT_MAX;
        for(int j = 0; j < m; j++){
            ans = min(ans,prev[j]);
        }
        return ans;
    }
};
```

## 12. Chocolate / Cherry Pickup II (3D DP Concept)

#### Approach 1 : Recursion + Memoization

- TC for recursion : 3^n x 3^n
- SC for recursion : O(n)
- TC for memo : O(N x M x M) X 9
- SC for memo : O(N x M x M) + O(N)

```cpp
class Solution {
public:
    
    typedef vector<int> vi;
    typedef vector<vi> vvi;
    typedef vector<vvi> vvvi;
    
    int f(int i,int j1,int j2,int r,int c,vvi& grid,vvvi& memo){
        if(j1 < 0 || j2 < 0 || j1 >= c || j2 >= c){
            return -1e8;
        }
        
        if(i == r - 1){
            if(j1 == j2) return grid[i][j1];
            else return grid[i][j1] + grid[i][j2];
        }
        
        if(memo[i][j1][j2] != -1) return memo[i][j1][j2];
        
        int maxi = -1e8;
        
        for(int ja = -1 ; ja <= 1; ja++){ // a - alice
            for(int jb = -1; jb <= 1; jb++){ // b - bob
                int val;
                if(j1 == j2){ // abhi vali value
                    val = grid[i][j1];
                }else{
                    val = grid[i][j1] + grid[i][j2];
                }
                val += f(i+1,j1+ja,j2+jb,r,c,grid,memo);
                maxi = max(maxi,val);
            }
        }
        return memo[i][j1][j2] = maxi;
    }
    
    int cherryPickup(vector<vector<int>>& grid) {
        int r = grid.size();
        int c = grid[0].size();
        vvvi memo(r,vvi(c,vi(c,-1)));
        return f(0,0,c-1,r,c,grid,memo);
    }
};
```

#### Tabulation :

```cpp
class Solution {
public:
    
    typedef vector<int> vi;
    typedef vector<vi> vvi;
    typedef vector<vvi> vvvi;
    
    int cherryPickup(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        vvvi dp(n,vvi(m,vi(m,-1)));
        
        // BASE CASE
        for(int j1 = 0; j1 < m; j1++){
            for(int j2 = 0; j2 < m; j2++){
                dp[n-1][j1][j2] = (j1 == j2) ? grid[n-1][j1] : (grid[n-1][j1] + grid[n-1][j2]);
            }
        }
        
        // Functionality
        for(int i = n-2; i>= 0; i--){
            for(int j1 = 0; j1 < m; j1++){
                for(int j2 = 0; j2 < m; j2++){
                    int maxi = -1e8;
                    for(int ja = -1 ; ja <= 1; ja++){ // a - alice
                        for(int jb = -1; jb <= 1; jb++){ // b - bob
                            int val;
                            if(j1 + ja >= 0 && j1 + ja < m && j2 + jb >= 0 && j2 + jb < m){
                                val = dp[i+1][j1+ja][j2+jb];
                            }else{
                                val = -1e8;
                            }
                            
                            if(j1 == j2){ // abhi vali value
                                val += grid[i][j1];
                            }else{
                                val += grid[i][j1] + grid[i][j2];
                            }
                            maxi = max(maxi,val);
                        }
                    }
                    dp[i][j1][j2] = maxi;
                }
            }
        }
        return dp[0][0][m-1];
    }
};
```

#### Approach 3 : Space Optimization 

```cpp
class Solution {
public:
    
    typedef vector<int> vi;
    typedef vector<vi> vvi;
    typedef vector<vvi> vvvi;
    
    int cherryPickup(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        vector<vector<int>> front(m,vector<int>(m,-1));
        vector<vector<int>> cur(m,vector<int>(m,-1));
        
        // BASE CASE
        for(int j1 = 0; j1 < m; j1++){
            for(int j2 = 0; j2 < m; j2++){
                if(j1 == j2){
                    front[j1][j2] = grid[n-1][j1];
                }else{
                    front[j1][j2] = grid[n-1][j1] + grid[n-1][j2];
                }
            }
        }
        
        // Functionality
        for(int i = n-2; i>= 0; i--){
            for(int j1 = 0; j1 < m; j1++){
                for(int j2 = 0; j2 < m; j2++){
                    int maxi = -1e8;
                    for(int ja = -1 ; ja <= 1; ja++){ // a - alice
                        for(int jb = -1; jb <= 1; jb++){ // b - bob
                            int val;
                            if(j1 + ja >= 0 && j1 + ja < m && j2 + jb >= 0 && j2 + jb < m){
                                val = front[j1+ja][j2+jb];
                            }else{
                                val = -1e8;
                            }
                            
                            if(j1 == j2){ // abhi vali value
                                val += grid[i][j1];
                            }else{
                                val += grid[i][j1] + grid[i][j2];
                            }
                            maxi = max(maxi,val);
                        }
                    }
                    cur[j1][j2] = maxi;
                }
            }
            front = cur;
        }
        return front[0][m-1];
    }
};
```

## Dp On Subsequences/Subsets & Target

|Defination|Image|
|---|---|
|Contigious as well as Non Contigious Elements are subsequence|![image](https://user-images.githubusercontent.com/35686407/177139853-6f1cdbfb-5ed0-4548-8f81-2ed3dc3336ee.png)|

## 14. Subset Sum equals to Target

#### Basic Approach
- Generate all subsequence and and find which gives sum K
- Two options : Power Set and Recursion
- Does it ask us to generate all > No.
- Question says - does there exists 1 subset with sum K ? no need to genetate all

#### Approach 1 : Recursion + Memoization

1. Express everyting in terms on Index , [Every array problem have index] | on every index we have to take care of the target we are looking for
    - `[THUMB RULE]` : express (index,target) 
2. Explore possibilities of that index
    - is part of subsequence : pick
    - not part of subsequence : not pick
3. if any of them give true, return true. `return T/F`

> express : f(n-1,target) ~ in the entire array till index n-1 does there exists target ?

- Base Cases :
    - target = 0 return true
    - idx == 0 return arr[0] == target

- Take and Not Take Concept,
- if i am at index 0, and if i found my target required, return true else return false;

#### Approach 1 : Recursion + Memoization

```cpp
bool f(int idx,int target,vector<int>& arr,vector<vector<int>>& memo){
    if(target == 0) return true;
    if(idx == 0) return (arr[0] == target);
    if(memo[idx][target] != -1) return memo[idx][target];
    // notpick
    bool notpick = f(idx-1,target,arr,memo);
    //pick
    bool pick = false;
    if(arr[idx] <= target){
        pick = f(idx-1,(target-arr[idx]),arr,memo);
    }
    return memo[idx][target] = pick || notpick;
}

bool subsetSumToK(int n, int k, vector<int> &arr) {
    vector<vector<int>> memo(n,vector<int>(k+1,-1));
    return f(n-1,k,arr,memo);
}
```

#### Approach 2 : Tabulation

- first base case is , when target is 0 no matter what the idx is, it is true, 
- therefore dp first column is always true;
- now second base case is, if idx == 0 , arr[0] == target then it is true else false,
- therefore, there is only one value which is equal to the target , idx == 0, means there is only one element in the array, it , then target is true if, arr[0] == target.
- so as there is onle element in the target, then, dp[0][arr[0]] = dp[0][first element of array] = true., 
- mtlb ye hai ki , hmare paas ek hi element hai and hme target bnana hai, target tbhi bnega na jb hmara a[0] equal hoga target ke, otherwise nhi bnega.
- TC : O(n x target)
- SC : O(n x target)

> Note :

![image](https://user-images.githubusercontent.com/35686407/177253195-20b9cbea-c760-43bb-abc9-db05aa6e97f2.png)
![image](https://user-images.githubusercontent.com/35686407/177253237-10d2ca02-e888-4746-9927-09abd933dcfd.png)
    
```cpp
bool subsetSumToK(int n, int k, vector<int> &arr) {
    vector<vector<bool>> dp(n,vector<bool>(k+1,false));
    
    // target == 0 ,  all true
    for(int idx = 0 ; idx < n; idx++){
        dp[idx][0] = true;
    }
    // Another base case
    dp[0][arr[0]] = true; // because there is only one element
    
    for(int idx = 1; idx < n; idx++){
        for(int target = 1; target < k+1; target++){
            bool notpick = dp[idx-1][target];
            bool pick = false;
            if(arr[idx] <= target){
                pick = dp[idx-1][target-arr[idx]];
            }
            dp[idx][target] = notpick || pick;
        }
    }
    return dp[n-1][k];
}
```

#### Appraoch 3 : Space Optimization

- Whenever you see idx - 1, then its always possible to make space optimization.
- But we have to take care of something,
- first time we always take the index 0,
- some a[i] is marked as true
- and in base case, for every 0th index , it is marked as true, always,
- `Thumb Rule` : every time you make the new Row,  index 0 is marked as true

> Note :

![image](https://user-images.githubusercontent.com/35686407/177253195-20b9cbea-c760-43bb-abc9-db05aa6e97f2.png)
![image](https://user-images.githubusercontent.com/35686407/177253237-10d2ca02-e888-4746-9927-09abd933dcfd.png)
    
```cpp
bool subsetSumToK(int n, int k, vector<int> &arr) {
    vector<bool> prev(k+1,false),cur(k+1,false);
    // Base case
    prev[0] = cur[0] = true;
    prev[arr[0]] = true; // because there is only one element
    
    for(int idx = 1; idx < n; idx++){
        for(int target = 1; target < k+1; target++){
            bool notpick = prev[target];
            bool pick = false;
            if(arr[idx] <= target){
                pick = prev[target-arr[idx]];
            }
            cur[target] = notpick || pick;   
        }
        prev = cur;
    }
    return prev[k];
}
```

## 15. Partition Equal Subset Sum

|Note|Image|
|---|---|
|we have to divide the array in such a way that two subsets have equal sum|![image](https://user-images.githubusercontent.com/35686407/177249834-a5307919-44f5-437e-a06a-cee00de52fc2.png)|

|Point|Image|
|---|---|
| 1. Entire Subset Sum = S , then Sum Subset of S1 = S/2 |![image](https://user-images.githubusercontent.com/35686407/177250081-8c57d7f1-daaa-43d0-9bbc-c0b24e5812ba.png)|

- Divide them in exactly two subsets, such that sum1 = sum2
- S : Odd ~ Not Possible
- S : Even , Looking for a subset with sum S/2
- if, one subset is S/2 then other will also be S/2 (remaning elements are bound to give S/2)
- Therfore, it boils down to , check Given an array there exists a target = S/2 , where S = Total Sum
- Statement 1 in code - [Subset Sum Equals To Target](#14-subset-sum-equals-to-target)

```cpp
bool canPartition(vector<int>& nums) {
    int sum = accumulate(nums.begin(),nums.end(),0);
    if((sum&1)) return false;
    int target = sum/2;
    int n = nums.size();
    return subsetSumEqualsTarget(nums,target); // Statement 1
}
```

## 16. Partiton of a Set into Two Subsets with Minimum absolute sum Difference

|abs(Sum1 - Sum2) is as minimal as possible|Example|
|---|---|
|![image](https://user-images.githubusercontent.com/35686407/177254141-12f5af49-7025-4e31-8a13-9a50fba2a0b3.png)|![image](https://user-images.githubusercontent.com/35686407/177254101-2bc05c55-16ca-4605-b9bc-8e96aaa4bbe4.png)|

|What `dp[i][j]` Signifies ?|Image|
|---|---|
|If we look at the dp table in Subset sum equal to target  table, them each dp[i][j] signifies something. Here, dp[4][0] signifies, is there is a possibility that with 4 elements we can create target sum 0, which is true,and if you think logically, it is true. Also, if we see at the dp[4][4] . it says is there is a possibility in creating target sum = 4 from the 4 elements, and it is true|![image](https://user-images.githubusercontent.com/35686407/177257684-eda781bb-9f07-4a72-b6b0-77e0866ec446.png)|


- f(n-1,target) means -> can array index upto n-1 achieve a given target ?
     - ans will lie at dp[n-1][target]
     - dp[4][7] == true, then we can have subset of sum 7.
- So , we want to achive the minimum sum difference, `abs(sum1 - sum2) is minimal`
- agar hum srf sum1 pr focus kre to kya sum2 nikal skte hai ? yes , if we know the total sum
- to hum sum1 mae hr possible target ko check krenge ki kya ye sum possible hai as sum1
    - minimum value of sum1 is 0
    - maxumum value of sum1 is sum of all array (take all elements to subset 1)
- So, we need to make the dp array such that, it have all possible sum from 0 to total sum of array
- and we will find the minimum by trying all valid subset sum 1 taken from 0 to total sum.
- Now after creating dp array, check if target is possible.
- if possible , then take it as sum1 and find the sum 2 and calculate the difference and then find the minimum difference. from all possible sum1.

> Example

- `arr[] : [3 2 7]`
- s1 - sum1 possible (from dp array)
- s2 - total - sum1
![image](https://user-images.githubusercontent.com/35686407/177259731-29ea984c-9881-44f6-971b-8046bba95545.png)
- observe : Repetative, s1 = 0, s2 = 12 | and after some moment , s1 = 12 , s2 = 0
- and other also follow same pattern,
- so , we will iterate for half 

> Steps :

- Subset sum ka dp array bnao upto total sum
- ab hr True value ko possible value mano s1 kifrom last row of dp array, as it include all elements of array and find kro s2 ki value
- ab unka difference nikalkr, minimum ke sath compare kro

```cpp
void createDPArray(vector<int>& arr,int n,int total,vector<vector<bool>>& dp){
    // subset sum dp array
    for(int idx = 0; idx < n; idx++){
        dp[idx][0] = true;
    }
    
    if(arr[0] <= total) dp[0][arr[0]] = true;
    
    for(int idx = 1; idx < n; idx++){
        for(int target = 1; target <= total ; target++){
            bool notpick = dp[idx-1][target];
            bool pick = false;
            if(arr[idx] <= target){
                pick = dp[idx-1][target-arr[idx]];
            }
            dp[idx][target] = pick || notpick;
        }
    }
}

int minSubsetSumDifference(vector<int>& arr, int n)
{
	int total = accumulate(arr.begin(),arr.end(),0);
    vector<vector<bool>> dp(n,vector<bool>(total+1,false));
    
    createDPArray(arr,n,total,dp);
    
    int mini = 1e9;
    for(int sum1 = 0; sum1 <= total/2; sum1++){
        if(dp[n-1][sum1] == true){
            int sum2 = total - sum1;
            mini = min(mini , abs(sum1-sum2));
        }
    }
    return mini;
}
```

## 17. Count Subsets with Sum K (Pattern : DP on Subsequence and Subset Sum , given is target)

![image](https://user-images.githubusercontent.com/35686407/177265006-29856c3d-a9ff-490e-ab3e-c927ec830f72.png)

> Whenever there is a problem related to count :

- Base Case :
    - condition satisfies : return 1
    - else : return 0
- all recursive calls will be add up , f() + f() + ... to count all possibilities

> How to geenerate recursion ?

1. Express in terms of indexes
2. explain all possibilities
3. Sum of all possibilities and return it gives total number of ways.

#### Approach 1 : Recursion + Memoization
- TC for Rec : O(2^n)
- SC for Rec : O(n)
- TC for Memoization : O(N x Sum)
- SC : O(N x Sum) + O(N)

```cpp
int f(int idx,int target,vector<int>& nums,vector<vector<int>>& memo){
    if(target == 0) return 1;
    if(idx == 0){
        if(nums[0] == target) return 1;
        else return 0;
    }
    if(memo[idx][target] != -1) return memo[idx][target];
    int notpick = f(idx-1,target,nums,memo);
    int pick = 0;
    if(nums[idx] <= target){
        pick = f(idx-1,target-nums[idx],nums,memo);
    }
    return memo[idx][target] = pick+notpick;
}

int findWays(vector<int> &num, int tar)
{
    int n = num.size();
    vector<vector<int>> memo(n,vector<int>(tar+1,-1));
    return f(n-1,tar,num,memo);
}
```

#### Approach 2 : Tabulation

```cpp
int findWays(vector<int> &arr, int tar)
{
    int n = arr.size();
    vector<vector<int>> dp(n,vector<int>(tar+1,0));
    
    // Base Case
    for(int idx = 0; idx < n; idx++){
        dp[idx][0] = 1;
    }
    if(arr[0] <= tar) dp[0][arr[0]] = 1;
    
    for(int idx = 1; idx < n; idx++){
        for(int target = 1; target <= tar; target++){
            int notpick = dp[idx-1][target];
            int pick = 0;
            if(arr[idx] <= target){
                pick = dp[idx-1][target-arr[idx]];
            }
            dp[idx][target] = pick+notpick;
        }
    }
    
    return dp[n-1][tar];
}
```

#### Appraoch 3 : Space Optimization

```cpp
int findWays(vector<int> &arr, int tar)
{
    int n = arr.size();
    vector<int> prev(tar+1,0),cur(tar+1,0);
    
    // Base Case
    prev[0] = cur[0] = 1;
    if(arr[0] <= tar) prev[arr[0]] = 1;
    
    for(int idx = 1; idx < n; idx++){
        for(int target = 1; target <= tar; target++){
            int notpick = prev[target];
            int pick = 0;
            if(arr[idx] <= target){
                pick = prev[target-arr[idx]];
            }
            cur[target] = pick+notpick;
        }
        prev = cur;
    }
    return prev[tar];
}
```

### Array is given : [0,0,1] , code give 1 subset , ideally it should give 4
![image](https://user-images.githubusercontent.com/35686407/177273443-b644860c-649a-439b-98d7-2c1bbc377c5a.png)
- is 0 alter the sum ? NO, addition of 0 and removal of 0 didnt change the sum.
- Number of zeros = 2.
- In How many ways 2 zeros can be represented.
![image](https://user-images.githubusercontent.com/35686407/177279718-1be706f1-5be2-4dac-99f9-bc71d090911f.png)
![image](https://user-images.githubusercontent.com/35686407/177279724-5c5f6ee1-b5bb-4791-9032-226b2b31edb7.png)
![image](https://user-images.githubusercontent.com/35686407/177279766-a41387b8-b8fd-4b45-934f-4e7d301d9547.png)

How do you correct it ?
- there is a line sum == 0 return 1
- so i need to go deep, when sum = 0,
- remove sum == 0
- go deep till index == 0
- if(idx == 0) sum == 0 and arr[0] == 0 return 2; // 2 possible ways to form take or not take
- if(idx == 0) sum == 0 and arr[0] != 0, then its only 1 option , i.e., not takling arr[0] , return 1
- if(idx == 0) sum == 0 and sum == arr[0] return 1;

![image](https://user-images.githubusercontent.com/35686407/177280682-b7c796f1-cc1c-4cba-a8ca-43de7cd14971.png)


## 18. Count Partitions with given Difference

- Problem is to find , how many subsets are there which have S1 - S2 = D, where S1 > S2
![image](https://user-images.githubusercontent.com/35686407/177282068-0a08a677-645e-40d8-9152-8d27b5532dfa.png)
- Looking for total subsets whose sum is (total-D)/2
- Question boils down to , find the count of the subsets whose total sum = (total-D)/2 , modified target
- Edge Cases ? given : nums[i] >= 0
- total - D cannot be negative, it have to be > 0 , `(total - D) > 0`,
    - negative tb ho skta hai, jb array ke sare element 0 ho and D > 0 ho
- s2 = sum of subset, if it is a subset and numbers are > 0, how subset sum is negative
- given all are intergers , so, there should not be fractions and we are dividing it by 2, so `(totalSum - D)` has to be `even.`
- also, we are dividing by 2, so there will be no fractions

#### Appraoch 1 : Recursion + Memoization

```cpp
int mod = 1e9 + 7;

int f(int idx,int target,vector<int>& arr,vector<vector<int>>& memo){
    if(idx == 0){
        if(target == 0 && arr[idx] == 0) return 2;
        if(target == 0 ||  target == arr[0]) return 1;
        return 0;
    }
    if(memo[idx][target] != -1) return memo[idx][target];
    int notpick = f(idx-1,target,arr,memo);
    int pick = 0;
    if(arr[idx] <= target){
        pick = f(idx-1,target-arr[idx],arr,memo);
    }
    return memo[idx][target] = (pick+notpick)%mod;
}

int count(vector<int>& arr,int target){
    int n = arr.size();
    vector<vector<int>> memo(n,vector<int>(target+1,-1));
    return f(n-1,target,arr,memo);
}

int countPartitions(int n, int d, vector<int> &arr) {
    // s1 - s2 = D
    // s1 = total - s2
    // total - 2 x s2 = D
    // s2 = (total - D)/2
    // (total - D) > 0  and even, as there are no fractions
    
    int totalSum = accumulate(arr.begin(),arr.end(),0);
    int total_D = totalSum - d;
    if(total_D < 0 || (total_D %2)) return 0;
    int find = total_D/2;
    
    return count(arr,find);
}
```

#### Appraoch 2: Tabulation

- What are the base cases in the recurson ?

![image](https://user-images.githubusercontent.com/35686407/177302771-8cdac487-da14-4e37-b9d8-af068295c46f.png)

|Memoization|Tabulation|
|----|---|
|if our target is 0 , and arr[0] is also 0, then we have 2 cases because 0 uthao to bhi target 0 hi rhega , 0 na uthao to bhi target 0 hi rhega | if arr[0][0] == 0 : dp[0][0] = 2, it means that idx == 0 hai and sum == 0 hai, to i have two options , rather pick it or not pick it , as pick 0 and not pick 0 didnt affect my ans |
|and if target == 0 and arr[0] != 0 , suppose mera target 0 hai lekin array ka element at idx = 0 , 0 nhi hai suppose 5 hai, to how many options i have to choose pick or not pikc ? i can not pick it, because if target pehele se 0 hia , uthauya to 0-ele = -ele < 0 ho jayega jbki 0 pehle se hi hia, to 1 hi option hai as i will not pick | else dp[0][0] = 1 , because sum == 0  and arr[0] != 0 , we have only 1 option to leave it, not to pick it,|

- if arr[0] != 0 && arr[0] <= target : dp[0][arr[0]] = 1; isme hme ye pta hai ki agar arr[0] <= target hoga vha 1 krenge but, ye bhi to socho ki agar arr[0] == 0, ho gya to ? ye to first if condition hai ki sum == 0 hai as arr[0] = 0, then it should be equal to 2

```cpp
int count(vector<int>& arr,int target){
    int n = arr.size();
    vector<vector<int>> dp(n,vector<int>(target+1,0));
    
    // Base Case
    if(arr[0] == 0) dp[0][0] = 2; // 2 case pick or not pick
    else dp[0][0] = 1; // 1 case not pick
    
    // num[0] == 0 ?
    if(arr[0] != 0 && arr[0] <= target) dp[0][arr[0]] = 1;
    
    // functional
    for(int idx = 1; idx < n; idx++){
        for(int sum = 0; sum <= target; sum++){
            int notpick = dp[idx-1][sum];
            int pick = 0;
            if(arr[idx] <= sum){
                pick = dp[idx-1][sum-arr[idx]];
            }
            dp[idx][sum] = (pick+notpick)%mod;
        }
    }
    
    return dp[n-1][target];
}

int countPartitions(int n, int d, vector<int> &arr) {
    // s1 - s2 = D
    // s1 = total - s2
    // total - 2 x s2 = D
    // s2 = (total - D)/2
    // (total - D) > 0  and even, as there are no fractions
    
    int totalSum = accumulate(arr.begin(),arr.end(),0);
    int total_D = totalSum - d;
    if(total_D < 0 || (total_D %2)) return 0;
    int find = total_D/2;
    
    return count(arr,find);
}
```

#### Approach 3 : Space Optimizaton

```cpp
int mod = 1e9 + 7;
int count(vector<int>& arr,int target){
    int n = arr.size();
    vector<int> prev(target+1,0),cur(target+1,0);
    
    // Base Case
    if(arr[0] == 0) prev[0] = 2; // 2 case pick or not pick
    else prev[0] = 1; // 1 case not pick
    
    // num[0] == 0 ?
    if(arr[0] != 0 && arr[0] <= target) prev[arr[0]] = 1;
    
    // functional
    for(int idx = 1; idx < n; idx++){
        for(int sum = 0; sum <= target; sum++){
            int notpick = prev[sum];
            int pick = 0;
            if(arr[idx] <= sum){
                pick = prev[sum-arr[idx]];
            }
            cur[sum] = (pick+notpick)%mod;
        }
        prev = cur;
    }
    
    return prev[target];
}

int countPartitions(int n, int d, vector<int> &arr) {
    // s1 - s2 = D
    // s1 = total - s2
    // total - 2 x s2 = D
    // s2 = (total - D)/2
    // (total - D) > 0  and even, as there are no fractions
    
    int totalSum = accumulate(arr.begin(),arr.end(),0);
    int total_D = totalSum - d;
    if(total_D < 0 || (total_D %2)) return 0;
    int find = total_D/2;
    
    return count(arr,find);
}
```

## 19. 0-1 KnapSack (Very Very Important) [Most Common Asked Question] [Variation can be asked]

#### Approach 1 : Recrusion + Memoization

- we write the base case on 0, as we start from n-1
- if idx == 0 :
    - f(0,W) means, single element bag weight W
    - max value he can get ? if weight of element is <= W return value[0]
    - but if W > weight value, he cannot able to pick else return 0
- TC of recursion : 2^n
- SC of recrusion : O(N)
- TC of memoization : O(NxW)
- SC of Memoization : O(NxW)

```cpp
int f(int idx,int W,vector<int>& weight,vector<int>& value,vector<vector<int>>& memo){
    if(idx == 0){
        if(weight[idx] <= W) return value[idx];
        else return 0;
    } 
    if(memo[idx][W] != -1) return memo[idx][W];
    // not pick
    int notpick = 0 + f(idx-1,W,weight,value,memo);
    int pick = INT_MIN;
    if(weight[idx] <= W){
        pick = value[idx] + f(idx-1,W-weight[idx],weight,value,memo);   
    }
    return memo[idx][W] = max(notpick,pick);
}

int knapsack(vector<int> weight, vector<int> value, int n, int maxWeight) 
{
    vector<vector<int>> memo(n,vector<int>(maxWeight+1,-1));
	return f(n-1,maxWeight,weight,value,memo);
}
```

#### Approach 2 : Tabulation

- write the base case
- int dp[N][W+1]
- for i = wt[0] to W , i can steal it, because, wt <= W , i can steal dp[0][i] = value[0]
- index : n-1 to 0 in rec, therefore in tab : its 1 to n-1
- and weight : W to 0 in rec , therfore in tab : its 0 to W
![image](https://user-images.githubusercontent.com/35686407/177473591-7facd1ba-6f0a-4eb9-8b90-2b707346a639.png)

```cpp
int knapsack(vector<int> weight, vector<int> value, int n, int maxWeight) 
{
    vector<vector<int>> dp(n,vector<int>(maxWeight+1,0));
    
    // i have to fill dp[0] , idx = 0, base case
    // all W greater then wt[0] will pick the 0th element
    for(int i = weight[0] ; i <= maxWeight; i++){
        dp[0][i] = value[0];
    }
    
    for(int i = 1; i < n; i++){
        for(int j = 0; j <= maxWeight; j++){
            int notpick = 0 + dp[i-1][j];
            int pick = INT_MIN;
            if(weight[i] <= j){
                pick = value[i] + dp[i-1][j-weight[i]];
            }
            dp[i][j] = max(notpick,pick);
        }
    }
    
	return dp[n-1][maxWeight];
}
```

#### Approach 3 : 2 Row Space Optimization

```cpp
int knapsack(vector<int> weight, vector<int> value, int n, int maxWeight) 
{
    vector<int> prev(maxWeight+1),cur(maxWeight+1);
    
    // i have to fill dp[0] , idx = 0, base case
    // all W greater then wt[0] will pick the 0th element
    for(int i = weight[0] ; i <= maxWeight; i++){
        prev[i] = value[0];
    }
    
    for(int i = 1; i < n; i++){
        for(int j = 0; j <= maxWeight; j++){
            int notpick = 0 + prev[j];
            int pick = INT_MIN;
            if(weight[i] <= j){
                pick = value[i] + prev[j-weight[i]];
            }
            cur[j] = max(notpick,pick);
        }
        prev = cur;
    }
    
	return prev[maxWeight];
}
```

#### Appraoch 4 : 1 Row Space Optimization

- in recursion we use W-wt[idx]
- you see that if w is somewhere between, then w-wt[idx] will be in its left side, and right side is empty for that,
- but how will this helps ?,
- as who say us to write W from 0 to W, write it from W to 0,
- use same prev again and again, cur not needed.

|W is dependent on its left values|When we fill from right to left, W take tahe value as W-wt[idx] from left, so run 2nd loop from W to 0|
|---|---|
|![image](https://user-images.githubusercontent.com/35686407/177475538-f97bfa49-0658-4317-b330-ddc84ac8c3e8.png)|![image](https://user-images.githubusercontent.com/35686407/177476125-0ea7d6fe-e45b-48b4-92f3-a1e909edeaa4.png)|

- when i fill it from right, it only need its left values , so that is why it is working in only in 1 Row Array Space

```cpp
int knapsack(vector<int> weight, vector<int> value, int n, int maxWeight) 
{
    vector<int> prev(maxWeight+1);
    
    // i have to fill dp[0] , idx = 0, base case
    // all W greater then wt[0] will pick the 0th element
    for(int i = weight[0] ; i <= maxWeight; i++){
        prev[i] = value[0];
    }
    
    for(int i = 1; i < n; i++){
        for(int j = maxWeight; j >= 0; j--){
            int notpick = 0 + prev[j];
            int pick = INT_MIN;
            if(weight[i] <= j){
                pick = value[i] + prev[j-weight[i]];
            }
            prev[j] = max(notpick,pick);
        }
    }
    
	return prev[maxWeight];
}
```

## Coin Change (Minimum Coins)
- I can pick the same coin again and again.
- in the idx == 0 base case, how many coins i can take think ?
    - if arr[0] = 6 and target = 7, i can take probably no coints such as by taking infinite coins i can not make that 7, take 6,6,6,6,6 again and again. so return 1e9
    - if arr[0] = 4 and target = 12 , then i can take probably 3 coins. 12/4
    - So, i can take the coins only when target%coins[0] == 0


#### Appraoch 1: Recursion + Memoization
- TC for rec : >> O(2^n)
- SC : O(n)

```cpp
class Solution {
public:
    int solve(int idx,int target,vector<int>& coins,vector<vector<int>>& memo){
        
        if(idx == 0){
            if(target%coins[0] == 0) return target/coins[0];
            return 1e9;
        }
        if(memo[idx][target] != -1) return memo[idx][target];
        int notpick = 0+solve(idx-1,target,coins,memo);
        int pick = 1e9;
        if(coins[idx] <= target){
            pick = 1+solve(idx,target-coins[idx],coins,memo);
        }
        return memo[idx][target] = min(pick,notpick);
    }
    
    int coinChange(vector<int>& coins, int amount) {
        int n = coins.size();
        vector<vector<int>> memo(n,vector<int>(amount+1,-1));
        int x = solve(coins.size()-1,amount,coins,memo);
        if(x == 1e9) return -1;
        return x;
    }
};
```

#### Approach 2 : Tabulation

```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        int n = coins.size();
        vector<vector<int>> dp(n,vector<int>(amount+1,0));
        
        for(int target = 0; target <= amount; target++){
            dp[0][target] = (target%coins[0] == 0) ? target/coins[0] : 1e9;
        }
        
        for(int idx = 1; idx < n; idx++){
            for(int target = 0; target <= amount; target++){
                int notpick = 0+dp[idx-1][target];
                int pick = 1e9;
                if(coins[idx] <= target){
                    pick = 1+dp[idx][target-coins[idx]];
                }
                dp[idx][target] = min(pick,notpick);
            }
        }
        
        int x = dp[n-1][amount];
        if(x == 1e9) return -1;
        return x;
    }
};
```

#### Appraoch 3 : Space Optimization

```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        int n = coins.size();
        vector<int> prev(amount+1,0),cur(amount+1,0);
        
        for(int target = 0; target <= amount; target++){
            prev[target] = (target%coins[0] == 0) ? target/coins[0] : 1e9;
        }
        
        for(int idx = 1; idx < n; idx++){
            for(int target = 0; target <= amount; target++){
                int notpick = 0+prev[target];
                int pick = 1e9;
                if(coins[idx] <= target){
                    pick = 1+cur[target-coins[idx]];
                }
                cur[target] = min(pick,notpick);
            }
            prev = cur;
        }
        
        int x = prev[amount];
        if(x == 1e9) return -1;
        return x;
    }
};
```

## 21. Target Sum (Assign + and - sign)

- we can do this with recursion assigning + or - sign to each element and explore all the paths
- Can we do better ? Yes
- we have already done with the question, find the subset partiton with sum difference = D
- |S1 - S2| = D
![image](https://user-images.githubusercontent.com/35686407/177512837-cb574829-308a-4460-833d-bf0b6e4c067f.png)

> Now problem boils down to Count Partitions with given Difference [Link](#18-count-partitions-with-given-difference)


## 22. Coin Change 2 (Number of ways target can be maked)

![image](https://user-images.githubusercontent.com/35686407/177514578-22c74483-f4e8-4722-9833-addaa392e599.png)

|Note|Note|
|---|---|
|if question says any number of times you can pick, then always you have to land on the same index|if Question says about number of ways, then base case always return 1 or 0, if it reaches destination or not respectivelt.|

#### Appraoch 1 : Recursion + Memoization

- TC : O(2^n)
- SC : >> O(n) , worst O(target) [1] target = 100 
- TC for rec : O(n x target)
- SC : O(n x target) + O(target)

```cpp
int f(int idx,int target,vector<int>& coins,vector<vector<int>>& memo){
    if(idx == 0){
        if(target%coins[0] == 0) return 1;
        else return 0;
    }   
    if(memo[idx][target] != -1) return memo[idx][target];
    int nottake = f(idx-1,target,coins,memo);
    int take = 0;
    if(coins[idx] <= target){
        take = f(idx,target-coins[idx],coins,memo);
    }
    return memo[idx][target] = nottake + take;
}

int change(int amount, vector<int>& coins) {
    int n = coins.size();
    vector<vector<int>> memo(n,vector<int>(amount+1,-1));
    return f(n-1,amount,coins,memo);
}
```

#### Appraoch 2 : Tabulation

- TC : O(n x target)
- SC : O(n x target)

```cpp
int change(int amount, vector<int>& coins) {
    int n = coins.size();
    vector<vector<int>> dp(n,vector<int>(amount+1,0));
    
    for(int target = 0; target <= amount; target++){
        if(target%coins[0] == 0) dp[0][target] = 1;
        else dp[0][target] = 0;
    }
    
    for(int idx = 1; idx < n; idx++){
        for(int target = 0; target <= amount; target++){
            int nottake = dp[idx-1][target];
            int take = 0;
            if(coins[idx] <= target){
                take = dp[idx][target-coins[idx]];
            }
            dp[idx][target] = nottake + take;
        }
    }
    return dp[n-1][amount];
}
```

#### Appraoch 3 : Space Optimization

- TC : O(n x target)
- SC : O(target)

```cpp
int change(int amount, vector<int>& coins) {
    int n = coins.size();
    vector<int> prev(amount+1,0),cur(amount+1,0);
    
    for(int target = 0; target <= amount; target++){
        if(target%coins[0] == 0) prev[target] = 1;
        else prev[target] = 0;
    }
    
    for(int idx = 1; idx < n; idx++){
        for(int target = 0; target <= amount; target++){
            int nottake = prev[target];
            int take = 0;
            if(coins[idx] <= target){
                take = cur[target-coins[idx]];
            }
            cur[target] = nottake + take;
        }
        prev = cur;
    }
    return prev[amount];
}
```

## 23. Unbounded Knapsack

- Pick single item multiple times
![image](https://user-images.githubusercontent.com/35686407/177521451-6bd8e476-383e-450b-af7b-b2ae4ac03d88.png)
- Find the maximum possible value, you can get in knapsack.

#### Appraoch 1 : Recursion + Memoization

- Base Case, if weight is 8, and item weight is 3, then it takes only 2 times the same item, as there are infinite supply.

|Example|Base Case|
|---|---|
|![image](https://user-images.githubusercontent.com/35686407/177525345-610fef49-1b9c-43c4-8801-e8d7105d1871.png)|![image](https://user-images.githubusercontent.com/35686407/177525530-59525fd2-6580-4352-bb48-347ea73c8e92.png)|

```cpp
int f(int idx,int W,vector<int>& profit,vector<int>& weight,vector<vector<int>>& memo){
    if(idx == 0){
        return (W/weight[0])*profit[0];
    }
    if(memo[idx][W] != -1) return memo[idx][W];
    int nottake = 0 + f(idx-1,W,profit,weight,memo);
    int take = 0;
    if(weight[idx] <= W){
        take = profit[idx] + f(idx,W-weight[idx],profit,weight,memo);
    }
    return memo[idx][W] = max(take,nottake);
}

int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight)
{
    vector<vector<int>> memo(n,vector<int>(w+1,-1));
    return f(n-1,w,profit,weight,memo);
}
```

#### Tabulation

```cpp
int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight)
{
    vector<vector<int>> dp(n,vector<int>(w+1,0));
    
    for(int wt = 0; wt <= w; wt++){
        dp[0][wt] = (wt/weight[0])*profit[0];
    }
    
    for(int idx = 1; idx < n; idx++){
        for(int wt = 0; wt <= w; wt++){
            int nottake = 0 + dp[idx-1][wt];
            int take = 0;
            if(weight[idx] <= wt){
                take = profit[idx] + dp[idx][wt-weight[idx]];
            }
            dp[idx][wt] = max(take,nottake);
        }
    }
    
    return dp[n-1][w];
}
```

#### Appraoch 3 : Space Optimization

```cpp
int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight)
{
    vector<int> prev(w+1,0),cur(w+1,0);
    
    for(int wt = 0; wt <= w; wt++){
        prev[wt] = (wt/weight[0])*profit[0];
    }
    
    for(int idx = 1; idx < n; idx++){
        for(int wt = 0; wt <= w; wt++){
            int nottake = 0 + prev[wt];
            int take = 0;
            if(weight[idx] <= wt){
                take = profit[idx] + cur[wt-weight[idx]];
            }
           cur[wt] = max(take,nottake);
        }
        prev = cur;
    }
    
    return prev[w];
}
```

## 23. Unbounded Knapsack

- Pick single item multiple times
![image](https://user-images.githubusercontent.com/35686407/177521451-6bd8e476-383e-450b-af7b-b2ae4ac03d88.png)
- Find the maximum possible value, you can get in knapsack.

#### Appraoch 1 : Recursion + Memoization

- Base Case, if weight is 8, and item weight is 3, then it takes only 2 times the same item, as there are infinite supply.

|Example|Base Case|
|---|---|
|![image](https://user-images.githubusercontent.com/35686407/177525345-610fef49-1b9c-43c4-8801-e8d7105d1871.png)|![image](https://user-images.githubusercontent.com/35686407/177525530-59525fd2-6580-4352-bb48-347ea73c8e92.png)|

```cpp
int f(int idx,int W,vector<int>& profit,vector<int>& weight,vector<vector<int>>& memo){
    if(idx == 0){
        return (W/weight[0])*profit[0];
    }
    if(memo[idx][W] != -1) return memo[idx][W];
    int nottake = 0 + f(idx-1,W,profit,weight,memo);
    int take = 0;
    if(weight[idx] <= W){
        take = profit[idx] + f(idx,W-weight[idx],profit,weight,memo);
    }
    return memo[idx][W] = max(take,nottake);
}

int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight)
{
    vector<vector<int>> memo(n,vector<int>(w+1,-1));
    return f(n-1,w,profit,weight,memo);
}
```

#### Tabulation

```cpp
int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight)
{
    vector<vector<int>> dp(n,vector<int>(w+1,0));
    
    for(int wt = 0; wt <= w; wt++){
        dp[0][wt] = (wt/weight[0])*profit[0];
    }
    
    for(int idx = 1; idx < n; idx++){
        for(int wt = 0; wt <= w; wt++){
            int nottake = 0 + dp[idx-1][wt];
            int take = 0;
            if(weight[idx] <= wt){
                take = profit[idx] + dp[idx][wt-weight[idx]];
            }
            dp[idx][wt] = max(take,nottake);
        }
    }
    
    return dp[n-1][w];
}
```

#### Appraoch 3 : Space Optimization

```cpp
int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight)
{
    vector<int> prev(w+1,0),cur(w+1,0);
    
    for(int wt = 0; wt <= w; wt++){
        prev[wt] = (wt/weight[0])*profit[0];
    }
    
    for(int idx = 1; idx < n; idx++){
        for(int wt = 0; wt <= w; wt++){
            int nottake = 0 + prev[wt];
            int take = 0;
            if(weight[idx] <= wt){
                take = profit[idx] + cur[wt-weight[idx]];
            }
           cur[wt] = max(take,nottake);
        }
        prev = cur;
    }
    
    return prev[w];
}
```

#### Approach 4 : 1 Row Space Optimization

- if you analize the code of space optimization, you will see, what are you taking from prev row to the current row ? its not take , `prev[wt]` , so we are taking the same guy currently on which we are standing ar, so what if we paste it directly there, as take only work on the cur array.

|Image 1|Image 2|
|---|---|
|![image](https://user-images.githubusercontent.com/35686407/177529531-bce25910-fd49-4a45-968c-c8f83ff567af.png)|![image](https://user-images.githubusercontent.com/35686407/177529756-2f411b6c-0eb2-41d7-9a4e-80e96e000f6e.png)|

- previous value from the current index of prev array , we didnt need them. so we just use single array as space optimization.

```cpp
int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight)
{
    vector<int> prev(w+1,0);
    
    for(int wt = 0; wt <= w; wt++){
        prev[wt] = (wt/weight[0])*profit[0];
    }
    
    for(int idx = 1; idx < n; idx++){
        for(int wt = 0; wt <= w; wt++){
            int nottake = 0 + prev[wt];
            int take = 0;
            if(weight[idx] <= wt){
                take = profit[idx] + prev[wt-weight[idx]];
            }
           prev[wt] = max(take,nottake);
        }
    }
    
    return prev[w];
}

```

## 24. Rod Cutting Problem

![image](https://user-images.githubusercontent.com/35686407/177530995-996793c5-f446-4e4a-9f80-62e7e2ffd545.png)
- cut the rod into pieces, 
- for the length 1 rod, you will get the price = 2 Rs (for every length of rod), so 1 x 2 = 10 Rs.,
- another way to cut the rod is 1,2,2 ~ 2 + 5 + 5 = 12 Rs.
- maximize the cost

> Think in opposite fashion, try to make the rod length n from given lengths, we knwo that index 4 is of length 5, index 3 is of length 4 rod, etc.

![image](https://user-images.githubusercontent.com/35686407/177532105-93b77f57-04bd-4fb6-adde-11773839ce15.png)

> problem is similar to unbounded knapsack , in which we have given its weights and values to weights.

- Try to pick lengths and sum them up to make N, try in all possible ways.

![image](https://user-images.githubusercontent.com/35686407/177533002-7bb682b2-95ef-429f-b604-05b29bbab4fd.png)

- f(4,N) means till index 4 what is the max price you can obtain.
- Problem is similar to unbounded knap sack , rod lengths (index) as weights and and prices as values. 
- BASE CASE : f(0,N) it requires N rod of length 1 , what will be the price : N * value[0]

#### Approach 1 : Recursion + Memoization

```cpp
int f(int idx,int W,vector<int>& prices,vector<vector<int>>& memo){
    if(idx == 0){
        return (W/1)*prices[0];
    }
    if(memo[idx][W] != -1) return memo[idx][W];
    int notTake = 0 + f(idx-1,W,prices,memo);
    int take = -1e9;
    int rodLength = (idx+1);
    if(rodLength <= W){
        take = prices[idx] + f(idx,W-rodLength,prices,memo);
    }
    return memo[idx][W] = max(take,notTake);
}

int cutRod(vector<int> &price, int n)
{
    int idx = price.size()-1;
	vector<vector<int>> memo(idx+1,vector<int>(n+1,-1));
    return f(idx,n,price,memo);
}
```

#### Approach 2 : Tabulation

```cpp
int cutRod(vector<int> &prices, int n)
{
    int idx = prices.size()-1;
	vector<vector<int>> dp(idx+1,vector<int>(n+1,0));
    
    for(int wt = 0; wt <= n; wt++){
        dp[0][wt] = wt*prices[0];
    }
    
    for(int i = 1; i < idx+1 ; i++){
        for(int wt = 0; wt <= n; wt++){
            int notTake = 0 + dp[i-1][wt];
            int take = 0;
            int rodLength = (i+1);
            if(rodLength <= wt){
                take = prices[i] + dp[i][wt-rodLength];
            }
            dp[i][wt] = max(take,notTake);
        }
    }
    return dp[idx][n];
}

```

#### Approach 3 : Space Optimization

```cpp
int cutRod(vector<int> &prices, int n)
{
    int idx = prices.size()-1;
	vector<int> prev(n+1,0),cur(n+1,0);
    
    for(int wt = 0; wt <= n; wt++){
        prev[wt] = wt*prices[0];
    }
    
    for(int i = 1; i < idx+1 ; i++){
        for(int wt = 0; wt <= n; wt++){
            int notTake = 0 + prev[wt];
            int take = 0;
            int rodLength = (i+1);
            if(rodLength <= wt){
                take = prices[i] + cur[wt-rodLength];
            }
            cur[wt] = max(take,notTake);
        }
        prev = cur;
    }
    return prev[n];
}
```

#### Appraoch 4 : 1 Row Space Optimization

```cpp
int cutRod(vector<int> &prices, int n)
{
    int idx = prices.size()-1;
	vector<int> prev(n+1,0);
    
    for(int wt = 0; wt <= n; wt++){
        prev[wt] = wt*prices[0];
    }
    
    for(int i = 1; i < idx+1 ; i++){
        for(int wt = 0; wt <= n; wt++){
            int notTake = 0 + prev[wt];
            int take = 0;
            int rodLength = (i+1);
            if(rodLength <= wt){
                take = prices[i] + prev[wt-rodLength];
            }
            prev[wt] = max(take,notTake);
	}
     }
     return prev[n];
}
```

## DP on Strings

#### General Problems on : Comparison / Replaces / Edits

## 25. Longest Commoon Subswquence

![image](https://user-images.githubusercontent.com/35686407/177567179-2910f485-3349-4a90-bca7-13a73c985157.png)
- bc : consecutive and maintating the orer
- ac : didnt concecutive and maintain the order
- Subsequence : it can and cannot be consiqutive and as long as it maintains the order , it is subsequences.

> To print Subsequences : either use power set or user recursion(Pick or Non pick)

- 2^n subsequences in total

> Longest Common Subsequences

![image](https://user-images.githubusercontent.com/35686407/177567862-c9327a3f-c887-4c86-a3ae-c0f1d322ae1a.png)

- here from s1 , does a exisits in s2 as subsequence ? Yes, so till now length of longest subsequence is 1,
- and we keep finding on them.
- Longest Subsequnce in both is [adb] , length = 3

#### Appraoch 1 : Brute Force, generate all subsequences of both and compare. [Exponential in nature]

#### Approach 2 : `Genetate all subsequences and Compare on the Way` | Recursion

- Recursion | Dp ON strings
- Technically follow rec method, not generate these, instead of using parameters to generate them
- We try to the `some reccurance` which `give me the ans in through the way`

`Rules`:

1. Express everything in terms of index (idx1,idx2) for both strings
2. Explore possibility on that index
3. Take the best among them.

> f(2) signify the string at index 2, a single index cannot express both the string thereby i have to represent them by two indexes, where idx1 represent s1 and idx2 represent idx2

> f(2,2) : tell me the LCS of string s1 from 0 to 2 and string s2 friom 0 to 2
![image](https://user-images.githubusercontent.com/35686407/177569993-79f88845-ab07-44b1-97fd-f51df2c416f5.png)

f(2,5) : give me the LCS between s1 0 to 2 and string s2 0 to 5 , smaller and larger string.

> Now explore all possibilities

> SOLUTION : Do comparison on characters

- f(2,2) : s1[idx1] == s2[idx2] , it means i got subsequence of length 1 and shrink the string , new strings are ac | ce [ 1 + ac | ce ] = 1 + f(1,1);
- s1[idx1] != s2[idx2] , now something i am sure that ac will match with c of ce , or if there is ec | ce , then maybe it happends that e of ec match with ce's e , then we have to expplore both possibilities ,
    - v1 = f(idx1-1,idx2)
    - v2 = f(idx1,idx2-1)
    - return max of both , 0 + max(v1,v2); , 0 because there is no match.

![image](https://user-images.githubusercontent.com/35686407/177571869-fcf93a72-3112-40ae-b1eb-371fc9376338.png)

- If some of the index goes negative, rec ends and return 0; , either idx1 is negative or either idx2 is negative
- idx is negative means end the string. if its end of the string , `it length ? 0.`

> NOTE : IN STRING - MATHCH OR NOT MATCH PATTERN

#### Appraoch 1 : Recursion + Memoization

- TC : O(N x M)
- SC : O(N x M) + O(N+M)

```cpp
int f(int idx1,int idx2,string& text1,string& text2,vector<vector<int>>& memo){
        if(idx1 < 0 || idx2 < 0){
            return 0;
        }
        if(memo[idx1][idx2] != -1) return memo[idx1][idx2];
        if(text1[idx1] == text2[idx2]){
            return memo[idx1][idx2] = 1 + f(idx1-1,idx2-1,text1,text2,memo);
        }
        int v1 = f(idx1-1,idx2,text1,text2,memo);
        int v2 = f(idx1,idx2-1,text1,text2,memo);
        return memo[idx1][idx2] = max(v1,v2);
    }
    
    int longestCommonSubsequence(string text1, string text2) {
        int n1 = text1.size();
        int n2 = text2.size();
        vector<vector<int>> memo(n1,vector<int>(n2,-1));
        return f(n1-1,n2-1,text1,text2,memo);
    }
```

#### Appproach 2: Tabulation

1. Copy base case,
2. write changing parameter in opposite parameter
3. copy the reccurance

> But copy base case is bit tricky here, Why ? if(i < 0 || j < 0) return 0

- In base case, i and j are negative then it return 0,
- so we can't write base cases for -1
- we do `shifting of index, in order to write tabulation`.

![image](https://user-images.githubusercontent.com/35686407/177575336-22dea9aa-cda4-4799-9973-52718789e357.png)

- we have to right shift of the index. f(n,m) here n means n-1, m means m-1 , we shift it 1 right.

![image](https://user-images.githubusercontent.com/35686407/177575565-e77ded47-c537-4b65-96d3-911176ecdca9.png)

- So can i say ? f(i,j) , every i should be treated as i-1 and every j should be treated as j-1
- therefore, instead of i < 0 pr j < 0 , we write i == 0 or j == 0 retrurn 0

```cpp
// shifting index in recursion
int f(int idx1,int idx2,string& text1,string& text2,vector<vector<int>>& memo){
        if(idx1 == 0 || idx2 == 0){
            return 0;
        }
        
        if(memo[idx1][idx2] != -1) return memo[idx1][idx2];
        
        if(text1[idx1-1] == text2[idx2-1]){
            return memo[idx1][idx2] = 1 + f(idx1-1,idx2-1,text1,text2,memo);
        }
        int v1 = f(idx1-1,idx2,text1,text2,memo);
        int v2 = f(idx1,idx2-1,text1,text2,memo);
        return memo[idx1][idx2] = max(v1,v2);
    }
    //  return f(n1,n2,text1,text2,memo); // call
```

###### Tabulation : 

- Now, Base case is, i == 0 || j == 0 return 0;
- i == 0 means dp[0][anything] = 0
- j == 0 means dp[anything][0] = 0
- Now copy reccurance of shifted index and do process.

```cpp
class Solution {
public:
    
    int longestCommonSubsequence(string text1, string text2) {
        int n1 = text1.size();
        int n2 = text2.size();
        vector<vector<int>> dp(n1+1,vector<int>(n2+1,0));
        
        // BASE CASE
        for(int j = 0; j <= n2; j++){
            dp[0][j] = 0;
        }
        
        for(int i = 0; i <= n1; i++){
            dp[i][0] = 0;
        }
        
        // FUNCTIONAL
        for(int i = 1; i <= n1; i++){
            for(int j = 1; j <= n2; j++){
                if(text1[i-1] == text2[j-1]){
                    dp[i][j] = 1 + dp[i-1][j-1];
                }else{
                    int v1 = dp[i-1][j];
                    int v2 = dp[i][j-1];
                    dp[i][j] = max(v1,v2);   
                }
            }
        }
        
        return dp[n1][n2];
    }
};
```

#### Approach 3 : Space Optimization

```cpp
int longestCommonSubsequence(string text1, string text2) {
        int n1 = text1.size();
        int n2 = text2.size();
        vector<int> prev(n2+1,0),cur(n2+1,0);
        
        prev[0] = cur[0] = 0;
        
        for(int i = 1; i <= n1; i++){
            for(int j = 1; j <= n2; j++){
                if(text1[i-1] == text2[j-1]){
                    cur[j] = 1 + prev[j-1];
                }else{
                    int v1 = prev[j];
                    int v2 = cur[j-1];
                    cur[j] = max(v1,v2);   
                }
            }
            prev = cur;
        }
        
        return prev[n2];
    }
```

## Print Longest Common Subsequence

> Printing is simpler from the 2d dp array.

- string s1 = abcde
- string s2 = bdgek
- 2d dp array of longest common subsequence
- ans is on dp[5][5] , because we shift the index as we did in longest common subsequence.

![image](https://user-images.githubusercontent.com/35686407/177595967-ea46e721-a349-4b4e-8ebe-e19b5a0ed37a.png)

- meaning of dp[5][5] = i = 5 , entire string s1 and j = 5 , entire string s2
- meaning of dp[4][2] , i = 4 , take s1 of length 4 and take s2 of length 2 dp[4][2] = 2, longest length
 
> Understand how tabulation 2d dp filled up.

- if they char matched then , it checks to its previous that it matchs or not if yes then 1 + dp[i-1][j-1]
- if they didn't match then it take the maximum, which means that till now what is the maximum length which is matched. max(v1,v2) , v1 = dp[i-1][j] and v2 = dp[i][j-1];
- Now, we have to backtrack from the n,m position to 0th position in LCS
- so we move according to the same condition that
- if s1[i-1] == s2[j-1] move diagonall left upwards
- if they didn't match then we see that which is max , dp[i-1][j] or dp[i][j-1] whatever is maximum we move to that direction only.
![image](https://user-images.githubusercontent.com/35686407/177658125-139bf071-bf28-4d87-9ba7-dce0dd4fd3a3.png)

```cpp
string printLCS(string& s1,string& s2){
    int n1 = s1.size();
    int n2 = s2.size();

    vector<vector<int>> dp(n1+1,vector<int>(n2+1,-1));
    // BASE CASE
    for(int j = 0; j <= n2;j++){
        dp[0][j] = 0;
    }

    for(int i = 0; i <= n1;i++){
        dp[i][0] = 0;
    }

    // functional
    for(int i = 1; i <= n1; i++){
        for(int j = 1; j <= n2; j++){
            if(s1[i-1] == s2[j-1]){
                dp[i][j] = 1 + dp[i-1][j-1];
            }else{
                int v1 = dp[i-1][j];
                int v2 = dp[i][j-1];
                dp[i][j] = max(v1,v2);
            }
        }
    }

    // Printing
    int i = n1, j = n2;
    string ans(dp[n1][n2],'$'); 
    int index = ans.size()-1;
    while(i > 0 && j > 0){
        if(s1[i-1] == s2[j-1]){
            ans[index] = s1[i-1];
            index--;
            i--;j--;
        }else{
            if(dp[i-1][j] > dp[i][j-1]){
                i--;
            }else{
                j--;
            }
        }
    }
    return ans;
```

## 27. Longest Common Substring

> String s1 = abcd and s2 = abzd

![image](https://user-images.githubusercontent.com/35686407/177660532-5c1f8391-7c38-4d3a-80e1-258b12aba735.png)


- isme subsequence ki trh hi bharna hai 2d array ko ,
- 2d array subsequence mae kese bharta hai ? , vo dekhta hai ki kya abhi vala char matched hai . if yes hai to picle vale ke paas jata (i-1,j-1) hai check krta hai kya tu matched hai, mtlb tere tk kitni length ki subsequence bni hai, usme +1 kr deta hui, taki vo us subsequence mae khud ko bhi jod de
- if they match nhi krte vo max lete hai 2 values ka dp[i-1][j] and dp[i][j-1] , is max lene ka mtlb ye hai ki abhi tk maximum kitne char match ho chuke hai vhi idar cell mae likh do.
- But here substring is there, so, hum yha pr max nhi lenge dono ka, kyuki substing hota hai contiguous, to isme max lene se to hum subsequence ka pta lgayange instead we write 0, as hme discontiguous fashion ko aage nhi bhadana hai.
- jb substring ke liye 2d array fill krenge then hm ye dekhte hai ki, agar abhi vala char match krta hai to vo piche (i-1,j-1) ke paas jakr check krta hai ki tumhare tk kitne contiguous char match ho chuke hai, usme mera +1 kr do else dp[i][j] = 0 if char didn't match.
- so, we see in diagram also, when b matches, it checks for the a that how mnany char matches for string of len1 , and we also see we fill up 0 when a and b not matches in (1,2)

```cpp
int printLCSubstring(string& s1,string& s2){
    int n1 = s1.size();
    int n2 = s2.size();

    vector<vector<int>> dp(n1+1,vector<int>(n2+1,-1));
    // BASE CASE
    for(int j = 0; j <= n2;j++){
        dp[0][j] = 0;
    }

    for(int i = 0; i <= n1;i++){
        dp[i][0] = 0;
    }

    // functional
    int maxi = -1e9;

    for(int i = 1; i <= n1; i++){
        for(int j = 1; j <= n2; j++){
            if(s1[i-1] == s2[j-1]){
                dp[i][j] = 1 + dp[i-1][j-1];
                maxi = max(dp[i][j],maxi);
            }else{
                dp[i][j] = 0;
            }
        }
    }

    return maxi;
}
```

## 28. Longest Palindromic Subsequence

> Solution : lcs(string , reverse(string));

Why so ? because we know palindrome is the string which reads in both direction is same. so when we reverse the palindromic string it remains the same.

> Example : in this, we see that we have "babcbab" is palindromic substrng, which came when we comapre the two string one normal and second it's reverse, because it's reverse string starting char matches with the normal string starting char, which may lead to palindrome as it property says, reading from front or back remains same.

![image](https://user-images.githubusercontent.com/35686407/177661993-ed30812c-1007-483c-8a9e-9269aeb2ecea.png)


## 29. Minimum Insertions required to make the string Palindrome.

- you can insert any char to anywhere
- maximum number of operation is string + reverse(string)
- to find the minimum , keep the palindromic portion (subsequence) of string side, and check which portion left, just add that in reverse order, and put it between to make string palindrome.
- Always the portion left is (N - longestPalindromicSubsequence) which is my ans, as minimum insertions required to make string palindrome.
- `Solution:` `(n - longestPalindromicSubsequence)`

> Example

- string s1 = abcaa
- now we see that, aca, aba, aaa , these 3 are longest Palindrome suubsequence
- just pick anyone, suppose aaa
- a   a   a , now which portion left ? bc => a bc a __ a , just add reverse if bc that is cb => abcacba which is palindrome
- take any other palindromic subsequene, suppose aca => a `b` c `a` a , we have to put b and a in opposite direction from medium , => a `ab` c `ba` a ,
which is again palindromic subsequence.

Solution : `n - longest Palindromic Subsequence`


## 30. Minimum Operation to convert string1 to string2

- perform deletions and insertions
- maximum number of operations is `n+m` string lengths, because, delete all struing s1 and add all string s2.
- but we need to find minimum operations so,
- keep the common part so that we can touch only minimum portion so that to get the ans minimum.
- Common part is LCS (longest common subsequence)

> Example:

- string s1 = abcd
- string s2 = anc

- now, common porton of both is , ac 
- to convert abcd to ac , how many deletions required ? len(abcd) - len(ac)
- to convert ac to anc . how many insertion equired ? len(anc) - len(ac)
- `DELETION : (n - lcs)`
- `INSERTION : (m - lcs)`
- `TOTAL OPERATIONS : (n + m - 2 x lcs)`

> Solution : (n+m - 2 x lcs) where (n - lcs) is number of deletions and (m-lcs) is number of insertions. 


## 31.A. Shortest Common SuperSequence

- given string s1 and string s2, make a string s such that s1 and s2 both are in new string named as super sequence
![image](https://user-images.githubusercontent.com/35686407/177746929-281d276f-4614-4f1e-8275-6d71a70b889f.png)
- Join Both : brute+groot = brutegroot ~ One of the super sequence, can we have shortest from that ?
- Shotest Super Sequence : `bgruoote` ; length = 8
- s1 = bleed s2 = blue , Shortest Super Sequence : `bleued`

> Solution : take the `common things only once`:: `n + m - length(lcs)`

- n+m length have twice lcs, we have to remove one from that, which is my ans.

## 31.B. Print the Shortest Common Supersequence

- Print LCS DP table will be used.
![image](https://user-images.githubusercontent.com/35686407/177748147-dea65bad-454b-44ad-aa96-7ef3709ce565.png)

|Image 1|Image 2 (Fully Filled DP Table)|
|---|---|
|![image](https://user-images.githubusercontent.com/35686407/177748309-b0be0019-9a3d-4c0e-9019-c1cb56ce3fde.png)|![image](https://user-images.githubusercontent.com/35686407/177748344-8074f98b-ad94-4ba6-986b-defe63ce007b.png)|

- How to print shortest common supersequence,
- we know ans lie on dp[n][m]
- check does this t match with e ? NO , where it come from max(dp[i-1][j],dp[i][j-1]) , so in this you move up
- so what will happen when you move up, and see which string reduces, its string s1 ~ brute , to brut, so we add up t,
- when we move left, which string reduces its str2 , then we have to write its char.


|Steps|Image|Answer|
|---|---|---|
|1. e and t not matches, move to max side.|![image](https://user-images.githubusercontent.com/35686407/177748825-b20d0ecc-5c1c-48f6-9de8-f35d22ece931.png)|ans = "e"|
|2.t and t matches, both string reduces, Commmon Guy added once |![image](https://user-images.githubusercontent.com/35686407/177749253-9e7e6315-5907-47cc-a330-b81fee26955a.png)|ans = "et" (Common Guy added once)|
|3. here o didnt not match with u, so it moves to the max side, but both are same, move to any part, so it's moving to left side.|![image](https://user-images.githubusercontent.com/35686407/177749605-fe8129c6-4ce2-465b-910f-1bad56c55bd1.png)|ans = "eto"|
|4. Strings left till now|![image](https://user-images.githubusercontent.com/35686407/177749847-a940095a-db0a-40f3-9d56-516df76b5f70.png)|ans = "eto"|
|5. u and o not matches, suppose we go upwards, string s1 reduces|![image](https://user-images.githubusercontent.com/35686407/177750087-a5820ed1-d94a-48b5-83ba-3bd689b48a71.png)|ans = "etou"|
|6. o and r not matches , suppose it goes to left|![image](https://user-images.githubusercontent.com/35686407/177750362-f53eead1-cf77-4f64-a7b3-b8ba4d7ac900.png)|ans = "etouo"|
|7. Now r and r matches, go diagonal upward|![image](https://user-images.githubusercontent.com/35686407/177750586-9030f0a3-1797-4386-a411-2c624260f3a1.png)|ans = "etouor"|
|8. b and g didn't matches, go upward or left whatever you want |![image](https://user-images.githubusercontent.com/35686407/177751191-ca9b8b1f-6d06-45c5-80cc-92dcd0db1618.png)|ans = "etouorb"|
|9. Now, still left with g elements of str2 and str1 ends as beyond 1 index , but in 2nd string str2 only 1 char left|We have to write that left chars also in left string|ans = "etouorbg"|

- Now reverse the string : "etouorbg" ~ `gbouorbg`, which is Shortest common supersequence.

```cpp
class Solution {
public:
    
    void createLCSDpArray(string& str1,string& str2,vector<vector<int>>& dp){
        int n = str1.size();
        int m = str2.size();
        
        // BASE CASE
        for(int j = 0; j <= m; j++){
            dp[0][j] = 0;
        }
        
        for(int i = 0; i <= n; i++){
            dp[i][0] = 0;
        }
        
        // Functional
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                if(str1[i-1] == str2[j-1]){
                    dp[i][j] = 1+dp[i-1][j-1];
                }else{
                    int v1 = dp[i-1][j];
                    int v2 = dp[i][j-1];
                    dp[i][j] = max(v1,v2);
                }
            }
        }
    }
    
    string printSCS(vector<vector<int>>& dp,string& str1,string& str2){
        int i = str1.size();
        int j = str2.size();
        string ans = "";
        
        while(i > 0 && j > 0){
            if(str1[i-1] == str2[j-1]){
                ans.push_back(str1[i-1]);
                i--;j--;
            }else{
                if(dp[i-1][j] > dp[i][j-1]){
                    // going up
                    // str1 reduces
                    ans.push_back(str1[i-1]);
                    i--;
                }else{
                    ans.push_back(str2[j-1]);
                    j--;
                }
            } 
        }
        
        while(i > 0){
            ans.push_back(str1[i-1]);
            i--;
        }
        
        while(j > 0){
            ans.push_back(str2[j-1]);
            j--;
        }
        reverse(ans.begin(),ans.end());
        return ans;
    }
    
    string shortestCommonSupersequence(string str1, string str2) {
        int n = str1.size();
        int m = str2.size();
        
        vector<vector<int>> dp(n+1,vector<int>(m+1,-1));
        
        createLCSDpArray(str1,str2,dp);
        
        return printSCS(dp,str1,str2);
        
    }
};
```

## String Matching in Dp On Strings

## 32. Distinct Subsequences
- str1 ="babgbag" , str2 = "bag"
- tell , how many times string 2 apprears on string 1 ?
- In total there will be 5 occurance of str2 in str1
![image](https://user-images.githubusercontent.com/35686407/177755429-85f7c662-77f8-4cb6-9f2a-d4144ef08dd6.png)

> How to solve ? Something we have to apply recursion

Why Recrusion ? there are multiple b and g, so there are many options to take b and g, so we have to explore all paths / different method of comparing/ `trying all ways ~ Recursion`

> Question Says : `Count Number of Ways`

- Whenever ther is something like count + ways then
![image](https://user-images.githubusercontent.com/35686407/177755842-8218b68b-aa16-47c3-b206-0a4910651906.png)

**How to write Reccurance ?**
1. Whenever there are two strings, we take 2 parameters, (i,j) , i for str1 and j for str2
2. Explore All Possibilities 
3. Return the summition of All possibilities
4. Write down the base case

> Try to write f(i,j), base case baad mae sochenge

|Image 1|f(n-1,m-1) => Number if distinct subsequences of s2[0 ... j] in s1[0 ... i]|
|---|---|
|![image](https://user-images.githubusercontent.com/35686407/177756308-362c1e4b-a766-4b00-b964-2de8a08ed29d.png)|![image](https://user-images.githubusercontent.com/35686407/177756444-ae3c6b6b-7239-4cfc-90f0-b155f0eb13e4.png)|

- g is matching with g, so we will take g and not take g, so that we can find out another g aage.
- same for other a's and b's
- if they are matching , i know 1 thing for sure bag reduce to ba, take g, [f(i-1,j-1)] what if i am not interseted, i am not matching g, lets looking for another occurance of g, [f(i-1,j)],
- what if you came to the case when you are on the case, where a and g not matches, so what you will do ? i will not match it, else [f(i-1,j)]
- If Matching 2 States :
    - f(i-1,j-1)
    - f(i-1,j)
    - return f(i-1,j-1) + f(i-1,j)
- If not Matching only 1 State : 
     - f(i-1,j)
     - return f(i-1,j)

> Base Case : 

- Base case has to return 1 and return 0
- When will it return 1 or 0 ?
- Base case is asking yourself what will happen , 
- what if i am still looking to b and my pointer is negative index in str1 , some portion of string s2 remaining
![image](https://user-images.githubusercontent.com/35686407/177758460-95ec4832-ed4f-4121-9050-c14cd41ab116.png)
- or i can say i might end up coming to -1 also on j, i == -1 and j == -1, actually matched everyone, that is my case which i am looking for
- if all chars of s2 matches then return 1
- if (i < 0) still matching to be done in j counter part , then return 0
![image](https://user-images.githubusercontent.com/35686407/177758820-a840d38e-c5e4-466e-8e11-64ae8a6a2bb8.png)

> Codes :

#### Approach 1 : Recursion + Memoization

- TC for rec : 2^n (s1) and 2^m (s2) , exponentional in nature
- SC for rec : O(n) + O(m)
- TC for memo : O(NxM)
- SC for memo : O(NxM) + O(N+M)

```cpp
// Without Shifting Indexes.
int f(int i,int j,string& s1,string& s2,vector<vector<int>>& memo){
    if(j < 0) return 1;
    if(i < 0) return 0;
    if(memo[i][j] != -1) return memo[i][j];
    if(s1[i] == s2[j]){
        return memo[i][j] = f(i-1,j-1,s1,s2,memo) + f(i-1,j,s1,s2,memo);
    }else{
        return memo[i][j] = f(i-1,j,s1,s2,memo);
    }
}
```

>  `Shifting Index` , as for tabulation we have to store the base cases, so we shift the indexes.

```cpp
int f(int i,int j,string& s1,string& s2,vector<vector<int>>& memo){
        if(j == 0) return 1;
        if(i == 0) return 0;
        if(memo[i][j] != -1) return memo[i][j];
        if(s1[i-1] == s2[j-1]){
            return memo[i][j] = f(i-1,j-1,s1,s2,memo) + f(i-1,j,s1,s2,memo);
        }else{
            return memo[i][j] = f(i-1,j,s1,s2,memo);
        }
    }
    
    int numDistinct(string s, string t) {
        int n = s.size();
        int m = t.size();
        vector<vector<int>> memo(n+1,vector<int>(m+1,-1));
        return f(n,m,s,t,memo);
    }
```

#### Approach 2 : Tabulation

TC : O(N x M)
SC : O(N x M)

```cpp
class Solution {
public:
    
    int numDistinct(string s, string t) {
        int n = s.size();
        int m = t.size();
        vector<vector<double>> dp(n+1,vector<double>(m+1,0));
        
        // BASE CASE
        for(int i = 0; i <= n; i++){
            dp[i][0] = 1;
        }
        
        // for j = 0 we already write on above for loop, 
        // so we have to write it from 1
        for(int j = 1; j <= m; j++){ // if we remove that loop, it also runs, because we make the dp array initiaize with 0
            dp[0][j] = 0;
        }
        
        // Functional
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                if(s[i-1] == t[j-1]){
                    dp[i][j] = dp[i-1][j-1] + dp[i-1][j];
                }else{
                    dp[i][j] = dp[i-1][j];
                }
            }
        }
        return (int)dp[n][m];
    }
};
```

#### Approach 3 : Space Optimization

```cpp
class Solution {
public:
    
    int numDistinct(string s, string t) {
        int n = s.size();
        int m = t.size();
        vector<double> prev(m+1,0),cur(m+1,0);
        
        // BASE CASE
        prev[0] = cur[0] = 1;
        
        // Functional
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                if(s[i-1] == t[j-1]){
                    cur[j] = prev[j-1] + prev[j];
                }else{
                    cur[j] = prev[j];
                }
            }
            prev = cur;
        }
        return (int)prev[m];
    }
};
```

> But how many arrays are we using ?, we are using 2 arrays.

- Let's analize, can we reduce that into single array optimization.
- we are using prev row's left value while computing the current value, so what is we start computing j from right to left 

```cpp
class Solution {
public:
    
    int numDistinct(string s, string t) {
        int n = s.size();
        int m = t.size();
        vector<double> prev(m+1,0);
        
        // BASE CASE
        prev[0] = 1;
        
        // Functional
        for(int i = 1; i <= n; i++){
            for(int j = m; j >= 1; j--){
                if(s[i-1] == t[j-1]){
                    prev[j] = prev[j-1] + prev[j];
                }else{
                    prev[j] = prev[j];
                }
            }
        }
        return (int)prev[m];
    }
};
```

## 33. Edit Distance

- Convert String str1 to String str2
- ![image](https://user-images.githubusercontent.com/35686407/178092040-09dfa2ae-2938-4a49-90d4-76f7d7049545.png)

> Is it always possible ? Yes ! , Delete all char of s1 and add char of s2

- Minimal Operations Example :

|Image 1 (3 Operations)|Image 2 (5 Operations)|
|---|---|
|![image](https://user-images.githubusercontent.com/35686407/178092116-26c7a130-52d3-4907-82db-8d32aaa057e0.png)|![image](https://user-images.githubusercontent.com/35686407/178092353-dec6f96d-d76c-4806-a0da-36d16cc6ecd2.png)|

- We will go with string matching algorithm, and try to match char recursively
- Example : str1 = "horse" and str2 = "ros"
    - from last s and e not lets delete e from str1
    - now s and s matches from both
    - r and o not matching delete r from str1
    - now o and o matches
    - now h and r not matches, replace h with r in str1 

> Intutation : I have to do string matching where i take 1 charr from s2 and other char from s2 if they are matching good, if not then i have alot of options. Options are - Insert the same char, I will delete that char and find somewhere else, I try to replace and they got match, these 3 opterations i can think in case of string matching.

- If i am trying to do all possible stuffs, and take out the best ~ Try all ways ~ Recursion and then take the minimum operations

> How to write reccurance ?

1. Two Strings, express in terms of (i,j) , i represent str1 and j represent str2
2. explore all possibilities
3. return the best ans, minimal of all paths
4. Base Case.

> f(i,j) singnifies ? example : str1 = "horse" str2 = "ros" , find me the minimum operations to convert from 0 to i in str1 to string str2 from 0 to j
![image](https://user-images.githubusercontent.com/35686407/178092607-d1a7d06b-ca87-4b31-88bc-b815de909537.png)

- Cases :
    - 2 possible cases :
        - Either they match or not match :
            - if they match `if(str[i] == str[j])`
                - do we need to perform operation ? No. if they are matching already , why you need to insert/delete/replace
                - shrink the string, there is no need to do any operation insert, delete and replace
                - `return 0 + f(i-1,j-1)`
            - if they didn't match `if(str[i] != str[j])`
                - What thing i can do ? insert/delete/replace
                    1. I can insert 's' and str1 = 'horse`s`' and str2 = 'ro`s`' and s matches with s and move j-- in str2 and i stays at the same place (Hypotheticallly place this s and e can be matched with o) `f(i,j-1)`
                    ![image](https://user-images.githubusercontent.com/35686407/178092788-53a74011-6c9b-437a-8406-48f04f934ee7.png)
                    2. I can delete `e` and match s with s of str1 and str2 respectively. str1 = hor`s`e and str2 = ro`s` , i reduces and i deleted and j remains the same place because you are still looking to s after deletion (i-1) `f(i-1,j)` , deleted `e` in str1 and still looking for `s` in str2
                    ![image](https://user-images.githubusercontent.com/35686407/178092864-4cee35db-4dbd-4ccf-81d0-14afc56d7b9b.png)
                    3. replace `s` and `e` in str1 and str2 respectively, will you replace with 'a' NO, why you do a fool , you know you will replace with `s` because you want to match these guys, so replace it and reduce both the strings `f(i-1,j-1)`
                    ![image](https://user-images.githubusercontent.com/35686407/178092925-b52aecac-c12a-406b-b951-57798f8c72b6.png)
                - Return best possibility, return minimum
            - Base Case :
                - Base cases when it's over :
                    - When it over ?
                        1. if str1 get exausted :
                            - i < 0 and j > 0 str1 exausted , and str2 not exausted how many operation you required ? `j+1` operations , because minimum operations to convert and empty string from [0...j] is `j+1` `insert` operations.  
                            - `return j+1`
                             ![image](https://user-images.githubusercontent.com/35686407/178093035-21858fb8-44ed-4390-b781-05d2e2a83a4a.png)
                        2. if str2 get exausted :
                            - if j < 0 and i > 0  return `i+1` because we need i+1 `delete operations` to convert rest of the string
                             ![image](https://user-images.githubusercontent.com/35686407/178093129-76a880f3-edac-4bae-a5eb-e17761301475.png)

#### Approach 1 : Recursion + Memoization

- TC for rec : exponential
- SC for rec : O(N+M)
- TC for Memo : 
- SC for Memo : 

```cpp
int f(int i,int j, string& word1,string& word2,vector<vector<int>>& memo){
    if(i < 0) return j+1;
    if(j < 0) return i+1;
    if(memo[i][j] != -1) return memo[i][j];
    if(word1[i] == word2[j]){
        return memo[i][j] = 0 + f(i-1,j-1,word1,word2,memo);
    }else{
        int v1 = 1 + f(i,j-1,word1,word2,memo); // insert
        int v2 = 1 + f(i-1,j,word1,word2,memo); // delete
        int v3 = 1 + f(i-1,j-1,word1,word2,memo); // replace
        return memo[i][j] = min({v1,v2,v3});
    }
}
int minDistance(string word1, string word2) {
    int n = word1.size();
    int m = word2.size();
    vector<vector<int>> memo(n,vector<int>(m,-1));
    return f(n-1,m-1,word1,word2,memo);
}
```

#### Appraoch 1  : Shifting of Index Recursion + Memo (to write tabulation easily)

- i < 0 and j < 0 ~ i == 0 and j == 0
- word[i] == word[j] ~ word[i-1] == word[j-1] , because we have to check for index, and we are giving length in recursion parameter.

```cpp
int f(int i,int j, string& word1,string& word2,vector<vector<int>>& memo){
    if(i == 0) return j;
    if(j == 0) return i;
    if(memo[i][j] != -1) return memo[i][j];
    if(word1[i-1] == word2[j-1]){
        return memo[i][j] = 0 + f(i-1,j-1,word1,word2,memo);
    }else{
        int v1 = 1 + f(i,j-1,word1,word2,memo); // insert
        int v2 = 1 + f(i-1,j,word1,word2,memo); // delete
        int v3 = 1 + f(i-1,j-1,word1,word2,memo); // replace
        return memo[i][j] = min({v1,v2,v3});
    }
}
int minDistance(string word1, string word2) {
    int n = word1.size();
    int m = word2.size();
    vector<vector<int>> memo(n+1,vector<int>(m+1,-1));
    return f(n,m,word1,word2,memo);
}
```

#### Appraoch 2: Tabulation

```cpp
int minDistance(string word1, string word2) {
    int n = word1.size();
    int m = word2.size();
    vector<vector<int>> dp(n+1,vector<int>(m+1,-1));
    
    // BASE CASE
    
    for(int j = 0; j<= m; j++){
        dp[0][j] = j;
    }
    
    for(int i = 0; i <= n; i++){
        dp[i][0] = i;
    }
    
    // FUNCTIONAL
    for(int i = 1; i <= n; i++){
        for(int j = 1; j <= m; j++){
            if(word1[i-1] == word2[j-1]){
                dp[i][j] = 0 + dp[i-1][j-1];
            }else{
                int v1 = 1 + dp[i][j-1]; // insert
                int v2 = 1 + dp[i-1][j]; // delete
                int v3 = 1 + dp[i-1][j-1]; // replace
                dp[i][j] = min({v1,v2,v3});
            }
        }
    }
    
    return dp[n][m];
}
```

#### Approach 3 : Space Optimization

```cpp
class Solution {
public:

    int minDistance(string word1, string word2) {
        int n = word1.size();
        int m = word2.size();
        vector<int> prev(m+1,-1),cur(m+1,-1);
        
        for(int j = 0; j<= m; j++){
            prev[j] = j;
        }
        // FUNCTIONAL
        for(int i = 1; i <= n; i++){
            cur[0] = i;
            for(int j = 1; j <= m; j++){
                if(word1[i-1] == word2[j-1]){
                    cur[j] = 0 + prev[j-1];
                }else{
                    int v1 = 1 + cur[j-1]; // insert
                    int v2 = 1 + prev[j]; // delete
                    int v3 = 1 + prev[j-1]; // replace
                    cur[j] = min({v1,v2,v3});
                }
            }
            prev = cur;
        }
        
        return prev[m];
    }
};
```

## 34. WildCard Matching

#### Approach 1 : Recursion + Memoization

```cpp
class Solution {
public:
    
    bool f(int i,int j, string& pattern,string& text,vector<vector<int>>& memo){
        
        if(i < 0 && j < 0) return true;
        if(i < 0 && j >= 0) return false;
        if(j < 0 && i >= 0){
            for(int k = 0; k <= i; k++){
                if(pattern[k] != '*') return false;
            }
            return true;
        }
        
        if(memo[i][j] != -1) return memo[i][j];
        
        if(pattern[i] == text[j] || pattern[i] == '?'){
            return memo[i][j] = f(i-1,j-1,pattern,text,memo);
        }else if(pattern[i] == '*'){
            return memo[i][j] = f(i-1,j,pattern,text,memo) || f(i,j-1,pattern,text,memo);
        }
        return memo[i][j] = false;
    }
    
    bool isMatch(string s, string p) {
        string& pattern = p;
        string& text = s;
        int n = pattern.size();
        int m = text.size();
        
        vector<vector<int>> memo(n,vector<int>(m,-1));
        
        return f(n-1,m-1,pattern,text,memo);
        
    }
};
```

### Index Shifting

```cpp
bool f(int i,int j, string& pattern,string& text,vector<vector<int>>& memo){
    
    if(i == 0 && j == 0) return true;
    if(i == 0 && j > 0) return false;
    if(j == 0 && i > 0){
        for(int k = 1; k <= i; k++){
            if(pattern[k-1] != '*') return false;
        }
        return true;
    }
    
    if(memo[i][j] != -1) return memo[i][j];
    
    if(pattern[i-1] == text[j-1] || pattern[i-1] == '?'){
        return memo[i][j] = f(i-1,j-1,pattern,text,memo);
    }else if(pattern[i-1] == '*'){
        return memo[i][j] = f(i-1,j,pattern,text,memo) || f(i,j-1,pattern,text,memo);
    }
    return memo[i][j] = false;
}
// vector<vector<int>> memo(n+1,vector<int>(m+1,-1));
// return f(n,m,pattern,text,memo);
```

#### Appraoch 2 : Tabulation 

```cpp
class Solution {
public:
    
    bool isMatch(string s, string p) {
        string& pattern = p;
        string& text = s;
        int n = pattern.size();
        int m = text.size();
        
        vector<vector<bool>> dp(n+1,vector<int>(m+1,false));
        
        // BASE CASE
        dp[0][0] = true;
        
        for(int j = 1; j <= m; j++){
            dp[0][j] = false;
        }
        
        for(int i = 1; i <= n; i++){
            bool flag = true;
            for(int k = 1; k <= i; k++){
                if(pattern[k-1] != '*'){
                    flag = false;
                    break;
                }
            }
            dp[i][0] = flag;
        }
        
        // Functional
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                if(pattern[i-1] == text[j-1] || pattern[i-1] == '?'){
                    dp[i][j] = dp[i-1][j-1];
                }else if(pattern[i-1] == '*'){
                    dp[i][j] = dp[i-1][j] || dp[i][j-1];
                }else{
                    dp[i][j] = false;   
                }
            }
        }
        
        return dp[n][m];
    }
};
```

#### Appraoch 3 : Space Optimization

```cpp
class Solution {
public:
    
    bool isMatch(string s, string p) {
        string& pattern = p;
        string& text = s;
        int n = pattern.size();
        int m = text.size();
        
        vector<bool> prev(m+1,false),cur(m+1,false);
        
        // BASE CASE
        prev[0] = true;
        
        for(int j = 1; j <= m; j++){
            prev[j] = false;
        }
        
        for(int i = 1; i <= n; i++){
            
        }
        
        // Functional
        for(int i = 1; i <= n; i++){
            
            bool flag = true;
            for(int k = 1; k <= i; k++){
                if(pattern[k-1] != '*'){
                    flag = false;
                    break;
                }
            }
            cur[0] = flag;
            
            for(int j = 1; j <= m; j++){
                if(pattern[i-1] == text[j-1] || pattern[i-1] == '?'){
                    cur[j] = prev[j-1];
                }else if(pattern[i-1] == '*'){
                    cur[j] = prev[j] || cur[j-1];
                }else{
                    cur[j] = false;   
                }
            }
            prev = cur;
        }
        
        return prev[m];
    }
};
```


## DP ON STOCKS
(Space Optimization is Important to learn)

## 35. Best time to Buy and Sell Stock

- n , number of days
- prices[i] : price on the ith day.
- you have to buy the stock and sell the stock
- in this , you are allowed to buy and sell only once.
- `Buy is one before selling` , you can't do like sell before and buy after it's illogical.

> Note : if you are selling on the ith day, it means you have to buy it on the day 1 to i-1, and if you want to maximize the profit then you have to choose min from day 1 to i-1.Therefore, while moving we keep track of the minimum, and try to sell it on every day.

```cpp
int maxProfit(vector<int>& prices) {
    int mini = prices[0];
    int profit = 0;
    for(auto& val:prices){
        profit = max(profit,val - mini);
        mini = min(val,mini);
    }
    return profit;
}
```

## 36. Best Time to Buy and Sell Stock II

- isme hm buy kitni bhi bari kr skte hai and sell kitni bhi bari kr skte hai
- but make sure, ki agar buy krne ja rhe ho to pichla stock you already sell it, otherwise it is not possible to buy,
- mtlb ese ni kr skte buy buy buy sell sell buy 
- ese kr skte hai , buy sell buy sell buy sell
- hme maximum profit nikal kr dena hai.
-  You can only hold at most one share of the stock at any time. However, you can buy it then immediately sell it on the same day.

> Example : [7,1,5,3,6,4]
Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
Total profit is 4 + 3 = 7.

- So how to approach this problem ?
- so, here hme ye dekh rha hai ki 1 day pr kai option hai Buy it / Sell it
- mtlb hum all possible ways nikalkr maximum profit calculate kr skte hai
- Many ways in one option : Recursion

> How to write recursion ?

1. Express all in terms of (index, ?) , 
    a) do we need another parameter like in knaosack we track our weight how many it is left , do we need here any extra variable ? Yes, as agar hum buy krte hai, to aage hme buy allowed nhi hai hme bechna hi pdega uske baad hum aage allowed hai dobara buy ke liye    
    b) So, there is question on each day that Is i am allowed to buy today or not ?
    c) So, there is need of extra vairable `buy` having value 1 or 0, 1 means allowed to buy and 0 means not allowed to buy, you can only sell prev ones.
    d) `f(index,buy)`
2. Now, explore all possibilities on that day
3. Return the best one , in this case, it is maximum
4. Base Case

> Explore All Possibilities :

- so what are the possibilitites on each day ?
    1. if i am allowed to buy on a day `buy = 1`, then i have 2 options :
        - buy it 
            - if i buy it, you know how profit is calculated, price(sell) - price(buy) , here buy price have sign -ve and sell price have sign +ve
            - `-value[idx] + f(idx+1,0);` // 0 because you are not now allowed to buy, you are allowed to sell.
        - not buy it
            - `0 + f(idx+1,1);` // i am still allowed to buy.
    2. if i am not allowed to buy that is `buy = 0`, then in this case also i have 2 options
        - sell it
            - if i sell it, you know how profit is calculated, price(sell) - price(buy) , here buy price have sign -ve and sell price have sign +ve
            - `+value[idx] + f(idx+1,1)` // not i am allowed to buy aage as i sold stock    
        - not sell it
            - `0 + f(idx+1,0)` // i didn't sold it, so i am not able to buy in the future untill i sold it.

> Base Cases : There is only one base case, when you reach at `index == n`, are you able to sell it ? No, profit is 0, as if you buy it, and dont able to sell it, there is no profit, and it is not negative because there is no selling price, if there is a selling price then it may be negative or not, but here there is no selling price so profit = 0 so base case is : `if index == n : return 0;`

#### Approach 1 : Recursion + Memoization

```cpp
class Solution {
public:
    int f(int idx,int buy,vector<int>& prices,vector<vector<int>>& memo){
        if(idx == prices.size()) return 0;
        if(memo[idx][buy] != -1) return memo[idx][buy];
        if(buy == 1){
            // i am allowed to buy, 2 choice : buy or not buy
            int v1 = -prices[idx] + f(idx+1,0,prices,memo); // buy, didn't allowed to buy in future untill i sell
            int v2 = 0 + f(idx+1,1,prices,memo); // not buy , allowed to buy in future.
            return memo[idx][buy] = max(v1,v2);
        }else{
            // i am not allowed to buy, only allowed to sell
            // 2 options : sell it or not sell it
            int v1 = +prices[idx] + f(idx+1,1,prices,memo); // sold it, allowed to buy in future
            int v2 = 0 + f(idx+1,0,prices,memo); // didn't sell, not allowed to buy in future
            return memo[idx][buy] = max(v1,v2);
        }
    }
    
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<vector<int>> memo(n,vector<int>(2,-1));
        return f(0,1,prices,memo);    
    }
};
```

#### Appraoch 2 : Tabulation

```cpp
int maxProfit(vector<int>& prices) {
    int n = prices.size();
    vector<vector<int>> dp(n+1,vector<int>(2,-1));
    
    // BASE CASE 
    dp[n][0] = dp[n][1] = 0;
    
    for(int idx = n-1; idx >= 0; idx--){
        for(int buy = 1; buy >= 0; buy--){
            if(buy == 1){
                int v1 = -prices[idx] + dp[idx+1][0];
                int v2 = 0 + dp[idx+1][1];
                dp[idx][buy] = max(v1,v2);
            }else{
                int v1 = +prices[idx] + dp[idx+1][1];
                int v2 = 0 + dp[idx+1][0];
                dp[idx][buy] = max(v1,v2);
            }
        }
    }
    
    return dp[0][1];    
}
```

#### Apporach 3 : Space Optimization :

```cpp
int maxProfit(vector<int>& prices) {
    int n = prices.size();
    vector<int> ahead(2,0),cur(2,0);
    
    // BASE CASE 
    ahead[0] = ahead[1] = 0;
    
    for(int idx = n-1; idx >= 0; idx--){
        for(int buy = 1; buy >= 0; buy--){
            if(buy == 1){
                int v1 = -prices[idx] + ahead[0];
                int v2 = 0 + ahead[1];
                cur[buy] = max(v1,v2);
            }else{
                int v1 = +prices[idx] + ahead[1];
                int v2 = 0 + ahead[0];
                cur[buy] = max(v1,v2);
            }
        }
        ahead = cur;
    }
    
    return ahead[1];    
}
```

#### Approach 4 : Space Optimization to 4 Variables
- as we know there are only 4 spaces (fixed size ahead and cur array) which are used to store the results and calculation of the results.
- So we make 4 varaibles :
    - ahead[1] : aheadBuy
    - ahead[0] : aheadNotBuy
    - cur[1] : curBuy
    - cur[0] : curNotBuy

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        
        int aheadNotBuy,aheadBuy,curNotBuy,curBuy;
        
        // Base Case
        aheadNotBuy = aheadBuy = 0;
        
        for(int idx = n-1; idx >= 0; idx--){
            for(int buy = 1; buy >= 0; buy--){
                if(buy == 1){
                    int v1 = -prices[idx] + aheadNotBuy;
                    int v2 = 0 + aheadBuy;
                    curBuy = max(v1,v2);
                }else{
                    int v1 = +prices[idx] + aheadBuy;
                    int v2 = 0 + aheadNotBuy;
                    curNotBuy = max(v1,v2);
                }
            }
            aheadNotBuy = curNotBuy;
            aheadBuy = curBuy;
        }
        
        return aheadBuy;    
    }
};
```

##### if we omit the inner for loop, it works, as we calucate both simultaneously

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        
        int aheadNotBuy,aheadBuy,curNotBuy,curBuy;
        
        // Base Case
        aheadNotBuy = aheadBuy = 0;
        
        for(int idx = n-1; idx >= 0; idx--){
            
            int v1 = -prices[idx] + aheadNotBuy;
            int v2 = 0 + aheadBuy;
            curBuy = max(v1,v2);
            
            int v3 = +prices[idx] + aheadBuy;
            int v4 = 0 + aheadNotBuy;
            curNotBuy = max(v3,v4);
            
            aheadNotBuy = curNotBuy;
            aheadBuy = curBuy;
        }
        
        return aheadBuy;    
    }
};
```

## 36. Best Time to Buy and Sell Stock III

- ye problem lgbhag same hai 35. Best Time to Buy and Sell Stock II jesi
- bs frk itna hai ki, isme hme atmost 2 transactions krni hai,
- jbki II vale mae hmare paas infinite transactions krna allowed tha.
- ab srf 2 transaction krni hai, isse jayeda nhi, to ye thoda dekho knapsack ke sath match kra jese usme hme W weight ka bag fill krna hota tha.
- Yha bhi hum ek `cap (capacity)` name ka variable lenge, and `if capacity == 0 : return 0`
- or kb buy krke vo sell ho jayegi tbhi 1 trasaction complete hoga tbhi hme `cap-1` krna hai.

#### Approach 1 : Recursion + Memoization

```cpp
int f(int idx,int buy,int cap,vector<int>& prices,vector<vector<vector<int>>>& memo){
    if(cap == 0) return 0;
    if(idx == prices.size()) return 0;
    if(memo[idx][buy][cap] != -1) return memo[idx][buy][cap];
    if(buy == 1){
        int v1 = -prices[idx] + f(idx+1,0,cap,prices,memo);
        int v2 = 0 + f(idx+1,1,cap,prices,memo);
        return memo[idx][buy][cap] = max(v1,v2);
    }else{
        int v1 = +prices[idx] + f(idx+1,1,cap-1,prices,memo);
        int v2 = 0 + f(idx+1,0,cap,prices,memo);
        return memo[idx][buy][cap] = max(v1,v2);
    }
}

int maxProfit(vector<int>& prices) {
    int n = prices.size();
    vector<vector<vector<int>>> memo(n,vector<vector<int>>(2,vector<int>(3,-1)));
    return f(0,1,2,prices,memo);   
}
```

#### Appraoch 2 : Tabulation

```cpp
int maxProfit(vector<int>& prices) {
    int n = prices.size();
    vector<vector<vector<int>>> dp(n+1,vector<vector<int>>(2,vector<int>(3,0)));
    
    // BASE CASE
    for(int idx = 0; idx < n; idx++){
        for(int buy = 0; buy <= 1; buy++){
            dp[idx][buy][0] = 0;
        }
    }
    
    for(int buy = 0; buy <= 1; buy++){
        for(int cap = 0; cap < 3; cap++){
            dp[n][buy][cap] = 0;
        }
    }
    
    for(int idx = n-1; idx >= 0; idx--){
        for(int buy = 0; buy <= 1; buy++){
            for(int cap = 2; cap >= 1; cap--){
                if(buy == 1){
                    int v1 = -prices[idx] + dp[idx+1][0][cap];
                    int v2 = 0 + dp[idx+1][1][cap];
                    dp[idx][buy][cap] = max(v1,v2);
                }else{
                    int v1 = +prices[idx] + dp[idx+1][1][cap-1];
                    int v2 = 0 + dp[idx+1][0][cap];
                    dp[idx][buy][cap] = max(v1,v2);
                }
            }
        }
    }
    
    return dp[0][1][2];   
}
```

#### Appraoch 3 : Space Optimization

```cpp
int maxProfit(vector<int>& prices) {
    int n = prices.size();
    vector<vector<int>> after(2,vector<int>(3,0)),cur(2,vector<int>(3,0));
    
    for(int idx = n-1; idx >= 0; idx--){
        for(int buy = 0; buy <= 1; buy++){
            for(int cap = 2; cap >= 1; cap--){
                if(buy == 1){
                    int v1 = -prices[idx] + after[0][cap];
                    int v2 = 0 + after[1][cap];
                    cur[buy][cap] = max(v1,v2);
                }else{
                    int v1 = +prices[idx] + after[1][cap-1];
                    int v2 = 0 + after[0][cap];
                    cur[buy][cap] = max(v1,v2);
                }
            }
            after = cur;
        }
    }
    
    return after[1][2];   
}
```

### Other Intuative To Write Solution

- as we know there are at max 2 transaction, so we give id to each transaction , e.g. B S B S where B is Buy and Sell is S,
- So id would be given as 0 1 2 3 (B S B S) , now you can see Buy is at id 0,2 which is even id and sell is at odd id.
- So rather taking the 3 variables, we will take only 2 variables.

#### Appraoch 1 : Recursion + Memoization

```cpp
int f(int idx,int transID,vector<int>& prices,vector<vector<int>>& memo){
    if(idx == prices.size() || transID == 4) return 0;
    
    if(memo[idx][transID] != -1) return memo[idx][transID];
    
    if(transID % 2 == 0){
        // even then buy
        return memo[idx][transID] = max(-prices[idx] + f(idx+1,transID+1,prices,memo),0 + f(idx+1,transID,prices,memo));
    }else{
        // odd then sell
        return memo[idx][transID] = max(+prices[idx] + f(idx+1,transID+1,prices,memo),0 + f(idx+1,transID,prices,memo));
    }
    
}
int maxProfit(vector<int>& prices) {
    int n = prices.size();
    vector<vector<int>> memo(n,vector<int>(4,-1));
    return f(0,0,prices,memo);   
}
```

#### Appraoch 2 : Tabulation :
```cpp
int maxProfit(vector<int>& prices) {
    int n = prices.size();
    vector<vector<int>> dp(n+1,vector<int>(5,0));
    
    for(int idx = n-1; idx >= 0; idx--){
        for(int transID = 3; transID >= 0; transID--){
            if(transID % 2 == 0){
        // even then buy
                dp[idx][transID] = max(-prices[idx] + dp[idx+1][transID+1],0 + dp[idx+1][transID]);
            }else{
                // odd then sell
                dp[idx][transID] = max(+prices[idx] + dp[idx+1][transID+1],0 + dp[idx+1][transID]);
            }
        }
    }
    
    return dp[0][0];   
}
```

#### Space Optimization

```cpp
int maxProfit(vector<int>& prices) {
    int n = prices.size();
    vector<int> ahead(5,0),cur(5,0);
    
    for(int idx = n-1; idx >= 0; idx--){
        for(int transID = 3; transID >= 0; transID--){
            if(transID % 2 == 0){
        // even then buy
                cur[transID] = max(-prices[idx] + ahead[transID+1],0 + ahead[transID]);
            }else{
                // odd then sell
                cur[transID] = max(+prices[idx] + ahead[transID+1],0 + ahead[transID]);
            }
        }
        ahead = cur;
    }
    
    return ahead[0];   
}
```


















































































































































































