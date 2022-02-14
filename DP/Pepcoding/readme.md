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
