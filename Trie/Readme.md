# Trie

## 1. Implementation (Insert/Search/StartsWith)

```cpp
class Node{
private:
    Node* links[26];
    bool flag = false;
public:
    bool containsKey(char ch){
        return links[ch-'a'] != NULL;
    }
    
    void put(char ch,Node* node){
        links[ch-'a'] = node;
    }
    
    Node* get(char ch){
        return links[ch-'a'];
    }
    
    void setEnd(){
        flag = true;
    }
    
    bool isEnd(){
        return flag;
    }
};

class Trie {
private:
    Node* root;   
public:
    Trie() {
        root = new Node();
    }
    
    void insert(string word) {
        Node* node = root;
        int n = word.size();
        for(int i = 0; i < n; i++){
            if(!node->containsKey(word[i])){
                node->put(word[i],new Node());            
            }
            node = node->get(word[i]);
        }
        node->setEnd();
    }
    
    bool search(string word) {
        Node* node = root;
        int n = word.size();
        for(int i = 0; i < n; i++){
            if(!node->containsKey(word[i])){
                return false;
            }
            node = node->get(word[i]);
        }
        return node->isEnd();
    }
    
    bool startsWith(string prefix) {
        Node* node = root;
        int n = prefix.size();
        for(int i = 0; i < n; i++){
            if(!node->containsKey(prefix[i])){
                return false;
            }
            node = node->get(prefix[i]);
        }
        return true;
    }
};
```

## 2. Implementation (INSERT / CountWordsEqualTo / CountWordsStartingWith) :

```cpp
class Node{
private:
    Node* links[26];
    int cntEndsWith = 0;
    int cntPrefix = 0;
public:
    bool containsKey(char ch){
        return links[ch-'a'] != NULL;
    }
    
    Node* get(char ch){
        return links[ch-'a'];
    }
    
    void put(char ch,Node* node){
        links[ch-'a'] = node;
    }
    
    void incEnd(){
        cntEndsWith++;
    }
    
    void incPrefix(){
        cntPrefix++;
    }
    
    void decEnd(){
        cntEndsWith--;
    }
    
    void decPrefix(){
        cntPrefix--;
    }
    
    int getEnd(){
        return cntEndsWith;
    }
    
    int getPrefix(){
        return cntPrefix;
    }
    
};

class Trie{
    private:
        Node* root;
    public:

    Trie(){
        root = new Node();
    }

    void insert(string &word){
        int n = word.size();
        Node* node = root;
        for(int i = 0; i < n; i++){
            char ch = word[i];
            if(!node->containsKey(ch)){
                node->put(ch,new Node());
            }
            node = node->get(ch);
            node->incPrefix();
        }
        node->incEnd();
    }

    int countWordsEqualTo(string &word){
        int n = word.size();
        Node* node = root;
        for(int i = 0; i < n; i++){
            char ch = word[i];
            if(!node->containsKey(ch)){
                return 0;
            }
            node = node->get(ch);
        }
        return node->getEnd();
    }

    int countWordsStartingWith(string &word){
        int n = word.size();
        Node* node = root;
        for(int i = 0; i < n; i++){
            char ch = word[i];
            if(node->containsKey(ch)){
                node = node->get(ch);
            }else{
                return 0;
            }
        }
        return node->getPrefix();
    }

    void erase(string &word){
        int n = word.size();
        Node* node = root;
        for(int i = 0; i < n; i++){
            char ch = word[i];
            if(node->containsKey(ch)){
                node = node->get(ch);
                node->decPrefix();
            }else{
                return;
            }
        }
        node->decEnd();
    }
};
```
## 3. Complete String

```cpp
class Node{
    private:
        Node* links[26];
        bool flag = false;
    public:
        
        bool containsKey(char ch){
            return links[ch-'a'];
        }
    
        void put(char ch,Node* node){
            links[ch-'a'] = node;
        }
    
        Node* get(char ch){
            return links[ch-'a'];
        }
    
        void setEnd(){
            flag = true;
        }
    
        bool isEnd(){
            return flag;
        }
};

class Trie{
    private: Node* root;
    
    public: Trie(){
        root = new Node();
    }
    
    public: void insert(string& word){
        int n = word.size();
        Node* node = root;
        for(int i = 0; i < n; i++){
            if(!node->containsKey(word[i])){
                node->put(word[i],new Node());
            }
            node = node->get(word[i]);
        }
        node->setEnd();
    }
    
    public: bool isPossible(string& word){
        int n = word.size();
        Node* node = root;
        for(int i = 0; i < n; i++){
            if(node->containsKey(word[i])){
                node = node->get(word[i]);
                if(!node->isEnd()) return false;
            }else{
                return false;
            }
        }
        return true;
    }
    
};

string completeString(int n, vector<string> &words){
    Trie trie;
    for(auto& word:words){
        trie.insert(word);
    }
    
    string ans = "";
    for(auto& word:words){
        bool check = trie.isPossible(word);
        if(check && ans.size() < word.size()){
            ans = word;
        }else if(check && ans.size() == word.size() && word < ans){
            ans = word;
        }
    }
    return ans == "" ? "None" : ans;
}
```
## 4. Count Distinct Substring
```cpp
class Node{
    private:
        Node* links[26];
    public:
        bool containsKey(char ch){
            return links[ch-'a'] != NULL;
        }
    
        void put(char ch,Node* node){
            links[ch-'a'] = node;
        }
    
        Node* get(char ch){
            return links[ch-'a'];
        }
};

int countDistinctSubstrings(string &s){
    int n = s.size();
    Node* root = new Node();
    int ans = 0;
    for(int i = 0; i < n; i++){
        Node* node = root;
        for(int j = i; j < n; j++){
            if(!node->containsKey(s[j])){
                node->put(s[j],new Node());
                ans++;
            }
            node = node->get(s[j]);
        }
    }
    return ans+1;
}
```

## 5. PreRequisities for Tries in Bits

- we will store all 32/64 bits
- index start from right
- xor : 
    - even number of 1's : 0
    - odd number of 1's : 1
- Check ith bit is set or not : (num >> i) & 1
- Set/Turn On the ith Bit : (1 << i) | num

## 6. Maxmimum XOR of Two Numbers in 2 Arrays / an Array

```cpp
class Node{
    private: 
        Node* links[2];

    public: 
        bool contains(int bit){
            return links[bit] != NULL;
        }
    
        void put(int bit,Node* node){
            links[bit] = node;
        }
    
        Node* get(int bit){
            return links[bit];
        }
};

class Trie{
  
    private:
        Node* root;
    public:
        Trie(){
            root = new Node();
        }
        
        void insert(int num){
            Node* node = root;
            for(int i = 31 ; i >= 0 ; i--){
                int bit = (num >> i) & 1;
                if(!node->contains(bit)){
                    node->put(bit,new Node());
                }
                node = node->get(bit);
            }
        }
        
        int getMax(int x){
            int maxi = 0;
            Node* node = root;
            
            for(int i = 31; i >= 0; i--){
                int bit = (x >> i) & 1;
                if(node->contains(1-bit)){
                    maxi = maxi | (1 << i);
                    node = node->get(1-bit);
                }else{
                    node = node->get(bit);
                }
            }
            return maxi;
        }
    
};

class Solution {
public:
    
    int findMaximumXOR(vector<int>& nums) {
        Trie trie;
        for(auto& num : nums) trie.insert(num);
        
        int ans = 0;
        for(auto& num : nums) ans = max(ans,trie.getMax(num));
        
        return ans;
    }
};
```
## 7. Max Xor with an element from an array (Queries)

```cpp
class Node{
private:
    Node* links[2];
public:
    bool containsKey(int bit){
        return links[bit] != NULL;
    }    
    
    void put(int bit,Node* node){
        links[bit] = node;
    }
    
    Node* get(int bit){
        return links[bit];
    }
};

class Trie{
private:
    Node* root;
public:
    Trie(){
        root = new Node();
    }
    
    void insert(int num){
        Node* node = root;
        for(int i = 31; i >= 0; i--){
            int bit = (num >> i) & 1;
            if(!node->containsKey(bit)){
                node->put(bit,new Node());
            }
            node = node->get(bit);
        }
    }
    
    int getMax(int x){
        int maxi = 0;
        Node* node = root;
        for(int i = 31; i>= 0; i--){
            int bit = (x >> i) & 1;
            if(node->containsKey(1-bit)){
                maxi = maxi | (1 << i);
                node = node->get(1-bit);
            }else{
                node = node->get(bit);
            }
        }
        return maxi;
    }
};

class Solution {
public:
    vector<int> maximizeXor(vector<int>& nums, vector<vector<int>>& queries) {
        sort(nums.begin(),nums.end());
        vector<vector<int>> offQueries;
        int n = nums.size();
        int qn = queries.size();
        
        for(int i = 0; i < qn; i++){
            int xi = queries[i][0];
            int mi = queries[i][1];
            offQueries.push_back({mi,xi,i});
        }
        
        sort(offQueries.begin(),offQueries.end(),[](const vector<int>& a1,const vector<int>& a2){
            return a1[0] < a2[0];
        });
        
        int idx = 0;
        vector<int> ans(qn);
        int oqn = offQueries.size();
        Trie trie;
        for(int i = 0; i < oqn ; i++){
            int mi = offQueries[i][0];
            int xi = offQueries[i][1];
            int qIdx = offQueries[i][2];
            
            while(idx < n && nums[idx] <= mi){
                trie.insert(nums[idx]);
                idx++;
            }
            
            if(idx == 0) ans[qIdx] = -1;
            else ans[qIdx] = trie.getMax(xi);
        }
        return ans;
    }
};
```
