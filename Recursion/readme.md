# Recursion
- A Functin who call itself is called recursion.
- It can be `related with mathematics` in `mathematical induction`.
- We just have faith that the function is true for n = k, then we find only for n = k+1

Example : let we have to find the sum of n natural numbers, so we have to find: sum(n),
now let n = 5, sum(5)  = 1 + 2 + 3 + 4 + 5
we know that thing, but suppose we have faith that my sum function knows the answer for sum(4) = 1 + 2 + 3 + 4 then we have to just add 5 in sum(4),

i.e., sum(5) = sum(4) + 1; 

`Important :` we assume that it run for k-1 automatically without thingking too much about base case and anything, we have to just work for k and think how the result should be like.

So, We assume sum(k-1) is true always
then sum(k) = sum(k-1) + k;

*Now,* main thing is we have to find the base case, it is the case where the function could stop so, what we will do we dry run it, now we see  sum(1) = sum(0) + 1, and when we call for sum(0) then what should be its answer ? its 0 then we write an extra condition in starting sum(0) = 0;

```cpp
int sum(int n){
    if(n == 0) return 0;
    return sum(n-1) + n;
}
```
****
**HIGH LEVEL THINKING**
- *Expactaion jano kya chhaiye*
- *Establish Faith, ki agar n ke litye chlega to n-1 ke liye khud chl jayega socho mt kese chlega*
- *Now, Create connection in Expectation + Faith*

**LOW LEVEL THINKING**
- *AB detailing Krenge*
- *Create stack and dry run it.*
- *Find where you have to stop the function, that is the base case.*
****

Question 1: Print Number upto 10;

- Expectation [print(10)] : 1 2 3 4 5 6 7 8 9 10
- Faith [print(9)] : 1 2 3 4 5 6 7 8 9 (Vishwas rkha hai ki print(9) pehle 9 number ko print kr dega khud)
- Expectation fullfull from faith : 
    print(10) = print(9) and 10
    simillarly => print(9) = print(8) and 9
So , when the function will stop ?  jb hmare paas n = 0 hoga to kuch bhi print nhi hoga.

```cpp
void print(int n){
    if(n==0) return;
    print(n-1);
    cout<<n<<endl;
}
```

Question 2 : Print Decreasing Increasing
n = 5, Output : 5 4 3 2 1 1 2 3 4 5

- Expectation : print(5) = 5 .... 5
- Faith : print(4) will work by himself
- Expectation + Faith = print(5) = 5 , print(4) , 5
- Base Case, when n == 0 it not prints so return at this time.

```cpp
void printDI(int n){
    if(n==0) return;
    cout<<n<<endl;
    printDI(n-1);
    cout<<n<<endl;
}
```
`Question 3` : Find Factorial of number n i.e. n!

- Expectatiion: fact(5) = 5 x 4 x 3 x 2 x 1
- Faith: fact(4) will return 4! i.e. 4 x 3 x 2 x 1
- Expectation + Faith: fact(5) = 5 x fact(4)
- Base Case : when n = 0 it will return 1 i.e., 0! = 1 or you can also return 1 when n = 1

```cpp
int factorial(int n){
    if(n==1) return 1;
    return n * factorial(n-1);
}
```
