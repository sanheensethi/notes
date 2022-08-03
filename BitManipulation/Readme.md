# Bit Manipulation

## 1. Basics
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

## 2. kernighans Algorithm

```cpp
int solve(n){
    int count = 0;
    while(n){
        int rsbm = n & -n;
        n -= rsbm;
        count++;
    }
    return count;
}
```
## 3. Josephus Problem

```cpp
int powerof2(int n){
  int i = 1;
  while(i * 2 <= n){
    i = i * 2;
  }
  return i;
}

int solution(int n){
  int hp2 = powerof2(n);
  int l = n - hp2;
  return 2*l + 1;
}
```
