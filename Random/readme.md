# Random Learning

```cpp

1. min({a,b,c}) // min(a,b,c)

2. sort(a,a+n) // a is array - ascending order
   sort(a.begin(),a.end()) // a is vector - ascending order

3. sort(a,a+n,greater<int>()); // descending order
   sorT(a.begin(),a.end(),greater<int>()); // descending order

4. isdigit(char) // to check char is digit or not
   isalpha(char) // to check char is alpha or not

5. There is NO __builtin_popcount in c++, it's a built in function of GCC.

   The function prototype is as follows:
    int  __builtin_popcount(unsigned int)

   It returns the numbers of set bits in an integer (the number of ones in the binary representation of the integer).

6. N & 1 == 1 // odd
   N & 1 == 0 // even

7. void swap(int *a,int *b){ // swap two numbers 
      *a^=*b; // *a = *a^*b
      *b^=*a; // *b = *b^*a
      *a^=*b; // *a = *a^*b
   }

8. log10(N) + 1 // number of digits in base 10 number

9. char ch = 'c'; // Lower To Upper
   ch &= '_' // ch = C
   
10. char ch = 'C'; // Upper To Lower
   ch |= ' ' // ch = c
   
11. 1<<k; // k-th power of 2

12. index++;
    if(index >= n) index = 0;
    
    To overcome above : index = (index+1)%n;
    
13. index--;
    if(index < 0) index = n-1;
    
    To Overcome above : index = (index+n-1)%n;
    
14. if(x==N) return true;
    else return false;
    
    Above can also be written as : return x==N;
    
15. Setting all values of array is 0 -
    for(int i=0;i<n;i++) array[i] = 0;
    
    For that - memset(arrayName,value,sizeOfArray); - memset(array,0,n);
    
16. Example: if an array has elements as [a,a,a,a,a,a,a,a,a,a] then number of pairs (a,a) such that i<j is n*(n-1)/2 wheren n is count of a.
 ```
