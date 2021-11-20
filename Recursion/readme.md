# Recursion
- A Functin who call itself is called recursion.
- It can be `related with mathematics` in `mathematical induction`.
- We just have faith that the function is true for n = k, then we find only for n = k+1

> Note: Practice Basic Question from PEPCODING Website or Youtube first then from Aditya Verma Youtube

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
`Question 4` : Find ![](http://www.sciweavers.org/upload/Tex2Img_1637398319/render.png), create a function pow(x,n)

-  ![Expectation: pow(3,5) = 3^5 = 3 x 3^4](http://www.sciweavers.org/upload/Tex2Img_1637398535/render.png)
- ![Faith: pow(3,4) return its ans](http://www.sciweavers.org/upload/Tex2Img_1637398617/render.png)
- Expectation + Faith: pow(3,5) = 3 x pow(3,4)
- Base Case : when n = 0 it will return 1 i.e., power 0 of 3 = 1

```cpp
int power(int x,int n){
    if(n==0) return 1;
    return x * power(x,n-1);
}
```

### `Important Function of Power`:

![](http://www.sciweavers.org/upload/Tex2Img_1637399250/render.png)

Example  : 

![](http://www.sciweavers.org/upload/Tex2Img_1637399397/render.png)

```cpp
    int powerFast(int x,int n){
        if(n==0) return 1;
        else if(n%2==0){ // power is even
            int a = powerFast(x,n/2);
            return a*a;
        }else if(n%2 != 0){ // power is odd
            return x*powerFase(n-1);
        }
    }
```

`Question 5: ` **Tower OF Hanoi**

- Print the instructios to move the disk
- from tower 1 to tower 2 using tower 3
- following are the rules:
    - move 1 disk at a time
    - never place smaller disk under large
    - you can only move the disk at the top.

![](https://www.tutorialspoint.com/data_structures_algorithms/images/tower_of_hanoi.gif)

- Expectation: toh(3,source,destination,helper)
- Faith: toh(2,source,destination,helper) [Vishwas rkhenge 2 disk ka kaam khud ho jayega, hme nhi sochna kese hoga]
- Expectation + Faith
    - toh (3,A,B,C) -> 3 disk A se B mae using C
    hum maan kr chlenge 2 disk upar ki already C mae hai to hum srd 3rd jo sbse niche ki disk hogi use move krenge.
    toh(2,A,C,B) -> hmne 2 disk upar ki A se C mae dali hai dont know kese bas daal di hai, using B.
    - hum ab 3rd disk ko move krenge A se B mae
    - then, 2 disk ko B mae move krenge C se taking help from A. toh(2,B,C,A).
    
- Algorithm:
    1. Move n-1 disk from source to destination using helper tower
    2. move nth disk from source to destination i.e., print nth disk : source -> destination
    3. Move n-1 disk again from source to destination using helper tower

```cpp
void TOH(int n,char A,char B,char C){ // A - kha se , B - Kha pr , C - Helper tower
    if(n==0) return;
    TOH(n-1,A,C,B); // move n-1 disk from A to C using B
    cout<<n<<": "<<A<<" -> "<<B<<endl;
    TOH(n-1,C,B,A); // move n-1 disk from C to B using A
}

int main(){
    TOH(3,'A','B','C');
    return 0;
}
```

`Question 6:` Print Array using recursion
```cpp
void arrayPrint(int* arr,int index,int size){
    if(index == size) return;
    cout<<arr[index]<<" ";
    arrayPrint(arr,index+1,size); // in every call we inc. index
}
int main(){
    ...
    arrayPrint(arr,0,n); // starting index, n is size of array.
    ...
}
```

`Question 7:` Print Array in Reverse using recursion
```cpp
/* first go completely last in array to print the last element first, when returning just print the current index element.*/

void arrayPrintReverse(int* arr,int index,int size){
    if(index == size) return;
    arrayPrint(arr,index+1,size); // in every call we inc. index
    cout<<arr[index]<<" "; 
}
int main(){
    ...
    arrayPrint(arr,0,n); // starting index, n is size of array.
    ...
}
```
`Question 6:` Maximum of an array using recursion
```cpp
/* Firstly, go to the last element,then when there is nothing left we return -infinity because in iteration when we find max, we initialize a number to some negative number, then start comparing*/

/*Comparing in Backward Direction */
int maxElement(int* arr,int index,int size){
    if(index == size) return INT_MIN;
    int prevMax = maxElement(arr,index+1,size);
    return max(prevMax,arr[index]);
}

/* Comparing in forward direction */
int maxElement(int *arr,int index,int size,int prevAns){
    if(index == size) return prevAns;
    int ans = max(prevAns,arr[index]);
    return maxElement(arr,index+1,size,ans);
}
// call - maxElement(arr,0,size,INT_MIN);
```
