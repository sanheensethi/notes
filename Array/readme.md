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
