# Stack

## 1. Next Greater Element (Nearest Greater To Right) 
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

## 2. Next Greater Element to Left 

- `Left to Right Push` and compare

> Other Variation : Next Small to Right , Next Small to Left (in this comparison is opposite to upper two questions)

## 3. Next Greater Element II [Link](https://leetcode.com/problems/next-greater-element-ii/)

- Circular Array is Given.
- Last Element is joined with the first Element.
- In this, we process first from index n-2 to 0, but not creating the ans array.
- then it changes the stack which is having some elements or maybe not.
- then do Next Greater element to right
- 2 paas bystack from right to left

```cpp
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        stack<int> st;
        // process from n-2 to 0
        int n = nums.size();
        for(int i = n-2;i>=0;i--){
            if(st.empty()){
                st.push(nums[i]);
            }else if(st.top() > nums[i]){
                st.push(nums[i]);
            }else if(st.top() <= nums[i]){
                while(!st.empty() && st.top() <= nums[i]){
                    st.pop();
                }
                st.push(nums[i]);
            }
        }
        
        // now do next greater element
        vector<int> ans;
        for(int i = n-1;i>=0;i--){
            if(st.empty()){
                ans.push_back(-1);
                st.push(nums[i]);
            }else if(st.top() > nums[i]){
                ans.push_back(st.top());
                st.push(nums[i]);
            }else{
                while(!st.empty() && st.top() <= nums[i]){
                    st.pop();
                }
                if(st.empty()){
                    ans.push_back(-1);
                }else{
                    ans.push_back(st.top());
                }
                st.push(nums[i]);
            }
        }
        reverse(ans.begin(),ans.end());
        return ans;
    }
};
```
## 4. Largest Rectangle in Histogram [Question](https://leetcode.com/problems/largest-rectangle-in-histogram/)

- find next smaller to right
- find next smaller to left
- by smaller right and smaller left we will find the width and then calculate the area.

```cpp
	class Solution {
public:
    vector<int> sr;
    vector<int> sl;
    
    void nextSmallRight(vector<int>& heights){
        int n = heights.size();
        stack<int> st;
        for(int i = n-1; i>=0 ; i--){
            if(st.empty()){
                sr.push_back(n);
                st.push(i);
            }else if(heights[st.top()] >= heights[i]){
                while(!st.empty() && heights[st.top()] >= heights[i]){
                    st.pop();
                }
                if(st.empty()){
                    sr.push_back(n);
                    st.push(i);
                }else{
                    sr.push_back(st.top());
                    st.push(i);
                }
            }else if(heights[st.top()] < heights[i]){
                sr.push_back(st.top());
                st.push(i);
            }
        }
        reverse(sr.begin(),sr.end());
    }
    
    void nextSmallLeft(vector<int>& heights){
        int n = heights.size();
        stack<int> st;
        for(int i = 0; i<n ; i++){
            if(st.empty()){
                sl.push_back(-1);
                st.push(i);
            }else if(heights[st.top()] >= heights[i]){
                while(!st.empty() && heights[st.top()] >= heights[i]){
                    st.pop();
                }
                if(st.empty()){
                    sl.push_back(-1);
                    st.push(i);
                }else{
                    sl.push_back(st.top());
                    st.push(i);
                }
            }else if(heights[st.top()] < heights[i]){
                sl.push_back(st.top());
                st.push(i);
            }
        }
    }
    
    int largestRectangleArea(vector<int>& heights) {
        nextSmallRight(heights);
        nextSmallLeft(heights);
        int ans = INT_MIN;
        int n = heights.size();
        for(int i = 0; i < n; i++){
            ans = max(ans,(heights[i]*(sr[i]-sl[i]-1)));
        }
        return ans;
    }
};
```

## 5. Maximal Rectangle [Question](https://leetcode.com/problems/maximal-rectangle/)

- for each row calculate heights and find Maximum rectangle histogram
- if row[i] == 0 then make heights[i] = 0 chahe pehle us heights ki position pr kuch bhi ho, kuki building hwa mae udegi isliye (Aditya verma)

```cpp
class Solution {
public:
    
    vector<int> sl,sr;
    
    void nextSmallLeft(vector<int>& arr){
        sl.clear();
        int n = arr.size();
        stack<int> st;
        for(int i=0;i<n;i++){
            if(st.empty()){
                sl.push_back(-1);
                st.push(i);
            }else if(arr[st.top()] < arr[i]){
                sl.push_back(st.top());
                st.push(i);
            }else if(arr[st.top()] >= arr[i]){
                while(!st.empty() && arr[st.top()] >= arr[i]){
                    st.pop();
                }
                if(st.empty()){
                    sl.push_back(-1);
                }else{
                    sl.push_back(st.top());
                }
                st.push(i);
            }
        }
    }
    
    void nextSmallRight(vector<int>& arr){
        sr.clear();
        int n = arr.size();
        stack<int> st;
        for(int i=n-1;i>=0;i--){
            if(st.empty()){
                sr.push_back(n);
                st.push(i);
            }else if(arr[st.top()] < arr[i]){
                sr.push_back(st.top());
                st.push(i);
            }else if(arr[st.top()] >= arr[i]){
                while(!st.empty() && arr[st.top()] >= arr[i]){
                    st.pop();
                }
                if(st.empty()){
                    sr.push_back(n);
                }else{
                    sr.push_back(st.top());
                }
                st.push(i);
            }
        }
        reverse(sr.begin(),sr.end());
    }
    
    int MAH(vector<int>& heights){
        nextSmallLeft(heights);
        nextSmallRight(heights);
        
        int ans = INT_MIN;
        int n = heights.size();
        for(int i = 0;i<n;i++){
            ans = max(ans,(heights[i]*(sr[i] - sl[i] - 1)));
        }
        return ans;
    }
    
    int maximalRectangle(vector<vector<char>>& matrix) {
        int n = matrix.size();
        int m = matrix[0].size();
        vector<int> heights(m,0);
        for(int i = 0;i < m ; i++){
            if(matrix[0][i] == '1'){
                heights[i] = 1;
            }
        }
        
        int ans = MAH(heights);
        
        for(int i = 1; i < n ; i++){
            for(int j = 0;j < m ; j++){
                if(matrix[i][j] == '0'){
                    heights[j] = 0;
                }else{
                    heights[j] = heights[j]+1;
                }
            }
            ans = max(ans,MAH(heights));
        }
        
        return ans;
    }
};
```

## 6. Validate Sequqnce [Question](https://leetcode.com/problems/validate-stack-sequences/)

> My Solution, using O(n) space

- create a vector named compare
- fill the compare vector:
	1. pushed[i] != popped[j] && st.top() == popped[j]
	2. pushed[i] == popped[j]
- fill the stack when pushed[i] != popped[j]
- after that empty the remaining stack in compare vector
- compare popped and pushed

```cpp
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        vector<int> compare;
        int i = 0,j = 0;
        stack<int> st;
        while(i < pushed.size()){
            if(pushed[i] != popped[j]){
                if(!st.empty() && st.top() == popped[j]){
                    compare.push_back(st.top());
                    st.pop();
                    j++;
                }else{
                    st.push(pushed[i]);
                    i++;
                }
            }else{
                compare.push_back(pushed[i]);
                j++;
                i++;
            }
        }
        
        while(!st.empty()){
            compare.push_back(st.top());
            st.pop();
        }
        
        for(int i = 0;i<compare.size();i++){
            if(compare[i] != popped[i]){
                return false;
            }
        }
        return true;
        
    }
};
```
> Other Solution: O(1) Space

- push element and if you find stack top == popped[j] then remove the elements from stack and j++;
- we can check rest elements with while loop or another thing is that, we will see patterns
- if all elements are correct then j is going to out of array otherwise not so we can also use
- `return j == popped.size();`

```cpp
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        stack<int> st;
        int j = 0;
        for(auto& val:pushed){
            st.push(val);
            while(!st.empty() && st.top() == popped[j]){
                st.pop();
                j++;
            }
        }
        while(!st.empty()){
             if(st.top() != popped[j]){
                 return false;
             }
             j++;
         }
         return true;
        // return j == popped.size();
    }
};
```
## 7. Minimum add to make valid paranthesis [Question](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/)

> My Solution O(n) TC, O(1) space

- push if (
- pop if ) and not empty , if empty ans += 1
- return ans + st.size(); //maybe some elements left in stack (((
- Idea is to remove valid paranthesis, to count invalid parts

```cpp
class Solution {
public:
    int minAddToMakeValid(string s) {
        int ans = 0;
        stack<char> st;
        for(auto& ch:s){
            if(ch == '('){
                st.push('(');
            }else if(ch == ')'){
                if(!st.empty()){
                    st.pop();
                }else{
                    ans += 1;
                }
            }
        }
        ans += st.size();
        return ans;
    }
};
```
## 8. Remove Outermost Parantheses [Question](

- if '(' then check first, if st empty then it is outermost, not add in ans and if not empty then it is innermost add in ans
- if ')' then first pop , if st empty then it is outermost otherwise it is innermost and add in ans

```cpp
class Solution {
public:
    string removeOuterParentheses(string s) {
        string ans = "";
        stack<char> st;
        for(auto& ch:s){
            if(ch == '('){
                if(!st.empty()){
                    ans += '(';
                }
                st.push('(');
            }else{
                st.pop();
                if(!st.empty()){
                    ans += ')';
                }
            }
        }
        return ans;
    }
};
```
