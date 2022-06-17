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

![image](https://raw.githubusercontent.com/sanheensethi/notes/main/Array/image/autodraw%203_12_2021.png?token=AIQIQB7X4VB3YXU47JOPROTBVGXUM)

## Power Set:

- Power Set Power set P(S) of a set S is the set of all subsets of S. For example S = {a, b, c} then P(s) = {{}, {a}, {b}, {c}, {a,b}, {a, c}, {b, c}, {a, b, c}}.
- If S has n elements in it then P(s) will have 2^n elements

```cpp
Algorithm:
Input: Set[], set_size
1. Get the size of power set
    powet_set_size = pow(2, set_size)
2  Loop for counter from 0 to pow_set_size
     (a) Loop for i = 0 to set_size
          (i) If ith bit in counter is set
               Print ith element from set for this subset
     (b) Print separator for subsets i.e., newline
     
Set  = [a,b,c]
power_set_size = pow(2, 3) = 8
Run for binary counter = 000 to 111

Value of Counter            Subset
    000                    -> Empty set
    001                    -> a
    010                    -> b
    011                    -> ab
    100                    -> c
    101                    -> ac
    110                    -> bc
    111                    -> abc
```

```cpp
void printPowerSet(char *set, int set_size)
{
    /*set_size of power set of a set with set_size
    n is (2**n -1)*/
    unsigned int pow_set_size = pow(2, set_size);
    int counter, j;
 
    /*Run from counter 000..0 to 111..1*/
    for(counter = 0; counter < pow_set_size; counter++)
    {
    for(j = 0; j < set_size; j++)
    {
        /* Check if jth bit in the counter is set
            If set then print jth element from set */
        if(counter & (1 << j))
            cout << set[j];
    }
    cout << endl;
    }
}
```

![image](https://raw.githubusercontent.com/sanheensethi/notes/main/Array/image/autodraw%203_12_2021(1).png?token=AIQIQB2AFDEV7VIOXZPF7ALBVGXUO)

![image](https://raw.githubusercontent.com/sanheensethi/notes/main/Array/image/autodraw%203_12_2021(2).png?token=AIQIQB7IQBZGEBOHZYRX4OTBVGXUO)

## Subsequence:

- A subsequence is a sequence that can be derived from another sequence by zero or more elements, without changing the order of the remaining elements. 
- For example, consider the array [1,2,3,4],  there are 15 sub-sequences. 
- They are (1), (2), (3), (4), (1,2), (1,3),(1,4), (2,3), (2,4), (3,4), (1,2,3), (1,2,4), (1,3,4), (2,3,4), (1,2,3,4).
-  More generally, we can say that for a sequence of size n, we can have (2n-1) non-empty sub-sequences in total. 

> Note:  Every subarray is a subsequence. More specifically, Subsequence is a generalization of substring.
