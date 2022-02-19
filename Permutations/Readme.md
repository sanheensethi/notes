## Print all Permutations

> Using Recursion (Pepcoding)

```cpp
void printPermutations(string question,string ans){
	if(question == ""){
		cout<<ans<<endl;
		return;
	}
	for(int i = 0;i<question.size();i++){
		char ch = question[i];
		string left = question.substr(0,i);
		string right = question.substr(i+1);
		string newQues = left + right;
		printPermutations(newQues,ans + ch);
	}
}
```
