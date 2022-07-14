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


## 2. Union of Two Sorted Arrays

```cpp
vector<int> findUnion(int arr1[], int arr2[], int n, int m)
{
    int i = 0;
    int j = 0;
    vector<int> ans;
    while(i < n && j < m){
        if(arr1[i] == arr2[j]){
            ans.push_back(arr1[i]);
            i++;
            while(i > 0 && i < n && arr1[i] == arr1[i-1]) i++;
            j++;
            while(j > 0 && j < m && arr2[j] == arr2[j-1]) j++;
        }else if(arr1[i] < arr2[j]){
            ans.push_back(arr1[i]);
            i++;
            while(i > 0 && i < n && arr1[i] == arr1[i-1]) i++;
        }else if(arr1[i] > arr2[j]){
            ans.push_back(arr2[j]);
            j++;
            while(j > 0 && j < m && arr2[j] == arr2[j-1]) j++;
        }
    }
    
    while(i >= 0 && i < n){
        ans.push_back(arr1[i]);
        i++;
        while(i > 0 && i < n && arr1[i] == arr1[i-1]) i++;
    }
    
    while(j >= 0 && j < m){
        ans.push_back(arr2[j]);
        j++;
        while(j > 0 && j < m && arr2[j] == arr2[j-1]) j++;
    }
    
    return ans;
}
```

## 3. Search in a 2D matrix I

```cpp
bool searchMatrix(vector<vector<int>>& matrix, int target) {
    int cols = matrix[0].size();
    int low = 0;
    int high = matrix.size() * cols - 1;
    while(low <= high){
        int mid = low + (high-low)/2;
        int row = mid/cols;
        int col = mid%cols;
        if(matrix[row][col] == target) return true;
        else if(matrix[row][col] < target){
            low = mid+1;
        }else if(matrix[row][col] > target){
            high = mid-1;
        }
    }
    return false;
}
```

## 4. Search in a 2D Matrix II

```cpp
bool searchMatrix(vector<vector<int>>& matrix, int target) {
    int i = 0;
    int j = matrix[0].size()-1;
    int n = matrix.size();
    
    while(i < n && j >= 0){
        int cur = matrix[i][j];
        if(cur == target){
            return true;
        }else if(target < cur){
            j--;
        }else if(target > cur){
            i++;
        }
    }
    return false;
}
```

## 5. Find pivot Index in Array

#### Approach 1 : (Efficient)

- take the prev left sum and current right sum, if they are same at index i, then index i has the pivot element

```cpp
int pivotIndex(vector<int>& nums) {
    int sum = accumulate(nums.begin(),nums.end(),0);
    
    int prev_left = 0;
    int right = sum;
    int i = 0;
    for(auto& val:nums){
        right -= val;
        if(prev_left == right) return i;
        i++;
        prev_left += val;
    }
    return -1;
}
```

#### Approach 2 : 
- Take the left_prefix and right_prefix and the index where both are equal is my ans.

```cpp
int pivotIndex(vector<int>& nums) {
    int n = nums.size();
    vector<int> leftPrefix(n);
    vector<int> rightPrefix(n);
    
    leftPrefix[0] = nums[0];
    for(int i = 1;i < n; i++){
        leftPrefix[i] = leftPrefix[i-1] + nums[i];
    }
    
    rightPrefix[n-1] = nums[n-1];
    for(int i = n-2; i >= 0; i--){
        rightPrefix[i] = rightPrefix[i+1] + nums[i];
    }
    
    for(int i = 0; i < n; i++){
        if(leftPrefix[i] == rightPrefix[i]) return i;
    }
    return -1;
    
}
```

## 6. Find K Closest Elements

- Max Heap Implementation

```cpp
class compare{
    public:
    bool operator()(const pair<int,int>& p1,const pair<int,int>& p2){
        if(p1.first != p2.first){
            return p1.first < p2.first;
        }
        else{
            return p1.second < p2.second;
        }
    }     
};
    

class Solution {
public:
    vector<int> findClosestElements(vector<int>& arr, int k, int x) {
        priority_queue<pair<int,int>,vector<pair<int,int>>,compare> pq;
        
        for(auto& val : arr){
            int distance = abs(val-x);
            pq.push({distance,val});
            if(pq.size() > k) pq.pop();
        }
        
        vector<int> ans;
        while(!pq.empty()){
            ans.push_back(pq.top().second);
            pq.pop();
        }
        sort(ans.begin(),ans.end());
        return ans;
    }
};
```

























