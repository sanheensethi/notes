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
