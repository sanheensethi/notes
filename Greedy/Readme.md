# Greedy

## 1. N- Meeting Rooms

```cpp
class Solution
{
    public:
    //Function to find the maximum number of meetings that can
    //be performed in a meeting room.
    int maxMeetings(int start[], int end[], int n)
    {
        vector<vector<int>> timings(n);
        for(int i = 0; i < n; i++){
            timings[i] = {start[i],end[i]};
        }
        
        sort(timings.begin(),timings.end(),[](vector<int>& v1,vector<int>& v2){
            return v1[1] < v2[1];
        });
        
        
        int ending = timings[0][1];
        int ans = 1;
        for(int i = 1; i < n; i++){
            auto& starting = timings[i][0];
            if(starting > ending){
                ending = timings[i][1];
                ans++;
            }
        }
        return ans;
    }
}
```

## 2. MInimum Platforms

```cpp
int findPlatform(int arr[], int dep[], int n){
    sort(arr,arr+n);
    sort(dep,dep+n);
    int i = 0, j = 0;
    int plat = 0;
    int maxi = 0;
    while(i < n && j < n){
        if(dep[j] >= arr[i]){
            i++;
            plat++;
        }else if(dep[j] < arr[i]){
            j++;
            plat--;
        }
        maxi = max(maxi,plat);
    }
    return maxi;
}
```
## 3. Job Sequencing

```cpp
vector<int> JobScheduling(Job arr[], int n) { 
    sort(arr,arr+n,[](Job& j1,Job& j2){
       return j1.profit > j2.profit; 
    });

    int maxi = 0;
    for(int i = 0; i < n; i++){
        maxi = max(maxi,arr[i].dead);
    }

    vector<int> jobs(maxi+1,-1);
    int ans = 0;
    int count = 0;
    for(int i = 0; i < n; i++){
        auto& k = arr[i].dead;
        while(k > 0 && jobs[k] != -1){
            k--;
        }
        if(k > 0){
            jobs[k] = arr[i].id; 
            ans += arr[i].profit;
            count += 1;
        }
    }
    return {count,ans};
} 
```
