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
