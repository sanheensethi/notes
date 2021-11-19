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

### Basic Euclidean Algorithm for GCD

Using Division method to find gcd.

- If we subtract a smaller number from a larger (we reduce a larger number), GCD doesn’t change. So if we keep subtracting repeatedly the larger of two, we end up with GCD.
- Now instead of subtraction, if we divide the smaller number, the algorithm stops when we find remainder 0.
- When remainder is 0 divisor is GCD.

[Reference Foundation - Video 3]
```cpp
    int gcd(int a,int b){
        if(a%b == 0) return b; // if(b=0) return a; [1 more call of recursion]
        return gcd(b,a%b);
    }
```


