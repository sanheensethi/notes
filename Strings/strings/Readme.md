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

```cpp

```
