# HashMaps

## 1. Number of Employees under Every Manager

```cpp
class Solution{
public:

    int generateAns(string root,unordered_map<string,vector<string>>& umap,map<string,int>& ans){
        if(umap.count(root) == 0){
            ans[root] = 0;
            return 1;
        }

        int size = 0;
        for(auto& emp : umap[root]){
            size += generateAns(emp,umap,ans);
        }
        ans[root] = size;
        return size+1;
    }

    vector<pair<string,int>> numberOfEmoloyes(vector<vector<string>>& data,int n){
        unordered_map<string,vector<string>> umap;
        string root = "";
        for(int i = 0; i < n; i++){
            string employee = data[i][0];
            string manager = data[i][1];

            if(employee == manager){
                root = manager;
            }else{
                umap[manager].push_back(employee);
            }
        }

        map<string,int> ans;
        generateAns(root,umap,ans);

        vector<pair<string,int>> rans;
        for(auto& pr : ans){
            rans.push_back(pr);
        }
        return rans;
    }
};
```

## 2. Find Itinerary From Tickets

```cpp
class Solution{
public:

    void dfs(string start,unordered_map<string,vector<string>>& umap,
unordered_map<string,bool>& visited,stack<string>& st){
        visited[start] = true;
        for(auto& dest : umap[start]){
            if(visited[dest]) continue;
            dfs(dest,umap,visited,st);
        }
        st.push(start);
    }
};
int main(){
    int n;cin>> n;
    int k = n;
   string a,b;
   unordered_map<string,vector<string>> umap;
   while(k--){
       cin>>a>>b;
       umap[a].push_back(b);
   }
   stack<string> st;
   Solution obj;
   unordered_map<string,bool> visited;
   for(auto& pr : umap){
        string src = pr.first;
       if(visited[src] == true) continue;
       obj.dfs(src,umap,visited,st);
   }

   vector<string> ans;
   while(!st.empty()){
       ans.push_back(st.top());
       st.pop();
   }

   // reverse(ans.begin(),ans.end());

    string rans = "";
   for(int i = 0; i < ans.size()-1; i++){
       rans += ans[i] + " -> ";
   }
   rans += ans[ans.size()-1] + ".";

    cout<<rans;
   return 0;
}
```
