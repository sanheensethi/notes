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
    - index = (row+col) to check

![take U forward - L14  N-Queens Leetcode Hard Backtracking  i05Ju7AftcM - 885x498 - 32m31s](https://user-images.githubusercontent.com/35686407/173183756-b888eac8-53a2-465b-b558-20e30cab2583.png)

- Upper back Diagonal
    - Create hash of size (2n-1)
    - Formula to check : `(n-1) + (col-row)`

![take U forward - L14  N-Queens Leetcode Hard Backtracking  i05Ju7AftcM - 885x498 - 34m20s](https://user-images.githubusercontent.com/35686407/173183817-691cbb65-9793-417d-88d0-e51226eb91f1.png)

Code:
![take U forward - L14  N-Queens Leetcode Hard Backtracking  i05Ju7AftcM - 885x498 - 35m41s](https://user-images.githubusercontent.com/35686407/173183847-e11a7cf7-fdbf-429d-b3dc-a8077728e684.png)

```cpp

```
