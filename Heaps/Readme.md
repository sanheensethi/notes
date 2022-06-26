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
## 3. Sort Nearly Sorted Array / K Sorted Array

- isme bola hai ki each element is at most k away from its target position, 
- mtlb element true position is between [i-k,i+k] anywhere.
- we have to sort the array

#### Appoach 1: Sort array : nlogn

![Screenshot of Welcome Board _ Sketchboard (3)](https://user-images.githubusercontent.com/35686407/175804322-8f4b74f9-fc0c-4d62-ae7f-1dc5c7736116.jpg)

#### Approach 2: Heap of size K,

- isme bola hai ki K distance ke andar aa skta hai, to kyu na pehle k elements ko compare krle, usme jo small hai use daal de
- hum isme k size ka heap lenge, min heap, because we want to sort, and pehle chota element hi aayega asc order mae

![Screenshot of Welcome Board _ Sketchboard (4)](https://user-images.githubusercontent.com/35686407/175804387-1c99d258-e195-470f-9bbe-f26bda60fec3.jpg)

![Screenshot of Welcome Board _ Sketchboard (5)](https://user-images.githubusercontent.com/35686407/175804513-05c6c62a-3c35-46bd-9974-619ff7e8388c.jpg)


```cpp
vector <int> nearlySorted(int arr[], int n, int k){
  vector<int> ans;
  priority_queue<int,vector<int>,greater<int>> pq;
  for(int i = 0; i < n; i++){
      pq.push(arr[i]);
      if(pq.size() > k){
          ans.push_back(pq.top());
          pq.pop();
      }
  }
  while(!pq.empty()){
      ans.push_back(pq.top());
      pq.pop();
  }
  return ans;
}
```
## 4. Find K Closest Elements

![Screenshot Capture - 2022-06-26 - 13-25-03](https://user-images.githubusercontent.com/35686407/175805073-f52122f7-ded0-444c-903c-e70a0ef353af.png)

- as closest element manga hai, to mtlb x and array element ke bich ka difference as min as possible
- to jinka difference jada hai unhe ignore krna hai

#### Approach 1 : Sort vector according to the distance from x , min to max distance 

![Screenshot of Welcome Board _ Sketchboard (6)](https://user-images.githubusercontent.com/35686407/175805191-ecc373da-8094-427a-8ccf-8d20f36c8e6a.jpg)

#### Appraoch 2: Make a heap with size K, now, which heap ?

![Screenshot Capture - 2022-06-26 - 14-34-02](https://user-images.githubusercontent.com/35686407/175807204-63d64e61-29c9-4057-b535-13e4ef7051d6.png)

- as minimum distance chahiye, to minimum distance valo ko bchana hai, to hum max heap bnayege, jisse jada distance vale khtm ho jaye
- use heap of size k, then if pq.size > k, pop, same as find the kth smallest element

![Screenshot of Welcome Board _ Sketchboard (7)](https://user-images.githubusercontent.com/35686407/175807325-e0b900c3-dfd2-444c-a01c-f8a58477e5fe.jpg)

```cpp
vector<int> findClosestElements(vector<int>& arr, int k, int x) {
  priority_queue<pair<int,int>> pq; // max heap

  for(auto& val:arr){
      int distance = abs(x-val);
      pq.push({distance,val});
      if(pq.size() > k) pq.pop();
  }

  vector<int> ans;
  while(!pq.empty()){
      ans.push_back(pq.top().second);
      pq.pop();
  }

  sort(ans.begin(),ans.end());
  return ans;
}
```

## 5. Top K Frequent Elements

#### Approach 1 : Count Frequency, Sort Complete Array

- Count frequency put in map
- now put {freq,ele} in vector again
- sort the vector according to freq
- select first K elements

#### Appraoch 2: Priority Queue

- Same as question 4, just in that we are sorting with frequency key
- first count the frequency in unordered_map
- then, treat unordered_map as vector and do the question same as we did
- but which heap we have to use,
- as it said top K frequent elements,
- means we have to choose elements whose frequency is high, so
- hme jada frequency vale element bchane hai, to mtlb hum minimum ko uda skte hai,
- to min heap use krenge
- when size of min heap > k pop;
- the left elements are my ans.

![Screenshot of Welcome Board _ Sketchboard (8)](https://user-images.githubusercontent.com/35686407/175807883-7b8202ad-30e0-4de8-aeb3-5acb8ee86c5e.jpg)

```cpp
vector<int> topKFrequent(vector<int>& nums, int k) {
  unordered_map<int,int> umap;

  for(auto&val : nums){
      umap[val]++;
  }

  priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>> pq;

  for(auto& pr:umap){
      pq.push({pr.second,pr.first});
      if(pq.size() > k) pq.pop();
  }

  vector<int> ans;
  while(!pq.empty()){
      ans.push_back(pq.top().second);
      pq.pop();
  }
  return ans;
}
```

## 6. Sort array by increasing order of Frequency

- ye upar jesa hi hai question , bs isme k given nhi hai,
- isme hum pehle umap mae daal lenge frequency
- then min-heap(freq,ele) bnayenge
- ab ye banane ke baad hme bs sare elements ko dalna hai
- and fr bhr nikal kr vector mae dalna hai

> Note : Read about compare function.

### Class Compare (Important) , Min Heap, if pair first element are same, sort in inc order by second element

```cpp
class compare
    {    
        public:
        // Since as you can see we have to sort decreasing order if frequency of two elements
        // is same, so we need *Custom Comparator Function* which is this 👇
        bool operator()(pair<int, int> p1, pair<int, int> p2) 
        {    
            if(p1.first==p2.first)
                return p1.second < p2.second;
            return p1.first > p2.first;
        }
    };
    
    vector<int> frequencySort(vector<int>& nums) {
        unordered_map<int,int> umap;
        
        for(auto& val:nums){
            umap[val]++;
        }
        
        // min freq should be on top
        priority_queue<pair<int,int>,vector<pair<int,int>>,compare> pq;
        
        for(auto& pr:umap){
            pq.push({pr.second,pr.first});
        }
        
        vector<int> ans(nums.size());
        int i = 0;
        while(!pq.empty()){
            auto pr = pq.top();pq.pop();
            int freq = pr.first;
            int ele = pr.second;
            while(freq--){
                ans[i] = ele;
                i++;
            }
        }
        return ans;
    }
```
