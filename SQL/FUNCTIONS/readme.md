`,` is cross product.

## Arithmetic Functions

> LIST 1:

- PI()
- ROUND()
- CEIL()
- FLOOR()
- POW(base,exp)
- SQRT()
- RAND() , randum number b/w 0 and 1
- ABS()
- SIGN() , x > 0 then 1 else 0 
- DIV and / difference / gives float value
- MOD

> LIST 2:

- SIN()
- COS()
- TAN()
- ASIN()
- ACOS()
- ATAN()
- ATAN2()
- COT()
- RADIANS()

## String Functions:

> List 1:

- UPPER() / UCASE()
- LOWER() / LCASE()
- LENGTH()
- CHAR_LENGTH()
- CONCAT()
     - CONCAT(name," ",percentage)
     - concat multiple columns
- CONTACT_WS()
    - CONCAT_WS("@","A","B","C") : A@B@C
- LTRIM()
- RTRIM()
- TRIM()
- POSITION()
    - Char/Word ko search kr rhe hai, then it return position
    - POSITION("Baba" IN "Yahoo Baba") : 7 (1 based indexing)
    - gives first position of Baba
- LOCATE()
    - 3rd Parameter : Isme jha se searching start krni hai, vo bhi daal skte hai.
    - LOCATE("a","Yahoo Baba Youtube Channel") : 2
    - LOCATE("a","Yahoo Baba Youtube Channel") : 9
- INSTR()
    - Work same as position,
    - doesn't write IN
    - INSTR("Search String","To Be Search")
    - INSTR("Yahoo Baba","Baba") : 7


> List 2:

- SUBSTRING()/SUBSTR()
    - First Parameter : String Name
    - Second parameter : Index , kha se string todna start krna hai
        - if negative: piche se count kro -1,-2,-3,...
    - Third Parameter : By Default, full length , else you can write the length kitni length ki chahiye
    - Example: SUBSTRING("Yahoo Baba",3) : hoo Baba
- MID()
    - same as substring()
- SUBSTRING_INDEX()
    - Second parameter: delimeter - kha se break krna chahte hai, and write index number of that delimeter if multiple are there
    - left vale part ko return krega
    - SUBSTRING_INDEX("www.yahoobaba.net",'.',1) : www
    - SUBSTRING_INDEX("www.yahoobaba.net",'.',2) : www.yahoobaba
- LEFT()
    - left ka string return kr dega
    - LEFT("www.yahoobaba.net",3) : www (pehle ke 3 char)
- RIGHT()
    - jitne bhi right mae char honge, last ke return kr dega
    - RIGHT("www.yahoobaba.net",3) : net (last ke 3 char)
- LPAD()
    - Include padding 
    - LPAD("Sanheen",10,"-") : ---Sanheen 
- RPAD()
    - Include padding
    - RPAD("Sanheen",10,"-") : Sanheen--- 
- SPACE()
    - SPACE(100) , 100 sapces add kr dega
- REVERSE()
    - Reverse a string
- REPEAT()
- REPLACE()
    - Second Parameter : dhundna kya hai ?
    - Third Parameter : Jiske sath replace krna hai
    - REPLACE("Yahoo Baba","Baba","WOW")
    - replace all baba
- STRCMP()
    - Comapre 2 strings
    - match 2 strings
    - STRCMP("SANHEEN","sanheen")
    - if equal then 0
    - if left > right : 1
    - if left < right : -1
- FIELD()
    - Multiple String ki list dete hai, and usme se ek string ko find kr lete hai
    - FIELD("to search : a","X","a","K") : 2 (index number) , case insensitive
    - also we can use integers
- FIND_IN_SET()
    - List ke andar find krega, lekin find krne ke liye set de denge
    - FIND_IN_SET("RAM","RAM,SHYAM,MOHAN") 
    - comma ke bich mae space nhi deni hai
- FORMAT()
    - Numeric values ke sath use hota hai
    - FORMAT(255.3568,2) : 255.36
- HEX(str)
    - string ki hexadecimal form return krega
















