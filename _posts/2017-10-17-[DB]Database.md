---
title : Database 기본 Query
description : 기본 query 공부야!
date : 2017-10-12
categories :
- DB
tags :
- DB

---

# 일반

## Distinct
중복 제외
SELECT DISTINCT Country FROM Customers;

## Count
갯수 확보
SELECT COUNT(DISTINCT Country) FROM Customers;

## Order by
SELECT * FROM Customers
ORDER BY Country DESC;
- desc : 내림차순
- ASC : 오름차순

### 정렬 중첩
SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;
- country는 오름차순, 그 중 동일 country를 가진 레코드의 customerName은 내림차순

## Insert Into values
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES ('Cardinal','Tom B. Erichsen','Skagen 21','Stavanger','4006','Norway');

## NULL VALUES
SELECT column_names
FROM table_name
WHERE column_name IS NULL;
- column_name의 값이 NULL인 것

SELECT column_names
FROM table_name
WHERE column_name IS NOT NULL;
- NULL이 아닌 것

## Update
UPDATE Customers
SET ContactName='Alfred Schmidt', City='Frankfurt'
WHERE CustomerID=1;
- 기존 테이블의 컬럼의 값을 변경해라.

## Delete
DELETE FROM Customers
WHERE CustomerName='Alfreds Futterkiste';
- 특정 레코드를 지워라

## Limit
SELECT * FROM Customers LIMIT 3;
- 출력 갯수 한정

## AS
SELECT MIN(Price) AS SmallestPrice
FROM Products;
- AS 이 후의 컬럼명으로 출력하라.
- MIN(price) : price컬럼의 값 중 최소 값
- MAX
- AVG(price) : price컬럼들의 평균 값
- SUM


# Where
SELECT * FROM Customers
WHERE Country='Mexico';

### Where A AND B
SELECT * FROM Customers
WHERE Country='Germany' AND City='Berlin';

### Where A AND (B OR C)
SELECT * FROM Customers
WHERE Country='Germany' AND (City='Berlin' OR City='München');

### Where AND NOT
SELECT * FROM Customers
WHERE NOT Country='Germany' AND NOT Country='USA';

## Where A LIKE
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%';
- customerName의 컬럼 값이 a로 시작되는 레코드

SELECT * FROM Customers
WHERE CustomerName LIKE 'a_%_ %';
- 언더바는 하나의 문자

## Where NOT LIKE
SELECT * FROM Customers
WHERE CustomerName NOT LIKE 'a%';
- a로 시작하지 않는 레코드

## Where LIKE %%
SELECT * FROM Customers
WHERE City LIKE '%es%';
- 앞/뒤로 뭐가 있던 es 단어가 포함.

## where like []%
SELECT * FROM Customers
WHERE City LIKE '[bsp]%';
- b나 s나 p로 시작하는 것.

## where in ()
SELECT * FROM Customers
WHERE Country IN ('Germany', 'France', 'UK');
- 중 하나를 포함하는

## where in (select from table)
SELECT * FROM Customers
WHERE Country IN (SELECT Country FROM Suppliers);

## 중첩 조건
SELECT * FROM Products
WHERE (Price BETWEEN 10 AND 20)
AND NOT CategoryID IN (1,2,3);

# 일반2

## 출력 컬럼 연결
SELECT CustomerName, Address + ', ' + PostalCode + ' ' + City + ', ' + Country AS Address
FROM Customers;

## 테이블 별칭 사용
SELECT o.OrderID, o.OrderDate, c.CustomerName
FROM Customers AS c, Orders AS o
WHERE c.CustomerName="Around the Horn" AND c.CustomerID=o.CustomerID;

# JOIN

## INNER JOIN ON
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers
ON Orders.CustomerID=Customers.CustomerID;

## 중첩 INNER JOIN
SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName
FROM ((Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID)
INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID);

## LEFT JOIN
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID=Orders.CustomerID
ORDER BY Customers.CustomerName;

## RIGHT JOIN
SELECT Orders.OrderID, Employees.LastName, Employees.FirstName
FROM Orders
RIGHT JOIN Employees
ON Orders.EmployeeID = Employees.EmployeeID
ORDER BY Orders.OrderID;

## FULL OUTER JOIN
SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2 ON table1.column_name = table2.column_name;
- 양쪽 다 출력

## 중첩
SELECT A.CustomerName AS CustomerName1, B.CustomerName AS CustomerName2, A.City
FROM Customers A, Customers B
WHERE A.CustomerID <> B.CustomerID
AND A.City = B.City
ORDER BY A.City;
- != 와 <>는 같은 연산자이다.


# UNION
SELECT City FROM Customers
UNION
SELECT City FROM Suppliers
ORDER BY City;
- 테이블 결과 함꼐 보여줌

## UNION ALL
SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers
ORDER BY City;
- 중복되는 레코드도 다 포함해서

## UNION 조건
SELECT City, Country FROM Customers
WHERE Country='Germany'
UNION
SELECT City, Country FROM Suppliers
WHERE Country='Germany'
ORDER BY City;

# GROUP

## GROUP BY
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
ORDER BY COUNT(CustomerID) DESC;
- distinct와 같다.
- 국가별로 모아서, 동일 국가의 ID 개수를 센다.

## LEFT JOIN 패턴
SELECT Shippers.ShipperName,COUNT(Orders.OrderID) AS NumberOfOrders FROM Orders
LEFT JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID
GROUP BY ShipperName;

## HAVING COUNT
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5
ORDER BY COUNT(CustomerID) DESC;
- customerID의 개수가 5개 이상인


# 일반3

## EXISTS
SELECT SupplierName
FROM Suppliers
WHERE EXISTS (SELECT ProductName FROM Products WHERE SupplierId = Suppliers.supplierId AND Price = 22);
- 존재하는

## any
SELECT ProductName
FROM Products
WHERE ProductID = ANY (SELECT ProductID FROM OrderDetails WHERE Quantity = 10);
- 이중에 아무 거나 하나

## ALL
SELECT ProductName
FROM Products
WHERE ProductID = ALL (SELECT ProductID FROM OrderDetails WHERE Quantity = 10);
-

## SELECT into
SELECT *
INTO newtable [IN externaldb]
FROM oldtable
WHERE condition;
- 테이블을 가져와서 newtable이란 이름으로 DB에 넣어라


## INSERT INTO SELECT
INSERT INTO table2
SELECT * FROM table1
WHERE condition;

## NULL FUNCTION
[참고 사이트](https://www.w3schools.com/sql/sql_isnull.asp)

## COMMENTS
[참고 사이트](https://www.w3schools.com/sql/sql_comments.asp)
