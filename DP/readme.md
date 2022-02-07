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

## Longest Common Substring

> Recursion
 - We are taking max of count,val1,val2 because suppose if we didn't encounter the same char then we have to start with 0 length again, but for that we can't forget to consider already solved problem maybe it is the max substring therefore we can't return from if statement as subsequence, rather we calculate further for no matching char and return the max of these three.
For Visulization visit : [Visulize Link](https://recursion.vercel.app/)

```cpp
int LCSubstring(string& x,string& y,int n,int m,int len){
	if(n == 0 || m == 0){
		return len;
	}
	int count = len;
	if(x[n-1] == y[m-1]){
		count = LCSubstring(x,y,n-1,m-1,len+1); 
	}
	int val1 = LCSubstring(x,y,n-1,m,0);
	int val2 = LCSubstring(x,y,n,m-1,0);
	return max({count,val1,val2});
}
```
> Memo
```cpp
int LCSubstring(string& x,string& y,int n,int m,int len,vector<vector<vector<int>>>& dp){
	if(n == 0 || m == 0){
		return len;
	}
	if(dp[n][m][len] != -1) return dp[n][m][len];
	int count = len;
	if(x[n-1] == y[m-1]){
		count = LCSubstring(x,y,n-1,m-1,len+1,dp); 
	}
	int val1 = LCSubstring(x,y,n-1,m,0,dp);
	int val2 = LCSubstring(x,y,n,m-1,0,dp);
	return dp[n][m][len] = max({count,val1,val2});
}

int n,m;
  	n = x.size();
  	m = y.size();
  	vector<vector<vector<int>>> dp(n+1,vector<vector<int>>(m+1,vector<int>(min(n+1,m+1),-1)));
  	cout<<LCSubstring(x,y,n,m,0,dp);
```

> Tabular
```cpp
int LCSubstringTabular(string& x,string& y){
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
	int maxi = INT_MIN;
	for(int i=1;i<=n;i++){
		for(int j=1;j<=m;j++){
			if(x[i-1] == y[j-1]){
				dp[i][j] = 1 + dp[i-1][j-1];
				maxi = max(maxi,dp[i][j]);
			}else{
				dp[i][j] = 0;
			}
		}
	}
	return maxi;
}
```

## Shortest Common Subsequence (Length)

> Lenght of Shortest Common Subsequence is n + m - LCS(x,y,n,m), because when we concatenate the both string we have to remove the common part, common part is nothing but a LCS, therefore we substract length of common subsequence.


function fn(n,m) {
  if(n == 0 || m == 0){
    let set = new Set();
    set.add('');
    return [0,[... set]];
  }

  if(x[n-1] == y[m-1]){
    let pr = fn(n-1,m-1);
    pr[0] = pr[0]+1;
    let set = new Set();
    let val = pr[1];
    for(const v of val){
      set.add(v + x[n-1]);
    }
    return [pr[0],[... set]];
  }

  let v1 = fn(n-1,m);
  let v2 = fn(n,m-1);

  if(v1[0] >= v2[0]){
    if(v1[0] == v2[0]){
      let set = new Set();
      let val1 = v1[1];
      let val2 = v2[1];
      for(const v of val1){
        set.add(v);
      }
      for(const v of val2){
        set.add(v);
      }
      return [v1[0],[... set]];
    }else{
      return v1;
    }
  }else{
    return v2;
  }
}
