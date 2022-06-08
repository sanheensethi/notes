# Subsequence

## 1. Remove Palindromic Subsequence [Question](https://leetcode.com/problems/remove-palindromic-subsequences/)

- we have given only 2 characters 'a' and 'b'.
- we also know that we have to remove subsequence
- these 2 hints will help us.
- if string == "" return 0;
- if string is palindrome return 1;
- else return 2; ~ because in this case, first we remove all 'a' then all 'b' as 'a' is itself palindrome and 'b' is itself palindrome.

```cpp
bool isPalindrome(string& s){
        int i = 0;
        int j = s.size()-1;
        while(i <= j){
            if(s[i] != s[j]){
                return false;
            }
            i++;j--;
        }
        return true;
    }
    
    int removePalindromeSub(string s) {
        if(s == "") return 0;
        if(isPalindrome(s)) return 1;
        return 2;
    }
```
