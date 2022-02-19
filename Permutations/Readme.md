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
> Using Recursion (Striver) [More Space Complaxity] (Approach 1) [Using Map]

```cpp
void permutations(vector<int>& arr,vector<int>& vec,umap<int,bool>& umap,vector<vector<int>>& ans){
	if(vec.size() == arr.size()){
		ans.push_back(vec);
		return;
	}
	for(int i=0;i<arr.size();i++){
		if(umap.find(i) == umap.end()){
			// pick that element
			umap[i] = true;
			vec.push_back(arr[i]);
			permutations(arr,vec,umap,ans);
			vec.pop_back();
			// remove that element
			umap[i] = false;
			umap.erase(i);
		}
	}
}
unordered_map<int,bool> umap;
vector<int> vec;
permutations(arr,vec,umap,ans);
```

> Recursion 
