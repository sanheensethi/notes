# Strings

## 1. Check one string is rotation of other string or not [Question](https://www.geeksforgeeks.org/a-program-to-check-if-strings-are-rotations-of-each-other/)

#### Appraoch 1:

- rotate a string by 1 - 1 rotation, moment it matches return true
- else return false
- rotate it to the end of the string
- e.g. ABCD ~ BCDA ~ CDAB ~ DABC ~ ABCD = which is same as starting string. if string is of 4 size, possible rotations = 3

![undefined-1655807742537](https://user-images.githubusercontent.com/35686407/174780536-56e1c023-339b-4a4e-95d6-28c6b824937b.jpg)


#### Approach 2:

- temp = str1 + str1;
- now check the str2 in temp, as it is substring in temp

> Check with Find Function

> Check with strstr Function (KMP Algorithm)

![undefined-1655807719136](https://user-images.githubusercontent.com/35686407/174780556-0a65898c-026e-43d3-bf25-0ce786a24d48.jpg)

```cpp
bool areRotations(string s1,string s2){
    if(s1.size() != s2.size()) return false;
    string temp = s1 + s1;
    return (temp.find(s2) != string::npos);
}
```

#### Approach 3:

- Take Queue,
- put str1 and str2 in queue
- ab k = q2.length
- jb tk k 0 nhi ho jata , tb tk q2 mae se element nikalo piche daal do queue mae,
- isse actually hum rotations hi generate kr rhe hai ek trh se
- q1 q2 ko compare kro, if same then return true
- when k == 0 and same bhi nhi aaye to return false;

![undefined-1655807730726](https://user-images.githubusercontent.com/35686407/174780571-7230ac30-5c40-4aa6-a9dc-6ea3d0075861.jpg)

```cpp
bool areRotations(string s1,string s2){
    if(s1.size() != s2.size()) return false;

    queue<char> q1;
    queue<char> q2;
    for(auto& ch:s1){
        q1.push(ch);
    }
    for(auto& ch:s2){
        q2.push(ch);
    }

    int k = q2.size();
    while(k--){
        auto ch = q2.front();
        q2.pop();
        q2.push(ch);
        if(q1 == q2) return true;
    }
    return false;
}
 ```

## 2. Check if the given string is shuffled substring of another string [Question](https://www.geeksforgeeks.org/check-if-the-given-string-is-shuffled-substring-of-another-string/)

NOTE: As it is substring, so it is obvious that they will be continuous surely.

> Input : str1 = “onetwofour”, str2 = “hellofourtwooneworld” 

> Output: YES 

> Explanation: str1 is substring in shuffled form of str2 as 
str2 = “hello” + “fourtwoone” + “world” 
str2 = “hello” + str1 + “world”, where str1 = “fourtwoone” (shuffled form) 
Hence, str1 is a substring of str2 in shuffled form.

#### Method 1: Sorting

> hum str1 ke size ki str2 mae se substring kaat ke match kr rhe hai hr index se, agar khi pr bhi hme uske sort ke equal mila hum return kr denge true

1. Sort string str1
2. Traverse str2 and take substring of size str1 and sort it
3. compare it, if equal then return true
4. if all ends then return false
5. just like 2 string are anagram if there sort matches with each other

- TC : O(nlogn) + O(m*nlogn) , sorting str1 and for each index we are creating string and sorting them.
- SC : O(m*n) , for each index of bigger string we are making new substring of length n 

```cpp
bool isShuffledSubstring(string& str1, string& str2){

    // we have to check str1 is substring of str2 or not

    sort(str1.begin(),str1.end());

    // str2.size() - str1.size() is because if i reaches at that index
    // from where we are not able to make a substring of size str1.size()
    // therefore we have to loop untill we will make such substrings

    for(int i = 0;i <= str2.size() - str1.size(); i++){
        string str = str2.substr(i,str1.size());
        sort(str.begin(),str.end());
        if(str1 == str) return true;
    }
    return false;
}
```

#### Method 2: Anagram matching using sliding window

1. Make a sliding window of size str1
2. and compare it with str1 as anagram matchig, that all characters should be of same size
3. dhyan dene vali chij hai ki jb >= 0 hai to hi -1 krna hai count ko
4. and jb i ke case mae agar koi 0 se upar jata hai to hi +1 krna hai.

- TC : O(n + m) ~ n for putting str1 in hashmap and O(m) for traversing str2, if in case of map then it takes logn time for access and insert
- SC : O(n)

```cpp
bool isShuffledSubstring(string& str1, string& str2){
    bool found = false;

    unordered_map<char,int> umap;

    for(auto& ch:str1){
        umap[ch]++;
    }

    int count = str1.size();
    int k = str1.size();

    int i = 0,j = 0;
    int n = str2.size();

    while( j < n ){
        char ch = str2[j];
        if(umap.find(ch) != umap.end()){
            
            umap[ch]--;
            if(umap[ch] >= 0){
                count--;
            }
        }
        if(count == 0) return true;

        if(j - i + 1 < k){
            j++;
        }else if(j - i + 1 == k){
            if(count == 0) return true;
            char ich = str2[i];
            if(umap.find(ich) != umap.end()){
                umap[ich]++;
                if(umap[ich] > 0){
                    count++;
                }
            }
            i++;
            j++;
        }
    }

    return false;
}
```
## 3. String is a valid shuffle of two distinct strings

- 1XY2 is a valid shuffle of XY and 12
- Y1X2 is a valid shuffle of XY and 12 
- Y21XX is not a valid shuffle of XY and 12

#### Approach 1: SORTING

- make new string temp = str1 + str2
- sort temp
- sort given string
- if they are equal the it is valid shuffle
- TC : O((n+m)log(n+m)) + O(k) , where n and m are length of str1 and str2 ~ temp = str1 + str1 , and sorting input string of length k O(k)
- SC : O(n+m)

```cpp
bool validShuffle(string str1,string str2,string str3){
    
    string temp = str1 + str2;

    sort(temp.begin(),temp.end());
    sort(str3.begin(),str3.end());

    return temp == str3;
 }
```
 
#### Appraoch 2: SORTING, TWO POINTERS TO COMPARE

- sort given string
- sort str1 and str2
- Compare them with 2 pointers
- TC : O(nlogn) + O(mlogm) + O(klogk)
- SC : O(1)

```cpp
bool validShuffle(string str1,string str2,string str3){
    sort(str1.begin(),str1.end());
    sort(str2.begin(),str2.end());
    sort(str3.begin(),str3.end());

    int i = 0,j = 0;
    int k = 0;
    int n = str1.size();
    int m = str2.size();
    int len = str3.size();

    while(k < len){
        if(i < n && str1[i] == str3[k]) i++;
        else if(j < m && str2[j] == str3[k]) j++;
        else return false;
        k++;
    }

    // if match krta hai to dono ko khtm hona hi pdega simultaneosly
    if( i < n || j < m) return false;

    return true;
 }
```

## 4. Count and Say 

![undefined-1655890184090](https://user-images.githubusercontent.com/35686407/174995460-d9de66e5-7dd8-48f3-b784-96ab6946135a.jpg)

- Just count the occurance of char and push back in string count + char

> Recursion:

- TC :  
- SC :


```cpp
string say(string& str){
    string ans = "";
    int i = 0;
    while(i < str.size()){
        int count = 1;
        while(i+1 < str.size() && str[i] == str[i+1]){
            count++;
            i++;
        }
        ans.push_back(count+'0');
        ans.push_back(str[i]);
        i++;
    }
    return ans;
} 

string countAndSay(int n) {
    if( n == 1) return "1";
    string str = countAndSay(n-1);
    return say(str);
}
```

> Iterative:

```cpp
string countAndSay(int n) {
    string s = "1";

    for(int i = 1; i < n; i++){
        s = say(s);    
    }

    return s;
}
```
## 5. Count Palindromic Substrings

> Recursion

- Store the results of already checked palindrome substrings.
- if it says, palindrome is of length 2 or more then we start j = i+1 not i, because when i = 0, then j = 0, it means only 1 char, but we have asked min of length 2.

```cpp
bool isPalindrome(string& str,int i,int j,vector<vector<int>>& memo){
        
    if( i > j ) return true;

    if(memo[i][j] != -1) return memo[i][j];

    if(str[i] != str[j]){
        return memo[i][j] = false;
    }

    return memo[i][j] = isPalindrome(str,i+1,j-1,memo);
}   

int countSubstrings(string str) {
    int count = 0;
    int n = str.size();
    vector<vector<int>> memo(n,vector<int>(n,-1));
    // generate all substrings
    for(int i = 0; i < str.size(); i++){
        for(int j = i; j < str.size(); j++){
            if(isPalindrome(str,i,j,memo)){
                count++;
            }
        }
    }
    return count;
}
```
## 6. Faulty Keyboard / Long Pressed Name [Question](https://leetcode.com/problems/long-pressed-name/)

- Two Pointer Appraoch, one on name and another on typed string
- if s[i] == s[j] , i++,j++
- if not equal , usse just pichle vala check krenge, agar equal hua to j++ else return false
- ab loop se bhr aane pr niche vale kuch edge testcases hai vo check krne hai.

> EDGE Testcases

![Screenshot Capture - 2022-06-23 - 10-35-25](https://user-images.githubusercontent.com/35686407/175219082-9a683f85-d5f7-4e23-aaa1-7587816e20aa.png)

![Screenshot Capture - 2022-06-23 - 10-36-04](https://user-images.githubusercontent.com/35686407/175219104-f6e97ddf-be4a-455c-8c2d-5045c70ed237.png)

![Screenshot Capture - 2022-06-23 - 10-37-11](https://user-images.githubusercontent.com/35686407/175219135-1a3dfe0f-c6d0-4c0f-8cfb-e95a0e16c0f9.png)

![Screenshot Capture - 2022-06-23 - 10-43-43](https://user-images.githubusercontent.com/35686407/175220323-ba5f9775-fd68-464b-9d61-336b68232608.png)

1. j khtm ho gya and i abhi baki hai
2. i and j starting mae hi equal nhi hai
3. j khtm ni hua and i khtm ho gya, ab hum jko n-1 last char ke sath hi compare krte rhenge, if khi equal nhi aaya to return false else return true
4. name length > type length, to kbhi nhi bna payenge. return false

```cpp
bool isLongPressedName(string name, string typed) {
    int i = 0;
    int j = 0;
    int n = name.size();
    int m = typed.size();

    if(m < n) return false;

    while(i < n && j < m){
        if(name[i] == typed[j]){
            i++;
            j++;
        }else if(i-1>=0 && name[i-1] == typed[j]){
            j++;
        }else{
            return false;
        }
    }

    if(i < n) return false;

    while(j < m){
        if(name[n-1] != typed[j]) return false;
        j++;
    }
    return true;
}
```
## 7. Patition Labels [Question](https://leetcode.com/problems/partition-labels/)

![Screenshot Capture - 2022-06-23 - 22-00-19](https://user-images.githubusercontent.com/35686407/175349117-775d2f69-be38-4db1-9efb-4ce4502e238d.png)

- hr char ka max index store kr lo, 
- and string mae jb dobara traverse krenge to dekhenge ki kiska max aa rha hai, jb maxindex == index ke equal hoga hum ans mae push kr denge length
- length ke liye prev pointer rkha hai ek taki length direct nikal sake

```cpp
vector<int> partitionLabels(string s) {
    unordered_map<char,int> umap;
    for(int i = 0; i < s.size(); i++){
        umap[s[i]] = i;
    }

    vector<int> ans;
    int prev = -1;
    int max_index = 0;

    for(int i = 0; i < s.size(); i++){
        char ch = s[i];

        max_index = max(max_index,umap[ch]);

        if(max_index == i){
            ans.push_back(max_index-prev);
            prev = max_index;
        }
    }
    return ans;
}
```

## 8. Reverse Vowels of a String

> Stack:

- jb vowel mila stack mae dalte jao, and dobara traverse krke jb vowel mila stack ke top se nikalo or daldo.
- TC : O(n) + O(n)
- SC : O(n)

```cpp
string reverseVowels(string s) {
    stack<char> st;
    for(auto& ch:s){
        if(isVowel(ch)) st.push(ch);
    }

    for(int i = 0; i < s.size(); i++){
        if(isVowel(s[i])){
            s[i] = st.top();
            st.pop();
        }
    }
    return s;
}
```

> Two Pointers:

- left and right pointer rkho, jb vowel mile tb ruk jao otherwise bhadao
- vowel milne pr swap krke, dono ko bhada do left++,right--;

TC : O(n)
SC : O(1)

```cpp
bool isVowel(char ch){
    if(ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u' || ch == 'A' || ch == 'E' || ch == 'I' || ch == 'O' || ch == 'U'){
        return true;
    }else{
        return false;
    }
}

string reverseVowels(string s) {
    int left = 0;
    int right = s.size()-1 ;

    while(left < right){
        while(left < s.size() && left < right && !isVowel(s[left])) left++;
        while(right >= 0 && left < right && !isVowel(s[right])) right--;
        swap(s[left],s[right]);
        left++;
        right--;
    }
    return s;
}
```
## 9. Add Two Strings

![Screenshot Capture - 2022-06-23 - 22-35-21](https://user-images.githubusercontent.com/35686407/175355167-81649839-dd9f-421b-a7e6-2e6412c30741.png)

- piche se add krte jao, and carry bhi lete jao.
- chote bche jese krte hai vese kri addition.

```cpp
string addStrings(string num1, string num2) {
        
    string &bigger = num1.size() >= num2.size() ? num1 : num2;
    string& small = num2.size() <= num1.size() ? num2 : num1;

    int i = bigger.size()-1;
    int j = small.size()-1;

    int carry = 0,sum = 0;

    string ans = "";

    while(i >= 0 && j >= 0){
        sum = (bigger[i]-'0') + (small[j]-'0') + carry;
        ans.push_back(((sum%10) + '0'));
        carry = sum/10;
        i--;
        j--;
    }

    while(i >= 0){
        sum = ((bigger[i] - '0') + carry);
        ans.push_back(((sum%10) + '0'));
        carry = sum/10;
        i--;
    }

    reverse(ans.begin(),ans.end());

    string carr = "";
    while(carry!=0){
        carr += (carry%10 + '0');
        carry = carry/10;
    }

    reverse(carr.begin(),carr.end());
    ans = carr + ans;

    return ans;
}
```

## 10. Valid Palindrome II

- atmost ek char ko skip kr skte ho, if koi portion palindrome nhi lga to
- ya to left ka chord skte ho, ya fr right ka portion chord skte ho. 2 options, kisi se bhi true aaya to return true;

![Pepcoding - Valid Palindrome 2 Leetcode 680 Solution in Hindi  nMjhRtYg2_A - 885x498 - 4m46s](https://user-images.githubusercontent.com/35686407/175357858-0980bdc4-0e11-41d9-b2f0-fbb4cd8710a0.png)

> Avoid To Write like below : It Gives `TLE`

![Screenshot Capture - 2022-06-23 - 22-48-48](https://user-images.githubusercontent.com/35686407/175357394-dbcea394-6716-4153-a504-b1cb989fcda4.png)

> Write like this :

```cpp
bool check(string& s,int i,int j){
    while(i < j){
        if(s[i] != s[j]) return false;
        i++;j--;
    }
    return true;
}

bool validPalindrome(string s) {
    int i = 0;
    int j = s.size()-1;
    while(i < j){
        if(s[i] == s[j]){
            i++;
            j--;
        }else{
            return check(s,i+1,j) || check(s,i,j-1);
        }
    }
    return true;
}
```
## 11. Find and Replace [Question](https://leetcode.com/problems/find-and-replace-pattern/)

- Isme hum hr word ki mapping krenge hmare pattern ke sath, if vo shi mapping ho pati hai to match kr rhe hai return true else return false;

- hum pattern ke char ko map kr rhe hai , string ke char se, 1 char pattern ka 1 hi word ke char se map hoga, if already mapped and is baar vhi same char ke corresponding koi alag char aaya to return false;

![Pepcoding - Find And Replace Pattern Leetcode 442 (Medium) Solution in Hindi  4Ze_vLq5tPQ - 884x498 - 10m47s](https://user-images.githubusercontent.com/35686407/175374521-a81c93ec-8771-4d80-a075-863606bf022a.png)

- edge case, isme hum dekh skte hai ki r - a se map hai, if agar m aaya as new pattern string to vo bhi a se map hone ko aayga, but a pehle se map ho chuka hai and we dont want it to be mapped again. so, uske liye hmne alag se map le liya jo ye btayega ki map ho chuka hai ya nhi. word ka char bhi

![Pepcoding - Find And Replace Pattern Leetcode 442 (Medium) Solution in Hindi  4Ze_vLq5tPQ - 852x480 - 18m50s](https://user-images.githubusercontent.com/35686407/175374535-cb55a398-d3a8-4c60-ad88-1aa4384f3522.png)

- in conclusion: hum pattern and word , dono ke uniqueness ko match kr rhe hai.

```cpp
class Solution {
public:
    bool isMatching(string& word,string& pattern){
        unordered_map<char,char> umap;
        unordered_map<char,bool> wchar_map; // word char should also be unique
        
        for(int i = 0; i < word.size(); i++){
            if(umap.find(pattern[i]) != umap.end()){
                // found element in umap
                if(umap[pattern[i]] !=  word[i]){
                    return false;
                }
            }else{
                // not found element insert in map
                if(wchar_map[word[i]] == true) return false;
                umap[pattern[i]] = word[i];
                wchar_map[word[i]] = true;
            }
        }
        return true;
    }
    
    vector<string> findAndReplacePattern(vector<string>& words, string pattern) {
        vector<string> ans;
        for(auto& word:words){
            if(isMatching(word,pattern)){
                ans.push_back(word);
            }
        }
        return ans;
    }
};
```
