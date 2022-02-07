# Dynamic Programming

## Longest Common Subsequence

> Recursion
```cpp
int LCS(string& x,string& y,int n,int m){
	if(n == 0 || m == 0){
		return 0;
	}
	if(x[n-1] == y[m-1]){
		return 1+LCS(x,y,n-1,m-1);
	}
	int val1 = LCS(x,y,n-1,m);
	int val2 = LCS(x,y,n,m-1);
	return max(val1,val2);
}

int n = x.size();
int m = y.size();
LCS(x,y,n,m);
```

> Memo
```cpp
int LCS(string& x,string& y,int n,int m,vector<vector<int>>& dp){
	if(n == 0 || m == 0){
		return 0;
	}
	if(dp[n][m] != -1) return dp[n][m];
	if(x[n-1] == y[m-1]){
		return dp[n][m] = 1+LCS(x,y,n-1,m-1,dp);
	}
	int val1 = LCS(x,y,n-1,m,dp);
	int val2 = LCS(x,y,n,m-1,dp);
	return dp[n][m] = max(val1,val2);
}

int n = x.size();
int m = y.size();
vector<vector<int>> dp(n+1,vector<int>(m+1,-1));
LCS(x,y,n,m,dp);
```

> Tabular
```cpp

```
