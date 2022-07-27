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
