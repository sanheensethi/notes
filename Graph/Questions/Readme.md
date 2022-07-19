## 1. Number of Proviences (Count Connected Components)

> Adjacency Matrix is Given :

```cpp
void BFS(int node,vector<bool>& visited,vector<vector<int>>& matrix,int V){
        queue<int> Q;
        Q.push(node);
        visited[node] = true;
        
        while(!Q.empty()){
            auto node = Q.front();Q.pop();
            vector<int>& nbrs = matrix[node];
            for(int i = 0; i < V; i++){
                if(nbrs[i] == 1 && !visited[i]){
                    Q.push(i);
                    visited[i] = true;
                }
            }
        }
    }
  
    int BFSDriver(vector<vector<int>>& matrix,int V){
        vector<bool> visited(V,false);
        int count = 0;
        for(int i = 0; i < V; i++){
            if(!visited[i]){
                BFS(i,visited,matrix,V);
                count++;
            }
        }
        return count;
    }
```

## Important : Mark 2D matrix Row Col Visited in 1D array

[Article](https://www.geeksforgeeks.org/emulating-a-2-d-array-using-1-d-array/)
> Formula : index = j + (i * total_no_of_columns_in_matrix)

## 2. 01 Matrix [Question](https://leetcode.com/problems/01-matrix/)

![image](https://user-images.githubusercontent.com/35686407/175925763-383ac91e-db5b-4dfa-a739-736c1be939fb.png)

- Distance vector bnana hai and 1 se nearest 0 ka distance nikalna hai.

#### Approach 1: Brute Force : (BFS from each 1)

- we will apply bfs from each 1 and find the shortest distance to 0.
- we have 4 options to move from 1, left right top and down
- and while moving, when we encounter 0, we return distance
- But, in this approach, we will only be able to update the distance of one 1 using one BFS, which could in fact, result in slightly higher complexity

```cpp
int mapIndex(int row,int col,int totalCol){
        return col + row*totalCol;
    }
    
bool isPossible(int x,int y,vector<bool>& visited,int row,int col){
    if(x < 0 || y < 0 || x >= row || y >= col || visited[mapIndex(x,y,col)]) return false;
    return true;
}

int bfs(int i,int j,vector<vector<int>>& mat){
    
    int row = mat.size();
    int col = mat[0].size();
    
    vector<bool> visited(row*col,false);
    
    queue<vector<int>> Q;
    Q.push({i,j,0});
    visited[mapIndex(i,j,col)] = true;
    
    while(!Q.empty()){
        int size = Q.size();
        while(size--){
            auto& vec = Q.front();
            int x = vec[0];
            int y = vec[1];
            int dist = vec[2];
            Q.pop();        
            if(mat[x][y] == 0){
                return dist;
            };
            // up
            if(isPossible(x-1,y,visited,row,col)){
                Q.push({x-1,y,dist+1});
                visited[mapIndex(x-1,y,col)] = true;
            }
            
            // down
            if(isPossible(x+1,y,visited,row,col)){
                Q.push({x+1,y,dist+1});
                visited[mapIndex(x+1,y,col)] = true;
            }
            // right
            if(isPossible(x,y+1,visited,row,col)){
                Q.push({x,y+1,dist+1});
                visited[mapIndex(x,y+1,col)] = true;
            }
            //left
            if(isPossible(x,y-1,visited,row,col)){
                Q.push({x,y-1,dist+1});
                visited[mapIndex(x,y-1,col)] = true;
            }
        }
        
    }
    return INT_MAX;
}
    
vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
    int rows = mat.size();
    int cols = mat[0].size();
    vector<vector<int>> ans(rows,vector<int>(cols));
    
    for(int i = 0; i < rows; i++){
        for(int j = 0; j < cols; j++){
            if(mat[i][j] == 1){
                mat[i][j] = bfs(i,j,mat);
            }else{
                mat[i][j] = 0;
            }
        }
    }
    return mat;
}
```
#### Approach 2: [Optimized] (Better BFS)

- what if we start the BFS from 0s and thereby, updating the distances of all the 1s in the path.
- means sare 0's ki position ko queue mae daal do,
- ek distance matrix bnao, jime agar mat[i][j] == 0, distance[i][j] = 0 bhrdo, else INT_MAX bhrdo
- ab, queue mae traverse kro
- pehla coorinate jo aaya 0 ka hai, us 0 se hum kha kha ja skte hai ? left, right, up, down
- ab, if distance[new_row][new_col] > distance[cur_row][cur_col] + 1 to updatre kro and new_row,new_col ko queue mae dalo.

![undefined-1656328070069](https://user-images.githubusercontent.com/35686407/175927901-867555a2-e581-4e61-ae95-e0bba965f9c2.jpg)

![undefined-1656328241948](https://user-images.githubusercontent.com/35686407/175928422-3be8a9b7-13cb-42eb-8fe3-fb972fb5ba0c.jpg)

- Now ab jo (1,1) hia, vo ab niche check krega to update, so INF > 1 + 1, YES , UPDATE
 
```cpp
vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
    // starting bfs from 0
    
    int rows = mat.size();
    int cols = mat[0].size();
    vector<vector<int>> dist(rows,vector<int>(cols,INT_MAX));
    
    queue<pair<int,int>> Q;
    
    for(int i = 0; i < rows; i++){
        for(int j = 0; j < cols; j++){
            if(mat[i][j] == 0){
                Q.push({i,j});
                dist[i][j] = 0;
            }
        }
    }
    
    while(!Q.empty()){
        auto& pr = Q.front();
        int x = pr.first;
        int y = pr.second;
        Q.pop();
        
        // left
        if(y-1 >= 0 && dist[x][y-1] > dist[x][y] + 1){
            dist[x][y-1] = dist[x][y] + 1;
            Q.push({x,y-1});
        }
        
        // right
        if(y+1 < cols && dist[x][y+1] > dist[x][y] + 1){
            dist[x][y+1] = dist[x][y] + 1;
            Q.push({x,y+1});
        }
        
        // up
        if(x-1 >= 0 && dist[x-1][y] > dist[x][y] + 1){
            dist[x-1][y] = dist[x][y] + 1;
            Q.push({x-1,y});
        }
        
        // down
        if(x+1 < rows && dist[x+1][y] > dist[x][y] + 1){
            dist[x+1][y] = dist[x][y] + 1;
            Q.push({x+1,y});
        }
    }
    return dist;
}
```

> Another Way to Write :

```cpp
class Solution {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        int rows = mat.size();
        int cols = mat[0].size();
        
        vector<vector<int>> dist(rows,vector<int>(cols,INT_MAX));
        
        queue<pair<int,int>> Q;
        for(int i = 0; i < rows; i++){
            for(int j = 0; j < cols; j++){
                if(mat[i][j] == 0){
                    Q.push({i,j});
                    dist[i][j] = 0;
                }
            }
        }
        
        pair<int,int> dxy[4] = {{0,+1},{0,-1},{-1,0},{+1,0}};
        while(!Q.empty()){
            int size = Q.size();
            while(size--){
                pair<int,int>& cord = Q.front();
                for(int k = 0; k < 4; k++){
                    int _i = cord.first + dxy[k].first;
                    int _j = cord.second + dxy[k].second;
                    
                    if(_i >= 0 && _j >= 0 && _i < rows && _j < cols && dist[_i][_j] > dist[cord.first][cord.second]+1){
                        dist[_i][_j] = dist[cord.first][cord.second]+1;
                        Q.push({_i,_j});
                    }
                }
                Q.pop();
            }
        }
        return dist;
    }
};
```

#### Appraoch 3: More Optimized (Dynamic Programming) [Not Proper DP, it's just algo.]

- For convinience, let's call the cell with value 0 as **zero-cell**, the cell has with value 1 as one-cell, the distance of the nearest 0 of a cell as **distance**.
- Firstly, we can see that the distance of all **zero-cells** are 0, so we skip zero-cells, we process **one-cells** only.
- **In DP**, we can only **use prevous values if they're already computed**.
- In this problem, a cell has at most 4 neighbors that are left, top, right, bottom. If we use dynamic programming to compute the distance of the current cell based on 4 neighbors simultaneously, it's impossible because we are not sure if distance of neighboring cells is already computed or not.
- That's why, we need to compute the distance one by one:
    - **Firstly**, for a cell, we restrict it to only 2 directions which are left and top. Then we iterate cells from **top to bottom**, and from **left to right**, we calculate the distance of a cell **based on its left and top neighbors.**
    - Secondly, for a cell, we restrict it only have 2 directions which are right and bottom. Then we iterate cells from **bottom to top**, and from **right to left**, we update the distance of a cell **based on its right and bottom neighbors.**

> basically, hum upar se niche aate hue minimum distance dekh rhe hai 1 ka 0 se, and niche se upar aate hue bhi minimum distance dekh rhe hai, if or bhi jada minimum distance aata hai niche se upar, to usko update krdenge.

![8da7965f-6cf4-4ac2-a307-33f661fea5ca_1627604534 7922251](https://user-images.githubusercontent.com/35686407/175929321-595301e6-5fb1-4a11-ae27-7115f25a871b.png)

```cpp
vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
    int rows = mat.size();
    int cols = mat[0].size();
    
    for(int i = 0; i < rows; i++){
        for(int j = 0; j < cols; j++){
            if(mat[i][j] == 0) continue;
            int TOP = i-1 >= 0 ? mat[i-1][j] : INT_MAX;
            int LEFT = j-1 >= 0 ? mat[i][j-1] : INT_MAX;
            
            int prev_dist = min(TOP,LEFT);
            if(prev_dist != INT_MAX){
                mat[i][j] = prev_dist + 1;
            }else{
                mat[i][j] = prev_dist;
            }
        }
    }
    
    for(int i = rows-1; i >= 0; i--){
        for(int j = cols-1; j>=0; j--){
            if(mat[i][j] == 0) continue;
            int BOTTOM = i+1 < rows ? mat[i+1][j] : INT_MAX;
            int RIGHT = j+1 < cols ? mat[i][j+1] : INT_MAX;
            
            int prev_dist = min(BOTTOM,RIGHT);
            if(prev_dist != INT_MAX){
                mat[i][j] = min(mat[i][j],prev_dist + 1);
            }else{
                mat[i][j] = min(mat[i][j],prev_dist);
            }
            
        }
    }
    return mat; 
}
```
## 2. Number of Islands

- hme isme numbr of islands count krne hai
- 1 is land and 0 is water

![image](https://user-images.githubusercontent.com/35686407/176653496-26d67356-5dd7-4618-a1f7-3b3c4d338351.png)
![image](https://user-images.githubusercontent.com/35686407/176653577-a58c3083-d470-4064-a131-0e2863fede4d.png)

![image](https://user-images.githubusercontent.com/35686407/176655123-da348837-9790-4bb9-a84d-48f5808ffd5b.png)


- grid mae dfs lgado, and mark krdo visited position ko ki its already visited,
- visited ke liye use kro, transformation, from 2d array to 1d array
- go to up, down, right, left, and if it is possible to move then move otherwise return back and try other direction.
- its just basically count total number of disconnected components.

> DFS :

```cpp
class Solution {
public:
    
    bool isPossible(int i,int j,int rows,int cols,vector<bool>& visited,vector<vector<char>>& grid){
        if(i < 0 || j < 0 || i >= rows || j >= cols || grid[i][j] == '0' || visited[mapIdx(i,j,cols)]) return false;
        return true;
    }
    
    void dfs(int i,int j,int rows,int cols,vector<bool>& visited,vector<vector<char>>& grid){
        visited[mapIdx(i,j,cols)] = true;
        
        // left 
        if(isPossible(i,j-1,rows,cols,visited,grid)){
            dfs(i,j-1,rows,cols,visited,grid);
        }
        // right
        if(isPossible(i,j+1,rows,cols,visited,grid)){
            dfs(i,j+1,rows,cols,visited,grid);
        }
        // up
        if(isPossible(i-1,j,rows,cols,visited,grid)){
            dfs(i-1,j,rows,cols,visited,grid);
        }
        // down
        if(isPossible(i+1,j,rows,cols,visited,grid)){
            dfs(i+1,j,rows,cols,visited,grid);
        }
    }
    
    int numIslands(vector<vector<char>>& grid) {
        int rows = grid.size();
        int cols = grid[0].size();
        
        vector<bool> visited(rows*cols,false); // 2d array visited
        
        int count = 0;
        for(int i = 0; i < rows; i++){
            for(int j = 0; j < cols; j++){
                if(grid[i][j] == '1' && visited[mapIdx(i,j,cols)] == false){
                    count++;
                    dfs(i,j,rows,cols,visited,grid);
                }
            }
        }
        return count;
    }
    
    int mapIdx(int i,int j,int cols){
        return j + i*cols;
    }
    
};
```

## 2. Course Schedule I

- [1 0] , 1 number course ko lene ke liye 0 vala course lena pdega
- example : [[2,3],[1,2],[4,3],[2,5],[5,6]]
- we need course 3 for the course 2
- we need course 2 for the course 1
- we need course 3 for the course 4
- Below Graph is shown

![image](https://user-images.githubusercontent.com/35686407/176831216-40695d85-a2a8-4eb7-beed-56e4ef94331f.png)

#### Appraoch 1 : Topological Sort
- find cycle in Directed Graph , if found then topological sort is not possible
- if not found then return true

```
class Solution {
public:
    
    void makeGraph(vector<int> graph[],int nodes,vector<vector<int>>& pre){
        int size = pre.size();
        for(int i = 0; i < size; i++){
            int u = pre[i][0];
            int v = pre[i][1];
            graph[v].push_back(u);
        }
    }
    
    
    void calcIndegree(vector<vector<int>>& pre,vector<int>& indegree){
        for(int i = 0; i < pre.size(); i++){
            int u = pre[i][0];
            int v = pre[i][1];
            indegree[u]++;
        }
    }
    
    bool isCycle(vector<vector<int>>& pre,vector<int> graph[],int nodes){
        vector<int> indegree(nodes,0);
        calcIndegree(pre,indegree);
        
        queue<int> Q;
        for(int i = 0; i < nodes; i++){
            if(indegree[i] == 0){
                Q.push(i);
            }
        }
        
        int count = 0;
        while(!Q.empty()){
            int size = Q.size();
            while(size--){
                int node = Q.front();Q.pop();
                count++;
                vector<int>& nbrs = graph[node];
                for(auto& nbr : nbrs){
                    indegree[nbr]--;
                    if(indegree[nbr] == 0){
                        Q.push(nbr);
                    }
                }
            }
        }
        
        return count == nodes ? false : true;
        
    }
    
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<int> graph[numCourses];
        makeGraph(graph,numCourses,prerequisites);
        
        if(isCycle(prerequisites,graph,numCourses) == false) return true;
        return false;
    }
};
```
## 3. Cheapest Flights with K Stops (Shortest distance from src to dest using K - edges)

#### Approach 1: DFS + Pruning

- we will use dfs technique to reach the destination
- while going we mark the visited and while returning we mark visited[node] = false because as shown in below graph, from 1 to 4 there are multiple paths, if 1 -> 3 -> 2 -> 4 then also there is a path of 1 -> 2 -> 4 , but when in the first path, if we mark 2 as visited, we cant able to achieve 1 -> 2 -> 4 path. so that is why we need visited array.
- But this may lead to TLE , as it is of very high time complexity.

![image](https://user-images.githubusercontent.com/35686407/176842839-0bca0dd8-3d00-4a88-82c3-f51d92cec441.png)

```cpp
class Solution {
public:
    
    void makeGraph(vector<vector<int>>& flights,vector<pair<int,int>> graph[]){
        for(auto& vec : flights){
            int src = vec[0];
            int dest = vec[1];
            int cost = vec[2];
            graph[src].push_back({dest,cost});
        }
    }
    
    void dfs(int src,int dst,int k, vector<pair<int,int>> graph[],int cost,int& finalCost,vector<bool>& visited){
        
        
        if(src == dst){
            finalCost = min(finalCost,cost);
            return;
        }
        
        if( k < 0 ) return;
        if(cost > finalCost) return;
        visited[src] = true;
        auto& nbrs = graph[src];
        
        for(auto& nbr : nbrs){
            int nbrNode = nbr.first;
            int wt = nbr.second;
            if(visited[nbrNode] != true){
                dfs(nbrNode,dst,k-1,graph,cost+wt,finalCost,visited);
            }
        }
        
        visited[src] = false;
    }
    
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {
        vector<pair<int,int>> graph[n];
        makeGraph(flights,graph);
        vector<bool> visited(n,false);
        int finalCost = INT_MAX;
        int cost = 0;
        dfs(src,dst,k,graph,cost,finalCost,visited);
        if(finalCost == INT_MAX) return -1;
        return finalCost;
    
    }
};
```

#### Approach 2 : Using DP [Storing Already Calculated Costs] [Optimized]

- in this, we didn't take the visited array, it is handeled by the dp itself
- we will make the dfs as in returning cost, so that we can memoize

```cpp
class Solution {
public:
    
    void makeGraph(vector<vector<int>>& flights,vector<pair<int,int>> graph[]){
        for(auto& vec : flights){
            int src = vec[0];
            int dest = vec[1];
            int cost = vec[2];
            graph[src].push_back({dest,cost});
        }
    }
    
    int dfs(int src,int dst,int k, vector<pair<int,int>> graph[],vector<vector<int>>& memo){
        
        if(src == dst){
            return 0;
        }
        
        if( k < 0 ) return INT_MAX;
        
        if(memo[src][k] != -1) return memo[src][k];
        
        auto& nbrs = graph[src];
        
        int ans = INT_MAX;
        
        for(auto& nbr : nbrs){
            int nbrNode = nbr.first;
            int wt = nbr.second;
            
                int dfsans = dfs(nbrNode,dst,k-1,graph,memo);
                if(dfsans != INT_MAX){
                    dfsans = dfsans + wt;
                    ans = min(ans,dfsans);
            }
        }
        return memo[src][k] = ans;
    }
    
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {
        vector<pair<int,int>> graph[n];
        makeGraph(flights,graph);
        vector<bool> visited(n,false);
        
        vector<vector<int>> memo(n+1,vector<int>(k+1,-1));
        
        int cost = dfs(src,dst,k,graph,visited,memo);
        if(cost == INT_MAX) return -1;
        return cost;
    
    }
};
```

#### Approach 3 : [Priority Queue] [Brute TLE]

```cpp
class Solution {
public:
    
    void makeGraph(vector<vector<int>>& flights,vector<pair<int,int>> graph[]){
        for(auto& vec : flights){
            int src = vec[0];
            int dest = vec[1];
            int cost = vec[2];
            graph[src].push_back({dest,cost});
        }
    }
    
    int dijkstraAlgo(vector<pair<int,int>> graph[],int nodes,int src,int dst,int k){
        priority_queue<tuple<int,int,int>,vector<tuple<int,int,int>>,greater<tuple<int,int,int>>> pq;
        
        pq.push({0,src,0});
        
        while(!pq.empty()){
            auto [cost,node,stop] = pq.top();
            pq.pop();
            
            if(node == dst) return cost;
            if(stop > k) continue;
            auto& nbrs = graph[node];
            for(auto& nbr:nbrs){
                auto [nbrNode,wt] = nbr;
                pq.push({wt+cost,nbrNode,stop+1});
            }
        }
        return -1;
    }
    
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {
        vector<pair<int,int>> graph[n];
        makeGraph(flights,graph);
        
        int ans =  dijkstraAlgo(graph,n,src,dst,k);
        if(ans == INT_MAX) return -1;
        return ans;
    }
};
```

## 4. Perfect Friends (Union Find) - [Pepcoding](https://nados.io/question/perfect-friends?zen=true)

```cpp
class unionFind{

   public:
      vector<int> parent;
      vector<int> size;

      unionFind(){}
      unionFind(int n){
         parent.resize(n);
         iota(parent.begin(),parent.end(),0);
         size.resize(n,1);
      }

      int findParent(int v){
         if(v == parent[v]) return v;
         return parent[v] = findParent(parent[v]);
      }

      void _union(int a,int b){
         a = findParent(a);
         b = findParent(b);
         if(a != b){
            if(size[a] < size[b]) swap(a,b);
            parent[b] = a;
            size[a] += size[b];
         }
      }

      int findAns(){
         set<int> ss;
         int n = parent.size();
         for(int i = 0; i < n; i++){
            ss.insert(findParent(i));
         }
         
         vector<int> comp(ss.size());

         int k = 0;
         for(auto& val:ss){
            comp[k++] = size[val];
         }

         int ans = 0;
         for(int i = 0; i < k; i++){
            for(int j = i+1; j < k; j++){
               ans = ans + (comp[i]*comp[j]);
            }
         }
         return ans;
      }
};

int main(){
   int n;
   cin>>n;
      
   int k;
   cin>>k;
      
   unionFind uf(n);
   while(k--){
      int a,b;
      cin>>a>>b;
      uf._union(a,b);
   }

   int ans = uf.findAns();
   cout<<ans<<endl;

          
   return 0;
 }
 ```
 
## 5. Hamiltonian Cycle

```cpp
void printPath(int src,vector<pair<int,int>> graph[],int n,
                unordered_map<int,bool>& visited,vector<int>& path,int endsrc){
    if(visited.size() == n-1){
        print(path);

        vector<pair<int,int>>& nbrs = graph[src];
        bool found = false;
        for(auto& prnbr:nbrs){
            int nbr = prnbr.first;
            if(nbr == endsrc){
                found = true;
                break;
            }
        }

        if(found){
            cout<<"This path is a Cycle"<<endl;
        }

        return;
    }

    visited[src] = true;
    vector<pair<int,int>>& nbrs = graph[src];
    for(auto& prnbr : nbrs){
        int nbr = prnbr.first;
        if(!visited.count(nbr)){
            path.push_back(nbr);
            printPath(nbr,graph,n,visited,path,endsrc);
            path.pop_back();
        }
    }
    visited.erase(src);
}

void hamiltonian(int src,vector<pair<int,int>> graph[],int n){
    unordered_map<int,bool> visited;
    vector<int> path;
    path.push_back(src);
    printPath(src,graph,n,visited,path,src);
}

void solve(){
    int n;cin>>n;
    vector<pair<int,int>> graph[n];
    int k;cin>>k;
    while(k--){
        int src,dest,wt;
        cin>>src>>dest>>wt;
        graph[src].push_back({dest,wt});
        graph[dest].push_back({src,wt});
    }
    int src;cin>>src;
    hamiltonian(src,graph,n);
}
```

## 6. Color a Border

```cpp
class Solution {
public:
    #define debug(x) cout<<#x<<":"<<x<<endl;
    vector<int> dx = {0,0,-1,1};
    vector<int> dy = {1,-1,0,0};
    void doColor(int i,int j,int val,int m,int n,vector<vector<int>>& grid){
        
        grid[i][j] = -val;
        int count = 0;
        // 4 calls
        for(int k = 0; k < 4; k++){
            
            int _i = i + dx[k];
            int _j = j + dy[k];
            
            if(_i < 0 || _j < 0 || _i >= m || _j >= n || abs(grid[_i][_j]) != val){
                continue;
            }
            
            if(abs(grid[_i][_j]) == val){
                count++;   
                if(grid[_i][_j] < 0) continue;
                // call
                doColor(_i,_j,val,m,n,grid);
            }            
        }
       
        if(count == 4){
            grid[i][j] = val;
        }else{
            // pass
            return;
        }                                        
    }
                   
    vector<vector<int>> colorBorder(vector<vector<int>>& grid, int row, int col, int color) {
        int i = row;
        int j = col;
        int m = grid.size();
        int n = grid[0].size();
        doColor(i,j,grid[i][j],m,n,grid);
        for(int l = 0; l < m; l++){
            for(int k = 0; k < n; k++){
                if(grid[l][k] < 0) grid[l][k] = color;
            }
        }
        return grid;
    }
};
```
## 2. Number of Enclaves

- isme hme vo 1's count krne hai jo hme out of boundary na lekr jaye, mtlb jo 1's boundary pr hai uske sath jo bhi joined hai unhe count nhi krna hai baki 1's ko count krna hai.
- iske liye hme i = 0, j = 0, i == last row , j = last col , ke liye dfs lgakr connected components ko ek krna hoga taki hm 1's count kr sake jo connected nhi hai, boundary se.

```cpp
class Solution {
public:
    
    int dx[4] = {0,0,-1,+1};
    int dy[4] = {-1,+1,0,0};
    
    int numEnclaves(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(i == 0 || j == 0 || i == n-1 || j == m-1){
                    dfs(i,j,grid);
                }
            }
        }
        
        int ans = 0;
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(grid[i][j] == 1) ans++;
            }
        }
        return ans;
    }
    
    void dfs(int i,int j,vector<vector<int>>& grid){
        int n = grid.size();
        int m = grid[0].size();
        
        if(i < 0 || j < 0 || i >= n || j>= m || grid[i][j] == 0) return;
        
        grid[i][j] = 0;
        
        for(int k = 0; k < 4; k++){
            int _i = i + dx[k];
            int _j = j + dy[k];
            dfs(_i,_j,grid);
        }
    }
    
};
```

## 3. Number of Distinct Islands

- starting position ko 'x' keh rhe hai.
- isme hm jb right ja rhe hai to define kr rhe hai path mae 'r'
- for left it's 'l' , up 'u' and down 'd'
- ab, hme ise set mae dalna hai, but isme ek problem ye hogi hm backtrack ko ek char nhi de rhe hai, to esa ho skta hai for two different islands , we have same path value so, backtrack ko bhi ek char dena pdega, let its be 'z'
- ab ye sb set mae daal denge, now, we got distinct number of islands as our size of set.

```cpp
class Solution {
  public:
  
    void dfs(int i,int j,string& path,vector<vector<int>>& grid){
        int n = grid.size();
        int m = grid[0].size();
        
        if(i < 0 || j < 0 || i >= n || j >= m || grid[i][j] == 0) return;
        
        grid[i][j] = 0;
        
        // right
        path += 'r';
        dfs(i,j+1,path,grid);
        path += 'z';
        // left
        path += 'l';
        dfs(i,j-1,path,grid);
        path += 'z';
        // up
        path += 'u';
        dfs(i-1,j,path,grid);
        path += 'z';
        // down
        path += 'd';
        dfs(i+1,j,path,grid);
        path += 'z';
        
    }
  
    int countDistinctIslands(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        
        set<string> ss;
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(grid[i][j] == 1){
                    string path = "x";
                    dfs(i,j,path,grid);
                    ss.insert(path);
                }        
            }
        }
        return ss.size();
    }
};
```

## 4. Rotten Oranges 

- Hme simultaneously fresh oranges ko roatten krna hai
- simultaneously means BFS

```cpp
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
        int rows = grid.size();
        int cols = grid[0].size();
        queue<pair<int,int>> Q;
        int fresh = 0;
        for(int i = 0; i < rows; i++){
            for(int j = 0; j < cols; j++){
                if(grid[i][j] == 2){
                    Q.push({i,j});
                }else if(grid[i][j] == 1){
                    fresh++;
                }
            }
        }
        
        int t = -1;
        pair<int,int> dxy[4] = {{0,-1},{0,+1},{-1,0},{+1,0}};
        while(!Q.empty()){
            int size = Q.size();
            while(size--){
                pair<int,int>& coord = Q.front();
                for(int k = 0; k < 4; k++){
                    int _i = coord.first + dxy[k].first;
                    int _j = coord.second + dxy[k].second;
                    if(_i < 0 || _j < 0 || _i >= rows || _j >= cols || grid[_i][_j] == 0 || grid[_i][_j] == 2){
                        continue;
                    }
                    
                    grid[_i][_j] = 2;
                    Q.push({_i,_j});
                    fresh--;
                }
                Q.pop();
            }
            t++;
        }
        if(fresh > 0) return -1;
        if(t == -1) return 0;
        return t;
    }
};
```
## 5. As far from Land as Possible

- Manhattan distance is nothing , just a jumps, similar as [zero one matrix Better Optimized](#approach-2-optimized-better-bfs)

```cpp
class Solution {
public:
    int maxDistance(vector<vector<int>>& grid) {
        int ans = 0;
        int rows = grid.size();
        int cols = grid[0].size();
        
        vector<vector<int>> dist(rows,vector<int>(cols,INT_MAX));
        
        queue<pair<int,int>> Q;
        bool noland = true;
        bool nowater = true;
        for(int i = 0; i < rows; i++){
            for(int j = 0; j < cols; j++){
                if(grid[i][j] == 1){
                    noland = false;
                    dist[i][j] = 0;
                    Q.push({i,j});
                }
                if(grid[i][j] == 0){
                    nowater = false;
                }
            }
        }
        
        if(noland || nowater) return -1;
        
        pair<int,int> dxy[4] = {{0,-1},{0,+1},{-1,0},{+1,0}};
        while(!Q.empty()){
            int size = Q.size();
            while(size--){
                pair<int,int>& cord = Q.front();
                
                for(int k = 0; k < 4; k++){
                    int _i = cord.first + dxy[k].first;
                    int _j = cord.second + dxy[k].second;
                    
                    if(_i < 0 || _j < 0 || _i >= rows || _j >= cols) continue;
                    
                    if(dist[_i][_j] > dist[cord.first][cord.second] + 1){
                        dist[_i][_j] = dist[cord.first][cord.second]+1;
                        ans = max(ans,dist[_i][_j]);
                        Q.push({_i,_j});
                    }
                    
                }
                Q.pop();
            }
        }
        return ans;
    }
};
```
## 6. Shortest Bridge
 
- isme exactly 2 island hai, to hme 1 island ko figureout krna hai and use queue mae daal dena hai
- uske baad us island ke hr ek 1 se jo queue mae hai, vha se dusra island search krna hai by bfs,
- jb vo mil jayega , jis level pr milega, vhi mera ans hoga.

```cpp
class Solution {
public:
    int dx[4] = {0,0,+1,-1};
    int dy[4] = {-1,+1,0,0};
    
    void dfs(int i,int j,queue<pair<int,int>>& Q,vector<vector<int>>& grid){
        int n = grid.size();
        int m = grid[0].size();
        
        if(i < 0 || j < 0 || i >= n || j >= m || grid[i][j] == 2 || grid[i][j] == 0) return;
        
        Q.push({i,j});
        grid[i][j] = 2;
        
        for(int k = 0; k < 4; k++){
            int _i = i + dx[k];
            int _j = j + dy[k];
            dfs(_i,_j,Q,grid);
        }
    }
    
    int shortestBridge(vector<vector<int>>& grid) {
        int rows = grid.size();
        int cols = grid[0].size();
        
        queue<pair<int,int>> Q;
        
        int flag = false;
        for(int i = 0; i < rows && !flag; i++){
            for(int j = 0; j < cols && !flag; j++){
                if(grid[i][j] == 1){
                    dfs(i,j,Q,grid);
                    flag = true;
                }
            }
        }
        
        if(flag == false) return -1;
        
        int level = 0;
        
        
        while(!Q.empty()){
            int size = Q.size();
            while(size--){
                pair<int,int>& cord = Q.front();
                
                for(int k = 0; k < 4; k++){
                    int _i = cord.first + dx[k];
                    int _j = cord.second + dy[k];        
                    if(_i < 0 || _j < 0 || _i >= rows || _j >= cols || grid[_i][_j] == 2) continue;
                    if(grid[_i][_j] == 1) return level;
                    grid[_i][_j] = 2;
                    Q.push({_i,_j});   
                }
                Q.pop();
            }
            level++;
        }
        
        return -1;
    }
};
```

## 7. Bus Routes (LeetCode)

- isme hme ye to pta hai, ki konc bus konse konse stops pr rukti hai
- lekin ye nikalna ki konse stop pr konc bus aati hai O(1) mae difficult hai
- mtlb hum O(1) mae bus number se sare stop nikal skte hai
- lekin O(1) mae stop number se bus number nhi,
- to iske liye hashmap lenge taki hum ye pta lga sake ki konse stop pr konc konc buses chlti hai O(1) mae
- map : <stopNumber,AllBusesFromThatStop>
- ab hum 2 bool vector lenge,
    1. jo hme ye btaye ki ye bus already le chuke hai (isse hme ye pta chlega ki hmne iske sare routes ko queue mae already daal dia hai, istead one by one checking of it's routes that it is visited or not)
    2. jo hme ye byatega ki ye route already visited hai (Node Visited)
- ab hum queue bnayenge , src dalenge and stopVisited[src] = true kr denge
- and jb queue mae aayenge, 1st stop nikalenge, nikalne ke baad hm vha se jane vali sari buses nikalenge hmare umap se, 
- ab sari buses ke vo routes Q mae dalenge jo visited na ho.
- jb dest == stopNumber aayega, tb return level (which is minimum buses)

```cpp
class Solution {
public:
    
    void makeStopBusMap(vector<vector<int>>& routes,unordered_map<int,vector<int>>& umap,int& maxi){
        int n = routes.size();
        for(int i = 0; i < n; i++){
            int bus = i;
            for(auto& stop : routes[i]){
                umap[stop].push_back(bus);
                maxi = max(maxi,stop);
            }
        }
    }
    
    int numBusesToDestination(vector<vector<int>>& routes, int source, int target) {
        unordered_map<int,vector<int>> umap; // stopNumber and Buses
        int maxi = -1;
        makeStopBusMap(routes,umap,maxi);
        
        return minimumBuses(routes,umap,maxi,source,target);
    }
    
    int minimumBuses(vector<vector<int>>& routes,unordered_map<int,vector<int>>& umap,const int& maxi,const int& src,const int& dest){
        
        int buses = routes.size();
        vector<bool> busTaken(buses,false);
        vector<bool> stopVisited(maxi+1,false);
        
        queue<int> Q;
        Q.push(src);
        stopVisited[src] = true;
        int level = 0;
        
        while(!Q.empty()){
            int size = Q.size();
            while(size--){
                int stopNumber = Q.front();Q.pop();
                if(stopNumber == dest) return level;
                vector<int>& allBuses = umap[stopNumber];
                for(auto& bus : allBuses){
                    if(busTaken[bus] == true) continue;
                    vector<int>& allStopsOfThisBus = routes[bus];
                    for(auto& stop : allStopsOfThisBus){
                        if(stopVisited[stop] == true) continue;
                        Q.push(stop);
                        stopVisited[stop] = true;
                    }
                    busTaken[bus] = true;
                }
            }
            level++;
        }
        return -1;
    }
    
};
```

## 8. Sliding Puzzle

```cpp
class Solution {
public:
    #define debug(x) cout<<#x<<":"<<x<<endl;
    string serialize(vector<vector<int>>& board){
        string str = "";
        int n = board.size();
        int m = board[0].size();
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                str += (board[i][j] + '0');
            }
        }
        return str;
    }
    int slidingPuzzle(vector<vector<int>>& board) {
        string target = "123450";
        string initial = serialize(board);
        int zeroIdx = -1;
        int n = initial.size();
        for(int i = 0; i < n; i++){
            if(initial[i] == '0'){
                zeroIdx = i;
                break;
            }
        }
        
        unordered_map<string,bool> visited;
        int level = 0;
        vector<vector<int>> swapWith = {{1,3},{0,2,4},{1,5},{0,4},{1,3,5},{4,2}};
        
        queue<pair<string,int>> Q; // board serialize,zeroidx
        Q.push({initial,zeroIdx});
        visited[initial] = true;
        
        while(!Q.empty()){
            int size = Q.size();
            while(size--){
                auto& pr = Q.front();
                string& str = pr.first;
                int& zeroidx = pr.second;
                if(str == target) return level;
                
                auto& allSwapsIdx = swapWith[zeroidx];
                
                for(auto idx:allSwapsIdx){
                    swap(str[zeroidx],str[idx]);
                    string newStr = str;
                    swap(str[zeroidx],str[idx]);
                    
                    if(visited[newStr] == false){
                        Q.push({newStr,idx});
                        visited[newStr] = true;
                    }
                }
                Q.pop();
            }
            level++;
        }
        return -1;
    }
};
```
