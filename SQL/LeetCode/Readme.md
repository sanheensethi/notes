# LeetCode

## 595. Big Countries [Question](https://leetcode.com/problems/big-countries/)

```sql
SELECT
name,population,area
FROM World
WHERE
area >= 3000000 OR population >= 25000000;
```

## 1757. Recyclable and Low Fat Products [Question](https://leetcode.com/problems/recyclable-and-low-fat-products/)

```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y' AND recyclable = 'Y';
```

### 584. Find Customer Referee [Question](https://leetcode.com/problems/find-customer-referee/)

- Here , `Customer.referee_id IS NULL` means that `NULL values are acceptable`

```sql
SELECT name
FROM Customer 
WHERE Customer.referee_id != 2 OR Customer.referee_id IS NULL;
```

### 183. Customers Who Never Order [Question](https://leetcode.com/problems/customers-who-never-order/)

> Using Left Joinselect customers.name as 'Customers'
from customers
where customers.id not in
(
    select customerid from orders
);

- We have to select the customer who never orders, and `WHERE Orders.customerId IS NULL;` will accept those id , which are not present in Customer
- when we do left join, then customer who never order has NULL value in Left Join Table View
- Therefore, by taking advantage of that we are selecting Cursomer who never order

```sql
SELECT Customers.name AS Customers
FROM Customers 
LEFT JOIN Orders ON 
Customers.id = Orders.customerId WHERE Orders.customerId IS NULL;
```

> Another Way : Using Sub-Query

- `select customerid from orders` give the list of customer who order
- now when we do `where curstomers.id not in ....` , then it will select those customer in customer table who never order, as subquery gives list of customer who order

```sql
select customers.name as 'Customers'
from customers
where customers.id not in
(
    select customerid from orders
);
```
