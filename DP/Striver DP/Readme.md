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
