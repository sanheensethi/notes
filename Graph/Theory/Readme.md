# Graph

## 1. Introduction

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

## 2. Graph Terminologies 

1. **Path** - A sequence of alternating nodes and edges such that each of the successive nodes are connected by the edge.
2. **Cycle** - A path where the starting and the ending node is the same.
3. **Simple Path** - A path where we do not encounter a vertex again.
4. **Bridge** - An edge whose removal will simply make the graph disconnected.
5. **Forest** - A forest is a graph without cycles.
6. **Tree** - A connected graph that doesn't have any cycles.
7. **Degree** - The degree in a graph is the number of edges that are incident on a particular node.
8. **Neighbour** - We say vertex "A" and "B" are neighbours if there exists an edge between them.

## 3. Degree of Graph

1. Undirected : No. of edges connected to it
2. Directed :
    - In-Degree : No. edges comning towards node.
    - Out-Degree : No. of edges going outwards from node.

## 4. Note : If Weights are not given but weights are necessary in question then assume weights = 1

## 5. Representation of Graph

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

## 6. Connected Components

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

## 7. BFS Traversal

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

## 8. DFS Traversal

> Recursion Method

- Go to depth , depth , depth

![image](https://user-images.githubusercontent.com/35686407/176089570-f178f945-c1c9-4cd5-83f0-c741c35e3d05.png)

- here, when start with 1,
- go to 2 , now it have 3 neighbours , {1,4,7} 
    - 1 is already visited,
    - so, we go to 4, and for 7 we come after we explore 4 first
    - it's recursive in nature
- when at 4, its neighbouts are {2,6}
    - 2 is already visited, so we go to 6
- now when we are at 6, we go to 7

> DFS : 1 2 4 6 7 3 5

#### Important : DFSDriver (For dis-connected Components)

```cpp
void DFSDriver(vector<int>* graph,int nodes){
    
    vector<bool> visited(nodes,false);
    vector<int> ans;
    for(int i = 0; i < nodes; i++){
        if(visited[i] == false){
            dfs(i,graph,visited,ans);
        }
    }
    print(ans);
}
```

![image](https://user-images.githubusercontent.com/35686407/176090298-23b015e6-00f0-4697-8bf1-c7760072a24b.png)

- Another Component
![image](https://user-images.githubusercontent.com/35686407/176090771-663b27a9-4c9d-44af-9b46-1f0d23c306a1.png)

![image](https://user-images.githubusercontent.com/35686407/176090880-544a118e-a13e-4d78-a51a-98dc3724d5ca.png)

> Code

```cpp
void dfs(int node,vector<int> graph[],vector<bool>& visited,vector<int>& ans){
    
    ans.push_back(node);
    visited[node] = true;

    auto& list = graph[node];
    // sort(list.begin(),list.end()); // ~ if want to traverse in lexographical/Increasing order.
    for(int nbr:list){
        if(!visited[nbr]){
            dfs(nbr,graph,visited,ans);
        }
    }
}

void DFSDriver(vector<int> graph[],int nodes){
    vector<int> ans;
    vector<bool> visited(nodes,false);
    for(int i = 0; i < nodes; i++){
        if(visited[i] == false){
            dfs(i,graph,visited,ans);
        }
    }
    print(ans);
}
```

## 9. Cycle Detection in Graph [BFS]

- isme hum queue lenge pair<int,int> such that, first is node and second is node's parent
- why we did this ? , because when node check for its neighbours, tb use uska parent bhi milega, agar visited[nbr] == true hai and vo nbr parent hai to koi dikkat nhi,
- but agar , visited[nbr] == true hai, and vo parent bhi nhi hai, iska mtlb usko kisi or nae visit kia hai and mae bhi visit krne ja rha hu , and vo pehle se visited tha, iska mtlb vha cycle hai.
- niche picture mae, 9, 8 ko queue me daal chuka hai such that {8,9} in queue and 8 visited bhi mark ho chuka hai,
- ab jb 7, 8 ko dalne ki koshish krega to use dekhega ki 8 visited mark hai, to kya vo mera parent hai ? jisse mae aaya hu , nhi mae to ({7,6}) 6 se aaya hu, iska mtlb 8 ko muje dalna chahiye but vo visited hai and mera parent nhi hai, iska mtlb vha cycle hai.
![image](https://user-images.githubusercontent.com/35686407/176100269-bec23310-b552-4419-a0d1-edd1e5d59f86.png)

![image](https://user-images.githubusercontent.com/35686407/176100849-3e6a7a6e-52ec-482b-9182-96cbc1890280.png)
 
```cpp
bool detectCycleBFS(int node,vector<int> graph[],vector<bool>& visited){
    queue<pair<int,int>> Q;
    Q.push({node,-1});
    visited[node] = true;
    
    while(!Q.empty()){
        int size = Q.size();
        while(size--){
            auto& pr = Q.front();
            int node = pr.first;
            int parent = pr.second;
            Q.pop();
            
            auto& nbrs = graph[node]; // list of node's neighbours
            
            for(auto& nbr : nbrs){
                if(visited[nbr] == true && nbr != parent){
                    // cycle detect
                    return true;
                }
                if(!visited[nbr]){
                    Q.push({nbr,node});
                    visited[nbr] = true;
                }
            }
            
        }
    }
    return false;
}

bool bfsDriver(vector<int> graph[],int nodes){
    vector<bool> visited(nodes,false);
    for(int i = 0; i < nodes; i++){
        if(visited[i] == false){
            if(detectCycleBFS(i,graph,visited)){
                return true;
            }
        }
    }
    return false;
}

// Function to detect cycle in an undirected graph.
bool isCycle(int V, vector<int> adj[]) {
    return bfsDriver(adj,V);
}
```

## 10. Detect Cycle in Undirected Graph [DFS]

- isme same concept hai bfs jesa,
- 2 chije paas krenge, node and node ka parent
- jb node apni neighbour list nikalega, usme parent hoga to parent to bound hai visited ke liye, isliye use skip krke next nodes ko dekhega
- aagr next node koi bhi visited aai , to mtlb use koi or kr chuka hai traverse
- iska mtlb us graph mae cycle hai.
- TC : O(n)
- SC : O(n)

![image](https://user-images.githubusercontent.com/35686407/176104322-d5e5d313-39f8-4a2e-9702-afd97e12a713.png)

```cpp
bool detectCycleDFS(int node,int parent,vector<int> graph[],vector<bool>& visited){
        
    visited[node] = true;
    
    auto& nbrs = graph[node];
    
    for(auto& nbr:nbrs){
        if(visited[nbr] == true && nbr != parent){
            return true;
        }
        if(!visited[nbr]){
            if(detectCycleDFS(nbr,node,graph,visited)) return true;
        }
    }
    return false;
}

bool dfsDriver(vector<int> graph[],int nodes){
    vector<bool> visited(nodes,false);
    for(int i = 0; i < nodes; i++){
        if(visited[i] == false){
            int parent = -1;
            if(detectCycleDFS(i,parent,graph,visited)){
                return true;
            }
        }
    }
    return false;
}

// Function to detect cycle in an undirected graph.
bool isCycle(int V, vector<int> adj[]) {
    return dfsDriver(adj,V);
}
```
## 11. Bipartite Graph [BFS]

> Bipartite Graph : Graph that can be colored with `exaclty 2 colors`, such that `no two adjacent nodes have same color` .

> Bipartite Graph

![image](https://user-images.githubusercontent.com/35686407/176113021-e6217e10-aee5-429f-abf1-c96f5880c9ff.png)

> Not a Bipartite Graph
![image](https://user-images.githubusercontent.com/35686407/176113064-793f592a-e11e-4800-aa2d-4530c8a0e5ef.png)

- Observation:
    1. if `cycle length` is `odd` ~ not a bipartite
    2. if `cycle length` is `not odd` ~ bipartite [we will not say it evenlength cycle, because if there is no cycle in the graph, then we can say that also that we can color it with two different colors.]

> Below graph is a bipartite graph:

![image](https://user-images.githubusercontent.com/35686407/176113760-a4546658-0286-4724-bc8e-0066b4573bfe.png)


- hum ek queue lenge and usme hmari stating node dalenge and use color krenge = 0;
- and traverse krenge and check krenge kya mera neigbhour colored hai ? if nhi to color krenge
- Hr node ke paas question hoga puchne ko : 
    - kya mera neighbour colored hai ? :
        1. No , to color kro mere se opposite color se, and queue mae push kro, [color work as visited array]
        - if yes :
            1. kya mere neigbour ka color mere se different hai ?
                - if yes : continue, move aage
                - if no : return false, it is not bipartite graph

```cpp
class Solution {
public:
    
    bool colorAndCheck(int node,vector<int>& color,vector<vector<int>>& graph){
        queue<int> Q;
        Q.push(node);
        color[node] = 0;
        
        while(!Q.empty()){
            int size = Q.size();
            while(size--){
                node = Q.front();Q.pop();
                int clr = color[node];
                
                auto& nbrs = graph[node];
                
                for(auto& nbr : nbrs){
                    if(color[nbr] != -1){
                        // nbr is already colored
                        if(color[nbr] == clr) return false;
                    }else{
                        // nbr is not colored
                        color[nbr] = clr == 0 ? 1 : 0; // also write this ~ !clr;
                        Q.push(nbr);
                    }
                }
                
            }
        }
        return true;
    }
    
    bool bfsDriver(vector<vector<int>>& graph){
        int nodes = graph.size();
        vector<int> color(nodes,-1);
        
        for(int i = 0; i < nodes; i++){
            if(color[i] == -1){
                if(colorAndCheck(i,color,graph) == false){
                    return false;
                }
            }
        }
        return true;
    }
    
    bool isBipartite(vector<vector<int>>& graph) {
        return bfsDriver(graph);
    }
};
```

## 12. Bipartite Check [DFS]

- In this, we do this same as BFS, 
- but before calling DFS we just update the color array first then call the DFS for neighbour.
- every node has Question:
    1. Is neighbour colored ?
        1. No : Color it and call and call dfs to next node
        2. Yes : is it color with different color ? :
            1. Yes : skip/continue
            2. No : return false;

![image](https://user-images.githubusercontent.com/35686407/176116374-3d6fcb7e-13ab-4850-93c5-2abc36b1a952.png)


```cpp
bool colorAndCheck(int node,vector<int>& color,vector<vector<int>>& graph){
    auto& nbrs = graph[node];
    
    for(auto& nbr : nbrs){
        if(color[nbr] == -1){
            // nbr is not colored
            color[nbr] = color[node] == 1 ? 0 : 1;
            if(colorAndCheck(nbr,color,graph) == false) return false;
        }else{
            // nbr is colored
            if(color[nbr] == color[node]) return false;
        }
    }
    return true;
    }
    
    bool dfsDriver(vector<vector<int>>& graph){
    int nodes = graph.size();
    vector<int> color(nodes,-1);
    
    for(int i = 0; i < nodes; i++){
        if(color[i] == -1){
            color[i] = 0;
            if(colorAndCheck(i,color,graph) == false){
                return false;
            }
        }
    }
    return true;
    }
```

#### Why we call dfs after updating color ? why dont we do normal dfs in which when we visit and update the visited array ? [here color is working as same visited array also.]

- we can do that surely, but to do that we have to update the color array for the current node, but for the current node to update the color, we have to know, what is the color of prev node ?, so we have to pass extra parameter that it's prev node color is this this, you have to color the current node with opposite color

```cpp
bool colorAndCheck(int node,int prevColor,vector<int>& color,vector<vector<int>>& graph){
    if(color[node] == -1){
        // not color
        if(prevColor == -1) color[node] = 0;
        else color[node] = prevColor == 0 ? 1 : 0;
    }else{
        if(prevColor == color[node]) return false;
    }
    
    auto& nbrs = graph[node];
    
    for(auto& nbr : nbrs){
        if(color[nbr] != -1){
            // nbr is colored
            if(color[nbr] == color[node]) return false;
        }else{
            // nbr is not colored
            if(colorAndCheck(nbr,color[node],color,graph) == false){
                return false;   
            }                
        }
    }
    return true;
}

bool dfsDriver(vector<vector<int>>& graph){
    int nodes = graph.size();
    vector<int> color(nodes,-1);
    
    for(int i = 0; i < nodes; i++){
        if(color[i] == -1){
            int prevColor = -1;
            if(colorAndCheck(i,prevColor,color,graph) == false){
                return false;
            }
        }
    }
    return true;
}
```
## 13. Cycle Check in Directed Graph [DFS]

--- wrtite here

```cpp
class Solution {
  public:
  
    bool isCycle(int node,vector<int> graph[],vector<bool>& visited,vector<bool>& dfsVisited){
        visited[node] = true;
        dfsVisited[node] = true;
        
        auto& nbrs = graph[node];
        for(auto& nbr : nbrs){
            if(visited[nbr] == false){
                if(isCycle(nbr,graph,visited,dfsVisited)) return true;
            }else if(dfsVisited[nbr] == true){
                return true;
            }
        }
        
        dfsVisited[node] = false;
        return false;
    }
  
    bool dfsDriver(vector<int> graph[],int nodes){
        vector<bool> visited(nodes,false);
        vector<bool> dfsVisited(nodes,false);
        
        for(int i = 0; i < nodes; i++){
            if(visited[i] == false){
                if(isCycle(i,graph,visited,dfsVisited)){
                    return true;
                }
            }
        }
        return false;
    }
  
    // Function to detect cycle in a directed graph.
    bool isCyclic(int V, vector<int> adj[]) {
        // code here
        return dfsDriver(adj,V);
    }
};
```
## 14. Topological Sorting [DFS]

```cpp
class Solution
{
    private:
    
        void dfsTopoSort(int node,vector<int> graph[],vector<bool>& visited,stack<int>& st){
            visited[node] = true;
            auto& nbrs = graph[node];
            for(auto& nbr : nbrs){
                if(!visited[nbr]){
                    dfsTopoSort(nbr,graph,visited,st);
                }
            }
            st.push(node);
        }
    
        void dfsDriver(vector<int> graph[],int nodes,vector<int>& ans){
            vector<bool> visited(nodes,false);
            stack<int> st;
            
            for(int i = 0; i < nodes; i++){
                if(visited[i] == false){
                    dfsTopoSort(i,graph,visited,st);
                }
            }
            
            for(int i = 0; i < nodes; i++){
                ans[i] = st.top();
                st.pop();
            }
            
        }
	public:
	//Function to return list containing vertices in Topological order. 
	vector<int> topoSort(int V, vector<int> adj[]) 
	{
	    vector<int> ans(V);
	    dfsDriver(adj,V,ans);
	    return ans;
	}
};
```
## 15. Topological Sort [BFS]

- indegree concept

```cpp
class Solution
{
    private:
    
    void Indegree(vector<int> graph[],int nodes,vector<int>& indegree){
        for(int i = 0 ; i < nodes; i++){
            for(auto& val:graph[i]){
                indegree[val]++;
            }
        }
    }
    
    void bfs(int nodes,vector<int> graph[],vector<int>& indegree,vector<int>& ans){
        // initialize
        queue<int> Q;
        for(int i = 0; i < nodes; i++){
            if(indegree[i] == 0){
                Q.push(i);
            }
        }
        
        while(!Q.empty()){
            int size = Q.size();
            while(size--){
                int node = Q.front();
                ans.push_back(node); // part of topo sort
                Q.pop();
                
                auto& nbrs = graph[node];
                
                for(auto& nbr : nbrs){
                    indegree[nbr]--;
                    if(indegree[nbr] == 0){
                        Q.push(nbr);
                    }
                }
                
            }
        }
        
    }
    
    void bfsDriver(vector<int> graph[],int nodes,vector<int>& ans){
        vector<int> indegree(nodes,0);
        Indegree(graph,nodes,indegree);
        
        bfs(nodes,graph,indegree,ans);
    }
    
	public:
	//Function to return list containing vertices in Topological order. 
	vector<int> topoSort(int V, vector<int> adj[]) 
	{   
	    vector<int> ans;
	    bfsDriver(adj,V,ans);
	    return ans;
	}
};
```
## 16. Shortest path in Undirected Graph with unit weights.

- TC : O(N+E)
- SC : O(N) + O(N)

![image](https://user-images.githubusercontent.com/35686407/176353332-e18bcaf4-af37-4f83-bff4-6b151c77aa93.png)

```cpp
class Solution {
  public:

    void bfs(int src,vector<int> graph[],int nodes,vector<int>& distance){
        queue<int> Q;
        Q.push(src);
        distance[src] = 0;

        while(!Q.empty()){
            int size = Q.size();
            while(size--){
                
                int node = Q.front();
                int dist = distance[node];
                Q.pop();

                auto& nbrs = graph[node];

                for(auto& nbr : nbrs){
                    if(dist + 1 < distance[nbr]){
                        distance[nbr] = dist+1;
                        Q.push(nbr);
                    }
                }

            }
        }

    }

    void undirectedShortestPath(vector<int> graph[],int nodes,int src){
        vector<int> distance(nodes,INT_MAX);
        bfs(src,graph,nodes,distance);
        print(distance);
    }
};
```

## 17. Shortest path in Direct Ascylic Graph having weights given

![image](https://user-images.githubusercontent.com/35686407/176354415-669d6ebe-3e2b-46fc-9f72-e4dd6ee9a676.png)

> Adj List is of type : vector<pair<int,int>> graph[nodes] , in this, u -> {v,w} , it tells that u is connected to v, with weight w

![image](https://user-images.githubusercontent.com/35686407/176354593-e2992562-415b-4296-a01e-c68c042afd71.png)

Step 1: Find Topological Sort [DFS]


```cpp
class Solution {
  public:

    void dfsTopoSort(int node,vector<pair<int,int>> graph[],vector<bool>& visited,stack<int>& st){
        visited[node] = true;
        vector<pair<int,int>>& nbrs = graph[node];
        for(auto& nbr:nbrs){
            if(!visited[nbr.first]){
                dfsTopoSort(nbr.first,graph,visited,st);
            }
        }
        st.push(node);
    }

    void topoSort(vector<pair<int,int>> graph[],int nodes,stack<int>& st){
        vector<bool> visited(nodes,false);
        for(int i = 0; i < nodes; i++){
            if(!visited[i]){
                dfsTopoSort(i,graph,visited,st);
            }
        }
        int size = st.size();
    }


    void shortestPath(vector<pair<int,int>> graph[],int nodes,int src){
        // Direct Ascylic Graph
        stack<int> st;
        topoSort(graph,nodes,st);

        vector<int> distance(nodes,INT_MAX);
        distance[src] = 0;

        while(!st.empty()){
            int node = st.top();st.pop();

            if(distance[node] != INT_MAX){

                vector<pair<int,int>>& nbrs = graph[node];

                for(auto& nbr : nbrs){

                    int nbrNode = nbr.first;
                    int wt = nbr.second;

                    if(distance[node] + wt < distance[nbrNode]){
                        distance[nbrNode] = distance[node] + wt; 
                    }

                }

            }

        }

        print(distance);

    }

};
```
## 18. Dijkstra Algorithm [Different Weightes in Undirected Graph]

- priority queue min heap
- we can also use set in case of priority queue

![image](https://user-images.githubusercontent.com/35686407/176370327-307faa81-49c4-4f70-bd91-98534da7b6a0.png)

![image](https://user-images.githubusercontent.com/35686407/176370932-f6cbff81-ba87-4a03-8fd3-1ce97d7aae53.png)

```cpp
class Solution
{
	public:
	
	void modifiedBFS(vector<vector<int>> graph[],int nodes,int source,vector<int>& distance){
	    distance[source] = 0;
	    priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>> pq;
	    
	    pq.push({0,source});
	    
	    while(!pq.empty()){
	        auto& pr = pq.top();
	        int node = pr.second;
	        pq.pop();
	        
	        vector<vector<int>>& nbrs = graph[node];
	        
	        for(auto nbr : nbrs){
	            int nbrNode = nbr[0];
	            int wt = nbr[1];
	            
	            if(distance[nbrNode] > distance[node] + wt){
	                distance[nbrNode] = distance[node] + wt;
	                pq.push({distance[nbrNode],nbrNode});
	            }
	            
	        }
	        
	    }
	   
	    
	}
	
	//Function to find the shortest distance of all the vertices
    //from the source vertex S.
    vector <int> dijkstra(int V, vector<vector<int>> adj[], int S)
    {
        vector<int> distance(V,INT_MAX);
        modifiedBFS(adj,V,S,distance);
        return distance;
    }
};
```
## 19. Prim Algorithm [Brute]

> Brute Force

```cpp
void primAlgorithmBrute(vector<pair<int,int>> graph[],int nodes){
    vector<int> key(nodes,INT_MAX);
    vector<int> mst(nodes,false);
    vector<int> parent(nodes,-1);

    int src = 0;
    key[src] = 0;
    parent[src] = -1;

    for(int count = 0; count < nodes-1; count++){

        // find the min key which is not part of mst
        int mini = INT_MAX;
        int node;
        for(int i = 0; i < nodes; i++){
            if(mst[i] == false && key[i] < mini){
                node = i;
                mini = key[i];
            }
        }
        
        // now this is part of mst
        mst[node] = true;

        // traverse the adjacent node
        // skip those nodes who are part of mst
        // update parent and key whose value is greater then new edge weight

        auto& nbrs = graph[node];
        
        for(auto& nbr:nbrs){
            int nbrNode = nbr.first;
            int weight = nbr.second;
            if(mst[nbrNode] == true) continue;
            if(weight < key[nbrNode]){
                key[nbrNode] = weight;
                parent[nbrNode] = node;
            }
        }

    }

    print(parent);

}
```

> Optimized : 

```cpp
void primAlgorithmOptimized(vector<pair<int,int>> graph[],int nodes){
    vector<int> key(nodes,INT_MAX);
    vector<int> mst(nodes,false);
    vector<int> parent(nodes,-1);

    int src = 0;
    key[src] = 0;
    parent[src] = -1;

    // min heap ~ key - min edge,index - node no.
    priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>> pq;

    pq.push({0,0});

    for(int i = 0; i < nodes-1; i++){

        // find the min key which is not part of mst
        int node = pq.top().second;
        pq.pop();

        // now it is part of mst
        mst[node] = true;

        // go to the adj nodes
        // skip nbr nodes which are part of mst 
        // update the parent and key array also push in queue if they satisfies the condition

        auto& nbrs = graph[node];

        for(auto& nbr : nbrs){
            int nbrNode = nbr.first;
            int weight = nbr.second;

            if(key[nbrNode] > weight){
                key[nbrNode] = weight;
                parent[nbrNode] = node;
                pq.push({key[nbrNode],nbrNode});
            }

        }

    }

    print(parent);
}
```
## 20. Union Find

```cpp
class unionFind{
public:

    vector<int> parent;
    vector<int> rank;

    unionFind(int nodes){
        parent.resize(nodes+1);
        rank.resize(nodes+1,0);
        for(int i = 0; i <= nodes; i++) parent[i] = i;
    }
    
    int _findParent(int node);
    void _union(int node1,int node2);
    
};

int unionFind :: _findParent(int node){
    // jb tk parent[node] = node na ho, tb tk node = parent[node];
    // 6 -> 4 -> 2 -> 2
    // while(node != parent[node]){
    //     node = parent[node];
    // }

    // return node;

    if(node == parent[node]) return node;

    return _findParent(parent[node]);
}

void unionFind :: _union(int node1,int node2){
    int parent1 = _findParent(node1);
    int parent2 = _findParent(node2);

    int rank1 = rank[parent1];
    int rank2 = rank[parent2];

    if(rank1 < rank2){
        parent[parent1] = parent2;
    }else if(rank2 < rank1){
        parent[parent2] = parent1;
    }else{
        parent[parent2] = parent1;
        rank[parent1]++;
    }
}
```

## 21. Krushkal Algorithm

1. Sort according to the weight
2. Take the first edge and check if they are belonging to the same component or not
3. Does 1 and 4 belong to the same component, if not take that edge

```cpp
class UnionFind{
private:
    int nodes;
    vector<int> parent;
    vector<int> rank;

public:

    UnionFind(int nodes){
        this->nodes = nodes;
        this->parent.resize(this->nodes);
        for(int i = 0; i < nodes; i++){
            parent[i] = i;
        }
        this->rank.resize(nodes,0);
    }

    int findParent(int node){
        if(node == parent[node]) return node;
        return parent[node] = findParent(parent[node]);
    }

    void unionn(int node1,int node2){
        int parent1 = findParent(node1);
        int parent2 = findParent(node2);

        if(rank[parent1] < rank[parent2]){
            parent[parent1] = parent2; 
        }else if(rank[parent2] < rank[parent1]){
            parent[parent2] = parent1;
        }else{
            parent[parent2] = parent1;
            rank[parent1]++;
        }
    }

    ~UnionFind(){}
};

class Solution{

public:
    static bool compare(vector<int>& a1,vector<int>& a2){
        return a1[0] < a2[0];
    }

private:
    int nodes;
    int edges;
    vector<vector<int>> sortedEdges;
    UnionFind *uf;
    vector<pair<int,int>> mst;

public:
    
    void takeInput(){
        cin>>this->nodes;
        cin>>this->edges;

        for(int i = 0; i < edges; i++){
            int src,dest,wt;
            cin>>src>>dest>>wt;
            sortedEdges.push_back({wt,src,dest});
        }

        sort(sortedEdges.begin(),sortedEdges.end(),compare);

        this->uf = new UnionFind(nodes);

    }

    void krushkalAlgo(){

        int cost = 0;
        for(auto& edge : sortedEdges){
            int weight = edge[0];
            int src = edge[1];
            int dest = edge[2];

            // will i take that edges, are they belong to same component
            if(uf->findParent(src) != uf->findParent(dest)){
                cost += weight; 
                mst.push_back({src,dest});
                uf->unionn(src,dest);
            }

        }

        print(cost);
        print(mst);
        
        delete uf;
        uf = NULL;
    }
};
```
## 22. Bellman's Ford Algorithm

- Find Shortest Distance with negative edges untill there is no negative edge cycle
- If there is negative edge cycle , them bellman's ford detect it, but can't find the distance with negative edge cycle

> Algorithm

1. Relax all nodes N-1 times
2. Realxing means : if dist[u] + weight < dist[v] : dist[v] = dist[u] + weight
3. after relaxing N-1 times, relax it also Nth time , i.e. one time more, if distance gets updated then , there is negatice edge cycle;

```cpp
vector<int> bellmanFord(int n,int m,vector<vector<int>>& edges){
    
    vector<int> distance(n,1e9);
    distance[0] = 0;

    for(int i = 1; i <= n-1; i++){
        for(auto& edge : edges){
            int u = edge[0];
            int v = edge[1];
            int wt = edge[2];
            if(distance[u] + wt < distance[v]){
                distance[v] = distance[u] + wt;
            }
        }
    }

    bool flag = false;
    for(auto& edge : edges){
            int u = edge[0];
            int v = edge[1];
            int wt = edge[2];
            if(distance[u] + wt < distance[v]){
                print("Negative Edge Cycle");
                flag = true;
                break;
                distance[v] = distance[u] + wt;
            }
        }
    
    if(flag) return {}; // there is negative edge cycle
    
    return distance;
}
```
## 23. Kosaraju's Algorithm (Strongly Connected Components)

```cpp
void dfs(int node,vector<vector<int>>& graph,vector<bool>& visited,stack<int>& st){
	visited[node] = true;
	for(auto& nbr : graph[node]){
		if(!visited[nbr]){
			dfs(nbr,graph,visited,st);
		}
	}
	st.push(node);
}

void topoSortDriver(vector<vector<int>>& graph,int N,stack<int>& st,vector<bool>& visited){
	for(int i = 0; i < N; i++){
		if(!visited[i]){
			dfs(i,graph,visited,st);
		}
	}
}

void reverseDFS(int node,vector<vector<int>>& graph,vector<bool>& visited){
	visited[node] = true;
	for(auto& nbr : graph[node]){
		if(!visited[nbr]){
			reverseDFS(nbr,graph,visited);
		}
	}
}

int reverseDFSDriver(vector<vector<int>>& graph,int N,vector<bool>& visited,stack<int>& st){
	int count = 0;

	while(!st.empty()){
		int i = st.top();st.pop();
		if(!visited[i]){
			count++;
			reverseDFS(i,graph,visited);
		}
	}

	return count;
}

int kosaraju(vector<vector<int>> & graph,int N){
   
   stack<int> st;
   vector<bool> visited(N,false);
   topoSortDriver(graph,N,st,visited);
   
   vector<vector<int>> transporse(N);

   for(int i = 0; i < N; i++){
	   visited[i] = false;
	   for(auto& nbr : graph[i]){
		   transporse[nbr].push_back(i);
	   }
   }

	return reverseDFSDriver(transporse,N,visited,st);
}
```
