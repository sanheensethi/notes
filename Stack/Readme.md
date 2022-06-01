# Stack

## Next Greater Element (Nearest Greater To Right) 
- `Right to Left Push` in stack and Compare
- Question [Link](https://leetcode.com/problems/next-greater-element-i/)

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

## Next Greater Element to Left 

- `Left to Right Push` and compare

> Other Variation : Next Small to Right , Next Small to Left (in this comparison is opposite to upper two questions)

## Next Greater Element II [Link](https://leetcode.com/problems/next-greater-element-ii/)

- Circular Array is Given.
- Last Element is joined with the first Element.
- In this, we process first from index n-2 to 0, but not creating the ans array.
- then it changes the stack which is having some elements or maybe not.
- then do Next Greater element to right
