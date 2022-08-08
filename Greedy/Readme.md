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
