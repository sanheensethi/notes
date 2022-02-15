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
	dp[n] = 0;
	for(int i = n-1;i>=0;i--){
		int steps = jumps[i];
		int mini = INT_MAX-1;
		while(steps){
			if(i + steps <= n){
				int val = dp[i+steps];
				mini = min(mini,val);
			}
			steps--;
		}
		dp[i] = 1 + mini;
	}

	if(dp[0] == INT_MAX){
		cout<<"null"<<endl;
	}else{
		cout<<dp[0]<<endl;
	}
}
```

## Minimum Cost Dynamic Programming

> Recursion (Wrong Way):
```cpp
int minCost(vector<vector<int>>& maze,int row,int col){
	if(row >= maze.size() || col >= maze[0].size()) return INT_MAX;
	if(row == maze.size()-1 && col == maze[0].size()-1){
		return maze[row][col];
	}
	int val1 = maze[row][col] + minCost(maze,row+1,col); // down
	int val2 = maze[row][col] + minCost(maze,row,col+1); // right
	return min(val1,val2); // current cell taken
}
```
- `Question:` Why Wrong ?
- `Answer:` We will not return `INT_MAX` from the base case.
- `Question:` Why we didn't return `INT_MAX` as base case when `row >= maze.size()` or `col >= maze.size()` ?
- `Answer:` It's difficult to think in the first go but when you dry run for smaller testcase you will got to know the main problem, as when you write this as base case, then when you get `INT_MAX` as return from parituclar row and col to preious partiular row and column, you end up with `maze[row][col] + INT_MAX` = `INT_MIN` that's wrong. Okay, now you will say that okay i will not add `maze[row][col]` to `val1` and `val2` directly but in the end `on returing` i will `add it`. Yes you can do it, I just tell you the case to think that while returning `INT_MAX` from base case you should care of that adding these numbers to `INT_MAX` which `make the bug in code`.

> Recursion: (Right way):
```cpp
int minCost(vector<vector<int>>& maze,int row,int col){
	if(row == maze.size()-1 && col == maze[0].size()-1){
		return maze[row][col];
	}
	int val1 = minCost(maze,row+1,col,dp); // down
	int val2 = minCost(maze,row,col+1,dp); // right
	return maze[row][col] + min(val1,val2); // current cell taken
}
```

> Recursion (Another Right Way):
```cpp
int minCost(vector<vector<int>>& maze,int row,int col){
	if(row == maze.size()-1 && col == maze[0].size()-1){
		return maze[row][col];
	}
	int val1 = INT_MAX;
	int val2 = INT_MAX;
	// down
	if(row+1 < maze.size() && col < maze[0].size()){
		val1 = maze[row][col] + minCost(maze,row+1,col);
	}
	// right
	if(col+1 < maze[0].size() && row < maze.size()){
		val2 = maze[row][col] + minCost(maze,row,col+1);
	}
	return min(val1,val2); // current cell taken
}
```



> Memoization
```cpp
int minCost(vector<vector<int>>& maze,int row,int col,vector<vector<int>>& dp){
	if(row == maze.size()-1 && col == maze[0].size()-1){
		return maze[row][col];
	}
	if(dp[row][col] != -1) return dp[row][col];
	int val1 = INT_MAX;
	int val2 = INT_MAX;
	if(row+1 < maze.size() && col < maze[0].size()){
		val1 = maze[row][col] + minCost(maze,row+1,col,dp);
	}
	if(col + 1 < maze[0].size() && row < maze.size()){
		val2 = maze[row][col] + minCost(maze,row,col+1,dp);
	}
	return dp[row][col] = min(val1,val2);
}
vector<vector<int>> dp(n+1,vector<int>(m+1,-1));
int ans = minCost(maze,0,0,dp);
```

> Tabular

- In Tabular, we will initialize last row(`n-1`) and last column(`m-1`) the 2D matrix.
- Why ? because, when man is standing in the last `row`, it have only one option to move in the right direction i.e., `col+1`. 
- Simillarly, when we man is in the last `column`, it have only one direction to move i.e. in downward direction i.e., `row+1`.
- And, we fill this array from bottom to up , because we know at `(n-1,m-1)` the ans will be itself value `maze[n-1][m-1]`.
- So, during initialization, we are adding last row as suffix sum and last col also as suffix sum. 

```cpp
void solve(){
	int n,m;cin>>n>>m;
	vector<vector<int>> maze(n,vector<int>(m));
	
	for(int i=0;i<n;i++){
		for(int j=0;j<m;j++){
			cin>>maze[i][j];
		}
	}

	vector<vector<int>> T(n,vector<int>(m,-1));
	T[n-1][m-1] = maze[n-1][m-1];

	// initialization
	// when man is on last row, its option
	// is only 1 move in right direction.

	for(int j= m-2;j >= 0;j--){
		T[n-1][j] = maze[n-1][j] + T[n-1][j+1];
	}

	// when man is in last column it have only
	// one option move in down direction only.

	for(int i = n-2;i >= 0;i--){
		T[i][m-1] = maze[i][m-1] + T[i+1][m-1];
	}

	// 2d matrix fill

	for(int i = n-2;i>=0;i--){
		for(int j = m-2;j>=0;j--){
			int val1 = INT_MAX;
			int val2 = INT_MAX
			val1 = maze[i][j] + T[i+1][j];
			val2 = maze[i][j] + T[i][j+1];
			T[i][j] = min(val1,val2);
		}
	}
	cout<<T[0][0]<<endl;
}
```
