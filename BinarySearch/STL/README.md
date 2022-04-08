# Binary Search Function

```cpp

A[] = {1,4,5,8,9};

bool res = binary_search(a,a+n,3) // false

bool res = binary_search(a,a+n,4) // true

```

# Lower Bound Function

```cpp

a[] = {1,4,5,6,9,9};

int ind = lower_bound(a,a+n,4) - a; // it will return iterator of 4 
// return 1

int ind = lower_bound(a,a+n,7) - a; // it return iterator of next greater element if not exists gives iterator of 9
// return 4

int ind = lower_bound(a,a+n,10) - a; // it return immediate greater to given number if not find then next greter element index
// return 6
```

# Upper Bound Function

```cpp
a[] = {1,4,5,6,9,9};

int ind = lower_bound(a,a+n,4) - a; // it will return iterator of 5 
// return 2

int ind = lower_bound(a,a+n,7) - a; // it return iterator of next greater element of 7 if fount and if not found then also it give next greater element of 7
// return 4

int ind = lower_bound(a,a+n,10) - a; // it return immediate greater to given number if not find then next greter element index is given.
// return 6
```
