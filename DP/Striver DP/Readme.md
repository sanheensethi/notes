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






