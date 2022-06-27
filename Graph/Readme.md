# Graph

## Introduction

- A graph is an advanced data structure that is used to organize items in an interconnected network.
- Each item in a graph is known as a node(or vertex) and these nodes are connected by edges.

![Screenshot Capture - 2022-06-27 - 10-22-42](https://user-images.githubusercontent.com/35686407/175862659-41787d4c-3e12-49fe-b442-30d6e5f77f99.png)

> Real World Example

![1601570264-76844](https://user-images.githubusercontent.com/35686407/175862738-85039143-3cba-4c91-bb12-d4a2fa6c1eb9.png)

## Types Of Graph:

[Article](https://www.studytonight.com/advanced-data-structures/introduction-to-graphs)

> Null Graph :

![1601623770-76844](https://user-images.githubusercontent.com/35686407/175862821-13da89f8-07ce-4f28-a4d4-2bd749e670a3.png)

> Undirected Graph :

![1601571315-76844](https://user-images.githubusercontent.com/35686407/175862937-ebb94bca-97f2-4750-a199-73c22099bab4.png)

> Directed Graph :

![1601571633-76844](https://user-images.githubusercontent.com/35686407/175862986-583d2cf9-9c5f-4432-a2f1-dce6ba9b8c32.png)

> Cyclic Graph :

![1601573458-76844](https://user-images.githubusercontent.com/35686407/175863027-8672c7fa-bcb2-4a1d-9599-5527cfd310fd.png)

> Ascylic Graph :

![1601575738-76844](https://user-images.githubusercontent.com/35686407/175863087-d4353c53-f1b2-425f-994b-2233d0d5d524.png)

> Weighted Graph :

![1601622376-76844](https://user-images.githubusercontent.com/35686407/175863111-c953e933-0b1d-4790-af94-a73cb774c9ae.png)

> Connected Graph :

![1601623135-76844](https://user-images.githubusercontent.com/35686407/175863153-fff84826-602b-4417-a819-7d76352952a8.png)

> Dis-Connected Graph :

![1601623424-76844](https://user-images.githubusercontent.com/35686407/175863202-a01612b4-7ee7-4dd3-9c91-d7ebb500c37c.png)

> Complete Graph :

![1601624018-76844](https://user-images.githubusercontent.com/35686407/175863270-fb51e71b-6835-4278-b9f1-273a7045989d.png)

> Milti Graph :

![1601624690-76844](https://user-images.githubusercontent.com/35686407/175863321-923ed0bf-358c-4727-9d8b-f10a30874df8.png)

> Bipartite Graph :

![Bipartite-Graph-Example-1](https://user-images.githubusercontent.com/35686407/175863700-ab3aca7d-0b56-4151-b05a-2aaa5776d1bf.png)

![Screenshot Capture - 2022-06-27 - 10-33-53](https://user-images.githubusercontent.com/35686407/175863751-54b6cd26-60a9-4a92-b7a9-f8968efcf628.png)

## Graph Terminologies 

1. **Path** - A sequence of alternating nodes and edges such that each of the successive nodes are connected by the edge.
2. **Cycle** - A path where the starting and the ending node is the same.
3. **Simple Path** - A path where we do not encounter a vertex again.
4. **Bridge** - An edge whose removal will simply make the graph disconnected.
5. **Forest** - A forest is a graph without cycles.
6. **Tree** - A connected graph that doesn't have any cycles.
7. **Degree** - The degree in a graph is the number of edges that are incident on a particular node.
8. **Neighbour** - We say vertex "A" and "B" are neighbours if there exists an edge between them.

## Degree of Graph

1. Undirected : No. of edges connected to it
2. Directed :
    - In-Degree : No. edges comning towards node.
    - Out-Degree : No. of edges going outwards from node.

## Note : If Weights are not given but weights are necessary in question then assume weights = 1

## Representation of Graph

> Input Format

- No. of Nodes (n) , No. of edges (m)
- in m lines there are u and v, which tells , there is edge between u and v

![Screenshot 2022-06-27 104322](https://user-images.githubusercontent.com/35686407/175865084-38e1e277-5221-4a32-a635-3df67333f4f1.png)

#### Method 1 : Adjacency matrix

![1601728714-76844](https://user-images.githubusercontent.com/35686407/175865763-8dfd6b23-b12e-4ada-ba1c-aa758fc1c553.png)

![1601702196-76844](https://user-images.githubusercontent.com/35686407/175865764-603b7fa4-d887-4894-adc3-65e124f4f80c.png)

![image](https://user-images.githubusercontent.com/35686407/175865908-abef3f26-90f6-4fd4-adf3-bb929dacac38.png)

```cpp
void adjacencyMatrix(){
    int nodes,edges;
    cin>>nodes>>edges;
    print(nodes);
    print(edges);
    vector<vector<int>> graph(nodes+1,vector<int>(nodes+1));

    while(edges--){
        int u,v;
        cin>>u>>v;
        graph[u][v] = 1; // in case of weighted, we write weight instead of 1
        graph[v][u] = 1;
    }

    for(auto& vec:graph){
        print(vec);
    }
}
```
![image](https://user-images.githubusercontent.com/35686407/175867282-5e2b4a67-62c0-4e33-9e0e-66b35571db5e.png)

> Disadvantes :
No. of nodes : 10^5 , can't create 2D array of 10^5 X 10^5 , space complexity O(N X N)

#### Method 2: Adjacency List

![1601728714-76844 (1)](https://user-images.githubusercontent.com/35686407/175866396-ff42beae-9532-409b-8b40-8574dc8db0ab.png)

![1601727391-76844](https://user-images.githubusercontent.com/35686407/175866433-ccc26f27-8488-4d6e-b56d-7cf3e2944d3d.png)

![image](https://user-images.githubusercontent.com/35686407/175866054-1053642f-47d7-4475-b698-a5dd3edfa8c9.png)


![image](https://user-images.githubusercontent.com/35686407/175866183-9a0b9e0f-08fc-43d8-b146-880a27679df3.png)

> If weights are also given then we have to make use of pairs in which first is node and second is weight.

![image](https://user-images.githubusercontent.com/35686407/175866304-d1d374d1-b0f3-4b3c-87da-57d2dfb5234b.png)

```cpp
void adjacencyList(){
    int nodes,edges;
    cin>>nodes>>edges;
    
    vector<int> graph[nodes+1]; // vector<pair<int,int>> in case of weighted graph

    while(edges--){
        int u,v;
        cin>>u>>v;
        graph[u].push_back(v); // {v,w} in case of weighted graph
        graph[v].push_back(u); // {u,w} in case of weighted graph
    }

    for(int i = 1; i < nodes+1; i++){
        print(i);
        print(graph[i]);
    }
}
```
![image](https://user-images.githubusercontent.com/35686407/175867744-3f23aa31-e254-4fb3-97a9-3fad01e3509d.png)

## Connected Components

- if in question this type of graph is given, these are not 3 graph this is single graph and it is called dis-connected graph
- we hever code we have to write , we have to write for multiple components

![image](https://user-images.githubusercontent.com/35686407/175868067-4838a85f-2153-4e7c-802d-92e72372e264.png)

- take visited array, let below we have 10 nodes, 10 size visited array
- when for loop runs, it seems that 1 is not visited, so it goes to 1 as dfs or bfs and mark all the nodes connected directly or indirectly with 1
- so when you again came back to the for loop, it seems that some of them are not visited as it is dis-connected graph, some componentes left and their mark value is false, so in for loop when checked it when it found to be false, it calls the dfs from that node and apply dfs/bfs

![image](https://user-images.githubusercontent.com/35686407/175868575-a9ca9884-923e-4187-8795-1940efe4fdb2.png)

![image](https://user-images.githubusercontent.com/35686407/175868480-c0070f78-63ac-468a-b417-286d92dd31e1.png)

```cpp
void disconnectedComponentes(int nodes){
    vector<bool> visited(nodes+1,false);
    for(int i = 0; i < nodes+1; i++){
        if(!visited[i]){
            // apply dfs or bfs , dfs(i) / bfs(i);
        }
    }
}
```

## BFS Traversal

- if we start from any given node
- we visit all its neighbour nodes, then take neighbour node, and explore again it adjacent nodes
- Data Structre Used : `Queue` , FIFO operation

![image](https://user-images.githubusercontent.com/35686407/175871283-9a3acf22-a095-4bf4-bd97-6f712c583804.png)

> Important : This is the code snippet we have to write before writing the bfs also, it will handle the dis-connected components.

![image](https://user-images.githubusercontent.com/35686407/175873895-c001fe03-cf8f-4052-bebb-42a2fbd69e96.png)

- Create visited array also, so you dont come to same node again.
![image](https://user-images.githubusercontent.com/35686407/175874803-808e1ed9-2af5-4d4b-8843-3e5a1c547b47.png)

```cpp
void bfs(int node,vector<int>* graph,vector<bool>& visited,vector<int>& ans){

    queue<int> Q;
    Q.push(node);
    visited[node] = true;

    while(!Q.empty()){
        auto node = Q.front();Q.pop();
        ans.push_back(node);
        for(auto& nbr : graph[node]){
            if(visited[nbr] == false){
                Q.push(nbr);
                visited[nbr] = true;
            }
        }
    }

}

/* This code is important to write, maybe there are disconnected components. */
void BFSDriver(vector<int>* graph,int nodes){
    
    vector<bool> visited(nodes,false);
    vector<int> ans;
    for(int i = 0; i < nodes; i++){
        if(visited[i] == false){
            bfs(i,graph,visited,ans);
        }
    }
    print(ans);
}
```
![undefined-1656313382781](https://user-images.githubusercontent.com/35686407/175879303-e1d89a2e-f336-428d-80c1-d08d33f32b65.jpg)

![image](https://user-images.githubusercontent.com/35686407/175879446-f372f361-7c92-448c-ac94-f351fc4d3c17.png)

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

## Mark 2D matrix Row Col Visited in 1D array

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










































