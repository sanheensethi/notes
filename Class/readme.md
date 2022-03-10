## Lab Manual 1 Solution:

> Riya
```cpp
  void bfs(vector<vector<int>> &graph,int start,int end){
	queue<int> q;
	vector<int> visited(graph.size(),0);
	q.push(start);
	cout<<start<<" ";
	while(q.size()){
		int curr = q.front(); q.pop();
		visited[curr] = 1;
		for(auto &it:graph[curr]){
			if(it == end){
				return;
			}else if(it != end && visited[it] == 0){
				cout<<it<<" ";
				q.push(it);
			}
		}
	}
}

int main(){
    int n; cin>>n;
    vector<vector<int>> graph(n);
    while(n--){
    	int node; cin>>node;
    	int connect; cin>>c
    	while(connect--){
    		int connNodes; cin>>connNodes;
    		graph[node].push_back(connNodes);
    	}
    }
    int start,end; cin>>start>>end;
    bfs(graph,start,end);
    return 0;
}
```

> Sanheen
```cpp
  void bfs(vector<vector<int>>& graph,int start,int end){
  queue<int> Q;
  vector<bool> visited(graph.size(),false);
  Q.push(start);
  while(!Q.empty()){
    auto curr = Q.front();Q.pop();
    
    if(curr == end){
      return;
    }else if(!visited[curr]){
      cout<<curr<<" ";
      visited[curr]=true;
      for(auto& child:graph[curr]){
        Q.push(child);
      }
    }
  }
}

void solve(){
	int n;cin>>n;
  vector<vector<int>> vec(n,vector<int>());
  for(int i=0;i<n;i++){
    int connected;cin>>connected;
    while(connected--){
      int x;cin>>x;
      vec[i].pb(x);
    }
  }
  for(auto& v:vec){
    debug(v);
  }

  int start,goal;
  cin>>start>>goal;

  bfs(vec,start,goal);

}
```
