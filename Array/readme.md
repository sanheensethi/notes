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

