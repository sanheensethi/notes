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
## 3. Check if Array Pairs are divisible by K

- isme sb remainder ka khel hai
- 2 numbers are divisible by 10 if their remainder sum = 10
- 2 number are divisible by k , if their remainder sum = k
- 0 and middle element (if k is even) , ye edge cases hai,
- if rem = 0 , then to make pair, even number of remainder 0 elements are required, simmilarly for middle remainder when k is even , example for k = 6, middle = 3 , then remainder = 3 elements should be even.
- Edge Case : When remainder is negative : rem < 0 : rem += k; , make negative remainder to positive remainder

```cpp
class Solution {
public:
    bool canArrange(vector<int>& arr, int k) {
        unordered_map<int,int> umap; // remainder,freq
        
        for(auto& val : arr){
            int rem = val%k;
            if(rem < 0) rem += k;
            umap[rem]++;
        }
        
        bool checkmiddle = true;
        if((k&1)) checkmiddle = false;
        int middle = k/2;
        
        for(int i = 0; i < k; i++){
            if(i == 0){
                if(umap[i]%2 != 0) return false;
            }else if(checkmiddle && i == middle){ // we can also check 2*i == k , to discard 2 checks checkmiddle vagera and i == middle
                if(umap[i]%2 != 0) return false;
            }else{
                if(umap[i] != umap[k-i]) return false;
            }
        }
        return true;
    }
};
```
## 4. Largest Subarray with 0 Sum

```cpp
class Solution{
    public:
    int maxLen(vector<int>&arr, int n)
    {   
        int ans = 0;
        unordered_map<int,int> umap;
        umap[0] = -1;
        int sum = 0;
        for(int i = 0; i < n; i++){
            sum += arr[i];
            if(umap.count(sum)){
                ans = max(ans,i-umap[sum]);
            }else{
                umap[sum] = i;
            } 
        }
        return ans;
    }
};
```

## 4. Largest Subarray with 0 Sum

```cpp
class Solution{
    public:
    int maxLen(vector<int>&arr, int n)
    {   
        int ans = 0;
        unordered_map<int,int> umap;
        umap[0] = -1;
        int sum = 0;
        for(int i = 0; i < n; i++){
            sum += arr[i];
            if(umap.count(sum)){
                ans = max(ans,i-umap[sum]);
            }else{
                umap[sum] = i;
            } 
        }
        return ans;
    }
};
```

## 5. Count 0 Sum Subarrays

```cpp
class Solution{
    public:
    //Function to count subarrays with sum equal to 0.
    ll findSubarray(vector<ll> arr, int n ) {
        ll ans = 0;
        ll sum = 0;
        unordered_map<ll,ll> umap;
        umap[0] = 1;
        for(auto& val : arr){
            sum += val;
            if(umap.count(sum)){
                ans += umap[sum];
            }
            umap[sum]++;
        }
        return ans;
    }
};
```
## 6. Largest Subarray with Contiguous Elements

```cpp
int solution(vector<int> &arr){
    unordered_map<int,bool> umap;
    int n = arr.size();
    int ans = 1;
    for(int i = 0; i < n-1; i++){
        umap.clear();
        int mini = arr[i];
        int maxi = arr[i];
        umap[arr[i]] = true;
        for(int j = i+1; j , n; j++){
            if(umap.count(arr[j])) break;

            umap[arr[j]] = true;
            mini = min(mini,arr[j]);
            maxi = max(maxi,arr[j]);

            if(maxi - mini == j - i){
                ans = max(ans,j-i+1);
            }
            // ans = (maxi - mini == j - i) ? max(ans,j-i+1) : ans;
        }
    }
    return ans;
}
```
## 7. Minimum Window Substring

```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        int i,j;
        i = j = 0;
        int n = s.size();
        if(n < t.size()) return "";
        int start = -1;
        unordered_map<char,int> umap;
        for(auto& ch : t){
            umap[ch]++;
        }
        
        int count = umap.size();
        int len = 1e9;
        while(j < n){
            char chj = s[j];
            if(umap.count(chj)){
                umap[chj]--;
                if(umap[chj] == 0){
                    count--;
                }
            }
            while(count == 0){
                if(j - i + 1 < len){
                    len = j - i + 1;
                    start = i;
                }
                char chi = s[i];
                if(umap.count(chi)){
                    umap[chi]++;
                    if(umap[chi] > 0){
                        count++;
                    }
                }
                i++;
            }
            j++;
        }
        if(start < 0) return "";
        return s.substr(start,len);
    }
};
```
## 8. Longest Distinct Chars in a String

```cpp
int longestSubstrDistinctChars (string str)
{
    unordered_map<char,int> umap;
    int i = 0, j = 0;
    int n = str.size();
    int ans = 0;
    int count = 0;
    while(j < n){
        char chj = str[j];
        umap[chj]++;
        count++;
        while(count > umap.size()){
            char chi = str[i];
            umap[chi]--;
            count--;
            if(umap[chi] == 0) umap.erase(chi);
            i++;
        }
        if(count == umap.size()){
            ans = max(ans,j-i+1);
        }
        j++;
    }
    return ans;
}
```

## 9. Count of Substring Having all Unique Charaters

```cpp
int countSubstring (string &s) {
  int n = s.size();
  int i = 0;
  int j = 0;
  int ans = 0;
  unordered_map<char,int> umap;
  int count = 0;
  while(j < n){
    char chj = s[j];
    umap[chj]++;
    count++;
    while(count > umap.size()){
      char chi = s[i];
      umap[chi]--;
      if(umap[chi] == 0) umap.erase(chi);
      count--;
      i++;
    }
    if(count == umap.size()){
      ans += (j-i+1);
    }
    j++;
  }
  return ans;
}
 
int main(int argc,char** argv){
 string s;
 cin>>s;
 cout<<countSubstring(s)<<endl;
}
```
