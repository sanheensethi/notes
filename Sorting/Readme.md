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

