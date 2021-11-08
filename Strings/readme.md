# Strings

- ### Rearrange characters in a string such that no two adjacent are same [Link](https://www.geeksforgeeks.org/rearrange-characters-string-no-two-adjacent/) 

- ### Round the given number to nearest multiple of 10.  [Link](https://www.geeksforgeeks.org/round-the-given-number-to-nearest-multiple-of-10/)
- `Note :` Not For very Big Numbers, Try Another String Solution.

- ### Find one extra character in a string [Link](https://www.geeksforgeeks.org/find-one-extra-character-string/)
```cpp
void extraChar(){
	string str1,str2;
	getline(cin,str1);
	getline(cin,str2);
	string completeString = str1+str2;
	char diffChar = completeString[0];
	for(int i=1;i<completeString.size();i++){
		diffChar = diffChar ^ completeString[i];
	}
	cout<<diffChar;
}
```

- ### Smallest number with sum of digits as N and divisible by 10^N [Link](https://www.geeksforgeeks.org/smallest-number-sum-digits-n-divisible-10n/)

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

