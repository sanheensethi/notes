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
