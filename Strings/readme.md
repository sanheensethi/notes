# Strings

- [ ] Rearrange characters in a string such that no two adjacent are same [Link](https://www.geeksforgeeks.org/rearrange-characters-string-no-two-adjacent/) 

- [x] Round the given number to nearest multiple of 10.  [Link](https://www.geeksforgeeks.org/round-the-given-number-to-nearest-multiple-of-10/)
- `Note :` Not For very Big Numbers, Try Another String Solution.
> Sanheen
```cpp
string nearest10(string str){
	int original = stoi(str);
	cout<<original<<endl;
	int num1 = (original/10)*10;
	int num2 = num1+10;
	int diff1 = original - num1;
	int diff2 = num2 - original;
	return diff1 <= diff2 ? to_string(num1) : to_string(num2);
}
```
> Riya
```cpp
int main(){
    int n; cin>>n;
    int a = (n/10)*10;
    int b = a + 10;
    int ans = (n-a < b-n)?a:b;
    cout<<ans;
}
```
