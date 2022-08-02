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

## 10. Equivalent Subarrays

```cpp
int solution(vector<int> &arr, int k) {
  int i = 0;
  int j = 0;
  int ans = 0;
  int n = arr.size();
  unordered_map<int,int> umap;
  while( j < n){
    umap[arr[j]]++;
    while(umap.size() == k){
      ans += n-1-j+1;
      umap[arr[i]]--;
      if(umap[arr[i]] == 0) umap.erase(arr[i]);
      i++;
    }
    j++;
  }
  return ans;
}
```

## 11. Maximum Consequtive Ones - I

```cpp
int findMaxConsecutiveOnes(vector<int>& arr) {
    int i = 0;
    int ans = 0;
    int n = arr.size();
    for(int i = 0; i < n; i++){
        int count = 0;
        while(i < n && arr[i] == 1){
            count++;
            i++;
        }
        ans = max(ans,count);
    }
    return ans;
}
```

## 12. Maximum Consequtive Ones - II

```cpp
int solution(vector<int>& arr) {
  int k = 1;
  int i = 0;
  int j = 0;
  int n = arr.size();

  int ans = 0;
  int ones = 0;
  while(j < n){
    if(arr[j] == 1 || k != -1){
      if(arr[j] == 0) k--;
      ones++;
      
    }
    while(k == -1){
      if(arr[i] == 1) ones--;
      if(arr[i] == 0){
        ones--;
        k++;
      }
      i++;
    }
    j++;
    ans = max(ans,ones);
  }
  return ans;
}

int main()
{
  int n;
  cin >> n;
  vector<int>arr(n, 0);
  for (int i = 0; i < n; i++)
  {
    cin >> arr[i];
  };

  cout << solution(arr);
  return 0;
}
```

## 13. Maximim Consequtive Ones - III

```cpp
int solution(vector<int> arr, int k) {
  int i = 0; 
  int j = 0;
  int n = arr.size();
  int ones = 0;
  int ans = 0;
  while(j < n){
    if(arr[j] == 1 || k != -1){
      if(arr[j] == 0){
        k--;
      }
      ones++;
    }

    while(k == -1){
      if(arr[i] == 1) ones--;
      if(arr[i] == 0){
        k++;
        ones--;
      }
      i++;
    }
    ans = max(ans,j-i+1);
    j++;
  }
  return ans;
}

int main()
{
  int n, k;
  cin >> n;
  vector<int>arr(n, 0);
  for (int i = 0; i < n; i++)
  {
    cin >> arr[i];
  };
  cin >> k;
  cout << solution(arr, k);
  return 0;
}
```
## 14. are K Anagrams ?

```cpp
class Solution {
  public:
    bool areKAnagrams(string str1, string str2, int k) {
        if(str1.size() != str2.size()) return false;
        unordered_map<char,int> umap;
        int count = 0;
        for(auto& ch : str1){
            umap[ch]++;
            count++;
        }
        
        for(auto& ch : str2){
            if(umap.count(ch) == 1){
                umap[ch]--;
                count--;
                if(umap[ch] == 0){
                    umap.erase(ch);
                }
            }
        }
        return count <= k;
    }
};
```
## 15. Find Anagram Mappings

```cpp
vector<int> findMapping(int a1[],int a2[],int n){
    unordered_map<int,queue<int>> umap;
    for(int i = 0; i < n; i++){
        umap[a1[i]].push(i);
    }

    vector<int> ans;
    for(int i = 0; i < n; i++){
        auto& q = umap[a2[i]];
        ans.push_back(q.front());
        q.pop();
    }
    return ans;
}
```

## 15. Group Shifted String

```cpp
class solution{
    public:
    string serialize(string& str){
        int n = str.size();
        string code = "";
        for(int i = 1; i < n; i++){
            int k = str[i] - str[i-1];
            if(k < 0) k+= 26;
            code += to_string(k);
            code += '#';
        }
        return code;
    }
    vector<vector<string>> groupStrings(vector<string>& strings) {
        int n = strings.size();
        unordered_map<string,vector<string>> umap;
        for(int i = 0; i < n; i++){
            string key = serialize(strings[i]);
            umap[key].push_back(strings[i]);
        }

        vector<vector<string>> ans;
        for(auto& pr : umap){
            vector<string> vec;
            for(auto& val : pr.second){
                vec.push_back(val);
            }
            ans.push_back(vec);
        }
        return ans;
    }
};
```

## 16. Isomorphic Strings

```cpp
bool isIsomorphic(string s, string t) { 
    if(s.size() != t.size()) return false;

    unordered_map<char,char> umap;
    unordered_map<char,bool> used;

    for(int i = 0; i < s.size(); i++){
            // is already mapped ?
        if(umap.count(s[i])){
            if(umap[s[i]] != t[i]) return false;
        }else{
            if(used.count(t[i]) == 1) return false;
            else{
                umap[s[i]] = t[i];
                used[t[i]] = true;
            }
        }
    }
    return true;
}
```
## 17. Word Pattern

```cpp
bool wordPattern(string pattern, string s) {
    unordered_map<char,string> umap;
    unordered_map<string,bool> used;

    int j = 0;
    int n = s.size();

    for(int i = 0; i < pattern.size(); i++){
        string temp = "";
        while(j < n && s[j] != ' '){
            temp += s[j];
            j++;
        }
        j++;
        if(temp == "") return false;
        // char already mapped
        if(umap.count(pattern[i])){
            if(umap[pattern[i]] != temp) return false;
        }else{
            if(used.count(temp)) return false;
            umap[pattern[i]] = temp;
            used[temp] = true;
        }
    }
    if(j < n) return false;
    return true;
}
```

## 18. Longest Subarray Sum divisible by K

```cpp
int longSubarrWthSumDivByK(int arr[], int n, int k){
    unordered_map<int,int> umap;
    umap[0] = -1;
    int sum = 0;
    int ans = 0;
    for(int i = 0; i < n; i++){
        sum += arr[i];
        int rem = sum%k;
        if(rem < 0) rem += k;
        if(umap.count(rem)){
            ans = max(ans,i-umap[rem]);
        }else{
            umap[rem] = i;
        }
    }
    return ans;
}
```
## 19. Count of Subarrays with sum divisible by K

```cpp
int subarraysDivByK(vector<int>& nums, int k) {
    int sum = 0;
    unordered_map<int,int> umap;
    umap[0] = 1;
    int ans = 0;
    for(int i = 0; i < nums.size(); i++){
        sum += nums[i];
        int rem = sum%k;
        if(rem < 0) rem += k;
        if(umap.count(rem)){
            ans += umap[rem];
        }
        umap[rem]++;
    }
    return ans;
}
```

## 20. Number of Subarrays with equal 0's and 1's

- Trick : isme hum 0 ko -1 maan lenge and sum = 0 vale subarrays find krenge

```cpp
long long int countSubarrWithEqualZeroAndOne(int arr[], int n){
    long long sum = 0;
    long long ans = 0;
    unordered_map<int,int> umap;
    umap[0] = 1;
    for(int i = 0; i < n; i++){
        if(arr[i] == 0){
            sum += (-1);
        }else{
            sum += 1;
        }
        if(umap.count(sum)){
            ans += umap[sum];
        }
        umap[sum]++;
    }
    return ans;
}
```

## 21. Longest Subarray with Equal 0's 1's 2's

- hum find krenge (count 0's - count 1's) and (count 1's - count 2's) if they both are same aage also, then in between them there are equal number of 0's 1's and 2's.
- Key : c1-c0#c2-c1

```cpp
string createKey(int zero,int ones,int two){
    return to_string(zero-ones) + "#" + to_string(ones-two);
}

int solution(vector<int> &v){
   int zeros = 0;
   int ones = 0;
   int two = 0;
    unordered_map<string,int> umap;

    string key = createKey(zeros,ones,two);
    umap[key] = -1;
    int ans = 0;
    int i = 0;
   for(auto& num : v){
       if(num == 0) zeros++;
       else if(num == 1) ones++;
       else two++;
       key = createKey(zeros,ones,two);
        if(umap.count(key)){
            ans = max(ans,i-umap[key]);
        }else{
            umap[key] = i;
        }
        i++;
   }
   return ans;
}
```

## 22. Equal Number of 0's 1's and 2's

![image](https://user-images.githubusercontent.com/35686407/182282709-74f9942a-6f13-4b5b-a7aa-477f945667be.png)

- hum find krenge (count 0's - count 1's) and (count 1's - count 2's) if they both are same aage also, then in between them there are equal number of 0's 1's and 2's.
- Key : c1-c0#c2-c1

```cpp
string createKey(long long zero,long long one,long long two){
    return to_string(one-zero) + "#" + to_string(two-one);
}
long long getSubstringWithEqual012(string str) {
    long long count = 0;
    long long zero = 0;
    long long one = 0;
    long long two = 0;
    unordered_map<string,int> umap;
    string k = createKey(zero,one,two);
    umap[k] = 1;
    string key = to_string(zero) + to_string(one) + to_string(two);
    for(auto& ch : str){
        if(ch == '0'){
            zero++;
        }else if(ch == '1'){
            one++;
        }else if (ch == '2'){
            two++;
        }
        
        string key = createKey(zero,one,two);
        count += umap[key];
        umap[key]++;
    }
    return count;
}
```

## 23. Pairs with Equal Sum

- if there exsts A + B = C + D, the, tjem return true;

```cpp
bool solution(vector<int>& arr, int n) {
  unordered_map<int,int> umap;
  for(int i = 0; i < n; i++){
    for(int j = i+1; j < n; j++){
      int sum = arr[i] + arr[j];
      if(umap.count(sum)){
        return true;
      }
      umap[sum]++;
    }
  }
  return false;
}
```
