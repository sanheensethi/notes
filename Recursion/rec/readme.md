# Recursion

## 1. Print all Subsequences of Arrray/String

- `Pick and Not Pick algorithm`

![take U forward - L6  Recursion on Subsequences Printing Subsequences  AxNNVECce8c - 853x480 - 4m00s](https://user-images.githubusercontent.com/35686407/173178796-2d717717-ae56-4612-81e5-b6c57c9c6881.png)

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
## 2. Other Patterns

- Print all subsequence whose sum is K
- Print only one subsequence whose sum is K : in this the moment you print one subsequence return true, make it as  boolean type function for recursion
- Count subsequence whose sum is K : return 1 when found else 0 from base case

![take U forward - L7  All Kind of Patterns in Recursion Print All Print one Count  eQCS_v3bw0Q - 885x498 - 24m36s](https://user-images.githubusercontent.com/35686407/173178900-a4e2ebc2-2fa7-46aa-8bc5-094f56930c4c.png)

## 3. Combination Sum I [Question](https://leetcode.com/problems/combination-sum/)

- `Pick and Non Pick algorithm`
- if you pick the element , land on same index
- TC : 2^T * K
- SC : K * x (x is number of subsequence found), Hypothetical , Not exactly sure about the space complexity because we didnt know how many subsequences we found.

![take U forward - L8  Combination Sum Recursion Leetcode C++ Java  OyZFFqQtu98 - 853x480 - 11m50s](https://user-images.githubusercontent.com/35686407/173178949-35e328e1-bf42-4c98-90ed-bd04234694f5.png)

```cpp
void findComb(vector<int>& nums,int i,int target,vector<vector<int>>& ans,vector<int>& ds){
    if(target == 0){
        ans.push_back(ds);
        return;
    }
    if( i >= nums.size()) return;

    if(nums[i] <= target){
        ds.push_back(nums[i]);
        findComb(nums,i,target-nums[i],ans,ds);
        ds.pop_back();
    }

    findComb(nums,i+1,target,ans,ds);

}

vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
    vector<vector<int>> ans;
    vector<int> ds;
    findComb(candidates,0,target,ans,ds);
    return ans;
}
```
