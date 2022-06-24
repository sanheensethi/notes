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
if(index != n && a[index] == x) cout<<index<<endl; /* index = 1 */
else cout<<-1<<endl;
```

```cpp
a[] = {1,4,4,4,4,9,9,10,11};

int x = 2;

int index = lower_bound(a,a+n,x) - a;

/* lower bound of 2 gives iterator of 4 , it means 2 does not exists, therefore we apply check */
/* a[index] == x */

/* for x = 12, it gives idex = n, we have to print -1, therefore we put check index != n */
```
