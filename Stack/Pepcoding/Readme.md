## Dublicate Brackets

```cpp
void DublicateBrackets(){
	string str;
	getline(cin,str);
	//cin.ignore();
	stack<char> st;
	for(auto& ch:str){
		if(ch != ')'){
			st.push(ch);
		}else if(ch == ')'){
			if(st.top() == '('){
				cout<<"true"<<endl;
				return;
			}else{
				while(!st.empty() && st.top() != '('){
					st.pop();
				}
				st.pop();
			}	
		}
	}
	cout<<"false"<<endl;
}
```
