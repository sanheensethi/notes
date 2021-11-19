# Strings

# Concepts -
1. A string is said to be a `palindrome` if the string `read from left to right` is `equal` to the string `read from right to left`.
2. Reverse of all substrings of `str` will exist in `str` if and only if the entire string `str` is palindrome.We can justify this fact by considering the whole string, a reverse of it will exist only if it is palindrome. And if a string is palindrome, then all reverse of all substrings exist. [Link](https://www.geeksforgeeks.org/perfect-reversible-string/)
	- str = "ab" , all substrings are "a","b","ab" but reverse of "ab" is not present in str.
	- Input : str = "aba" , Output: "YES"

## Basic
### Rearrange characters in a string such that no two adjacent are same [Link](https://www.geeksforgeeks.org/rearrange-characters-string-no-two-adjacent/) 

### Round the given number to nearest multiple of 10.  [Link](https://www.geeksforgeeks.org/round-the-given-number-to-nearest-multiple-of-10/)
- `Note :` Not For very Big Numbers, Try Another String Solution.

### Find one extra character in a string [Link](https://www.geeksforgeeks.org/find-one-extra-character-string/)
```cpp
void extraChar(string str1,string str2){
	string completeString = str1+str2;
	char diffChar = completeString[0];
	for(int i=1;i<completeString.size();i++){
		diffChar = diffChar ^ completeString[i];
	}
	cout<<diffChar;
}
```
### Change string to a new character set [Link](https://www.geeksforgeeks.org/find-one-extra-character-string/)
```cpp
string stringToNewChar(string keyboard,string str){
	char alpha[27];
	for(int i=0;i<keyboard.size();i++){
		char store = i+'a';
		int index = keyboard[i]-'a';
		alpha[index] = store;
	}
	for(int i=0;i<str.size();i++){
		str[i] = alpha[str[i]-'a'];
	}
	return str;
}
```


## Arithmatic Opetraions
### Smallest number with sum of digits as N and divisible by 10^N [Link](https://www.geeksforgeeks.org/smallest-number-sum-digits-n-divisible-10n/)

```cpp
To make a number divisible by 10^N we need at least N zeros at the end of the number. 
To make the number smallest, we append exactly N zeros to the end of the number. 
Now, we need to ensure the sum of the digits is N. For this, 
we will try to make the length of the number as small as possible to get the answer. 
Thus we keep on inserting 9 into the number till the sum doesn’t exceed N. 
If we have any remainder left, 
then we keep it as the first digit (most significant one) 
so that the resulting number is minimized.
```

```cpp
void digitsNum(int N)
{
    // If N = 0 the string will be 0
    if (N == 0)
        cout << "0\n";
     
    // If n is not perfectly divisible
    // by 9 output the remainder
    if (N % 9 != 0)
        cout << (N % 9);
     
    // Print 9 N/9 times
    for (int i = 1; i <= (N / 9); ++i)
        cout << "9";
     
    // Append N zero's to the number so
    // as to make it divisible by 10^N
    for (int i = 1; i <= N; ++i)
        cout << "0";
     
    cout << "\n";
}
```

