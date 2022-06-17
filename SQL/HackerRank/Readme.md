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
