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
## 8. Remove Outermost Parantheses [Question](https://leetcode.com/problems/remove-outermost-parentheses/)

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

## 9. Score of Parantheses [Question](https://leetcode.com/problems/score-of-parentheses/)

> Open Bracket mile to dalo, closing mile to jb tk open na mile kaam kro

- if '(' push -1
- if ')' and top is '(' i.e. -1 then pop it and push 1
- if ')' and top is not '(' it means that it have childs in it then sum all childes and multiply them by 2 and push it again
- finally empty stack and return ans.

```cpp
class Solution {
public:
    int scoreOfParentheses(string s) {
        stack<int> st;
        for(auto& ch:s){
            if(ch == '('){
                st.push(-1);
            }else if(ch == ')' && st.top() == -1){
                st.pop();
                st.push(1);
            }else if(ch == ')' && st.top() != -1){
                int sum = 0;
                while(!st.empty() && st.top() != -1){
                    sum += st.top();
                    st.pop();
                }
                st.pop();
                st.push(sum*2);
            }
        }
        int ans = 0;
        while(!st.empty()){
            ans += st.top();st.pop();
        }
        return ans;
    }
};
```
## 10. Reverse Substring between each pair of parantheses [Question](https://leetcode.com/problems/reverse-substrings-between-each-pair-of-parentheses/)

- open '(' and other char dalte jao
- jb ')' dekhe pop krke kaam kro
- pop krne pr queue mae dalo kuki reverse krna hai string ko (FIFO)
- vapis stack mae daal do

```cpp
class Solution {
public:
    string reverseParentheses(string s) {
        stack<char> st;
        queue<char> Q;
        for(auto& ch:s){
            if(ch != ')'){
                st.push(ch);
            }else if(ch == ')'){
                while(!st.empty() && st.top() != '('){
                    Q.push(st.top());
                    st.pop();
                }
                st.pop();
                while(!Q.empty()){
                    st.push(Q.front());Q.pop();
                }
            }
        }
        vector<char> v(st.size());
        for(int i = st.size()-1;i >= 0;i--){
            v[i] = st.top();
            st.pop();
        }
        
        string ans(v.begin(),v.end());
        return ans;
    }
};
```
## 10. Minimum remove to make valid parantheses [Question]()

- in stack only '(' indexes is there
- ignore chars
- when '(' came and if stack is empty then we put marker in string as '.' that this parantheses is invalid not part of ans.
- simmilarly when string ends, if stack has '(' indexes it means that they are also invalid , so we have to mark.
- after that we create our ans by skipping the '.'

```cpp
class Solution {
public:
    string minRemoveToMakeValid(string s) {
        int n = s.size();
        stack<int> st;
        for(int i = 0; i < n; i++){
            if(s[i] == '('){
                st.push(i);
            }else if(s[i] == ')'){
                if(st.empty()){
                    s[i] = '.';
                }else{
                    st.pop();
                }
            }
        }
        while(!st.empty()){
            s[st.top()] = '.';
            st.pop();
        }
        string ans = "";
        for(auto& ch:s){
            if(ch == '.') continue;
            ans += ch;
        }
        return ans;
    }
};
```

## 11. Stock Sapn [Question](https://nados.io/question/stock-span?zen=true)

- stock span : esa number jo ye btata hai ki abhi vala number pichle kitne `consecutive numbers` se bda hai,
- ya fr pichle bde number se kitni door hai abhi vala number.

- find next greater element to left
- find the distance between tow (current and bigger)

```cpp
vector<int> solve(vector<int>arr)
{
  vector<int> ans;
  stack<int> st;
  int n = arr.size();
  for(int i = 0 ; i < n ; i++){
      if(st.empty()){
          ans.push_back(i+1);
          st.push(i);
      }else if(arr[st.top()] > arr[i]){
          ans.push_back(i - st.top());
          st.push(i);
      }else if(arr[st.top()] <= arr[i]){
          while(!st.empty() && arr[st.top()] <= arr[i]){
              st.pop();
          }
          if(st.empty()){
              ans.push_back(i+1);
          }else{
              ans.push_back(i - st.top());
          }
          st.push(i);
      }
  }
  return ans;
}
```

## 12. Online Stock Span [Question](https://leetcode.com/problems/online-stock-span/)

- Same as stock span.
- Difference is only, that one by one number is given.
- You have to take indexes by own and find the previous greater element and find difference
- store the both element in stack - {price,index} // index tell which position the number came.

```cpp
class StockSpanner {
public:
    int idx;
    stack<pair<int,int>> st;
    StockSpanner() {
        idx = 0;
    }
    
    int next(int price) {
        if(st.empty()){
            st.push({price,idx});
            idx++;
            return idx;
        }else if(st.top().first > price){
            int ans = idx - st.top().second;
            st.push({price,idx});
            idx++;
            return ans;
        }else if(st.top().first <= price){
            while(!st.empty() && st.top().first <= price){
                st.pop();
            }
            int ans = -1;
            if(st.empty()){
                ans = idx + 1;
            }else{
                ans = idx - st.top().second;
            }
            st.push({price,idx});
            idx++;
            return ans;
        }
        return -1;
    }
};

/**
 * Your StockSpanner object will be instantiated and called as such:
 * StockSpanner* obj = new StockSpanner();
 * int param_1 = obj->next(price);
 */
```

## 13. Exclusive Time of Functions [Question]()

- we will create stack of 3 values, id,starttime,childtime
- interval time of id = endTime - startTime + 1 [it includes id's child interval time also]
- execution time of id = intervalTime - childTime
- when child gets executed, if parent exists then it tell the parent about it's interval

![Photo](https://drive.google.com/uc?export=view&id=1HPW97zN8uPofHHbnHvVuyqEt9qLFquSD)

```cpp
class Solution {
public:
    vector<string> split(string& log,char delimeter){
        vector<string> ans;
        string temp = "";
        for(auto& ch:log){
            if(ch != delimeter){
                temp += ch;
            }else{
                ans.push_back(temp);
                temp = "";
            }
        }
        ans.push_back(temp);
        return ans;
    }
    
    vector<int> exclusiveTime(int n, vector<string>& logs) {
        stack<vector<int>> st;
        vector<int> ans(n,0);
        for(auto& status:logs){
            auto log = split(status,':');
            if(log[1] == "start"){
                int id = stoi(log[0]);
                int startTime = stoi(log[2]);
                int childTime = 0;
                st.push({id,startTime,childTime});
            }else{
                auto startPr = st.top();st.pop();
                int id = stoi(log[0]);
                int endTime = stoi(log[2]);
                int interval = endTime - startPr[1] + 1; // it includes child time also
                int executionTime = interval - startPr[2]; // subtracting child time
                
                ans[id]+=executionTime;
                
                if(st.size()){
                    // if it have parent tell parent about its execution time
                    // for parent it is child
                    (st.top())[2] += interval; // interval because it have its child time also.
                }
            }
        }
        return ans;
    }
};
```
## 14. Asteroid Collision: [Question](https://leetcode.com/problems/asteroid-collision/)

- Collision Happenes only in 1 direction i.e., opposite direction
- val > 0 : push in stack 
- val < 0 : 3 case arises:
	1. st.top() > current value - do not push current value
	2. st.top() == current value - pop the value, also not push current value
	3. st.top() < current value - pop
	4. else st.push current value

![Pepcoding - Asteroid Collision Leetcode 735  Y82zCeJft-Q - 885x498 - 15m31s](https://user-images.githubusercontent.com/35686407/171734873-6641e32c-dfff-44ac-831d-0fd3dbf992fc.png)

```cpp
class Solution {
public:
    vector<int> asteroidCollision(vector<int>& asteroids) {
        stack<int> st;
        for(auto& val:asteroids){
            if(val > 0){
                st.push(val);
            }else if(val < 0){
                int v = abs(val);
                if(!st.empty() && st.top() > v){
                    continue;
                }else{
                    while(!st.empty() && st.top() > 0 && st.top() < v){
                        st.pop();
                    }
                    if(!st.empty() && st.top() == v){
                        st.pop();
                    }else if(!st.empty() && st.top() > v){
                        //pass
                    }else{
                        st.push(val);
                    }
                }
            }
        }
        vector<int> ans;
        while(!st.empty()){
            ans.push_back(st.top());
            st.pop();
        }
        reverse(ans.begin(),ans.end());
        return ans;
    }
};
```

## 15. Remove K Digits [Question](https://leetcode.com/problems/remove-k-digits/)

num : abcd

- if st.top() > current : pop untill k != 0 and st.top() > current
- else push elements [if st.top() <= current]
- if k is left after completing string, then pop elements k times from stack

![Pepcoding - Remove K Digits Leetcode 402  RCE2L0Zk7xE - 1536x864 - 8m38s](https://user-images.githubusercontent.com/35686407/171746873-be968332-1a4c-4246-b3e0-89c54744d8c1.png)

![Pepcoding - Remove K Digits Leetcode 402  RCE2L0Zk7xE - 885x498 - 13m38s](https://user-images.githubusercontent.com/35686407/171747032-7cdf0496-db0d-4579-8d88-1b77befdb347.png)


```cpp
class Solution {
public:
    string removeKdigits(string num, int k) {
        if( k == num.size()) return "0";
        stack<char> st;
        for(auto& ch:num){
            if(st.empty()){
                st.push(ch);
            }else if(st.top() <= ch){
                st.push(ch);
            }else if(st.top() > ch){
                while(!st.empty() && k!=0 && st.top() > ch){
                    st.pop();k--;
                }
                st.push(ch);
            }
        }
        while(!st.empty() && k!=0){
            st.pop();k--;
        }
        
        string ans = "";
        while(!st.empty()){
            ans += st.top();
            st.pop();
        }
        
        reverse(ans.begin(),ans.end());
        
        int i = 0;
        while(ans[i] == '0') i++;
        ans = ans.substr(i);
        if(ans == ""){
            return "0";
        }
        return ans;
        
    }
};
```

## 16. Remove Dublicate Letters [Question](https://leetcode.com/problems/remove-duplicate-letters/)

![Pepcoding - Remove Duplicate Letters Leetcode 316  luCn7p2CIbI - 885x498 - 24m08s](https://user-images.githubusercontent.com/35686407/171791444-b2698373-c419-422d-9ef3-a5a9d7405e37.png)

> In this question, agar hme smaller element mile current jo pichle valo se chota hai, and pichle valo ki agar freq > 0 hai to iska mtlb vo bigger element pichle vale aage bhi exists krte hai, to hum pichle valo ko remove kr denge , aage valo ko ke lenge isse hmara jo string hoga vo dictionary order mae bnega.

- we create freq of chars map and it exists map
- if st.top() < ch :
	push ch to stack
	exists[ch] = true
	freq[ch]--;
- if exists[ch] == true, i.e., char already exists, then freq[ch]--; and continue;
- if st.top() > ch :
	while st is not empty and st.top() > ch and st ke top ki frequency > 0 :
		exists[st.top()] = false
		st.pop();



Solution Writing `Type 1`:

```cpp
class Solution {
public:
    string removeDuplicateLetters(string s) {
        int freq[26] = {0};
        int exists[26] = {false};
        stack<int> st;
        int n = s.size();
        
        for(auto& ch:s){
            int index = ch-'a';
            freq[index]++;
        }
        
	// Two Ways to write this loop
        int idx;
        for(auto& ch:s){
            idx = ch-'a';
            if(exists[idx] == true){
                freq[idx]--;
                continue;
            }else if(st.empty()){
                st.push(ch);
                freq[idx]--;
                exists[idx] = true;
            }else if(st.top() < ch){
                st.push(ch);
                freq[idx]--;
                exists[idx] = true;
            }else if(st.top() > ch){
                // it means it is possible to delete big char if its occurance exists in aage vale string part mae
                while(!st.empty() && st.top() > ch && freq[st.top() - 'a'] > 0){
                    exists[st.top() - 'a'] = false;
                    st.pop();
                }
                st.push(ch);
                freq[idx]--;
                exists[idx] = true;
            }
        }
        string ans = "";
        while(!st.empty()){
            ans += st.top();
            st.pop();
        }
        reverse(ans.begin(),ans.end());
        return ans;
    }
};
```

> Another way to write that loop

```cpp
for(auto& ch:s){
    idx = ch-'a';
    if(exists[idx] == true){
	freq[idx]--;
	continue;   
    }

    while(!st.empty() && st.top() > ch && freq[st.top() - 'a'] > 0){
	exists[st.top() - 'a'] = false;
	st.pop();
    }

    st.push(ch);
    exists[idx] = true;
    freq[idx]--;
}
```
## 17. Trapping Rain Water [Question](https://leetcode.com/problems/trapping-rain-water/)

> Brute Force 

- For each index , we find left max element and right max element
- water at index = min(leftmax,rightmax) - height[current] , leftmax and rightmax can be taken in O(n)
- TC : O(n^2) , we iterate left and right parts of array for each element
- SC : O(1)

> Solution 2 (Optimized) : (Prefix and Suffix)/DP

- In this method, we will find left max and right max already before process and store them in an array
- now water at index = min(leftmax,rightmax) - height[current] , leftmax and rightmasx can be taken in O(1) from created arrays.
- TC : O(n)
- SC : O(n) + O(n) = O(2n) ~ O(n)

> Solution 3 (Further Optimized) : Two Pointers

- Before understanding the intuation, run the algorithm dry run it

![take U forward - Trapping Rainwater Brute Better Optimal with INTUITION  m18Hntz4go8 - 703x395 - 19m54s](https://user-images.githubusercontent.com/35686407/171883941-5586f152-8d7a-4c84-83bf-f4b02328b7e8.png)


`Intuation` :  In Brute : `Water = min(leftMax,rightMax) - a[i];`

- Agar right mae 3 na ho to how I am sure that 1 (index = 4) is storing water which has leftMax 2 ? because if there is no bigger building on right side of 1 (index = 4) , then it didn't store water.
- So, How i am sure that there are building on right hand side which is >= 2, that is 1 (index = 4) stores water.
- So, if you look at the algorithm, vha pr water = leftMax - a[i] or water = rightMax - a[i] le rhe hai, but how i am make sure, leftMax is min in Brute method and rightMax is min in Brute method.
- By algorithm, Jo bhi hum leftMax utha rhe hai, hum make sure kr rhe hai ki vo a(r) ke equal ya usse chota hoga, it means , hum make sure kr rhe hai, right side mae koi na koi to hai jo leftmax se bda hai, 
- `if(a(l) <= a(r)` : this condition tells/make sure, right side mae jo koi na koi to hai jo current leftMax se bda hai,
- `if(leftMax <= a(l)) leftMax = a(l)` : now leftMax update tb hoga jb purana leftMax chota hoga current element se, mtlb ye hai ki abhi vala element bda hai pichle leftMax se, to vo water store nhi krega.
- Same concept is for rightSide, `else if(a(r) < a(l))` : it tells we are making sure that someone is bigger building on left if i am currently at rth index,
That is why leftMax - a[i] and rightMax - a[i] is working.

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int l = 0;
        int r = height.size()-1;
        int leftMax = 0;
        int rightMax = 0;
        int ans = 0;
        while(l <= r){
            if(height[l] <= height[r]){
                // making sure that someone is bigger from the current element i.e. l on right side
                // now check what is the max value in left
                if(height[l] >= leftMax) leftMax = height[l];
                else ans += leftMax - height[l];
                l++;
            }else if(height[r] < height[l]){
                // making sure that someone is bigger from the current element i.e., r on left side
                // now check if right has rightLeft or not
                if(height[r] >= rightMax) rightMax = height[r];
                else ans += rightMax - height[r];
                r--;
            }
        }
        return ans;
    }
};
```

## 18. Number of Valid Subarrays [Question](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/stacks/number-of-valid-subarrays-official/ojquestion)


- find index next smaller element to right
- smaller element index - i is my current number of valid subarrays.
- do this for all and add them.

```cpp
int validSubarrays(vector<int>& arr){
    int ans = 0;
    int n = arr.size();
    stack<int> st;
    for(int i = n-1 ; i >= 0 ; i--){
        if(st.empty()){
            ans += (n-i);
            st.push(i);
        }else if(arr[st.top()] >= arr[i]){
            while(!st.empty() && arr[st.top()] >= arr[i]){
                st.pop();
            }
            if(st.empty()){
                ans += (n-i);
            }else{
                ans += (st.top() - i);
            }
            st.push(i);
        }else if(arr[st.top()] < arr[i]){
            ans += (st.top() - i);
            st.push(i);
        }
    }
    return ans;
}
```
## 19. Sort Stack Using Recursion (Same as Sort Array using Recursion):

- Make Input Small for next recursion call
- To put the element which is popped. another recursion call is happend (insert) to insert the value.

```cpp
void insert(stack<int>& st,int temp){
    if(st.size() == 0 || st.top() <= temp){
        st.push(temp);
        return;
    }
    int val = st.top();
    st.pop();
    insert(st,temp);
    st.push(val);
}

void sortStack(stack<int>& st){
    if(st.size() == 1){
        return;
    }
    int val = st.top();
    st.pop();
    sortStack(st);
    insert(st,val);
}
```

## 20. Delete Middle Element From Stack

```cpp
void deleteMiddleStack(stack<int>& st,int k){
    if(st.size() == k){ // or k == 1 if we pass in rectusion k-1 for next calls
        st.pop();
        return;
    }
    int val = st.top();
    st.pop();
    deleteMiddleStack(st,k);
    st.push(val);
}
```

## 21. Reverse Stack using Recursion (It is done also with another stack)

- SC : O(1) , if we didn't see auxillary stack space of call stack

```cpp
void insert(stack<int>& st,int temp){
    if(st.size() == 0){
        st.push(temp);
        return;
    }
    int val = st.top();
    st.pop();
    insert(st,temp);
    st.push(val);
}

void reverseStack(stack<int>& st){
    if(st.size() == 1) return;
    int val = st.top();
    st.pop();
    reverseStack(st);
    insert(st,val);
}
```
