# Array

## 1. Set Matrix Zeros [Question](https://leetcode.com/problems/set-matrix-zeroes/)

![Screenshot Capture - 2022-06-18 - 08-52-15](https://user-images.githubusercontent.com/35686407/174420952-10edc845-0dd7-41e2-a930-4dcc6a22c0e0.png)


#### Brute Force

- Approach 1: Store 0's Position
    - Queue mae sare 0 ki position daal do {x,y} (esa ilsiye suppose if nhi dalte to agar 0 kr denge sare 1 zero ke krn, to jb hum traverse krke jayemge jo change hokr 0 hua hai vo catch ho jayega if else mae and uski vjh se bhi change ho jayega jbki hme jo 0 present hai srf unki row and col ko zero krna hai)
    - ab ek ek krke position nikalo, and us position ki puri row and pure col ko 0 kr do
    - TC : O(NxM) + O(N+M) ~ Traversing 2 times
    - SC : O(NxM) - all position have zeros

```cpp
void setZeroes(vector<vector<int>>& matrix) {
        int row = matrix.size();
        int col = matrix[0].size();
        queue<pair<int,int>> Q;
        for(int i = 0; i < row ; i++){
            for(int j = 0; j < col; j++){
                if(matrix[i][j] == 0){
                    Q.push({i,j});
                }
            }
        }
        
        while(!Q.empty()){
            auto pr = Q.front();Q.pop();
            setRow(pr,matrix);
            setCol(pr,matrix);
        }
        
    }
```

- Approach 2: Mark -1
    - Jha bhi 0 dikhe , uski puri row and pura col -1 se mark kr do.
    - ab dobara traverse krke -1 ko 0 kr do
    - TC : O(NxM) + O(N+M)
    - SC : O(1)
    
![Screenshot Capture - 2022-06-18 - 08-53-09](https://user-images.githubusercontent.com/35686407/174420987-bc17defe-401f-4bd8-8871-9062a34005ba.png)


#### Optimized

- Approach 1: (Taking 2 Extra arrays as row and col)
    - jha bhi 0 dikhe to, uske correspoding row vale and col vale array mae 0 daal do
    - Now Traverse the matrix again, and check if row array and col array have same 0 if yes then change it to 0
    - TC : O(NxM) + O(NxM)
    - SC : O(N) + O(M)
    
![Screenshot Capture - 2022-06-18 - 08-56-19](https://user-images.githubusercontent.com/35686407/174421107-bf624fc7-b09e-45b3-abc7-5244fdc14acb.png)

![Screenshot Capture - 2022-06-18 - 08-57-12](https://user-images.githubusercontent.com/35686407/174421131-c3ac86f5-8ded-4d48-ad64-8dba9ac3dfe0.png)

```cpp
void setZeroes(vector<vector<int>>& matrix) {
    int rows = matrix.size();
    int cols = matrix[0].size();

    vector<int> rowA(rows,-1);
    vector<int> colA(cols,-1);

    for(int i = 0; i < rows; i++){
        for(int j = 0; j < cols; j++){
            if(matrix[i][j] == 0){
                rowA[i] = 0;
                colA[j] = 0;
            }
        }
    }

    for(int i = 0; i < rows; i++){
        for(int j = 0; j < cols ; j++){
            if(rowA[i] == 0 || colA[j] == 0){
                matrix[i][j] = 0;
            }
        }
    }

}
```

#### Most Optimal Approach

- we take 2 dummy array as above inside the matrix
- 1st row as row dummy array and 1st col as col dummy matrix
- niche vali figure mae (0,0) position pr jo 0 aayega vo 1st col ke last element jo 0 hai uske krn aayega, to agar vo 0 hota hai , to uske krn hum uski row ko 0 nhi hone denge, because uske pehle se 0 nhi tha, vo 0 bna hai apne col ke last element ki madad se

![Screenshot Capture - 2022-06-18 - 09-00-10](https://user-images.githubusercontent.com/35686407/174421230-d49c5c7f-9d4c-4864-81dd-7515d66409b9.png)

- Therefore, hum row ke liye assume krenge ki jo (0,0) position hai vha 0 mark kia gya hai(mtlb 0 bnaya gya hai) by last element of 1st col, and col ke liye mark = true, means if col have 0 then col = false it means we have to set col = 0;
- jb pehli 0 milegi, tb hum dummy row col mae 0 daal denge, as marker

![Screenshot Capture - 2022-06-18 - 09-04-47](https://user-images.githubusercontent.com/35686407/174421362-9686924a-eec8-4a6d-bc4a-38e528d7a5b9.png)

- ab hum jb mark krte krte, 1st col ke 0 ke paas poche, hme pta chla ki ye 0 hme 1st col mae milta hai to hum col = false kr denge

![Screenshot Capture - 2022-06-18 - 09-05-39](https://user-images.githubusercontent.com/35686407/174421392-aad8bd5d-f674-43ee-98c4-551e8a057d5f.png)

- ye sb krne ke baad hum, piche se traverse krenge in all row , but for col >= 1 and check krenge ki koi ek 0 hai dummy mae ? if yes then 0 bna denge us position mae

![Screenshot Capture - 2022-06-18 - 09-07-37](https://user-images.githubusercontent.com/35686407/174421424-374d72e3-9630-46b4-8b92-85541486602f.png)

- ab jb hum 1st row mae pohchenge hme pta chlega ki (0,0) to 1 hai, to hum change nhi krenge 1st row ke last element ko,
- and jb hum (0,0) pr pochenge , tb col = false ke krn hum use bhi 0 krdenge

![Screenshot Capture - 2022-06-18 - 09-11-36](https://user-images.githubusercontent.com/35686407/174421543-22cbdcb8-da67-4360-abf5-20e77a30ed62.png)

- Hum piche se isliye traverse kre hai kyuki, agar aage se krte to dummy row, and col update ho jate, but vesa nhi krna hia ,
- pehle dummy row col ko chordkr baki ke update krne hai baad mae dummy.

> More Clear: Col = TRUE (flag) ye bta rha hai ki 1st col ko 0 krna hai ya nhi, mtlb 1st col mae 0 exist krta hai ye nhi

```cpp
void setZeroes(vector<vector<int>>& matrix) {
    bool colFlag = false; // there is no zero in dummy col
    int rows = matrix.size();
    int cols = matrix[0].size();

    for(int i = 0; i < rows; i++){
        if(matrix[i][0] == 0) colFlag = true; // it means first col have 0
        for(int j = 1; j < cols; j++){
            if(matrix[i][j] == 0){
                matrix[i][0] = matrix[0][j] = 0;
            }
        }
    }

    for(int i = rows-1; i >= 0 ; i--){
        for(int j = cols-1; j >= 1; j--){
            if(matrix[i][0] == 0 || matrix[0][j] == 0){
                matrix[i][j] = 0;
            }
        }
        if(colFlag == true) matrix[i][0] = 0;
    }
}
```
## 2. Pascal Triagnle [Leetcode](https://leetcode.com/problems/pascals-triangle/)

#### Variation 1: Generate Pascal Triangle (N is given)

![PascalTriangleAnimated2](https://user-images.githubusercontent.com/35686407/174424122-3260e741-d26c-4a4d-aca6-abff01448516.gif)

- Observe Pattern :
    - n = 1 , 1 element
    - n = 2 , 2 element, and so on.
    - 1st and last element of each row is 1
    - bich vale element upar vale ka sum left and right se
    - therefore, in code hum pehle (i+1) size ka vector bnayenge , because of 0 based indexing
    - ab, first and last positon pr 1 rkh denge
    - and bchi hui position mae jb n=3 hoga tb dikhegi ye positions, `vec[j] = matrix[i-1][j-1] + matrix[i-1][j]` krenge

```cpp
vector<vector<int>> generate(int numRows) {
    vector<vector<int>> mat;

    for(int i = 0; i < numRows; i++){
        int size = i+1;
        vector<int> vec(i+1);

        vec[0] = vec[i] = 1;

        for(int j = 1; j < i; j++){
            vec[j] = mat[i-1][j-1] + mat[i-1][j];
        }

        mat.push_back(vec);
    }

    return mat;
}
```

#### Variation 2: N/R and C dia hoga

- Row and Col number dia hoga, hme find krna hai vo element ki value,
- direct formula : C(R-1,C-1) , combination ~ permutation vala

![Screenshot Capture - 2022-06-18 - 11-00-05](https://user-images.githubusercontent.com/35686407/174424302-5ff36bb4-1d16-45eb-a05c-d0c5e53684fe.png)

#### Variation 3: N/R dia hua hai and kha hai puri row print kro [Question](https://leetcode.com/problems/pascals-triangle-ii/)

`Approach 1:` Compute factorial for every column 
- It is very costly, worst TC : O(N^2)

`Approach 2:` 

![take U forward - PASCAL Triangle Leetcode C++ Java 3 problems asked in Interviews related to Pascal discussed  6FLvhQjZqvM - 853x480 - 5m49s](https://user-images.githubusercontent.com/35686407/174424591-243752b5-10b1-44e4-87b2-18e155651b3d.png)

> Technique to find C(N,R) for every column

- See above, if Row = 4, we have to generate,
- if col = 0, then C(4,0) = 1
- if col = 1, then C(4,1) = 4 = 4/1
- if col = 2, then C(4,2) = (4x3)/(1x2) = (4/1) x (3/2)
- if col = 3, then C(4,3) = (4x3x2)/(1x2x3) = (4x3)/(1x2) x (2/3)
- see the pattern, when col = 2, then we multiply col = 2 in denomenator, and prev-val - 1 = 4-1 = 3 in numerator
- TC : for 1 col - O(1)
- TC : for row - O(n)
- SC : O(n)

> TC and SC for 3 Types:

![Screenshot Capture - 2022-06-18 - 11-13-00](https://user-images.githubusercontent.com/35686407/174424637-28330e68-81e3-4d28-92be-4a141821ca15.png)

```cpp
vector<int> getRow(int n) {
   int k = n+1;
    vector<int> ans;

    long long int res = 1;
    for(int i = 0; i < k; i++){
        ans.push_back((int)res);
        res = res * (n-i);
        res = res / (i+1);
    }
    return ans;
}
```

## 3. Next Permutation

![take U forward - NEXT PERMUTATION Leetcode Know the Intuition behind the Algorithm C++ Java Brute-Optimal  LuLCLgMElus - 853x480 - 7m19s](https://user-images.githubusercontent.com/35686407/174426073-5f360bf9-087e-404d-9f69-6fe0a37dd753.png)

- Algo:
    1. Find an index such that : a[i] < a[i+1], in reverse Let it be idx1
    2. Find an index such that : a[idx1] < a[i], in reverse Let it be idx2
    3. Swap idx1 , idx2
    4. reverse idx1+1 to end

`Intuation`

Eample : 1 3 5 4 2

![Screenshot Capture - 2022-06-18 - 12-01-48](https://user-images.githubusercontent.com/35686407/174425969-57c51ba8-78c3-42d0-b95a-217ead6e05c8.png)

- From , behind, its always in inc order, if we take case 1 2 3 , 3 is the number which is itself in inc order.
- So, have to find the next permutation,
- hum 3 se next greater dhundenge, 3 ko dhudne ke liye, hme sbse pehle 3 ki position chahiye, jo hogi , 3 < 5 vali ~ a[i] < a[i+1] 
- ab hum 3 se just bda element dhundenge , taki 2nd element of number hmara bda ho, iske liye dobara traverse krenge piche se and find 4 first number > 3
- ab indono ko jb swap krenge hmare paas bnega 1 4 5 3 2
- ab swap krne ke baad agar hum 4 se aage 5 to 2 reverse krde to vo inc order mae ho jayega it becomes 1 4 2 3 5 , which is the next permutation.

> For more clear: write down permutation for 1 2 3 5

> TC and SC : 

![Screenshot Capture - 2022-06-18 - 12-21-08](https://user-images.githubusercontent.com/35686407/174426522-e9b35c62-6e18-42d2-9a54-c19f9574ac99.png)

```cpp
void nextPermutation(vector<int>& nums) {
    int n = nums.size();
        
    int idx1,idx2;

    for(idx1 = n-2; idx1 >= 0; idx1--){
        if(nums[idx1] < nums[idx1+1]){
            break;
        }
    }


    if(idx1 < 0){
        // means we are in last permutation 5 4 3 2 1
        // just reverse array
        reverse(nums.begin(),nums.end());
    }else{

        for(idx2 = n-1; idx2 >= 0; idx2--){
            if(nums[idx2] > nums[idx1]){
                break;
            }
        }

        swap(nums[idx1],nums[idx2]);

        reverse(nums.begin()+ idx1 + 1,nums.end());

    }

}
```

## 4. Kadane's Algorithm (Max Subarray Sum)

#### Brute Force O(n^3)

![take U forward - Maximum Subarray Sum Leetcode Kadane's Algorithm Brute-Better-Optimal CPPJava  w_KEocd__20 - 885x498 - 1m50s](https://user-images.githubusercontent.com/35686407/174427442-eaefebba-8d7d-4148-a019-899bd3690ba0.png)

#### Better Brute Force O(n^2)

- we loop again to calculate sum from i to j in Brute Force, instead while moving j,we will calculate sum and update it.

![take U forward - Maximum Subarray Sum Leetcode Kadane's Algorithm Brute-Better-Optimal CPPJava  w_KEocd__20 - 853x480 - 2m50s](https://user-images.githubusercontent.com/35686407/174427471-3a214196-c450-4c66-9e92-90bf190c1e31.png)

#### Optimized Solution (Kadane's Algorithm)

[Archives](https://www.geeksforgeeks.org/tag/kadane/)

- Is algo mae hum, ek sum variable le rhe hai 
- and ek ans variable jo max sum value store krega
- ans ko mabhi arr[0] rkho, because question mae kha hai min 1 element jaror hai array mae
- ab, pointer ko bhadao and sum krte jao, and ans ko update krte jao,
- agle step pr jane se pehle if sum < 0 hai t0 sum = 0 krdo, kyuki negative number aage le jane se sum or jayeda kum hi hoga, na ki bhadega.

> Algo Work

- Initialize: local_max = 0 global_max = INT_MIN // local_max ~ sum, global_max ~ ans
- For each element we will follow these steps:
    - local_max = local_max + a[i]
    - if (local_max > global_max ) set global_max = local_max
    - if (local_max < 0) set local_max = 0

```cpp
int maxSubArray(vector<int>& nums) {
    int sum = 0;
    int ans = nums[0];
    for(int i = 0; i < nums.size(); i++){
        sum += nums[i];
        ans = max(ans,sum);
        if(sum < 0) sum = 0;
    }
    return maxi;
}
```

[Article](https://www.scaler.com/topics/kadanes-algorithm/)

> Note: The above algorithm will fail for the case, when there are only negative elements in the array, because our global_max is already set to 0. So, to handle that case we have to modify our algorithm. We will add current element to the previous subarray only if it results in a greater sum, else we will start the new subarray from that element.

- Initialize: local_max = 0 global_max = INT_MIN
- For each element we will follow these steps:
    1. if (a[i] <= local_max + a[i]) local_max = local_max + a[i]
    2. else local_max = a[i]
    3. global_max = max(global_max, local_max)

## 5. Sort 0's 1's and 2's (Dutch National Flag Algo)

#### 3 Way Quick Sort

![take U forward - Sort an array of 0's 1's   2's Leetcode C++ and Java Brute-Better-Optimal  oaVa-9wmpns - 885x498 - 6m51s](https://user-images.githubusercontent.com/35686407/174431768-5fc65aab-5172-4396-a237-3bb5ffb36655.png)

> ALGORITHM -

- Take three-pointers, namely - low, mid, high.
- We use low and mid pointers at the start, and the high pointer will point at the end of the given array.


> Idea : Left of low : all are 0's , Right of High : all are 2's and between low and high : all are 1's

a) arr[l..i] elements less than pivot.
b) arr[i+1..j-1] elements equal to pivot.
c) arr[j..r] elements greater than pivot.

In our Quetion we take pivot = 1

> CASES -

- array [mid] = 0 : swap arr[mid] and arr[low] , low++ , mid++
- array [mid] = 2 : swap arr[mid] and arr[high], high--
- array [mid] = 1 : mid++

> `NOTE` : Jarori nhi hai ki hmesha 0 1 2 hi honge, 2 3 4 , 5 6 7 , any 3 repeated numbers ho skte hai , e.g. {1, 4, 2, 4, 2, 4, 1, 2, 4, 1, 2, 2, 2, 2, 4, 1, 4, 4, 4}

```cpp
void sortColors(vector<int>& arr) {
        int low = 0,mid = 0,high = arr.size()-1;
        
        while(mid <= high){
            if(arr[mid] == 0){
                swap(arr[low],arr[mid]);
                mid++;
                low++;
            }else if(arr[mid] == 1){
                mid++;
            }else if(arr[mid] == 2){
                swap(arr[high],arr[mid]);
                high--;
            }
        }
        
    }
```
## 6. Minimum Time to Buy and Sell Stock

#### Approach 1: Brute Force:

- use 2 loops
- start i = 0 to n - 1
- start j = i to n-1
- if arr[i] < arr[j], profit = max(profit,arr[j] - arr[i])
- TC : O(n^2)
- SC : O(1)


#### Apprach 2: Optimal Approach

- hme pta hai ki profit max tbhi hoga agar hum min stock buy krenge
- to left ka minimum rkhe and current element if bda hai to hum uske sath difference nikale
- if abhi vala profit bda aaya to update krdo ans vale profit ko
- taking minimum element while runnning, which is the minimum of left from current element

![Screenshot Capture - 2022-06-18 - 15-49-06](https://user-images.githubusercontent.com/35686407/174433455-0d5f040a-6346-4b2b-9022-499c5544684b.png)

- jb hum 3 pr hai , to left ka mini = 1 hai, ese left ka min 1 rhega and hum aage bhdte jayenge and profit calc krte jayenge.
- TC : O(n)
- SC : O(1)

```cpp
int maxProfit(vector<int>& prices) {
    int profit = 0;
    int mini = prices[0];
    for(int i = 0; i < prices.size(); i++){
        mini = min(mini,prices[i]);
        profit = max(profit,prices[i] - mini);
    }
    return profit;
}
```

## 7. Rotate Matrix by 90 degree

![Screenshot Capture - 2022-06-18 - 15-51-07](https://user-images.githubusercontent.com/35686407/174433518-b7ec510a-c209-4191-8cc0-7794d43ce80d.png)

#### Approach 1 : Brute

- Take 1 more matrix,
- take 1st row, put in last col
- take 2nd row , put in 2nd last col ans so on
- TC : O(N^2)
- Sc : O(N^2)

#### Appraoch 2 : Optimal , Inplace

- Step 1: Transporse Matrix , ROWS <=> COLS
- Step 2: Reverse Every Row of the Resultant of Step 1 Matrix

![Screenshot Capture - 2022-06-18 - 15-53-06](https://user-images.githubusercontent.com/35686407/174433610-bb4b87c6-954d-4756-9e4f-e705a0b6761e.png)

> Intuation: 7 4 1 in result is reversal of the 1st col , 8 5 2 in result is reversal of the 2nd col, so to get 1st col as row, we transpose and then reverse it

- Transporse:

![Screenshot Capture - 2022-06-18 - 15-55-06](https://user-images.githubusercontent.com/35686407/174433651-488ce2c0-554f-4e2e-aeb3-6e7460b315d5.png)

```cpp
void Transporse(vector<vector<int>>& matrix){
    for(int i = 0; i < matrix.size(); i++){
        for(int j = 0; j < i ; j++){
            swap(matrix[i][j] , matrix[j][i]);
        }
    }    
}

void rotate(vector<vector<int>>& matrix) {
    Transporse(matrix);
    for(int i = 0; i < matrix.size(); i++){
        reverse(matrix[i].begin(),matrix[i].end());
    }
}
```
