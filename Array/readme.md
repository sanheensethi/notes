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
## 8. Merge Intervals 

#### Approach 1: Brute Force
- First check whether the array is sorted or not.
- If not sort the array.
- Now linearly iterate over the array and then check for all of its next intervals whether they are overlapping with the interval at the current index. 
- Take a new data structure and insert the overlapped interval. 
- If while iterating if the interval lies in the interval present in the data structure simply continue and move to the next interval.
- TC : O(NlogN)+O(N*N). O(NlogN) for sorting the array, and O(N*N) because we are checking to the right for each index which is a nested loop.
- SC : O(N), as we are using a separate data structure.

#### Approach 2: Optimal

- sort the intervals
- take ds = interval[0]
- traverse inteval
- if current idx is able to merge with ds , then merge it and go to next interval
- if not possible then, push the ds in ans, and change the ds to current idx
- in last push the ds as last element left
- then return ans

> Intuation:  Since we have sorted the intervals, the intervals which will be merging are bound to be adjacent. We kept on merging simultaneously as we were traversing through the array and when the element was non-overlapping we simply inserted the element in our data structure.

- we can do this problem with stack also, by taking ds as stack and comparing with stack top.

![take U forward - Merge Intervals Leetcode Problem-6 Brute-Optimal C++Java  2JzRBPFYbKE - 853x480 - 6m31s](https://user-images.githubusercontent.com/35686407/174434732-b1ae70b0-55e7-4c8d-96e2-2dacf474a927.png)


```cpp
vector<vector<int>> merge(vector<vector<int>>& intervals) {
    vector<vector<int>> ans;
    vector<int> ds(2);

    int n = intervals.size();

    sort(intervals.begin(),intervals.end());
    ds = intervals[0];

    for(int i = 0; i < n; i++){

        if(intervals[i][0] >= ds[0] && intervals[i][0] <= ds[1]){
            // merge
            ds[1] = max(ds[1],intervals[i][1]);
        }else{
            ans.push_back(ds);
            ds = intervals[i];
        }
    }

    ans.push_back(ds);
    return ans;
}
```
## 9. Merge Two Sorte Arrays in O(1) Space

## 10. Find the Dublicate Number

- Assuming only 1 dublicate is there

#### Appraoch 1 : Sort, and find dublicate

![Screenshot Capture - 2022-06-18 - 23-03-07](https://user-images.githubusercontent.com/35686407/174450023-c542481e-af84-4926-868e-12e6fc006c0c.png)

- TC : O(nLogn)
- SC : O(1)

#### Approach 2: Frequency Array / Map

![Screenshot Capture - 2022-06-18 - 23-04-54](https://user-images.githubusercontent.com/35686407/174450087-f8ba5ae9-60e4-4f70-aa15-65ea5d182ad0.png)

TC : O(n)
SC : O(n)

#### Approach 3: Linked List Cycle Method

- On first we have 2, then at 2nd index we have 9, then at 9th index we have 1, then at 1st index we have 5
- and hum ese hi values ko index maan kr aage bhad rhe hai , isse ek cycle create hoga is number dublicate hoga to,
- ab hum LinKed List jese slow and fast pointer move kr rhe hai
- We have to find the stating node of linked list cycle
- Move Slow and fast Pointer by 1 and 2 speed respectively
- ab move krne ke baad jb vo meet kre, fast ko first position pr rkho and dobara chlao by 1 speed both, 
- jb mile vhi dublicate number hai.

> Intuation: if there is a dublicate, then its sure that it have a cycle.

![take U forward - Find the duplicate number Leetcode C++ and Java Brute-Better-Optimal  32Ll35mhWg0 - 1536x864 - 4m38s](https://user-images.githubusercontent.com/35686407/174450208-c568180a-22be-46d4-91a1-f02cefe0c228.png)

![take U forward - Find the duplicate number Leetcode C++ and Java Brute-Better-Optimal  32Ll35mhWg0 - 1435x807 - 5m03s](https://user-images.githubusercontent.com/35686407/174450211-f6325e93-a6b2-4d1e-a525-1f116469c593.png)

```cpp
int findDuplicate(vector<int>& nums) {
    int slow = nums[0];
    int fast = nums[0];

    do{
        slow = nums[slow];
        fast = nums[nums[fast]];
    }while(slow != fast);


    fast = nums[0];
    while(slow != fast){
        slow = nums[slow];
        fast = nums[fast];
    }
    return slow;
}
```
## 11. Repeat and Missing Number from array

- Find missing and repeating number

![Screenshot Capture - 2022-06-19 - 14-02-21](https://user-images.githubusercontent.com/35686407/174472643-8b4aa926-dda9-419a-a995-5a661181c8c2.png)

#### Approach 1: Freq Array
- Number is between 1 to 6 as array size is 6
- Count Freq, if freq > 2, it's repeateded and if freq = 0 , that is missing number
- TC : O(N) + O(N) = O(2N)
- SC : O(N)

![Screenshot Capture - 2022-06-19 - 14-03-59](https://user-images.githubusercontent.com/35686407/174472695-8ba8257e-b33a-4727-868c-e55fbdb2b3b0.png)

<!-- #### Appraoch 2: Negation of Index (In Interview, avoid this appraoch) -->

#### Approach 2:

- Sum from 1 to N = n(n+1)/2
- Sum from 1^2 to N^2 = (n)(n+1)(2n+1)/6
- Now, Sum 1 to N - Array Sum
- Sum 1^2 to N^2 - Array Square Element Sum
- `X missing Number , Y repeating Number then X - Y = S` S is summition of 1 to N
-  `X^2 - Y^2 = S^2`

![take U forward - Find the Missing and Repeating Number GFG C++ and Java Brute-Better-Optimal-Optimal  5nMGY4VUoRY - 885x498 - 4m36s](https://user-images.githubusercontent.com/35686407/174472840-5ca01407-c651-4e3e-8bbb-02bce047c96a.png)

![take U forward - Find the Missing and Repeating Number GFG C++ and Java Brute-Better-Optimal-Optimal  5nMGY4VUoRY - 853x480 - 5m42s](https://user-images.githubusercontent.com/35686407/174472869-99a00177-f3df-4fe1-824e-6c3f13f9e5b9.png)

> Limitations : As using square, Summition might Exceed.

TC : O(N)
SC : O(1)

```cpp
vector<int> Solution::repeatedNumber(const vector<int> &Arr) {
    #define debug(x) cout<<#x<<":"<<x<<endl;
    long long int A,B;
    long long int Asum = 0;
    long long int ASqSum = 0;
    for(long long int val:Arr){
        Asum += val;
        ASqSum += (val*val);
    }
    long long int n = Arr.size();
    
    long long int sum = (n*(n+1)) / 2;
    long long int sqsum = (n*(n+1)*(2*n + 1)) / 6;
    
    long long int x_minus_y = sum - Asum;
    long long int xsq_minus_ysq = sqsum - ASqSum;
    
    long long int x_plus_y = (xsq_minus_ysq)/(x_minus_y);
    
    A = (x_plus_y + x_minus_y) / 2;
    B = (x_plus_y-x_minus_y) / 2;
    // debug(A);
    // debug(B);
    long long int repeated,missing;
    for(int i = 0; i < n; i++){
        if(Arr[i] == (int)A){
            repeated = A;
            missing = B;
            return {repeated,missing};
        }
        if(Arr[i] == (int)B){
            repeated = B;
            missing = A;
            return {repeated,missing};
        }
    }
}
```

#### Approach 3: XOR Property

- Take XOR of Array, Initialize XOR = 0
- Then XOR the result with 1 to N number we get some result
- XOR result is the result = X ^ Y , X = missing and Y is repeating

Intuation: XOR ARRAY and 1 TO N, you will find X ^ Y = Number, X = missing and Y = repeating

![take U forward - Find the Missing and Repeating Number GFG C++ and Java Brute-Better-Optimal-Optimal  5nMGY4VUoRY - 885x498 - 7m28s](https://user-images.githubusercontent.com/35686407/174473005-445a2abe-c33d-4f67-ac2d-510e6579b528.png)

- Now we seperate the numbers,
- we are sure that both numbers are different
- result - 4 means 1 0 0 
- so either x = 0/1 as first bit from right , or y = 1/0 first bit from right
- So we are sure about that we have some index where bits are different.
- Task is to find set bit rightmost in 4, we know that in result = 4, rightmost set bit is on 2nd index, 
- now we will traverse the array and find whose 2nd bit is set if set then put in one bucket , if not then put it in bucket 2
- Linearly traverse 1 to 6 and again find the 2nd set bit as in 4 2nd bit is set, we put that numbers in bucket.
- then find the xor of buckets,
- one give missing number and one gives repeated number.
- how to find which one is which ? , traverse array again and find.

TC : O()
SC : O()

![take U forward - Find the Missing and Repeating Number GFG C++ and Java Brute-Better-Optimal-Optimal  5nMGY4VUoRY - 885x498 - 11m49s](https://user-images.githubusercontent.com/35686407/174473394-ebaeac6b-9a6f-4114-9e0f-b496962ea093.png)

![take U forward - Find the Missing and Repeating Number GFG C++ and Java Brute-Better-Optimal-Optimal  5nMGY4VUoRY - 853x480 - 13m14s](https://user-images.githubusercontent.com/35686407/174473397-123100b1-3bdd-4a69-bded-07c25f8f6b48.png)

```cpp

```

## 12. Inversion of An Array

![Screenshot Capture - 2022-06-19 - 14-29-09](https://user-images.githubusercontent.com/35686407/174473476-741b4ba2-73de-42ef-a8f3-733b46a418dd.png)

![Screenshot Capture - 2022-06-19 - 14-29-28](https://user-images.githubusercontent.com/35686407/174473493-7b7d8987-ee69-470b-b126-8e2936239b3c.png)

#### Approach 1: Brute Force


#### Approach 2: Merge Sort Technique

![take U forward - COUNT INVERSIONS in an ARRAY Leetcode C++ Java Brute-Optimal  kQ1mJlwW-c0 - 885x498 - 3m18s](https://user-images.githubusercontent.com/35686407/174473593-65482bf7-6374-4554-afb5-4e086ab1990b.png)

- While Meging we modify merge algp

![Screenshot Capture - 2022-06-19 - 14-36-39](https://user-images.githubusercontent.com/35686407/174473735-a22cc3f3-af0c-4204-9d08-fb88576884bb.png)

- while merging 5 and 3, we write 3 and 5, it means 3 is the jth index element which comes first before 5, so every thing on the right of 5 will be greater then 3
- so 3 can be j , and everything on the right of 5 can also be pairs
- here 5,3 is a pair we get 1 inversion

- If you are taking something from the right, so every number right from 3 can make pair with 2

![Screenshot Capture - 2022-06-19 - 14-40-15](https://user-images.githubusercontent.com/35686407/174473873-b7e2d3ca-19b9-4b94-868b-de5f0a812e17.png)

![take U forward - COUNT INVERSIONS in an ARRAY Leetcode C++ Java Brute-Optimal  kQ1mJlwW-c0 - 853x480 - 8m42s](https://user-images.githubusercontent.com/35686407/174473929-5907b79e-1751-4bfe-89ae-8a28ec9fce05.png)

> Note: Jb bhi hum right mae se utha rhe hai merge sort mae se, to jo left vale array ka pointer pda hai, vo or usse aage vale sare pair bnayenge, because right vale index j hai and left vale array ke i hai.

![pasted image 0 (1)](https://user-images.githubusercontent.com/35686407/174473981-0d8871da-46ef-49cc-bf8d-1cd06baf0bac.png)

- The single element is always sorted after slicing to the bottom and getting them on an element as an array. Before returning the merged array with sorted numbers, we will count the inversion from there. How?
- 1st condition i < j above in the image, you can see that the right element’s index is always greater, so while computing the inversion, we should take care only 2nd condition, which is if i < j then A[j] < A[i] to make a pair and add one to the count.
- In the above example i < j as i is the 5’s index and j is 3’s index and (A[i] == 5) > (A[j] == 3) so we got our first inversion pair (5,3) after that merge then into one array [3,5] and return it for further computations now lets take another example:
- [2,3,5] and [1,4] and count = 3. How to calculate it further? 
- Compare elements in 1st array with the 2nd array’s all elements if 1’s array’s element is greater than 2’s array then we will count it as inversion pair as 1st condition for inversion will always satisfy with right arrays. 2 > [1], 3 > [1], 5 > [1,4] so we will get 4 inversion pairs from this. and total inversion pair from [5,3,2,1,4] is 7.

![pasted image 0](https://user-images.githubusercontent.com/35686407/174473963-a24b8bd4-6140-4b10-b88f-834865f43b2c.png)

![take U forward - COUNT INVERSIONS in an ARRAY Leetcode C++ Java Brute-Optimal  kQ1mJlwW-c0 - 1536x864 - 11m26s](https://user-images.githubusercontent.com/35686407/174474269-491b1800-d500-45fe-9f21-76eb2af15538.png)

```cpp
#include <bits/stdc++.h> 
#define debug(x) cout<<#x<<":"<<x<<endl;
long long merge(long long* arr,int n,int start,int mid,int end){
    int N = end-start+1;
    long long B[N];
    int left = start;
    int leftEnd = mid;
    int right = mid+1;
    int rightEnd = end;
 
    int k = 0;
    long long inversion = 0;
    while(left <= leftEnd && right <= rightEnd){
        if(arr[left] <= arr[right]){
            B[k] = arr[left];
            left++;
            k++;
        }else if(arr[right] < arr[left]){
            B[k] = arr[right];
            k++;
            right++;
            inversion = inversion + (leftEnd - left + 1);
        }
    }
  
    while(left <= leftEnd){
        B[k] = arr[left];
        k++;
        left++;
    }
    
    while(right <= rightEnd){
        B[k++] = arr[right++];
    }
    
    k = 0;
    for(int i = start;i <= end;i++){
        arr[i] = B[k++];
    }
    return inversion;
}

long long mergeSort(long long* arr,int start,int end,int n){
    if(start < end){
        long long inversion = 0;
        int mid = start + (end-start) / 2;
        inversion = inversion + mergeSort(arr,start,mid,n);
        inversion = inversion + mergeSort(arr,mid+1,end,n);
        inversion = inversion + merge(arr,n,start,mid,end);
        return inversion;
    }else{
        return 0;
    }
}

long long getInversions(long long *arr, int n){
    return mergeSort(arr,0,n-1,n);
}
```

## 13. Search in a 2D Matrix

> Leetcode Problem Statement , last Element of previous row is samller then first element of current row

> GFS - Row and Col wise Sorted

#### Brute Force : Linear Traversal

TC : O(N x M)
SC : O(1)

#### Appraoch 2: Rows are Sorted,

- Do binary search in each row, 
- if found return true

TC : O(N x LogM)
SC : O(1)

#### Approach 3 : Optimal Appraoch (For GFG)

- we use property, row wise sorted and col wise sorted
- target = 25
- we know everything left from 40 is smaller and bottom its greater
- move pointer to left, 25 < 30 , move pointer to left
- 25 > 20, so move bottom
- 25 > 21, move bottom
- 25 < 29, move left
- Print index or return true

![Screenshot Capture - 2022-06-19 - 15-00-57](https://user-images.githubusercontent.com/35686407/174474603-fe30f568-84cc-4c14-9444-92dec3ba9cf9.png)

- Target = 42
- 42 > 40 , move down
- 42 < 43 , move left
- 42 > 36 , move down
- 42 > 39 , move down
- 42 < 70, move left
- 42 < 60 , move left
- 42 < 50 , move left
- out of bound, no element found

- TC : O(m + n) 
- SC : O(1)

```cpp
int matSearch (int N, int M, int matrix[][M], int x)
{
    int row = 0;
    int col = M-1;
    
    while(row < N && col >= 0){
        if(matrix[row][col] == x){
            return 1;
        }else if(matrix[row][col] < x){
            row++;
        }else if(matrix[row][col] > x){
            col--;
        }
    }
    return 0;
}
```

#### Approach 4 : Optimal Appraoch (for LeetCode)

- 10 > 7

![Screenshot Capture - 2022-06-19 - 15-07-29](https://user-images.githubusercontent.com/35686407/174474828-775a12cf-fa35-4688-adfe-f46f047bee67.png)

- Easy do binary search

1. Using Extra Space, all elements are sorted, do with binary search
    - TC : O(log_(mxn))
    - SC : O(mxn)
  
2. Binary Search first to find the row ~ `target >= m[mid][0] && target <= m[mid][cols-1]` , then binary search to find the col , simple binary search
    - TC : O(log M x log N)
    - Sc : O(1) 

```cpp
int findRow(vector<vector<int>>& matrix,int target){
        int low = 0;
        int high = matrix.size()-1;
        int n = matrix[0].size()-1;
        while(low <= high){
            int mid = (low + high)>>1;
            if(matrix[mid][n] >= target && matrix[mid][0] <= target){
                return mid;
            }else if(matrix[mid][n] < target){
                low = mid+1;
            }else if(matrix[mid][n] > target){
                high = mid-1;
            }
        }
        return -1;
    }
    
    bool findCol(vector<int>& vec,int target){
        int low = 0;
        int high = vec.size()-1;
        while(low <= high){
            int mid = (low+high) >> 1;
            if(vec[mid] == target){
                return true;
            }else if(vec[mid] > target){
                high = mid-1;
            }else if(vec[mid] < target){
                low = mid+1;
            }
        }
        return false;
    }
    
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if(matrix.size()==1 && matrix[0].size()==1){
            return matrix[0][0] == target;
        }
        int row = findRow(matrix,target);
        debug(row);
        if(row == -1){
            return false;
        }
        debug(row);
        bool ans = findCol(matrix[row],target);
        return ans;
    }
```

> 3. Manually write index/ Imagenary Index [IMPORTANT] (Work in LeetCode)

![Screenshot Capture - 2022-06-19 - 15-08-15](https://user-images.githubusercontent.com/35686407/174474847-56edd192-94e1-420c-977c-bd7803e8144c.png)

![Screenshot Capture - 2022-06-19 - 15-09-28](https://user-images.githubusercontent.com/35686407/174474880-a3e36688-0b07-4784-8024-f41de6c12ad9.png)

- From mid, if `row = mid / Tcol` and `col = mid % Tcol`

![take U forward - Search in 2D-MATRIX Leetcode GFG C++ Java Brute-Better-Better-Optimal  ZYpYur0znng - 797x498 - 11m30s](https://user-images.githubusercontent.com/35686407/174475077-163638a6-4a29-45bc-a6d4-7337eab3ddc9.png)

- TC : O(log_2(N x M))
- SC : O(1)

```cpp
class Solution {
public:
    #define debug(x) cout<<#x<<":"<<x<<endl;
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        
        int n = matrix.size();
        int m = matrix[0].size();
        
        int low = 0;
        int high = n*m - 1;
        
        while(low <= high){
            int mid = low + (high-low)/2;
            
            int row = mid/m;
            int col = mid%m;
            
            if(matrix[row][col] == target){
                return true;
            }else if(matrix[row][col] > target){
                high = mid-1;
            }else{
                low = mid+1;
            }
        }
        return false;
    }
};
```

## 14. POW(X,N)

![Screenshot Capture - 2022-06-19 - 15-16-47](https://user-images.githubusercontent.com/35686407/174475232-4876a34e-4718-4e02-9470-545c1a99aa21.png)

- Can value of N is negative ?
- N is integer

#### Brute Force 

- Looping from 1 to n and keeping a ans(double) variable. Now every time your loop runs, multiply x with ans. At last, we will return the ans.

> For Negative Number

![Screenshot Capture - 2022-06-19 - 15-19-02](https://user-images.githubusercontent.com/35686407/174475305-078feb1e-ead6-460b-83d3-19b2b97819dc.png)

Limitation : 

![Screenshot Capture - 2022-06-19 - 15-19-37](https://user-images.githubusercontent.com/35686407/174475335-2646821e-8553-4586-9a7c-c99ae7f7aa26.png)

- if negative n is given INT_MIN, and if you make it positive, OVERFLOW ERROR EDGE CASE, Take long or long long

TC : O(n)
SC : O(1)

#### Optimal (Binary Exponention)

![Screenshot Capture - 2022-06-19 - 15-22-28](https://user-images.githubusercontent.com/35686407/174475452-f978d8a8-c703-41a8-86d6-407f4cdcfdd9.png)

![Screenshot Capture - 2022-06-19 - 15-23-58](https://user-images.githubusercontent.com/35686407/174475509-57e46306-d14a-46b9-b1a8-8a972e6b429c.png)

![Screenshot Capture - 2022-06-19 - 15-24-16](https://user-images.githubusercontent.com/35686407/174475520-33725f74-6922-4580-843f-4a9cda66d168.png)

- n == 0, return 1
- TC : log_2(N)

> Recursive:

```cpp
double pow(double x,int n){
    if(n == 0) return 1.0;

    if((n&1)){
        return x*pow(x,n-1);
    }else{
        double p = pow(x,n/2);
        return p*p;
    }
}

double myPow(double x, int n) {

    if(x == 1) return x;
    if(x == -1) return (n&1) ? -1 : 1;

    if(n <= INT_MIN || n >= INT_MAX) return 0;

    if(n > 0) return pow(x,n);

    return 1.0/pow(x,-n);

}
```

> Iterative:

- n ~ odd :  ans*x ; n = n-1 
- n ~ even : x = x*x ; n = n/2

```cpp
double pow(double x,int n){
    if(n == 0) return 1;

    double res = 1.0;
    while(n!=0){
        if((n&1)){
            // odd
            res = res * x;
            n = n-1;
        }else{
            // even
            x = x * x;
            n = n/2;
        }
    }
    return res;
}
```

## 15. Majority Element (>N/2 times)

#### Appraoch 1: Brute Force

- Check the count of occurrences of all elements of the array one by one. Start from the first element of the array and count the number of times it occurs in the array. 
- If the count is greater than the floor of N/2 then return that element as the answer. 
- If not, proceed with the next element in the array and repeat the process.
- Time Complexity: O(N^2) 
- Space Complexity: O(1)

#### Approach 2: Better (use Extra space, hashmap)

- Store the freq of each element in hashmap
- the element whose freq > N/2 times is my ans
- TC : O(n)
- SC : O(N)

#### Approach 3: Optimal (Moore’s Voting Algorithm)

> Algorithm:

- count = 0, ele = 0
- if count == 0 , ele = nums[i]
- if ele = nums[i] count++;
- else count--;
- return ele (majority element)

> Intuation:

- algo ki intuation ye hai ki, pehli baat hme ye kha gya hai ki majority element exist krta hai
- is algo mae hum , distinct elements ka pair bnane ki koshish kr rhe hai
- ![Screenshot Capture - 2022-06-20 - 10-57-38](https://user-images.githubusercontent.com/35686407/174531150-0ec01e11-7003-4c6b-92d5-ffb81bb8baf3.png)
- ab hum ye maan kr chl rhe hai ki current element is majority element, to count++ se vo increase ho rhe hai,
- or jb koi alag element milta hai to count-- kr rhe hai, isse ye pta chlta hai ki , jitne bhi abhi tk element mile hai, usme majority element = minority element hai, to jb bhi 0 aata hai, to iska mtlb mera majority element suffix mae present hai current 0 se, kyuki, majority element > n/2 hai, to agar vo ek moment pr 0 ho rha hai to iska mtlb vha tk majority = minority the, and majority element ki bhi surity hai ki vo hoga, to iska mtlb vo current count 0 ke aage vale suffix mae present krta hai.

![take U forward - Majority Element Leetcode C++ Java Brute-Better-Optimal Moore's Voting Algorithm  AoX3BPWNnoE - 797x498 - 9m41s](https://user-images.githubusercontent.com/35686407/174532935-8d30f911-c452-4405-936a-5eb4bc9473d9.png)

```cpp
int majorityElement(vector<int>& nums) {
    int count = 0;
    int ele = 0;
    for(int i = 0; i < nums.size(); i++){
        if(count == 0) ele = nums[i];
        if(ele == nums[i]) count++;
        else count--;
    }
    return ele;
}
```
