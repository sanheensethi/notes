# Stack

## Next Greater Element (Nearest Greater To Right) - Right to Left

```cpp
#define all(x) (x).begin(), (x).end()

vector<int> ngeRight(vector<int>& vec){
	// right to left as when i am at index i then i have to 
	// check i+1 th element first so it should be in top of stack
	stack<int> st;
	int n = vec.size();
	vector<int> ans;
	for(int i = n-1;i>=0;i--){
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
	reverse(all(ans)); // reverse(ans.begin(),ans.end());
	return ans;
}
```
