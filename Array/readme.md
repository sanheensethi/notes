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

![image](./image/autodraw 3_12_2021.png?raw=true)
