# Recursion

## 1. Print all Subsequences of Arrray/String

- `Pick and Not Pick algorithm`

![take U forward - L6  Recursion on Subsequences Printing Subsequences  AxNNVECce8c - 853x480 - 4m00s](https://user-images.githubusercontent.com/35686407/173178796-2d717717-ae56-4612-81e5-b6c57c9c6881.png)

```cpp
vector<vector<int>> ans;
void subseq(vector<int>& arr,int idx,vector<int>& ds){
  if(idx >= arr.size()){
    ans.push_back(ds);
    return;
  }
  
  // pick
  
  ds.push_back(arr[i]);
  
  subseq(arr,idx+1,ds);
  
  ds.pop_back();
  
  // not pick
  
  subseq(arr,idx+1,ds);
  
}
```
## 2. Other Patterns

- Print all subsequence whose sum is K
- Print only one subsequence whose sum is K : in this the moment you print one subsequence return true, make it as  boolean type function for recursion
- Count subsequence whose sum is K : return 1 when found else 0 from base case

![take U forward - L7  All Kind of Patterns in Recursion Print All Print one Count  eQCS_v3bw0Q - 885x498 - 24m36s](https://user-images.githubusercontent.com/35686407/173178900-a4e2ebc2-2fa7-46aa-8bc5-094f56930c4c.png)

## 3. Combination Sum I [Question](https://leetcode.com/problems/combination-sum/)

- `Pick and Non Pick algorithm`
- if you pick the element , land on same index
- TC : 2^T * K
- SC : K * x (x is number of subsequence found), Hypothetical , Not exactly sure about the space complexity because we didnt know how many subsequences we found.

![take U forward - L8  Combination Sum Recursion Leetcode C++ Java  OyZFFqQtu98 - 853x480 - 11m50s](https://user-images.githubusercontent.com/35686407/173178949-35e328e1-bf42-4c98-90ed-bd04234694f5.png)

![take U forward - L8  Combination Sum Recursion Leetcode C++ Java  OyZFFqQtu98 - 885x498 - 20m16s](https://user-images.githubusercontent.com/35686407/173179043-4f482fa2-7096-4358-9014-5b02da8bb303.png)


```cpp
void findComb(vector<int>& nums,int i,int target,vector<vector<int>>& ans,vector<int>& ds){
    if(target == 0){
        ans.push_back(ds);
        return;
    }
    if( i >= nums.size()) return;

    if(nums[i] <= target){
        ds.push_back(nums[i]);
        findComb(nums,i,target-nums[i],ans,ds);
        ds.pop_back();
    }

    findComb(nums,i+1,target,ans,ds);

}

vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
    vector<vector<int>> ans;
    vector<int> ds;
    findComb(candidates,0,target,ans,ds);
    return ans;
}
```
## 4. Combination Sum II [Question](https://leetcode.com/problems/combination-sum-ii/)

#### Approach 1: Brute Force:

- `pick and non pick algo`
- put ans in SET, then while returning copy elements from SET to VECTOR and return ans vector;
- TC : 2^n * k * log(something) - something is size of set
- `GIVES TLE`
![take U forward - L9  Combination Sum II Leetcode Recursion Java C++  G1fRTGRxXU8 - 885x498 - 4m29s](https://user-images.githubusercontent.com/35686407/173179767-b4bdfc1d-d3ea-4309-b08e-d290118eaa00.png)

#### Approach 2: Optimized

- Same algo of pick and not pick but in different manner
- first sort the array
- then pass it to function
- ab jb hum 1 utha rhe hai 1st position ke liye, agar aage bhi 1 aata hai to use nhi uthayenge 1st position ke liye kuki 1 vala kaam apna krke aa chuka hai already then why we take again 1 which will do the same work and produce dublicates dont call recursion on that
- simmilarly agar 1 bari 2 utha lia hai `a level` to again 2 nhi uthayenge `on same level`.
- but inko agle level mae utha skte hai, kuki ab position changee hogyi na bethane ki
- position kehne ka mtlb ye hia ki agar hum ds 1 store kr rhe hai 0 index vala jb vo kaam kr aayega to pop back ho jayega and ds khali ho jayega us level pr vapis aakr kaam krke, then aage 1 aaya ds khali hoga to agar 1 bhr denge usme 1st index vala to vo 0 index vala same kaam krke aayega, jo ki glt hai , isliye skip kr rhe hai.

![take U forward - L9  Combination Sum II Leetcode Recursion Java C++  G1fRTGRxXU8 - 853x480 - 9m55s](https://user-images.githubusercontent.com/35686407/173179900-fc8984e0-347d-4b68-a519-f3c64bdadfdc.png)

![take U forward - L9  Combination Sum II Leetcode Recursion Java C++  G1fRTGRxXU8 - 853x480 - 15m45s](https://user-images.githubusercontent.com/35686407/173179976-896b2c4a-59d8-44cb-990e-3e5c00dcb9fb.png)

- agar koi bhi element bda mila, hum usi time break kr denge kyuki, agar abhi vala element bda hai to aage vale sare bhi to bde honge target se, as array is sorted.
- so this is the optimized way to handle dublicates.

> Did not pick Dublicates

```cpp
void comb(vector<int>& arr,int idx,int target,vector<int> ds,vector<vector<int>>& ans){
        
    if(target == 0){
        ans.push_back(ds);
        return;
    }

    for(int i = idx ; i < arr.size() ; i++){
    // agar mera element, idx vala nhi hai usse jada hai, and vo pichle vale se same hai to mt uthao 
        if( i > idx && arr[i] == arr[i-1]) continue; 
        if(arr[i] > target) break;
        ds.push_back(arr[i]);
        comb(arr,i+1,target-arr[i],ds,ans);
        ds.pop_back();
    }

}

vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
    vector<vector<int>> ans;
    vector<int> ds;
    sort(candidates.begin(),candidates.end());
    comb(candidates,0,target,ds,ans);
    return ans;
}
```

## 5. Subset Sum I [Question](https://practice.geeksforgeeks.org/problems/subset-sums2234/1)

- `pick and non pick algorithm`
- if pick add in sum and call aage lgao
- if not puck sum ko function parameter vala hi rkho and call aage lgao
- initial sum = 0
- TC : 2^n + 2^n log(2^n) , 2^n for recursion and other for sorting 2^n elements
- SC : O(2^n) ~ to store the ans, O(n) ~ recursion call stack

![take U forward - L10  Subset Sum I Recursion C++ Java  rYkfBRtMJr8 - 885x498 - 11m50s](https://user-images.githubusercontent.com/35686407/173180306-8f4ab0f6-2ced-4e06-91f5-1e03d026878d.png)


```cpp
void generate(vector<int>& arr,int i,int sum,vector<int>& ans){
    if(i >= arr.size()){
        ans.push_back(sum);
        return;
    }

    // pick
    generate(arr,i+1,sum+arr[i],ans);
    // not pick
    generate(arr,i+1,sum,ans);

}

vector<int> subsetSums(vector<int>& arr, int N){
    vector<int> ans;
    int sum = 0;
    generate(arr,0,sum,ans);
    sort(ans.begin(),ans.end());
    return ans;
}
```
## 6. Subset Sum 2 [Question](https://leetcode.com/problems/subsets-ii/)

#### Approach 1: Brute force

- sort the array
- create a set and put created subsets in set for uniqueness
- after all calls done, copy the set elements in array as ans
- return ans
- Not Optimal, we generate all

#### Approach 2: Optimized

- Same Logic as of combination sum, just we need to generate unique subsets
- so , in subset we have extra {} - empty set, from subsequence
- so ultimately we are generating subsequence with one exta {} , empty set
- In this we use same approach to skip the elements that are same `on same level` of recursion tree.
- jese hi ek element push krte hai, mae ans mae push kr deta hu, ye kehkr ki haan 1/2/3/... size vala subset bn gya hai, push krne ke baad ans mae,
- mae call lga deta hu.
- TC : O(2^n) * O(n) , 2^n if every element is distinct then 2^n calls and O(n) is the stack space
- SC : O(2^n) x O(k) , 2^n is number of subsets, and k is average length of each subset.

> Did not pick dublicates

![take U forward - L11  Subset Sum II Leetcode Recursion  RIn3gOkbhQE - 885x498 - 17m39s](https://user-images.githubusercontent.com/35686407/173181064-91feed81-7fbd-4353-94a8-270f25aa68f0.png)


```cpp
void subset(vector<int>& arr,int idx,vector<int>& ds,vector<vector<int>>& ans){
        
  for(int i = idx ; i < arr.size(); i++){
      if(i > idx && arr[i] == arr[i-1]) continue;
      
      ds.push_back(arr[i]);

      ans.push_back(ds);

      subset(arr,i+1,ds,ans);

      ds.pop_back();
  }

}

vector<vector<int>> subsetsWithDup(vector<int>& nums) {
  vector<vector<int>> ans;
  vector<int> ds;
  ans.push_back({});
  sort(nums.begin(),nums.end());
  subset(nums,0,ds,ans);
}
```
### There are 2 variations only of this - pick - non pick and for loop vali ki agar dublicates hia to same level pr mt uthao

## 7. Print all Permutations [Important]

#### Approach 1: Extra Space - Map

- isme hum , ek khali map rkhenge and khali ds starting mae
- jb hum pehle level pr hai, to hum dekhenge ki 1st position pr konse konse element aa skte hai to jo mark nhi hai map mae vo aa skte hai, ek ek krke 3no ko 1st position pr layenge , pehle ek rkhkr aage call lgayenge 1 ka kaam pura krenge
- fr jb 2nd level pr hai, to vha dekh rhe hia 2nd position pr kon ko  aa skta hai:
    - if in 1st level map marked as 1 : then 2nd postion : 2 3
    - if in 1st level map marked as 2 : then 2nd position : 1 3
    - if in 1st level map marked as 3 : then 2nd position : 1 2
- 2nd postion told by 2nd recursion call.
- `by this hum hr element ko hr index pr betha rhe hai.`

![take U forward - L12  Print all Permutations of a StringArray Recursion Approach - 1  YK78FU5Ffjw - 885x498 - 4m17s](https://user-images.githubusercontent.com/35686407/173182049-b46195fc-5c7d-40e9-a087-7b5a258e664a.png)

![take U forward - L12  Print all Permutations of a StringArray Recursion Approach - 1  YK78FU5Ffjw - 853x480 - 8m22s](https://user-images.githubusercontent.com/35686407/173182056-93459ff1-c30f-405b-8e4f-881e30e269b7.png)

![take U forward - L12  Print all Permutations of a StringArray Recursion Approach - 1  YK78FU5Ffjw - 885x498 - 13m38s](https://user-images.githubusercontent.com/35686407/173182110-2514ffb5-a3ae-4bdf-a21c-616b1517edb1.png)

```cpp
vector<vector<int>> ans;
void generate(vector<int>& arr,vector<int>& ds,unordered_map<int,bool>& umap){
    if(arr.size() == ds.size()){
        ans.push_back(ds);
        return;
    }

    for(int i = 0;i < arr.size(); i++){
        if(umap.find(i) == umap.end()){

            umap[i] = true;
            ds.push_back(arr[i]);

            generate(arr,ds,umap);

            ds.pop_back();
            umap.erase(i);

        }
    }

}
vector<vector<int>> permute(vector<int>& nums) {
    vector<int> ds;
    unordered_map<int,bool> umap;
    generate(nums,ds,umap);
    return ans;
}
```
#### Approach 2: Without Map, Optimized Approach.

- we gonna use bit different technique.
- hme hr element ko hr index pr bethana hai.
- first we try everyone at 0 index,
- so we swap 1 with 1 , 1 with 2 , 1 with 3 in level 1 : 
    - considering ki permutaion start ho rha hai 1 se if swap (1-1)
    - considering ki permutation start ho rha hai 2 se if swap (1-2)
    - considering ki permutation start ho rha hia 3 se if swap (1-3)

![take U forward - L13  Print all Permutations of a StringArray Recursion Approach - 2  f2ic2Rsc9pU - 885x498 - 2m22s](https://user-images.githubusercontent.com/35686407/173182291-92d5c176-bbbd-42d6-8b80-dec5f37b2e44.png)

- now, in 2nd level , 1 is done, now we left with 2 elements in 2 and 3, so we swap 2 with 2 and 2 with 3 because we want 2 be at position 2 and also 3 will also be at postion 2

![take U forward - L13  Print all Permutations of a StringArray Recursion Approach - 2  f2ic2Rsc9pU - 853x480 - 3m15s](https://user-images.githubusercontent.com/35686407/173182339-ef55ab9b-c25e-487a-807d-fe2baabdf960.png)

Now, on level 3:

![take U forward - L13  Print all Permutations of a StringArray Recursion Approach - 2  f2ic2Rsc9pU - 853x480 - 5m00s](https://user-images.githubusercontent.com/35686407/173182351-188d1b85-1fab-48be-9187-eb8c22d242c4.png)

Whole Tree : 

![take U forward - L13  Print all Permutations of a StringArray Recursion Approach - 2  f2ic2Rsc9pU - 853x480 - 10m17s](https://user-images.githubusercontent.com/35686407/173182368-55857ecc-ebb8-473c-a196-0aec4fb14555.png)

Pseudo code and TC :

![take U forward - L13  Print all Permutations of a StringArray Recursion Approach - 2  f2ic2Rsc9pU - 853x480 - 14m32s](https://user-images.githubusercontent.com/35686407/173182399-ae61753a-075b-43e7-8b6a-d153e2981558.png)

![NewPermutation](https://user-images.githubusercontent.com/35686407/173182144-71138806-1488-49e4-89e8-7a283ad84a3b.gif)

- TC : n! * n
- SC : O(n) ~ store element and O(n) auxillary stack space.

```cpp
vector<vector<int>> ans;
void generate(vector<int>& arr,int idx){
    if(idx == arr.size()){
        ans.push_back(arr);
        return;
    }

    for(int i = idx; i<arr.size(); i++){

        swap(arr[i],arr[idx]);
        generate(arr,idx+1);
        swap(arr[i],arr[idx]);

    }
}
vector<vector<int>> permute(vector<int>& nums) {
    generate(nums,0);
    return ans;
}
```
## 8. N-Queens

![take U forward - L14  N-Queens Leetcode Hard Backtracking  i05Ju7AftcM - 1536x864 - 10m20s](https://user-images.githubusercontent.com/35686407/173183404-e374a7e6-618f-41cb-a652-cf809ea84b7f.png)

- column mae move kro, check kro kya possible hai rkhna queen ko,
- if yes then next column mae move kr jao rkhkr,
- if no anywhere in column, to piche vapis chle jao , jha queen rkhi thi pichli stage mae hta do vha se, backTrack

![take U forward - L14  N-Queens Leetcode Hard Backtracking  i05Ju7AftcM - 853x480 - 13m52s](https://user-images.githubusercontent.com/35686407/173183483-f6db4781-26e0-441f-a324-8d7e9bfb77b9.png)

![take U forward - L14  N-Queens Leetcode Hard Backtracking  i05Ju7AftcM - 853x480 - 15m54s](https://user-images.githubusercontent.com/35686407/173183491-d59b2bd2-6e00-4f85-9e89-46af6dd87dc0.png)

Pseudo Code:

![take U forward - L14  N-Queens Leetcode Hard Backtracking  i05Ju7AftcM - 885x498 - 19m44s](https://user-images.githubusercontent.com/35686407/173183513-8026e821-d22a-44b0-a4e8-6b6e5db6be80.png)

- We have to check 3 direction only in isPossible() boolean function to place Queen, code
- upper backward
- lower backward
- and in same row but col before current col

![take U forward - L14  N-Queens Leetcode Hard Backtracking  i05Ju7AftcM - 885x498 - 26m21s](https://user-images.githubusercontent.com/35686407/173183591-8107f69a-d404-4985-84e5-c0a037a2bfbe.png)

- But this Gives TLE

#### Optimized IsPossible() code:

- For row, 
    - we take map, that 
    - if Queen is already in some row, 
    - its not possible to place queen there.

![take U forward - L14  N-Queens Leetcode Hard Backtracking  i05Ju7AftcM - 885x498 - 29m12s](https://user-images.githubusercontent.com/35686407/173183675-517d1505-2992-436e-83b1-9c89c7f525dd.png)

So, in above already 1 is there , so 2nd queen is not possible to place , we erase it.

- For Lower back Diagonal 
    - we make a map of size (2n-1)
    - `index = (row+col)` to check

![take U forward - L14  N-Queens Leetcode Hard Backtracking  i05Ju7AftcM - 885x498 - 32m31s](https://user-images.githubusercontent.com/35686407/173183756-b888eac8-53a2-465b-b558-20e30cab2583.png)

- Upper back Diagonal
    - Create hash of size (2n-1)
    - Formula to check index : `(n-1) + (col-row)`

![take U forward - L14  N-Queens Leetcode Hard Backtracking  i05Ju7AftcM - 885x498 - 34m20s](https://user-images.githubusercontent.com/35686407/173183817-691cbb65-9793-417d-88d0-e51226eb91f1.png)

Code:
![take U forward - L14  N-Queens Leetcode Hard Backtracking  i05Ju7AftcM - 885x498 - 35m41s](https://user-images.githubusercontent.com/35686407/173183847-e11a7cf7-fdbf-429d-b3dc-a8077728e684.png)

```cpp
class Solution {
public:
    
    bool isPossible(int row,int col,int n,vector<bool>& rowCheck,vector<bool>& lbDiagonal,vector<bool>& ubDiagonal){
        if(rowCheck[row] == true) return false;
        if(lbDiagonal[row+col] == true) return false;
        if(ubDiagonal[n - 1 + col - row] == true) return false;
        return true;
    }
    
    #define debug(x) cout<<#x<<":"<<x<<endl;
    void solve(vector<string>& board,int col,vector<vector<string>>& ans,vector<bool>& rowCheck,vector<bool>& lbDiagonal,vector<bool>& ubDiagonal,int n){
        if(col == n){
            ans.push_back(board);
            return;
        }

        for(int row = 0; row < board.size() ; row++){
            
            bool isP = isPossible(row,col,n,rowCheck,lbDiagonal,ubDiagonal);
            if(isP){
                
                board[row][col] = 'Q';
                rowCheck[row] = true;
                lbDiagonal[row + col] = true;
                ubDiagonal[n - 1 + col - row] = true;
                
                solve(board,col+1,ans,rowCheck,lbDiagonal,ubDiagonal,n);
                
                board[row][col] = '.';
                rowCheck[row] = false;
                lbDiagonal[row + col] = false;
                ubDiagonal[n - 1 + col - row] = false;
                
            }
        }
        
    }
    
    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> ans;
        
        vector<string> board(n);
        string s(n,'.');
        for(int i = 0; i < n; i++){
            board[i] = s;
        }
        
        vector<bool> rowCheck(n,false);
        vector<bool> lbDiagonal(2*n-1,false);
        vector<bool> ubDiagonal(2*n-1,false);
        
        solve(board,0,ans,rowCheck,lbDiagonal,ubDiagonal,n);
        
        return ans;
    }
};
```
## 9. Suduko Solver

![take U forward - L15  Sudoko Solver Backtracking  FWAIf_EVUKE - 1435x807 - 3m06s](https://user-images.githubusercontent.com/35686407/173184685-314f3c4a-29e9-4093-ac5c-fab24fb87077.png)

- Whenever, there is a question of trying all possible way, so, its about trying `every` possible way
- isme hr khali box mae try krenge kya 1 rkh skte agar rkh skte to recursion call lgao aage check kro ki jha khali hai fill krke dekho, agar nhi rkh skte backtrack kr jao and fr se check kro 1 ko 2 krke aage i kya ab aage bhr skte hai.
- if board mera poora ho jata hai, to return true kr do
- if 1 to 9 kuch bhi fill nhi kr skte khali space mae return false krdo,
- hr possible bhrne ki koshsih kro, ek se bhi agar pura bn gya that our ans.

![take U forward - L15  Sudoko Solver Backtracking  FWAIf_EVUKE - 853x480 - 9m58s](https://user-images.githubusercontent.com/35686407/173219183-a9da79a9-489a-4d98-93e4-a8959ab07db0.png)

![take U forward - L15  Sudoko Solver Backtracking  FWAIf_EVUKE - 853x480 - 10m58s](https://user-images.githubusercontent.com/35686407/173219269-54cf1e25-a7b4-45a0-8521-125f83462b75.png)

![take U forward - L15  Sudoko Solver Backtracking  FWAIf_EVUKE - 853x480 - 11m36s](https://user-images.githubusercontent.com/35686407/173219274-b6e44a2f-f884-47ce-b3e8-30d25064a004.png)

![take U forward - L15  Sudoko Solver Backtracking  FWAIf_EVUKE - 853x480 - 12m21s](https://user-images.githubusercontent.com/35686407/173219278-bcf57238-8618-4228-896d-d51782e6eef5.png)

- Formula to check 3x3 matrix :
    - 3 x (row/3) - it tells which 3x3 matrix vertically you are present
    - 3 x (col/3) - it tells which 3x3 matrix horizontally you are present
    - now, for each cell
        - 3 x (row/3) + i/3
        - 3 x (col/3) + i%3

we are checking row, col, and 3x3 matrix simultaneously to know value is already present or not.

![take U forward - L15  Sudoko Solver Backtracking  FWAIf_EVUKE - 885x498 - 23m33s](https://user-images.githubusercontent.com/35686407/173219311-7df68b19-e9af-46ac-8f50-41da82875f31.png)

```cpp
class Solution {
public:
    void solveSudoku(vector<vector<char>>& board) {
        solve(board);
    }
    
    bool solve(vector<vector<char>>& board){
        int n = board.size();
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                
                if(board[i][j] == '.'){
                    
                    for(char num = '1' ; num <= '9' ; num++){
                        
                        if(isPossible(board,i,j,num)){
                            
                            board[i][j] = num;
                            
                            bool res = solve(board);
                            if(res == true) return true;
                            board[i][j] = '.';
                            
                        }
                        
                    }
                    return false;
                    
                }
                
            }
        }
        return true;
    }
    
    bool isPossible(vector<vector<char>>& board,int row,int col,char c){
        
        for(int i = 0; i < 9; i++){
            
            // col check
            if(board[i][col] == c) return false;
            
            // row check
            if(board[row][i] == c) return false;
            
            if(board[3* (row/3) + (i/3)][3 * (col/3) + (i%3)] == c){
                return false;
            }
            
        }
        return true;
    }
    
};
```
## 10. M-Coloring Problem

```cpp
bool isPossible(bool graph[101][101],int color[],int node,int col,int n){
    for(int i = 0;i < n; i++){
        if(i != node && graph[i][node] == 1 && color[i] == col) return false;
    }
    return true;
}

bool solve(bool graph[101][101],int node,int m,int n,int color[]){
    if(node == n){
        return true;
    }
    
    for(int i = 1; i<=m; i++){
        if(isPossible(graph,color,node,i,n)){
            color[node] = i;
            bool res = solve(graph,node+1,m,n,color);
            if(res == true) return true;
            color[node] = 0;
        }
    }
    
    return false;
}

bool graphColoring(bool graph[101][101], int m, int n) {
    int color[n] = {0};
    return solve(graph,0,m,n,color);
}
```

## 11. Palindrome Partitioning

- Which is the first position wherer you start partition, its palindrome substring ~ a and aa are palindrome but aab is not palindrome so , from that we can't create partition , simmillarly, aabb is not palindrome , so we can not partition it.

- `Substring should be Palindrome`
- Try to do partition, where it is possible

![take U forward - L17  Palindrome Partitioning Leetcode Recursion C++ Java  WBgsABoClE0 - 885x498 - 5m47s](https://user-images.githubusercontent.com/35686407/173818922-ef08c221-d85d-4e78-8fc3-54401dc6869e.png)

- So when we partition with first palindrome, abb is left string, now again do the same work, a is palindrome,partition it, and left with bb, here b is palindrome and bb is also palindrome, we partition it, moment when we left with nothing, we add our ans and backtrack to see more solutions.

![take U forward - L17  Palindrome Partitioning Leetcode Recursion C++ Java  WBgsABoClE0 - 885x498 - 7m53s](https://user-images.githubusercontent.com/35686407/173819808-3b735d97-c5eb-4178-86bf-960681756a3f.png)

![take U forward - L17  Palindrome Partitioning Leetcode Recursion C++ Java  WBgsABoClE0 - 853x480 - 11m07s](https://user-images.githubusercontent.com/35686407/173820322-049a2bb6-487b-44da-bf0b-4ce830dcbed1.png)

![take U forward - L17  Palindrome Partitioning Leetcode Recursion C++ Java  WBgsABoClE0 - 885x498 - 17m07s](https://user-images.githubusercontent.com/35686407/173820466-08493370-fa8b-4d67-9bde-4ca86f95afb8.png)

![take U forward - L17  Palindrome Partitioning Leetcode Recursion C++ Java  WBgsABoClE0 - 853x480 - 23m16s](https://user-images.githubusercontent.com/35686407/173820520-5be14923-f725-40a9-a247-2b20aa643fbe.png)

```cpp
class Solution {
public:
    
    bool isPalindrome(string& s,int start,int end){
        while(start <= end){
            if(s[start] != s[end]){
                return false;
            }
            start++;
            end--;
        }
        return true;
    }
    
    void solve(string& s,int idx,vector<string>& ds,vector<vector<string>>& ans){
        if(idx == s.size()){
            ans.push_back(ds);
            return;
        }
        
        for(int i = idx;i < s.size(); i++){
            if(isPalindrome(s,idx,i)){
                string toadd = s.substr(idx,i-idx+1); // i-idx+1 is len and idx se start kro 
                ds.push_back(toadd);
                solve(s,i+1,ds,ans);
                ds.pop_back();
            }
        }
        
    }
    
    vector<vector<string>> partition(string s) {
        vector<string> ds;
        vector<vector<string>> ans;
        solve(s,0,ds,ans);
        return ans;
    }
};
```

## 12. Rat in a Maze

![take U forward - L19  Rat in A Maze Backtracking  bLGZhJlt4y0 - 885x498 - 8m51s](https://user-images.githubusercontent.com/35686407/173822409-8c7c2fb6-e25e-412d-8e1b-684106b60678.png)

- question mae kha hai lexographically print krna hia to , move krenge Down | Left | Right | Vertical
- ek visited array bhi rkhna hoga jo ye btayega ki is cell pr already poch chuke ho, mt jao ispr.
- ya same given matrix ko visited jese bhi use kr skte hai

```cpp
class Solution{
    public:
    
    bool isPossible(vector<vector<int>>& m,int row,int col,int n){
        if(row < 0 || col < 0 || row >= n || col >= n || m[row][col] == 0) return false;
        return true;
    }
    
    void solve(vector<vector<int>>& m,int row,int col,int n,string& ds,vector<string>& ans){
        if(row == n-1 && col == n-1){
            ans.push_back(ds);
            return;
        }
        
        // down
        if(isPossible(m,row+1,col,n)){
            
            m[row][col] = 0;
            
            ds += 'D';
            solve(m,row+1,col,n,ds,ans);
            ds.pop_back();
            
            m[row][col] = 1;
            
        }
        // left
        if(isPossible(m,row,col-1,n)){
            
            m[row][col] = 0;
            
            ds+='L';
            solve(m,row,col-1,n,ds,ans);
            ds.pop_back();
            
            m[row][col] = 1;
            
        }
        
        // right
        if(isPossible(m,row,col+1,n)){
            
            m[row][col] = 0;
            
            ds+= 'R';
            solve(m,row,col+1,n,ds,ans);
            ds.pop_back();
            
            m[row][col] = 1;
            
        }
        
        // up
        if(isPossible(m,row-1,col,n)){
            
            m[row][col] = 0;
            
            ds+='U';
            solve(m,row-1,col,n,ds,ans);
            ds.pop_back();
            
            m[row][col] = 1;
            
        }
        
    }
    
    vector<string> findPath(vector<vector<int>> &m, int n) {
        // Your code goes here
        vector<string> ans;
        string ds= "";
        if(m[0][0] == 0) return {};
        map<pair<int,int>,bool> visited;
        solve(m,0,0,n,ds,ans);
        return ans;
    }
};
```

## 13. K-th Permutation

## 14. Kth Symbol in Grammer

- observation skill test
- n = 4 vale row ka first half, same hai n = 3 ke and second half first half ka complement hai
- if (k <= mid) return solve(n-1,k);
- else return !solve(n-1,k-mid);

![Aditya Verma - Kth Symbol in Grammar  5P84A0YCo_Y - 885x498 - 11m39s](https://user-images.githubusercontent.com/35686407/173826469-6e7adb18-2a4e-41c3-8c5e-76a36e4aa819.png)

![Aditya Verma - Kth Symbol in Grammar  5P84A0YCo_Y - 853x480 - 13m03s](https://user-images.githubusercontent.com/35686407/173826730-ff988067-6993-424c-a8a7-66e75c4ce661.png)

![Aditya Verma - Kth Symbol in Grammar  5P84A0YCo_Y - 853x480 - 16m46s](https://user-images.githubusercontent.com/35686407/173826739-85fd256e-0f82-4f1c-abe6-79bf709f6ef6.png)

```cpp
int kthGrammar(int n, int k) {
    if(n == 0) return 0;
    int mid = pow(2,n) - 1;
    if(k <= mid){
        return kthGrammar(n-1,k);
    }else{
        return !kthGrammar(n-1,k-mid);
    }
}
```

## 15. Permutations with spaces

- pehle char ko chordkr, aage ke sare char ke paas option hai, ya to space ke sath jaye ya fr bina space ke sath jaye
- option: with space and without space

![Aditya Verma - Permutation with spaces  1cspuQ6qHW0 - 885x498 - 8m06s](https://user-images.githubusercontent.com/35686407/173829057-81fe8260-86f7-490b-8d32-236c7fd9262a.png)

![Aditya Verma - Permutation with spaces  1cspuQ6qHW0 - 853x480 - 9m43s](https://user-images.githubusercontent.com/35686407/173829107-0bc17986-df5c-4355-a6aa-5e3d36d7f04e.png)

```cpp
class Solution{
public:

    void solve(string& s,int idx,string& ds,vector<string>& ans){
        if(idx == s.size()){
            ans.push_back(ds);
            return;
        }
        
        char ch = s[idx];
        
        ds.push_back(' ');
        ds.push_back(ch);
        
        solve(s,idx+1,ds,ans);
        
        ds.pop_back();
        ds.pop_back();
        
        ds.push_back(ch);
        solve(s,idx+1,ds,ans);
        ds.pop_back();
        
    }
    
    vector<string> permutation(string S){
        vector<string> ans;
        string ds = "";
        ds += S[0];
        solve(S,1,ds,ans);
        return ans;
    }
};
```
## 16. Permutation with Case Change

- hr char ke paas 2 option hai,
    1. vo chota ho jaye
    2. vo bda ho jaye

```cpp
void solve(string& s,int idx,string& ds,vector<string>& ans){
    if(idx == s.size()){
        ans.push_back(ds);
        return;
    }

    char ch = s[idx];

    // lower
    ch = tolower(ch);

    ds.push_back(ch);

    solve(s,idx+1,ds,ans);

    ds.pop_back();

    // upper
    ch = toupper(ch);

    ds.push_back(ch);

    solve(s,idx+1,ds,ans);

    ds.pop_back();
}

vector<string> permuteAString(string& s){
    vector<string> ans;
    string ds;
    solve(s,0,ds,ans);
    return ans;
}
```

## 17. Letter Case Permutation

- same as permutation with case change, just difference is that it include numeric value also,
- alpha char have 2 options
    1. chota ho jaye
    2. bda ho jaye

```cpp
class Solution {
public:
    
    void solve(string& s,int idx,string& ds,vector<string>& ans){
        if(idx == s.size()){
            ans.push_back(ds);
            return;
        }
        
        char ch = s[idx];
        if(isalpha(ch)){
            
            // lower
            ds.push_back(tolower(ch));
            solve(s,idx+1,ds,ans);
            ds.pop_back();
            
            //upper
            ds.push_back(toupper(ch));
            solve(s,idx+1,ds,ans);
            ds.pop_back();
            
        }else{
            ds.push_back(ch);
            solve(s,idx+1,ds,ans);
            ds.pop_back();
        }
        
    }
    
    vector<string> letterCasePermutation(string s) {
        vector<string> ans;
        string ds = "";
        solve(s,0,ds,ans);
        return ans;
    }
};
```

## 18. Generate all Paranthesis

1. Brute Force:

- sare possible solution bnao, mtlb hr position pr closing bhi aa skti hai and opening bhi
- to fr jb open and close bracket khtm ho jayenge open = 0 and close = 0 then check krlo, jo paranthesis bni hai vo valid hia ya nhi

2. Better/Optimized:

![Aditya Verma - Generate all Balanced Parentheses  eyCj_u3PoJE - 885x498 - 24m12s](https://user-images.githubusercontent.com/35686407/173837369-86c925a3-530b-4257-a728-4f0ff463adea.png)

- srf vhi rkho jo possible hai
- mtlb ye ki agar recursion tree mae dekhe, to open bracket '(' hr jagah possible hai
- when open < close, both possible open '(' and ')'
- jb open == close only 1 possible open '('
- when open = 0 but close != 0, tb close close lgate jao

```cpp
class Solution {
public:
    
    void solve(int open,int close,string& ds,vector<string>& ans){
        if(open == 0 && close == 0){
            ans.push_back(ds);
            return;
        }
        
        if(open == close){
            ds += '(';
            solve(open-1,close,ds,ans);
            ds.pop_back();
        }else if(open < close){
            if(open != 0){
                ds+='(';
                solve(open-1,close,ds,ans);
                ds.pop_back();
                ds+=')';
                solve(open,close-1,ds,ans);
                ds.pop_back();
            }else{
                ds+=')';
                solve(open,close-1,ds,ans);
                ds.pop_back();
            }
        }
        
    }
    
    vector<string> generateParenthesis(int n) {
        vector<string> ans;
        string ds = "";
        int open = n;
        int close = n;
        solve(open,close,ds,ans);
        return ans;
    }
};
```

## 19. Print N-Bit Binary Number having More 1's then 0's in Prefix

- generate all paranthesis jesa hi similar hai
- if ones == zeros , then only 1 will be pushed back
- else if ones > zeros , then 2 options, 1 and 0 both will be possible to push

![Aditya Verma - Print N-bit binary numbers having more 1’s than 0’s for any prefix  U81n0UYtk98 - 885x498 - 20m24s](https://user-images.githubusercontent.com/35686407/173839087-bd6d2a03-76ae-4b99-814d-9bd501a16585.png)

```cpp
class Solution{
public:	
    
    void solve(int ones,int zeros,int n,string& ds,vector<string>& ans){
        if(n == 0){
            ans.push_back(ds);
            return;
        }
        
        if(ones == zeros){
            // push only 1
            ds.push_back('1');
            
            solve(ones+1,zeros,n-1,ds,ans);
            
            ds.pop_back();
        }else if(ones > zeros){
            // 2 options 0 and 1
            
            ds.push_back('1');
            solve(ones+1,zeros,n-1,ds,ans);
            ds.pop_back();
            
            ds.push_back('0');
            solve(ones,zeros+1,n-1,ds,ans);
            ds.pop_back();
            
        }
        
    }

	vector<string> NBitBinary(int N)
	{
	    vector<string> ans;
	    string ds = "";
	    solve(0,0,N,ds,ans);
	    return ans;
	}
};
```

## 20. Josephus Problem

## 21. Get KeyPad Combination

## 22. Get Maze Paths

## 23. Maximum Score of Words Problem

## 24. Print In LexoGraphical Order

## 25. GoldMine

## 26. WordBreak Problem (Print, Backtracking vali - Dynamic Programming vali bhi hai)

- isme hme ek dictionary di hui hai and ek string dia hua hia,
- hme print krna hai ki konse konse sentence create kiye ja skte hai

![Screenshot Capture - 2022-06-15 - 19-05-34](https://user-images.githubusercontent.com/35686407/173840618-93093035-61db-4274-b390-a665559d2683.png)

- ab hum apne string pr traverse krege and substr find krenge , 0-0 , 0 - 1, 0 - 2, 0 - 3, etc., if substr dictionary mae huam usko ds mae space ke sath jodkr aage bhej denge and left string jo bchi usko as main string bhej denge
- jb main string khali ho jayegi, hum posans(possible ans) apne ans vector mae daal denge.
- 
![Pepcoding - Word Break Problem using Backtracking Word Break Solution in JAVA  LmHWIsBQBU4 - 885x498 - 2m25s](https://user-images.githubusercontent.com/35686407/173841316-e2ef9685-b714-4e34-b2ef-44d54606ea27.png)

```cpp
class Solution{
public:

    void solve(string s,string posans,unordered_map<string,bool>& umap,vector<string>& ans){
        if(s == ""){
            posans.pop_back(); // last mae bhi space aayega usko popback krdo
            ans.push_back(posans);
            return;
        }
        
        for(int i = 0;i < s.size(); i++){
            string possible = s.substr(0,i+1);
            if(umap.find(possible) != umap.end()){
                string left = s.substr(i+1);
                string sendaage = posans + possible;
                sendaage += ' '; // space jodo
                solve(left,sendaage,umap,ans);
            }
        }
        
    }

    vector<string> wordBreak(int n, vector<string>& dict, string s)
    {
        vector<string> ans;
        unordered_map<string,bool> umap;
        for(auto& word:dict){
            umap[word] = true;
        }
        solve(s,"",umap,ans);
        return ans;
    }
};
```
## 27. Remove Invalid Parantheses

- isme hme remove krne hai invalid parantheses ko and all possible result dene hai
- remove krne se pehle count krlo kitne invalid char / braces '(' or ')' hai
- ab hme pta hoga hme total kitne remove krne hai
- to hum srf utne hi remove krenge string mae se
- hr parantheses '(' , ')' , ke paas 2 option hongge ya to muje remove kro ya na kro, if krte ho to, ek kum krke aage calculation ko bhej do
- jb base case pr poch jayenge, tb hme string ko ans mae tbhi dalna hai agar vo valid hoga to
- or jayeda time complexity se bchne ke liye dublicate case handle krlo,
- umap[s] == true then return , ye sbse upar isliye lhgaya hai kyuki if koi pehle se generated hai, agli baar bhi same type ka pattern milta hai to pehle hi return krde solve krne se pehle.
- hr state mae jo new s hai vo daal rhe hai map mae.

```cpp
class Solution {
public:
    
    unordered_map<string,bool> umap;
    
    void solve(string s,int invalid,vector<string>& ans){
        if(umap[s] == true) return;
        umap[s] = true;
        
        if(invalid == 0){
            if(!invalidCount(s)){
                ans.push_back(s);
            }
            return;
        }
        
        for(int i = 0;i < s.size() ; i++){
            if(!isalpha(s[i])){
                string left = s.substr(0,i);
                string right = s.substr(i+1);
                string leftright = left + right;
                solve(leftright,invalid-1,ans);
            }
        }
        
    }
    
    int invalidCount(string& s){
        stack<char> st;
        int ans = 0;
        for(auto& ch:s){
            if(ch == '('){
                st.push('(');
            }else if(ch == ')'){
                if(st.empty()){
                    ans += 1;
                }else{
                    st.pop();
                }
            }
        }
        ans+=st.size();
        return ans;
    }
    
    vector<string> removeInvalidParentheses(string s) {
        vector<string> ans;
        int invalid = invalidCount(s);
        solve(s,invalid,ans);
        return ans;
    }
};
```
## 28. Partition Equal Subset Sum (Part of DP)

- array ko 2 subset mae divide kro jinka sum equal ho
- agar possible hai to return 1
- else return 0
- same as subset sum
- bs target = sum/2
- and if sum os odd then not possible
- hr number ke paas 2 option hai, ya to subset mae aaye ya na aaye
- memoization use hui hai otherwise TLE aarha tha

```cpp
class Solution{
public:

    int find(int arr[],int index,int target,int n,vector<vector<int>>& memo){
        if(target == 0) return 1;
        if(index == n) return 0;
        
        if(memo[index][target] != -1) return memo[index][target];
                
        // take
        int v1 = find(arr,index+1,target-arr[index],n,memo);
        if(v1 == 1) return memo[index][target] = 1;
        
        // not take
        int v2 = find(arr,index+1,target,n,memo);
        if(v2 == 1) return memo[index][target] = 1;

        return memo[index][target] = 0;
    }

    int equalPartition(int N, int arr[])
    {
        int sum = accumulate(arr,arr+N,0);
        if((sum&1)) return 0;
        int target = sum/2;
        int index = 0;
        vector<vector<int>> memo(N+1,vector<int>(target+1,-1));
        return find(arr,index,target,N,memo);
    }
};
```
