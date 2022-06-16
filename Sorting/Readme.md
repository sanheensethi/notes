# Sorting Techniques

> Criterion for Analysis

- Number of comparisons
- Number of swaps
- Adaptive
    - It means when the array is already in the sorted order thrn it shoulf take less time then that is called adaptive
- Stable
    - here stable eams eg- if we have an array (1 3 4 2 4 5) then after sorting it will become (1 2 3 4 4 5), here 4 comes two times , the first 4 will be the 1st 4 in the original array , means its sequence should not change
- Extra memory
    - some sorting algos require extra memory also

![vlcsnap-2022-06-16-10h36m04s072](https://user-images.githubusercontent.com/35686407/173995428-ba8d89cc-edba-4721-9ca2-e1e0f0c15d4f.png)

## Bubble Sort

- we perform n-1 passes,
- in each pass we move 1 element i.e. greatest element to the Last.

![Screenshot Capture - 2022-06-16 - 11-19-36](https://user-images.githubusercontent.com/35686407/174000547-e93fb29e-da50-49d7-a0e9-e02b0d6223b4.png)


![vlcsnap-2022-06-16-10h46m08s194](https://user-images.githubusercontent.com/35686407/173998986-0f3171ac-a8cc-4f35-bcc9-e76f80b51ded.png)

```cpp
void bubble_sort(vector<int>& arr){
    int n = arr.size();

    for(int pass = 0; pass < n-1; pass++){
        for(int i = 0; i < n-1-pass; i++){
            // -pass is because, we reduce the comparison by 1 in each pass
            if(arr[i] > arr[i+1]){
                swap(arr[i],arr[i+1]);
            }
        }
    }
}
```

- Adaptive : (Not by default, we make it adaptive)
- if comparison is not done in any pass we will break, it means array is sorted.

![vlcsnap-2022-06-16-10h55m55s001](https://user-images.githubusercontent.com/35686407/174000144-4f725321-caaa-4a0d-8fe5-758277e61c73.png)

```cpp
void bubble_sort(vector<int>& arr){
    int n = arr.size();

    bool flag;
    for(int pass = 0; pass < n-1; pass++){
        flag = false;
        for(int i = 0; i < n-1-pass; i++){
            if(arr[i] > arr[i+1]){
                flag = true;
                swap(arr[i],arr[i+1]);
            }
        }
        if(flag == false) break;
    }
}
```

- Stable : Its Stable

![vlcsnap-2022-06-16-11h06m11s757](https://user-images.githubusercontent.com/35686407/174000173-444e8f37-38c7-481f-b0bd-a4095425fa6d.png)

> Note About Bubble Sort

- Best TC : O(n) , if array is sorted and we make the algo adaptive
- Worst TC : O(n^2)
- Average TC : O(n^2)
- SC : O(1)
- Adaptive : By default no, we make it forcely by taking flag
- Stable : Yes
- In this, if kth biggest element is required , then do k passes.
- 1st biggest element is found only in 1 pass
- 2nd biggest element is found only in 2 pass, and so on,
- therefore k pass is useful here.

## Insertion Sort

1. What is Insertion ?
    - Inserting the element in its sorted position

- In case of array we shift the elements to the right
- we started comparing from the last postion, is 30 > 12 ? yes , shift 30 to right , simillarly we did that untill we find correct position
- In case of Linked List, we have only head, so we traverse from start and compare then insert.

![vlcsnap-2022-06-16-11h31m46s956](https://user-images.githubusercontent.com/35686407/174002609-af92c121-10eb-40e2-baf0-d19a44544f69.png)

> Insertion Sort

- we consider 0th element is already sorted,
- means before 1st index list is sorted and after 1 index list is unsorted,
- we have to put the 1st index in sorted list in correct position, as we do in insertion
- we will compare from index-1 to 0 , where we got correct place to sort, we will put that element in that position.

![vlcsnap-2022-06-16-11h49m33s268](https://user-images.githubusercontent.com/35686407/174011592-400443c1-298c-40c9-84af-75cab0924c84.png)

![Screenshot 2022-06-16 122909](https://user-images.githubusercontent.com/35686407/174011617-aaae7aeb-44bf-4e99-b9c6-4c62b047a0c0.png)

![vlcsnap-2022-06-16-12h38m35s127](https://user-images.githubusercontent.com/35686407/174012712-8022b4d6-c5dc-482f-98ab-b2f8634a7250.png)

![Screenshot 2022-06-16 124037](https://user-images.githubusercontent.com/35686407/174012960-269df998-c7fc-48ce-a461-ca03c8cd0cea.png)

```cpp
void insertionSort(vector<int>& nums){
        int n = nums.size();
        for(int i = 1; i < n; i++){
            int val = nums[i];
            int j = i-1;
            while(j >= 0 && val < nums[j]){
                swap(nums[j],nums[j+1]);
                j--;
            }
            nums[j+1] = val;
        }
    }
```

Note for Insertion Sort:

- Worst Case Time Complexity [ Big-O ]: O(n2)
- Best Case Time Complexity [Big-omega]: O(n)
- Average Time Complexity [Big-theta]: O(n2)
- Space Complexity: O(1)
- Adaptive : Yes
- Stable : Yes

> Characterstics : 

- It is efficient for smaller data sets, but very inefficient for larger lists.
- Insertion Sort is adaptive, that means it reduces its total number of steps if a partially sorted array is provided as input, making it efficient.
- It is better than Selection Sort and Bubble Sort algorithms.
- Its space complexity is less. Like bubble Sort, insertion sort also requires a single additional memory space.
- It is a stable sorting technique, as it does not change the relative order of elements which are equal.
- K pass is not useful there, because in 1st pass, we didnt get the biggest element
- in 2nd pass we didn't get the second biggest element
- there are intermediate elements.


## Comparison Between Insertion and Bubble Sort.

![Screenshot 2022-06-16 124821](https://user-images.githubusercontent.com/35686407/174015004-9ec99927-02d3-4631-b9a2-250014694901.png)

## Selection Dort

- This algorithm will first find the smallest element in the array and swap it with the element in the first position
- then it will find the second smallest element and swap it with the element in the second position,
- and it will keep on doing this until the entire array is sorted.
- it repeatedly selects the next-smallest element and swaps it into the right place.

![Screenshot Capture - 2022-06-16 - 14-09-29](https://user-images.githubusercontent.com/35686407/174030234-b2269b9c-8a3b-4720-8cb1-06814f7501c5.png)
