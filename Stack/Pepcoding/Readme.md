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
## Balanced Brackets

```cpp
void BalanceBrackets(string str){
	stack<char> st;
	for(auto& val:str){
		if(val == '(' || val == '[' || val == '{'){
			st.push(val);
		}else if(val == ')'){
			if(st.empty() || st.top() != '('){
				cout<<"false"<<endl;
				return;
			}else{
				st.pop();
			}
		}else if(val == ']'){
			if(st.empty() || st.top() != '['){
				cout<<"false"<<endl;
				return;
			}else{
				st.pop();
			}
		}else if(val == '}'){
			if(st.empty() || st.top() != '{'){
				cout<<"false"<<endl;
				return;
			}else{
				st.pop();
			}
		}
	}
	if(st.empty()){
		cout<<"true"<<endl;
	}else{
		cout<<"false"<<endl;
	}
}
```
