# Bit Manipulation

## Basics
- On
- Off
- Toggle
- Check ith bit is set or not

```cpp
int main(){
    int n,i,j,k,m;
    cin>>n>>i>>j>>k>>m;

    // set bit , on the bit , or operator is used

    int ans1 = n | (1 << i);

    // off the bit

    int ans2 = n & ~(1 << j);

    // toggle bit , xor operator

    int ans3 = n ^ (1 << k);

    // check mth bit is on or off

    bool check = n & (1 << m);

    cout<<ans1<<endl;
    cout<<ans2<<endl;
    cout<<ans3<<endl;
    if(check) cout<<"true";
    else cout<<"false";

}
```
