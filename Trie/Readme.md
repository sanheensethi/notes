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
