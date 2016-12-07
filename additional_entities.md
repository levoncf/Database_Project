# Additional Entities

## RATING
* Retrieve all books and their ratings
``` SQL
SELECT B.title, C.category, R.RATING
FROM BOOK AS B, RATING AS R, CATEGORY AS C
WHERE B.B_ID = R.b_id AND C.c_id = B.cid;
```
* Retrieve all the books with ratings above 3.5
```SQL
SELECT B.title, C.category, R.RATING
FROM RATING AS R, BOOK AS B, CATEGORY AS C
WHERE B.b_id = R.b_id AND C.c_id = B.cid AND R.RATING > 3.5;
```
## Retrive all categories and their ratings
```SQL
SELECT C.category, COUNT(C.category) AS Num_Books_In_Category, AVG(R.RATING) AS Average_Rating
FROM CATEGORY AS C, RATING AS R, BOOK AS B 
WHERE B.cid=C.c_id AND R.b_id = B.b_id
GROUP BY C.category
```
## Retrieve publishers, number of the books published and the average ratings of the books published by the publishers
```SQL
SELECT P.publisher, COUNT(P.publisher), AVG(R.RATING)
FROM PUBLISHERS AS P, RATING AS R, BOOK AS B
WHERE P.pid = B.pid AND R.b_id=B.b_id
GROUP BY P.publisher
```
#
#
## INVENTORY

## Retrieve information of the books (title, year, category, price) that have sold less than 1 book
```SQL
SELECT B.title, B.year, C.category, B.price, I.sold
FROM INVENTORY AS I, BOOK AS B, CATEGORY AS C 
WHERE I.bid = B.b_id AND C.c_id = B.cid AND I.sold < 1
GROUP BY B.title
```
## Retrieve information about the location of the books and the number of the books at the specific location
```SQL
SELECT B.title, I_S.ISBN, W.wid, W.wlocation, SUM(I.quantity) AS Num_Books
FROM INVENTORY AS I, WAREHOUSE AS W, BOOK AS B, ISBN AS I_S
WHERE W.wid = I.wid AND I.bid = B.b_id AND I_S.b_id = B.b_id
GROUP BY B.title
```
## Retrieve information about the books that have been published in 2003 and have sold no more than 5 books
```SQL
SELECT B.title, I_S.ISBN, B.year, B.price, SUM(I.quantity) AS Num_Books
FROM INVENTORY AS I, BOOK AS B, ISBN AS I_S
WHERE I.bid = B.b_id AND I_S.b_id = B.b_id AND B.year < 2003 AND I.sold < 5 
GROUP BY B.title
```
