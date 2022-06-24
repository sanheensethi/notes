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

## 6. Nth root of a number

![take U forward - Nth Root of a Number Using Binary Search  WjpswYrS2nY - 1536x864 - 0m18s](https://user-images.githubusercontent.com/35686407/175467366-ca9976e3-54a9-4db3-b32e-4157ac60f9ef.png)

- Nth root of M, and number of decimal places will be given

