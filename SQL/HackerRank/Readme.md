# HackerRank

## 1. Even ID Number

- mod(id,2) = 0

```sql
SELECT DISTINCT CITY FROM STATION WHERE mod(ID,2) = 0;
```

## 2. Exclude Dublicate / Distinct Values

- DISTINCT

```sql
SELECT DISTINCT CITY FROM STATION;
```

## 3. Count Total Values

- COUNT(*) / COUNT(COL_NAME) 

```sql
SELECT COUNT(*) FROM TABLE;
```

## 4. Count Distinct Values from Column

- COUNT(DISTINCT COL_NAME)

```sql
SELECT COUNT(DISTINCT CITY) FROM STATION;
```

## 5. Find Absolute Difference

- ABS

```sql
SELECT ABS(COUNT(CITY) - COUNT(DISTINCT CITY)) FROM STATION
```

- above statement gives total number of dublicate values.

## 6. Shortest and Longest Name According to length of Name [Question](https://www.hackerrank.com/challenges/weather-observation-station-5/problem?isFullScreen=true)

- If Someone, Collide, then print lexographically order

- The ORDER BY keyword is used to sort the result-set in ascending or descending order.
- Length ke according sort kr do, ORDER BY ASC | DESC 
- CITY ko ASC order mae rkho
- Shortest nikalne ke liye, length ke according sort kr dia, and city ko bhi asc order mae sort kr dia and Limit 1 lgakr 1st select kr lia
- Longest nikalne ke liye length ke accroding dec order mae sort kr dia and city ko asc mae hi rkha kyulo

> Using two statememnts

```sql
SELECT CITY,LENGTH(CITY) FROM STATION ORDER BY LENGTH(CITY) ASC ,CITY ASC LIMIT 1; /*Shortest City Name*/
SELECT CITY,LENGTH(CITY) FROM STATION ORDER BY LENGTH(CITY) DESC,CITY DESC LIMIT 1; /*Longest City Name*/
```


> Using One Statement

- UNION operator is used to combine the result-set of two or more SELECT statements.
- Every SELECT statement within UNION must have the same number of columns
- The columns must also have similar data types
- The columns in every SELECT statement must also be in the same order

[Link](https://www.w3schools.com/mysql/mysql_union.asp)

```sql
(SELECT CITY,LENGTH(CITY) FROM STATION ORDER BY LENGTH(CITY) ASC ,CITY ASC LIMIT 1)
UNION 
(SELECT CITY,LENGTH(CITY) FROM STATION ORDER BY LENGTH(CITY) DESC,CITY ASC LIMIT 1);
```

> Note: We can aslo use RLIKE insetead of REGEXP

## 7. SELECT Names Which Start with Vowels (a,e,i,o,u)

> Using [LIKE](https://www.w3schools.com/mysql/mysql_like.asp)

```sql
SELECT CITY FROM STATION
WHERE
CITY LIKE 'a%' OR
CITY LIKE 'e%' OR
CITY LIKE 'i%' OR
CITY LIKE 'o%' OR
CITY LIKE 'u%';
```

> Usign REGEXP (Regular Expression)

```sql
SELECT CITY FROM STATION
WHERE
CITY
REGEXP '^[aeiou]';
```
## 8. SELECT Names ending with Vowels (a,e,i,o,u)

> Using Like

```sql
SELECT DISTINCT CITY FROM STATION 
WHERE 
CITY LIKE '%a' OR
CITY LIKE '%e' OR
CITY LIKE '%i' OR
CITY LIKE '%o' OR
CITY LIKE '%u';
```

> Using RegExp

- DISTINCT used to get unique results, discarding dublicates

```sql
SELECT DISTINCT CITY FROM STATION 
WHERE CITY 
REGEXP '[aeiou]$';
```

## 9. Select names that Start and End with Vowels (a,e,i,o,u)

> LIKE Operator

```sql
SELECt CITY FROM STATION
WHERE 
CITY LIKE 'a%a' OR
CITY LIKE 'a%e' OR
CITY LIKE 'a%i' OR
CITY LIKE 'a%o' OR
CITY LIKE 'a%u' OR
CITY LIKE 'e%a' OR
CITY LIKE 'e%e' OR
CITY LIKE 'e%i' OR
CITY LIKE 'e%o' OR
CITY LIKE 'e%u' OR
CITY LIKE 'i%a' OR
CITY LIKE 'i%e' OR
CITY LIKE 'i%i' OR
CITY LIKE 'i%o' OR
CITY LIKE 'i%u' OR
CITY LIKE 'o%a' OR
CITY LIKE 'o%e' OR
CITY LIKE 'o%i' OR
CITY LIKE 'o%o' OR
CITY LIKE 'o%u' OR
CITY LIKE 'u%a' OR
CITY LIKE 'u%e' OR
CITY LIKE 'u%i' OR
CITY LIKE 'u%o' OR
CITY LIKE 'u%u';
```

> RegExp

```sql
SELECt CITY FROM STATION
WHERE CITY
REGEXP '^[aeiou].*[aeiou]$';
```
## 10. Select Name which do not start with vowels (a,e,i,o,u)

> Like Statement

```sql
SELECT DISTINCT CITY FROM STATION
WHERE 
CITY NOT LIKE 'a%' AND
CITY NOT LIKE 'e%' AND
CITY NOT LIKE 'i%' AND
CITY NOT LIKE 'o%' AND
CITY NOT LIKE 'u%';
```
> RegExp

```sql
SELECT DISTINCT CITY FROM STATION
WHERE CITY
REGEXP '^[^aeiou]';
```

## 11. Select Names that do not end with Vowels (a,e,i,o,u)

> Like Operator

```sql
SELECT DISTINCT CITY FROM STATION 
WHERE
CITY NOT LIKE '%a' AND
CITY NOT LIKE '%e' AND
CITY NOT LIKE '%i' AND
CITY NOT LIKE '%o' AND
CITY NOT LIKE '%u';
```

> RegExp

```sql
SELECT DISTINCT CITY FROM STATION 
WHERE CITY
REGEXP '[^aeiou]$'
```

## 12. Select Names that do not start with Vowels OR End with vowels

> Note: | operator work as OR in RegExp

```sql
SELECT DISTINCT CITY FROM STATION 
WHERE
CITY REGEXP '^[^aeiou].*' OR
CITY REGEXP '.*[^aeiou]$';
```

```sql
SELECT DISTINCT CITY FROM STATION 
WHERE
CITY REGEXP '^[^aeiou].*|.*[^aeiou]$';
```

## 13. Select Names that do not start and end with Vowels (a,e,i,o,u)

```sql
SELECT DISTINCT CITY FROM STATION
WHERE CITY
REGEXP '^[^aeiou].*[^aeiou]$';
```

## 14. Get Last 3 Char of Name

- We can also use `RIGHT(Name,3)`

```sql
SELECT SUBSTR(Name,-3) AS Last3 FROM TABLE
```

## 15. Sort According to the last 3 Char of Name

- if last 3 char of name are same eg. bobby,Robby, then sort them by id in asc order
- We can also use `RIGHT(Name,3)`

```sql
SELECT Name FROM STUDENTS
WHERE
ORDER BY SUBSTR(Name,-3),ID ASC;
```
