# Code Snippets

## 1. Split String with Delimeter

```cpp
vector<string> split(string& log,char delimeter){
        vector<string> ans;
        string temp = "";
        for(auto& ch:log){
            if(ch != delimeter){
                temp += ch;
            }else{
                ans.push_back(temp);
                temp = "";
            }
        }
        ans.push_back(temp);
        return ans;
    }
```
