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

