## Binary Search


## 1. STL

> Check if X exists in sorted array or not

```cpp
a[] = {1,4,5,8,9};

bool res = binary_search(a,a+n,3); // false

bool res = binary_search(a,a+n,4); // true
```

> Lower Bound Function

- return the first element iterator if it occurs
- it it does not occur, then it return next greater element iterator of the given element

```cpp
a[] = {1,4,5,6,9,9};

lower_bound(a,a+n,4); // iterator point at 4

lower_bound(a,a+n,7); // iterator point at next greater element of 7, as it's not present in array.

lowe_bound(a,a+n,10); //  iterator point at next greater element of 10, but 9 is largest number, so it point to end of array after last 9.
```

- Find Index from lower_bound

```cpp
// a is begin iterator
int idx = lower_bound(a,a+n,4) - a; // ~ 1
int idx = lower_bound(a,a+n,7) - a; // ~ 4
int idx = lower_bound(a,a+7,10) - a; // ~ 6

/* In Vectors */
int idx = lower_bound(a.begin(),a.end(),4) - a.begin();
```

> Upper Boud Function

- return the next greater element of x, wheather x is present in array or not.

```cpp
a[] = {1,4,5,6,9,9};

upper_bound(a,a+n,4); // it returns the iterator next greater to 4, i.e, iterator of 5

upper_bound(a,a+n,7); // it returns the iterator next greater to 7 , i.e. iterator of first 9

upper_bound(a,a+n,10); // end iterator , 10 not exists big element is 9, 10 lies always outside the array.

/* Finding index and for vectors , it is same as lower bound. */
```

## 2. Find the first occurace of X in a sorted array. If it does not exists, print -1.

```cpp
a[] = {1,4,4,4,4,9,9,10,11};

int x = 4;

int index = lower_bound(a,a+n,x) - a;
if(index != n && a[index] == x) return index /* index = 1 */
else return -1;
```

```cpp
a[] = {1,4,4,4,4,9,9,10,11};

int x = 2;

int index = lower_bound(a,a+n,x) - a;

/* lower bound of 2 gives iterator of 4 , it means 2 does not exists, therefore we apply check */
/* a[index] == x */

/* for x = 12, it gives idex = n, we have to print -1, therefore we put check index != n */
```

## 3. Find the last occurance of X in a sorted array. If it does not exists, print -1. (STL)

```cpp
a[]  = {1,4,4,4,4,9,9,10,11};

int x = 4;
int index = upper_bound(a,a+n,x) - a; // upper bound gives the index of next greater element to it, i.e., 9, therefore we have to do index--;
index--;
if(index >= 0 && a[index] == x) return index;
else return -1;

/* x = 0, it might happen that upper bound point to index = 0, so when index--, it goes to -1 point, which gives runtime error, so index >= 0 is check*/
/* x = 2 , it points to 4 move back ie., 1 but not equal to 2 therefore check for a[index] == x*/
```

## 4. Find the largest Number which is smaller then x (STL)

```cpp
a[] = {1,4,4,4,4,9,9,10,11};

int x = 4
int index = lower_bound(a,a+n,x) - a;
index--; // a[index] is largest number, as before it, all numbers are small as array is sorted.
if(index >= 0) return a[index];
else return -1;
```

## 5. Find the smallest Number greater then x (STL)

```cpp
a[] = {1,4,4,4,4,9,9,10,11};

int x = 4;
int index = upper_bound(a,a+n,x) - a; // upper bound always points to next greater element
if(index < n) return index;
else return -1;
```

> Note : Binary Search is not limited to finding an element, It is implemented to any search space where it is monotonic in nature, linearly increasing or decreasing.

## 6. Nth root of a number

![Screenshot Capture - 2022-06-24 - 11-27-59](https://user-images.githubusercontent.com/35686407/175471987-8d2638ac-d30e-4ded-9b4a-9a8c72d910d3.png)

- Above is monotonic increasing, here we can apply binary search.

![take U forward - Nth Root of a Number Using Binary Search  WjpswYrS2nY - 1536x864 - 0m18s](https://user-images.githubusercontent.com/35686407/175467366-ca9976e3-54a9-4db3-b32e-4157ac60f9ef.png)

- Nth root of M, and number of decimal places will be given

- Find the search space

![Screenshot Capture - 2022-06-24 - 11-28-49](https://user-images.githubusercontent.com/35686407/175472115-08795248-f021-4a7c-8b7b-471a7d50cc29.png)

![Screenshot Capture - 2022-06-24 - 11-29-05](https://user-images.githubusercontent.com/35686407/175472146-e5cf0c3d-0a0b-4bf9-9cf5-8df84aafd3c7.png)

- Now apply Binary Search

![Screenshot Capture - 2022-06-24 - 11-29-54](https://user-images.githubusercontent.com/35686407/175472257-ad0e505d-f31a-43f4-89cc-69c9d3523cd5.png)


- find the search space
- applhy binary search, find mid,
- reduce search space if 3rd root mid*mid*mid > targer ~ [1 ... mid]

![Screenshot Capture - 2022-06-24 - 11-31-40](https://user-images.githubusercontent.com/35686407/175472485-639c3798-e170-46df-b35a-1ff98c893347.png)

> How long we have to shrik search space ?

![Screenshot Capture - 2022-06-24 - 11-32-57](https://user-images.githubusercontent.com/35686407/175472670-a200ce54-e49c-45c8-b854-04479e6103bc.png)

- shrik search space untill difference between high and low if 5 decimal places, |high-low| > 10e-6

![Screenshot Capture - 2022-06-24 - 11-34-36](https://user-images.githubusercontent.com/35686407/175472855-3e7e8701-1d37-4a43-bd91-3d3fe203f9a4.png)

![take U forward - Nth Root of a Number Using Binary Search  WjpswYrS2nY - 885x498 - 15m39s](https://user-images.githubusercontent.com/35686407/175473522-51b0a367-0556-43d9-ac32-b507d50f570d.png)

TC : O(N x log_2(m x 10^d)), n times we multiply.
SC : O(1)

## 7. Median of Row wise Sorted Matrix

![Screenshot Capture - 2022-06-24 - 12-40-17](https://user-images.githubusercontent.com/35686407/175482464-abeec89c-e360-48b8-ad7e-4be10d7b190a.png)

- write all the intergers in sorted order, middle element is 6,
- constraint : all array elements is 1 to 10^9 , it can vary.

![Screenshot Capture - 2022-06-24 - 12-41-17](https://user-images.githubusercontent.com/35686407/175482577-e6326ace-88ed-4f4b-8ef0-579643b4a4d9.png)

#### Appraoch 1: Iteratre and Extra DS

- Create a ds, and put every element
- then sort
- middle index = median of matrix
- TC : O(n x m) + (n x m) log(n x m)
- SC : O(n x m)

#### Approach 2: Binary Search

> binary search can be implemented in any search space if it is monotonic in nature

- median will be an integer between 1 to 10^9
- this is search space

- as there are 9 elements in total, 1 2 3 3 5 6 6 9 9
- median = 5, here you can see, left of median there are 4 elements and in right of median there are 4 elements
- so number of elements < 5 = 9/2 = 4
- so, what if we can figure out number of smaller elements from a number which is considered to be median,
- if number of elements > 4, it means, that will not be our median kyuki hme median ke left mae n elements and median ke right mae n elements chahiye, where n = r*c/2, so high = mid-1
- else low = mid+1
- ans is low.

![Screenshot Capture - 2022-06-24 - 12-46-07](https://user-images.githubusercontent.com/35686407/175483348-8577f3a8-5e3f-42eb-8070-a4a2c58260ea.png)

```cpp
class Solution{   
public:
    
    int numEle(vector<vector<int>>& matrix,int& num){
        int n = matrix.size();
        int sum = 0;
        for(int i = 0; i < n; i++){
            sum += upper_bound(matrix[i].begin(),matrix[i].end(),num)-matrix[i].begin();
        }
        return sum;
    }

    int median(vector<vector<int>> &matrix, int r, int c){
        int low = 0;
        int high = 2000;
        int n = (r*c)/2;
        while(low <= high){
            int mid = (low + high)/2;
            int nele = numEle(matrix,mid);
            if(nele <= n){
                low = mid+1;
            }else{
                high = mid-1;
            }
        }
        return low;
    }
};
```
> Q1) Why r and c are always odd?

- If r and c both are odd then this means that number of elements int the matrix will also be odd which is actually necessary for binary search to be applicable here(only in this problem, binary serach works for both even and odd elements arrays when the array is linear but not here). Because here we are judging by considering the fact that no of elements less than or equal to current number, which in case of even no of elements can be a number which is not present in the matrix. Having odd number of elements has a property that the middle element is cleary defined (a single mid) so number of elements to the left of it and right of it will be equal but in case of even population we can sometime have a median element which is 
not present in the array which will not be possible to find in case of a matrix like this without traversing all the elements.

This method will give wrong result for even number of elements so let's not worry about it.

> Q2) Why half = (r * c) / 2 and not (r * c + 1) / 2 as no of elements are odd and we know middle for odd is (n + 1) / 2 ?

- To this I will reply that the condition if (cnt <= half) { low = mid + 1;  } will move the search space to the right even if we get a mid for which cnt == half this means it will never consider the element just left of the median and since we are considering the low as our answer after we break out of the loop it will always give us the right median as when we are less then median  we are pushed to right and when we have more than half then we are pushed to the left even when we have already found out the median element still loop will not terminate until our search space has only one elment left i.e the median itself.

## 8. Single Element in Sorted Array

#### Appraoch 1: XOR all elements and find the ans.

#### Approach 2: If elements are already sorted, we can use binary search

- we have to find the break point, break point is yellow line
- left of break point , all the elements appear twice
- right of break point, single element is there, and then all the elements to right appear twice.

![take U forward - Single Element In Sorted Array Leetcode  PzszoiY5XMQ - 885x498 - 3m16s](https://user-images.githubusercontent.com/35686407/175515422-d60fd372-eaaa-4568-8046-5b85b6850059.png)

> Observation:

- Right
    - 4 first instance at odd index
    - 4 second instance at even index

- Left
    - 1 first instance at even index
    - 1 second instacnce at odd index

![take U forward - Single Element In Sorted Array Leetcode  PzszoiY5XMQ - 853x480 - 3m08s](https://user-images.githubusercontent.com/35686407/175515865-a4a6538b-cea7-4bf7-b834-374199fcdd79.png)


- we will check for left half,
- if it is left half , low = mid+1;
- else if it is right half , high = mid-1;

> Why high = size-2;

![Screenshot Capture - 2022-06-24 - 15-52-23](https://user-images.githubusercontent.com/35686407/175516048-ff640816-24da-4d7e-9aa1-6efaf30f1ac0.png)

- in above, while shrinking the left half, automatically low goes to the last element which is single element, hence we start it with 2;
- if we take high = size-1 , then low goes out of bound, which is wrong as we consider low is our ans.

```cpp
int singleNonDuplicate(vector<int>& arr) {
    int low = 0;
    int high = arr.size()-2;
    while(low <= high){

        int mid = (low+high)/2;

        // check for left half
        if(mid%2 == 1){
            // odd
            if(arr[mid-1] == arr[mid]){
                // it is left half
                low = mid+1;
            }else{
                // it is right half
                high = mid-1;
            }
        }else if(mid%2 == 0){
            // even
            if(arr[mid+1] == arr[mid]){
                // it is left half
                low = mid+1;
            }else{
                // it is right half
                high = mid-1;
            }
        }
    }
    return arr[low]; 
}
```
#### Simple Trick to avoid Multiple IF ELSE Statements (Usign ^ xor operator)

if mid = 4 , then 4 ^ 1 = 5
if mid = 5, then 5 ^ 1 = 4
if mid = 3, then 3 ^ 1 = 2
if mid = 2, then 2 ^ 1 = 3

- we have to check this actually, if mid is odd, then it is 2nd occurance, then first occuranve is prev even index, mid^1 give prev even index
- if mid is even , then it is 1st occufrance, then second occurance is next odd index , mid^1 also gives next odd index, if mid is even

```cpp
int singleNonDuplicate(vector<int>& arr) {
    int low = 0;
    int high = arr.size()-2;
    while(low <= high){

        int mid = (low+high)/2;

        // check for left half
        if(arr[mid] == arr[mid^1]){
            low = mid+1;
        }else{
            high = mid-1;
        }
    }

    return arr[low]; 
}
```

## 9. Search Element in Rotated Sorted Array !

![Screenshot Capture - 2022-06-24 - 16-41-04](https://user-images.githubusercontent.com/35686407/175525480-b7c0da34-a292-46ef-bd32-4f4908eca96b.png)

![Screenshot Capture - 2022-06-24 - 16-42-42](https://user-images.githubusercontent.com/35686407/175525312-d5f95fd0-6204-490a-8153-acfc2e8f03aa.png)

- isme rotated sorted array hai,
- to ek trf se jb hum mid niaklenge, ya to left half sorted hoga ya fr right half sorted hogga.
- to conditions esi hia :
    1. mid hi target hai, to return mid
    2. check left half is sorted ? , a[low] <= a[mid] , if yes, then check target lies in left half ? , target >= a[low] && target <= a[mid] , if yes, then high = mid-1 else low = mid+1
    3. if left half is not sorted ,  then it means right half is sorted, so just check target lies in right half ? target >= a[mid] && target ,= a[high]. if yes then low = mid+1 , else high = mid-1; 



```cpp
int search(vector<int>& nums, int target) {
    int low = 0;
    int high = nums.size()-1;
    while(low <= high){
        int mid = (low+high) >> 1;

        if(nums[mid] == target) return mid;

        // check left half is sorted 
        if(nums[low] <= nums[mid]){
            // left half sorted. check target lies in it ?
            if(nums[low] <= target && target <= nums[mid]){
                high = mid-1;
            }else{
                low = mid+1;
            }
        }
        // right half is sorted
        else{
            // right half, check target lies in it ?
            if(nums[mid] <= target && target <= nums[high]){
                low = mid+1;
            }else{
                high = mid-1;
            }
        }
    }
    return -1;
}
```

## 10. Median of Two Sorted Arrays

#### Naive Solution: Merging same as merge sort

- mege the two sorted arrays, in another ds/vector
- then find the median
- TC : O(m+n) + O(1)
- SC : O(m+n)

#### Better Naive :

- Instead of storing in another ds, we know at which position numbers i have to take for median,
- so create a count variable, by taking an element just count that , when you got required count, find the median and return
- TC : O(m+n)
- SC : O(1)

#### Optimized Solution : Binary Search

- isme hum partitions krenge,
- median nikalne ke liye agar total element even hai, to left half and right half mae same number of elements hote hai
- if total elements odd hai to left half mae element jayeda hota hai as compared to right half
- jo sorted array hota hai after merging, uska left half ka max and right half ka min agar inka average nikale to vo hme median deta hai, in case of total element even
- if total element = odd , jo sorted array hota hai after merging usme keft half ka jo max element hota hai vo hme median deta hai.

> -

- ab hum bina merge kre ye try krne ki koshish kr rhe hai ki , hum left half and right half nikal paye, such that in left half, all elements are smaller then right half
- to esa krne ke liye sbse pehle hme dekhna hoga ki left half mae max kitne element rkh skte hai, ~ totalElement / 2 in case of even , totalElement / 2 + 1 in case of odd
- to ek to trika hai, ki smaller array mae se hum, 1 / 1 krke element bhadaye and check kre ki kya valid partition ho gyi hai ?
- ya dusra trika hai ki hum binary search se pehle find kre ki kha partition krna hai, fr check kre kya shi partition to hai na.

![undefined-1656139317755](https://user-images.githubusercontent.com/35686407/175761883-86d6bace-bea2-4f55-9d42-d0d2aa5d356d.jpg)

![undefined-1656139336654](https://user-images.githubusercontent.com/35686407/175761888-db09a4e5-6a77-4f97-8b0d-eec73c703a61.jpg)

- Upar linearly elements utha rhe hai.
- for valid partition, we have to cross checks some condition, in picture below:
- if valud return the median

![undefined-1656139606434](https://user-images.githubusercontent.com/35686407/175762017-934549f7-e1fe-4bbd-b847-4dfc60a041b2.jpg)

![Pepcoding - Median of Two Sorted Arrays - Optimised Approach Leetcode 4 Solution Searching and Sorting  jDJuW7tSxio - 853x480 - 29m00s](https://user-images.githubusercontent.com/35686407/175762072-ecbc2874-b109-41f7-8d9a-fd73932e1c01.png)

> Important Note

- Do the binary search on smaller size array
- before accessing mid-1 / mid / bel / bel - 1, check that they are valid index or not,
- if not, for left partition , l1 and l2 set it to INT_MIN
- and for right partititon, r1 and r2 set it to INT_MAX

```cpp
class Solution {
public:
    #define debug(x) cout<<#x<<":"<<x<<endl;
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        
        if(nums1.size() > nums2.size()){
            swap(nums1,nums2);
        }
        
        // nums1 always has smaller
        
        // binary search on smaller;
        
        int low = 0;
        int high = nums1.size();
        int total = nums1.size() + nums2.size();
        
        while(low <= high){
            
            int mid = (low + high)/2; // no. of elements in left part
            int bel = (total+1)/2 - mid; // index before all elements are in left part
            
            // valid partition / segregate
            
            int l1 = mid-1 >= 0 ? nums1[mid-1] : INT_MIN;
            int l2 = bel-1 >= 0 ? nums2[bel-1] : INT_MIN;
            int r1 = mid < nums1.size() ? nums1[mid] : INT_MAX;
            int r2 = bel < nums2.size() ? nums2[bel] : INT_MAX;

            
            if(l1 <= r2 && l2 <= r1){
                //find median
                if((total&1)){
                    return (double)max(l1,l2);
                }else{
                    return ((double)(max(l1,l2) + min(r1,r2)))/2.0;
                }
            }else if(l1 > r2){
                high = mid-1;
            }else if(l2 > r1){
                low = mid+1;
            }
        }
        return 0;
    }
};
```
## 11. K-th Element of Two Sorted Arrays

#### Better Naive : Megring Two Sorted arrays, as we do in merge sort

- Instead of storing in another ds, we know at which position numbers i have to take for median,
- so create a count variable, by taking an element just count that , when you got required count, find the median and return
- TC : O(k)
- SC : O(1)
![Screenshot Capture - 2022-06-25 - 12-22-48](https://user-images.githubusercontent.com/35686407/175762253-2a4368f0-4ccc-4478-9a38-cc0a385652b2.png)

![Screenshot Capture - 2022-06-25 - 12-23-01](https://user-images.githubusercontent.com/35686407/175762256-11239a6b-1305-489f-9f5a-cb373007a60c.png)

#### Appraoch 2 : GFG Blog

#### Approach 3: log(min(n,m)) solution , Same concept of merge two sorted arrays

- in this K is given, so we make partiton such that in left partiton there are K elements.

```cpp
class Solution{
    public:
    int kthElement(int nums1[], int nums2[], int n, int m, int K)
    {
        if( n > m ){
            return kthElement(nums2,nums1,m,n,K);
        }
        // num1 is smaller
        int low = max(0,K-m);
        int high = min(K,n);
    
        while(low <= high){
            int mid = (low+high)/2;
            int bel = K - mid;
    
            int l1 = mid-1 >= 0 ? nums1[mid-1] : INT_MIN;
            int l2 = bel-1 >= 0 ? nums2[bel-1] : INT_MIN;
            int r1 = mid < n ? nums1[mid] : INT_MAX;
            int r2 = bel < m ? nums2[bel] : INT_MAX;
    
            if(l1 <= r2 && l2 <= r1){
                return max(l1,l2);
            }else if(l1 > r2){
                high = mid-1;
            }else if(l2 > r1){
                low = mid+1;
            }
    
        }
        return -1;
    }
};
```
## 12. Allocate Minimum Number of Pages 

```cpp
class Solution 
{
    private:
    bool isPossible(int A[],int N,int maxPages,int students){
        int stu = 1;
        int pages = 0;
        for(int i = 0; i < N; i++){
            if(A[i] > maxPages) return false;
            if(pages + A[i] <= maxPages){
                pages += A[i];
            }else{
                stu++;
                pages = A[i];
            }
        }
        if(stu <= students) return true;
        return false;
    }
    public:
    //Function to find minimum number of pages.
    int findPages(int A[], int N, int M) 
    {
        int low = A[0];
        int high = 0;
        for(int i = 0 ; i < N;i++) high += A[i];
        int ans;
        while(low <= high){
            int mid = low + (high-low)/2;
            if(isPossible(A,N,mid,M)){
                ans = mid;
                high = mid-1;
            }else{
                low = mid+1;
            }
        }
        return ans;
    }
};
```
## 13. Aggressive Cows

```cpp
bool canPlace(vector<int>& stalls,int minDist,int k){
    int cow = 1;
    int cord = stalls[0];
    for(int i = 1; i < stalls.size(); i++){
        if(stalls[i] - cord >= minDist){
            cow++;
            cord = stalls[i];
        }
        if(cow == k) return true;
    }
    return false;
}

int aggressiveCows(vector<int> &stalls, int k)
{
    sort(stalls.begin(),stalls.end());
    int n = stalls.size();
    int low = 0;
    int high = stalls[n-1] - stalls[0];
    
    int ans;
    while(low <= high){
        int mid = (low + high) >> 1;
        if(canPlace(stalls,mid,k)){
            ans = mid;
            low = mid+1;
        }else{
            high = mid-1;
        }
    }
    return ans;
}
```
## 14. First Index of an Element

```cpp
int firstIndex(vector<int>& arr,int target){
    int n = arr.size();
    int low = 0;
    int high = arr.size()-1;
    int ans = -1;

    while(low <= high){
        int mid = (low+high)>>1;
        if(arr[mid] == target){
            ans = mid;
            high = mid-1;
        }else if(arr[mid] > target){
            high = mid-1;
        }else if(arr[mid] < target){
            low = mid+1;
        }
    }
    return ans;
}
```

## 15. Last Index of an Element

```cpp
int lastIndex(vector<int>& arr,int target){
    int n = arr.size();
    int low = 0;
    int high = arr.size()-1;
    int ans = -1;

    while(low <= high){
        int mid = (low+high)>>1;
        if(arr[mid] == target){
            ans = mid;
            low = mid+1;
        }else if(arr[mid] > target){
            high = mid-1;
        }else if(arr[mid] < target){
            low = mid+1;
        }
    }
    return ans;
}
```
## 16. Count Occurance of Element in sorted array

```cpp
int count(int arr[], int n, int x) {
    int f = firstIndex(arr,n,x);
    if(f == -1) return 0;
    int l = lastIndex(arr,n,x);
    return l-f+1;
}
```
## 17. How Many Times Array is rotated:

TestCases:
- [3,4,5,1,2]
- [4,5,6,7,0,1,2]

```cpp
int pivotIndex(vector<int>& arr){
    int low = 0;
    int high = arr.size()-1;
    int ans;
    int n = arr.size();

    while(low <= high){
        if(arr[low] <= arr[high]) return low; // important line

        int mid = (low + high) >> 1;
        int prev = (mid+n-1) % n;
        int next = (mid + 1)% n;

        if(arr[mid] < arr[prev] && arr[mid] < arr[next]){
            return mid;
        }else if(arr[low] <= arr[mid]){
            low = mid+1;
        }else if(arr[mid] <= arr[high]){
            high = mid-1;
        }
    }

    return -1;
}
```

## 18. Minimum element in rotated sorted array

```cpp
int findMin(vector<int>& nums) {
    int idx = pivotIndex(nums);
    return nums[idx];
}
```

## 19.
