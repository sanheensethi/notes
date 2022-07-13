# Sorting

## Comparator Function
- jesa chahiye vo return kr do bs
- suppose, ascending to a < b
- decending then a > b
- ye logic hr data type mae kaam krega ,
- a.first < b.first => sort acc to the first element of pair

## 1. Minimum moves to make equal array elements.

- isme agar dekhe to sort krne ke baad, if hum center element bnaye to minimum moves lg rhe hai
- kyuki, ek vhi esa element hai, jo sbse chote element ko and sbse bde element ko paas pdega.

```cpp
int minMoves2(vector<int>& nums) {
    int size = nums.size();
    sort(nums.begin(),nums.end());

    int ele = nums[size/2];

    int ans = 0;
    for(auto& val:nums){
        ans += abs(val-ele);
    }
    return ans;
}
```

## 1. Marks of PCM

```cpp
class Solution{
    public:
    void customSort (int phy[], int chem[], int math[], int N)
    {
        vector<vector<int>> vec(N);
        for(int i = 0; i < N; i++){
            vec[i] = {phy[i],chem[i],math[i]};
        }
        
        sort(vec.begin(),vec.end(),[](const vector<int>& v1,const vector<int>& v2){
            if(v1[0] != v2[0]){
                return v1[0] < v2[0];
            }else{
                if(v1[1] != v2[1]){
                    return v1[1] > v2[1];
                }else{
                    return v1[2] < v2[2];
                }
            }
        });
        
        for(int i = 0; i < N; i++){
            phy[i] = vec[i][0];
            chem[i] = vec[i][1];
            math[i] = vec[i][2];
        }
        
    } 
};
```


