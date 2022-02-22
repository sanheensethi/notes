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

## Sliding window maximum/maximum element of subarray of size k

- We will find the nextGreaterElement Index for each element then with help of this we will run the algo.
- If next greater element of element exists in same window we jump j to that element index, and repeat it untill we find the next greater element index out of the window.
- if we find index of next greater element of the current, which is out of window of size k, then the current element is the bigger element of current window.

```cpp
vector<int> maxKsubarray(vector<int>& arr,int k){
	vector<int> nge = nextGreaterElementIndex(arr); // vector of index of next greater element
	int i = 0;
	int n = arr.size();
	int j = i;
	vector<int> ans;
	while(i <= n-k){
		if(j < i){
			j = i;
		}
		while(nge[j] < i+k){
			j = nge[j];
		}
		ans.push_back(arr[j]);
		i++;
	}

	return ans;
}
```
