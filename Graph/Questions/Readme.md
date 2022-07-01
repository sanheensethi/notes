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

