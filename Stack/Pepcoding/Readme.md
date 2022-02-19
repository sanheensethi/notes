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

## Next Greater Element

```cpp
vector<ll> nextGreater(vector<ll>& vec){
	int n = vec.size();
	stack<ll> st;
	vector<ll> ans;
	for(int i=n-1;i>=0;i--){
		if(st.empty()){
			ans.push_back(-1);
			st.push(vec[i]);
		}else if(st.top() > vec[i]){
			ans.push_back(st.top());
			st.push(vec[i]);
		}else if(st.top() <= vec[i]){
			while(!st.empty() && st.top() <= vec[i]){
				st.pop();
			}
			if(st.empty()){
				ans.push_back(-1);
			}else{
				ans.push_back(st.top());
			}
			st.push(vec[i]);
		}
	}
	reverse(all(ans));
	return ans;
}
```
