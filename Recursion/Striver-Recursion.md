# Recursion

## 1. Print all Subsequences of Arrray/String

- `Pick and Not Pick algorithm`

```cpp
vector<vector<int>> ans;
void subseq(vector<int>& arr,int idx,vector<int>& ds){
  if(idx >= arr.size()){
    ans.push_back(ds);
    return;
  }
  
  // pick
  
  ds.push_back(arr[i]);
  
  subseq(arr,idx+1,ds);
  
  ds.pop_back();
  
  // not pick
  
  subseq(arr,idx+1,ds);
  
}
```
