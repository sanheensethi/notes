# Sliding Window

## 1. Identification

- arr/string given
- asked for subarray/substring
- Largest / Smallest
- k = window size / ya fr K ki value nikalni hogi (variable size sliding window)


## 2. Maximum Sum Subarray of Size K

- pehle window size hit kro i and j se, j ko j++ krke.
- fr maintain rkho window size ko, usme ans milega.

```cpp
class Solution{   
public:
    long maximumSumSubarray(int k, vector<int> &arr , int n){
        long sum = 0;
        int i = 0;
        int j = 0;
        
        long maxi = LONG_MIN;
        while(j < n){
            sum += arr[j];
            if(j - i + 1 < k){
                j++;
            }else{
                maxi = max(sum,maxi);
                // i htao
                sum -= arr[i];
                i++;
                j++;
            }
        }
        return maxi;
    }
};
```

## 3. First Negative Integer in every window of size K

```cpp
typedef long long int ll;
vector<long long> printFirstNegativeInteger(ll arr[],ll n, ll k) {
       vector<ll> ans;
       queue<ll> Q;
       int i = 0;
       int j = 0;
       while(j < n){
           if(arr[j] < 0){
               Q.push(arr[j]);
           }
           
           if(j-i+1 < k){
               j++;
           }else{
               if(!Q.empty()) ans.push_back(Q.front());
               else ans.push_back(0);
               
               if(!Q.empty() && arr[i] == Q.front()){
                   Q.pop();
               }
               i++;
               j++;
           }
       }
       return ans;
 }
```

## 3. Find all Anagrams in a string

```cpp
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        int i = 0, j = 0;
        int n = s.size();
        int k = p.size();
        unordered_map<char,int> umap;
        for(auto& ch:p){
            umap[ch]++;
        }
        
        int count = k;
        vector<int> ans;
        while(j < n){
            char chj = s[j];
            if(umap.count(chj) > 0){
                umap[chj]--;
                if(umap[chj] >= 0) count--;
            }
            
            if(j - i + 1 < k) j++;
            else{
                if(count == 0){
                    ans.push_back(i);
                }
                char chi = s[i];
                if(umap.count(chi) > 0){
                    umap[chi]++;
                    if(umap[chi] > 0) count++;
                }
                i++;
                j++;
                
            }
        }
        return ans;
    }
};
```

## 4. Sliding Window Maximum

- isme deque isliye use kra hai, kuki hum isme piche se remove kr rhe hai,
- if back is samller then current then pop
- aage se isliye nhi kr skte because kuch element reh jayenge jo max nhi bn skte fr bhi queue mae hai.
- take example : [1 3 1 2 0 5] , k = 3
- example 2 : [-7,-8,7,5,7,1,6,0] , k = 4

```cpp
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        int i = 0; int j = 0;
        int n = nums.size();
        deque<int> Q;
        vector<int> ans;
        while(j < n){
            while(!Q.empty() && Q.back() < nums[j]){
                Q.pop_back();
            }
            Q.push_back(nums[j]);
            
            
            if(j-i+1 < k){
                j++;
            }else{
                ans.push_back(Q.front());
                if(Q.front() == nums[i]) Q.pop_front();
                i++;
                j++;
            }
            
        }
        return ans;
    }
```

## Variable Size Sliding Window

## 5. Largest Subarray with sum = k (Note : All array elements are Positive)

- the sliding window approach only work in case of positive numbers

```cpp
int largestSubarrayWithSumK(vector<int>& arr,int n,int k){
    int i = 0;
    int j = 0;
    long sum = 0;
    int maxi = 0;
    while(j < n){
        sum += arr[j];
        if(sum < k){
            j++;
        }else if(sum == k){
            maxi = max(maxi,j-i+1);
            j++;
        }else if(sum > k){
            while(sum > k){
                sum -= arr[i];
                i++;
            }
            if(sum == k){
                maxi = max(maxi,j-i+1);
                j++;
            }
        }
    }
    return maxi;
}
```

## General Format of Variable size Sliding Window

![image](https://user-images.githubusercontent.com/35686407/178472584-bd77e275-b945-4248-b340-f26a69c4a242.png)

## 6. Longest K unique char Substring

```cpp
class Solution{
  public:
    int longestKSubstr(string s, int k) {
        unordered_map<char,int> umap;
        int i = 0;
        int j = 0;
        int n = s.size();
        int maxi = -1;
        while(j < n){
            char chj = s[j];
            umap[chj]++;
            if(umap.size() < k) j++;
            else if(umap.size() == k){
                maxi = max(maxi,j-i+1);
                j++;
            }else if(umap.size() > k){
                while(umap.size() > k){
                    char chi = s[i];
                    umap[chi]--;
                    if(umap[chi] == 0) umap.erase(chi);
                    i++;
                }
                if(umap.size() == k){
                    maxi = max(maxi,j-i+1);
                    j++;
                }
            }
        }
        return maxi;
    }
};
```

## 7. Longest Substring with non Repeating char / Uniuqe chars.

```cpp
int longestSubstringWithoutRepeatingChars(string& str){
    int n = str.size();
    int i = 0;
    int j = 0;
    unordered_map<char,int> umap;
    int maxi = -1;
    while(j < n){
        char chj = str[j];
        umap[chj]++;
       if(umap.size() == j-i+1){
            maxi = max(maxi,j-i+1);
            j++;
        }else if(umap.size() < j-i+1){
            while(umap.size() < j-i+1){
                char chi = str[i];
                umap[chi]--;
                if(umap[chi] == 0){
                    umap.erase(chi);
                }
                i++;
            }
            if(umap.size() == j-i+1){
                maxi = max(maxi,j-i+1);
                j++;
            }
        }
    }
    return maxi;
}
```

## 8. Pick Toys or Fruit Into Baskets

> Same As Longest K unique char substring,

- 2 type ki chije uthani hai , mtlb k = 2,
- row mae uthani hai , and maximum honi chahiye.
- sare 1 type ke bhi utha skta hai, jarori nhi hai 2no hi type ho, AtMAX there are only 2 types.

```cpp
class Solution {
public:
    int totalFruit(vector<int>& fruits) {
        int n = fruits.size();
        int k = 2;
        int i = 0;
        int j = 0;
        unordered_map<int,int> umap;
        int maxi = 0;
        while(j < n){
            int type = fruits[j];
            umap[type]++;
            if(umap.size() <= k){
                maxi = max(maxi,j-i+1);
                j++;
            }else if(umap.size() > k){
                while(umap.size() > k){
                    int typei = fruits[i];
                    umap[typei]--;
                    if(umap[typei] == 0) umap.erase(typei);
                    i++;
                }
                if(umap.size() == k){
                    maxi = max(maxi,j-i+1);
                    j++;
                }
            }
        }
        return maxi;
    }
};
```

## 9. Minimum Window Substring

```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        int n = s.size();
        int i = 0;
        int j = 0;
        unordered_map<char,int> umap;
        for(auto& ch:t){
            umap[ch]++;
        }
        int count = umap.size();
        int start = 0;
        int end = 0;
        int len = 1e9;
        
        while(j < n){
            char chj = s[j];
            if(umap.count(chj)){
                umap[chj]--;
                if(umap[chj] == 0) count--;
            }
            while(count == 0){
                if(j - i + 1 < len){
                    len = j - i + 1;
                    start = i;
                }
                char chi = s[i];
                if(umap.count(chi)){
                    umap[chi]++;
                    if(umap[chi] == 1) count++;
                }
                i++;
            }   
            j++;
        }
        if (len == 1e9) return "";
        return s.substr(start,len);
    }
};
```

















