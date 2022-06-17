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
