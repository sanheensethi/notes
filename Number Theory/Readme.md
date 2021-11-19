# Number Theory

## GCD (Greatest Common Divisor)

### Foundation GCD
- [Link](https://youtu.be/mCrf5SBPob8) - upto 44 min
- [Link](https://youtu.be/Y38hlnF_9KQ)
- [Link](https://youtu.be/utZcJ0leZ_g) [ Euclid's Algorithm]

- [x] `gcd(x,y)` : it is the `greatest natural number` which **divides both** `x and y`, where x and y both are natural number.
    - gcd(24,18) = 6 {24 and 18 is divided by 6 which is the greatest number} 
- [x] `lcm(x,y)` : it is the `least natural number` which is **divided by** both `x and y`.
    - lcm(24,18) = 72 {72 is divided by both 24 and 18 which is the least number.}
- [x] `coprime numbers` : gcd(x,y) = 1 , consecutive numbers are coprime numbers.
- [x] `relatively prime pair wise` : gcd(a,b) = 1 i.e., they are coprime numbers. 

### Properties of GCD and LCM

![1. LCM(A,B) x GCD(A,B) = AB](http://www.sciweavers.org/upload/Tex2Img_1637338492/render.png)

![2. GCD(A,B) = GCD(A,A+BK), where K belongs to I](http://www.sciweavers.org/upload/Tex2Img_1637338586/render.png)

![3. GCD(A,B) = GCD(A,A-B)](http://www.sciweavers.org/upload/Tex2Img_1637338652/render.png)

![4. GCD(n,n+1) = 1](http://www.sciweavers.org/upload/Tex2Img_1637345021/render.png)

![5. GCD(a,b,c) = GCD(GCD(a,b),c)](http://www.sciweavers.org/upload/Tex2Img_1637347135/render.png)

![6. ](http://www.sciweavers.org/upload/Tex2Img_1637349528/render.png)

![7. ](http://www.sciweavers.org/upload/Tex2Img_1637352266/render.png) [Obvious, c is greatest common divisor of both, so it divides a and b]

![8. ](http://www.sciweavers.org/upload/Tex2Img_1637352739/render.png)

![9. ](http://www.sciweavers.org/upload/Tex2Img_1637352928/render.png)

![10. ](http://www.sciweavers.org/upload/Tex2Img_1637353348/render.png)

![11. ](http://www.sciweavers.org/upload/Tex2Img_1637353314/render.png)

![12. ](http://www.sciweavers.org/upload/Tex2Img_1637353254/render.png)

![13. ](http://www.sciweavers.org/upload/Tex2Img_1637353215/render.png)

![14. ](http://www.sciweavers.org/upload/Tex2Img_1637353491/render.png)


### Basic Euclidean Algorithm for GCD

Using Division method to find gcd.

- If we subtract a smaller number from a larger (we reduce a larger number), GCD doesn’t change. So if we keep subtracting repeatedly the larger of two, we end up with GCD.
- Now instead of subtraction, if we divide the smaller number, the algorithm stops when we find remainder 0.
- When remainder is 0 divisor is GCD.

[Reference Foundation - Video 3]

![](http://www.sciweavers.org/upload/Tex2Img_1637346470/render.png)

**Time Complexity :** `O(log(min(a, b))`

```cpp
    int gcd(int a,int b){
        if(a%b == 0) return b; // also we can write there , if(b==0) return a; [1 more call of recursion]
        return gcd(b,a%b);
    }
```

```cpp
    int lcm(a,b){
        return (a*b)/gcd(a,b);
    }
```
**Inbuild Function :** ``__gcd(a,b)``

#### GCD Queries [Question] - [Link](https://youtu.be/e3qhRh4UOug)

### Geometrical View of GCD
Given Below, 24-by-60 rectangular area can be divided into a grid of: 1-by-1 squares, 2-by-2 squares, 3-by-3 squares, 4-by-4 squares, 6-by-6 squares or 12-by-12 squares. Therefore, 12 is the greatest common divisor of 24 and 60. A 24-by-60 rectangular area can thus be divided into a grid of 12-by-12 squares, with two squares along one edge (24/12 = 2) and five squares along the other (60/12 = 5). 

![](https://upload.wikimedia.org/wikipedia/commons/thumb/7/74/24x60.svg/170px-24x60.svg.png)

> Note : `Result (Generally):` an a-by-b rectangle can be covered with square tiles of side length c only if c is a common divisor of a and b.

Question on above result [Link](https://www.codechef.com/problems/ZACKHAN)


