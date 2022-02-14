# Dynamic Programming

![Link](https://github.com/Deeks900/Level2_Pepcoding/tree/main/Recursion%20And%20Backtracking)

## Fibonacci Series

> Recursion
```cpp
int fib(int n){
	if(n == 0) return 0;
	if(n == 1) return 1;
	return fib(n-1) + fib(n-2);
}

void solve(){
  int n;cin>>n;
	cout<<fib(n);
}
```

> Memoization
```cpp
int fib(int n,vector<int>& dp){
	if(n == 0) return 0;
	if(n == 1) return 1;
	if(dp[n] != -1) return dp[n];
	return dp[n] = fib(n-1,dp) + fib(n-2,dp);
}

void solve(){
	int n;cin>>n;
	vector<int> dp(n+1,-1);
	cout<<fib(n,dp);
}
```

> Tabular
```cpp
void solve(){
	int n;cin>>n;
	vector<int> dp(n+1,-1);
	// base case initializition
	if(n == 0) return 0;
	dp[0] = 0;
	dp[1] = 1;
	for(int i=2;i<=n;i++){
		dp[i] = dp[i-1] + dp[i-2];
	}
	cout<<dp[n];
}
```
> Space Optimized
```cpp
void solve(){
	int n;cin>>n;
	// base case initializition
	int prev2 = 0;
	int prev1 = 1;
	int current;
	for(int i=2;i<=n;i++){
		current = prev1 + prev2;
		prev2 = prev1;
		prev1 = current;
	}
	cout<<current;
}
```

## Climb Stairs
> Recursion
```cpp
int paths(int n){
	if(n < 0) return 0;
	if(n == 0) return 1;
	int v1 = paths(n-1);
	int v2 = paths(n-2);
	int v3 = paths(n-3);
	return v1+v2+v3;
}
```

> Memoization
```cpp
int paths(int n,vector<int>& dp){
	if(n < 0) return 0;
	if(n == 0) return 1;
	if(dp[n] != -1) return dp[n];
	int v1 = paths(n-1,dp);
	int v2 = paths(n-2,dp);
	int v3 = paths(n-3,dp);
	return v1+v2+v3;
}
vector<int> dp(n+1,-1);
```

> Tabular
```cpp
void solve(){
	int n;cin>>n;
	vector<int> dp(n+1,-1);
	// initialization
	dp[0] = 1;
	dp[1] = 1;
	dp[2] = 2;
	for(int i = 3;i<=n;i++){
		dp[i] = dp[i-1] + dp[i-2] + dp[i-3];
	}
	cout<<dp[n]<<endl;
}
```

> Memory Optimized
```cpp
void solve(){
	int n;cin>>n;
	// initialization
	int prev0 = 1;
	int prev1 = 1;
	int prev2 = 2;
	int current;
	for(int i = 3;i<=n;i++){
		current = prev2 + prev1 + prev0;
		prev0 = prev1;
		prev1 = prev2;
		prev2 = current;
	}
	cout<<current<<endl;
}
```

## Climb Stair Variable Jumps
> Recursion
```cpp
int paths(vector<int>& jumps,int i,int n){
	if(i > n) return 0;
	if(i == n) return 1;
	int total = 0;
	int steps = jumps[i];
	while(steps){
		total += paths(jumps,i+steps,n);
		steps--;
	}
	return total;
}
```

> Memoization
```cpp
int paths(vector<int>& jumps,int i,int n,vector<int>& dp){
	if(i > n) return 0;
	if(i == n) return 1;
	if(dp[i] != -1) return dp[i];
	int total = 0;
	int steps = jumps[i];
	while(steps){
		total += paths(jumps,i+steps,n,dp);
		steps--;
	}
	return dp[i] = total;
}
vector<int> dp(n+1,-1);
```

> Tabulation
```cpp
void solve(){
	int n;cin>>n;
	vector<int> jumps(n);
	for(int i=0;i<n;i++){
		cin>>jumps[i];
	}
	vector<int> dp(n+1,-1);
	// initialization
	dp[n] = 1;
	for(int i = n-1;i>=0;i--){
		int steps = jumps[i];
		int total = 0;
		while(steps){
			if(i+steps <= n){
				total += dp[i+steps];
			}
			steps--;
		}
		dp[i] = total;
	}
	cout<<dp[0]<<endl;
}
```
## Climbing Stairs Minimum Moves
> Recursion

- Why we take `mini=INT_MAX-1` -> if we didn't take -1 then for 0 jumps from particular position, mini is INT_MAX, but it will not iterate through while loop therefore after while loop while returning we add 1 + mini => 1 + INT_MAX as returning 1 + mini => INT_MAX + 1 = INT_MIN therefore we just take INT_MAX-1 as max value, so afer we add 1 it will not be INT_MIN, it will remain INT_MAX

- example n = 6 ; jumps = [4,2,0,2,2,3]

```cpp
int minSteps(vector<int>& jumps,int idx,int n){
	if(idx > n) return INT_MAX;
	if(idx == n) return 0;
	int steps = jumps[idx];
	int mini = INT_MAX-1;
	while(steps){
		int val = minSteps(jumps,idx+steps,n);
		mini = min(val,mini);
		steps--;
	}
	return 1 + mini; // current move have to be counted that yes we make this move
}
```
> Memoization
```cpp
int minSteps(vector<int>& jumps,int idx,int n,vector<int>& dp){
	if(idx > n) return INT_MAX;
	if(idx == n) return 0;
	if(dp[idx] != -1) return dp[idx];
	int steps = jumps[idx];
	int mini = INT_MAX-1;
	while(steps){
		int val = minSteps(jumps,idx+steps,n,dp);
		mini = min(val,mini);
		steps--;
	}
	return dp[idx] = 1 + mini; // current move have to be counted that yes we make this move
}

vector<int> dp(n+1,-1);
int ans = minSteps(jumps,0,n,dp);
if(ans == INT_MAX){
	cout<<"null"<<endl;
}else{
	cout<<ans<<endl;
}
```
