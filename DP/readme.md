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
int LCSTabular(string& x,string& y){
	int n = x.size();
	int m = y.size();
	vector<vector<int>> dp(n+1,vector<int>(m+1,-1));
	// initialization
	for(int j = 0;j <= m;j++){
		dp[0][j] = 0;
	}
	for(int i=0;i<=n;i++){
		dp[i][0] = 0;
	}
	// run
	for(int i=1;i<=n;i++){
		for(int j=1;j<=m;j++){
			if(x[i-1] == y[j-1]){
				dp[i][j] = 1 + dp[i-1][j-1];
			}else{
				int val1 = dp[i][j-1];
				int val2 = dp[i-1][j];
				dp[i][j] = max(val1,val2);
			}
		}
	}
	return dp[n][m];
}
```
