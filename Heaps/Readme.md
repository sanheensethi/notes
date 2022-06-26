# Heaps

## How to Know Heap Problem ?

1. `K` is given
2. Smallest / Largest will be asked

## Which heap to choose ? max-heap / min-heap

1. K + smallest = max heap
2. K + largest = min heap

e.g. K-th largest element - heap of size K, then top element is K-th largest element.

## Significance of K

1. Heap Question ~ Sorting Question
2. Sorting done in nlogn
3. so, with the help of heap , we try to reduct TC : O(nlogk)

## 1. K-th Smallest Element in array.

- K given, Smallest ask, ~ max heap of size k
- smallest manga hai, to smaller number ko bchana hai, bdo ko uda dena hai, to udane ke liye bde top pr chahiye to max heap

![Screenshot of Welcome Board _ Sketchboard](https://user-images.githubusercontent.com/35686407/175803511-584b5ac3-6515-4c5a-8a0c-56cadec9f36a.jpg)

![Screenshot of Welcome Board _ Sketchboard (1)](https://user-images.githubusercontent.com/35686407/175803594-b88a10ae-cbcd-4d32-ae3a-2dff0aeda0e7.jpg)

```cpp
int kthSmallest(int arr[], int l, int r, int k) {
      int n = r - l + 1;
      priority_queue<int> pq;
      for(int i = 0; i < n; i++){
          pq.push(arr[i]);
          if(pq.size() > k) pq.pop();
      }
      return pq.top();
  }
```
## 2. K-th Largest Element in array

- k given, Largest Ask ~ min Heap

![Screenshot of Welcome Board _ Sketchboard (2)](https://user-images.githubusercontent.com/35686407/175804056-d623597f-cb75-40cf-8c61-af7017bdccad.jpg)

```cpp
int findKthLargest(vector<int>& nums, int k) {
  // max heap

  priority_queue<int,vector<int>,greater<int>> pq;

  for(auto& val:nums){
      pq.push(val);
      if(pq.size() > k) pq.pop();
  }

  return pq.top();
}
```
