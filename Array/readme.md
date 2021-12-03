# Array

## Subarray/Substring:

- A subarray is a contiguous part of array. An array that is inside another array.
- For example, consider the array [1,2,3,4], There are 10 non-empty sub-arrays.
- The subarrays are (1), (2), (3), (4), (1,2), (2,3), (3,4), (1,2,3), (2,3,4) and (1,2,3,4)
- In general, for an array/string of size n, there are n*(n+1)/2 non-empty subarrays/substrings.

**How to generate all subarrays?**
We will run 3 nested loops,
1.  the outer loop(1st loop) picks starting element
2.  the inner loop(2nd loop) picks the ending element
3.  the innermost loop(3rd loop) print the values between i and j

```cpp
int arr[] = {1,2,3,4,5};
int n = 5;
for(int i=0;i<n;i++){ // starting point
  for(int j=0;j<n;j++){ // ending point
    for(int k=i;k<=j;k++){ // start to end printing
      cout<<arr[k]<<" ";
    }
    cout<<endl;
  }
}
```

![image](https://raw.githubusercontent.com/sanheensethi/notes/main/Array/image/autodraw%203_12_2021.png?token=AIQIQB7DV3QTC752VD7SLC3BVGTCK)
