# Basic Queries
* Retrieve all book and list author name
```SQL
SELECT BOOK.isbn, title, N.fname, N.fname
FROM BOOK, PUBLISHERS, NAMES AS  N, AUTHOR AS  A
WHERE BOOK.pid == PUBLISHERS.pid AND
  N.id == A.name_id AND
  BOOK.isbn == A.isbn;
```
* Retrieve all the book published by publisher named 'McGraw-Hill Osborne Media'
```SQL
SELECT title,isbn
FROM BOOK, PUBLISHERS
WHERE BOOK.pid == PUBLISHERS.pid AND
  PUBLISHERS.publisher == 'McGraw-Hill Osborne Media';
```
* Retrieve all the book written by author name 'Chip Dawes'
```SQL
SELECT B.isbn, B.title
FROM BOOK AS B, AUTHOR AS A , NAMES AS N
WHERE B.isbn == A.isbn AND
  N.id == A.name_id AND
  N.fname == 'Chip' AND
  N.lname == 'Dawes';
```
* Retrieve all customer information
```SQL
SELECT C.entity_id, N.fname, N.lname,phone ,email
FROM ENTITY AS E , NAMES AS  N, CUSTOMER AS  C
WHERE E.name_id == N.id AND
  C.entity_id == E.id;
```

* Retrieve a customer's order information
```SQL
SELECT C.entity_id, N.fname, N.lname, B.isbn, B.title
FROM BOOK AS B, ORDERITEM AS O, "ORDER",CUSTOMER AS C,ENTITY AS E, NAMES AS N
WHERE C.entity_id == E.id AND
  E.name_id == N.id AND
  C.entity_id == "ORDER".customer_id AND
  "ORDER".order_id == O.order_id AND
  O.product_id == B.isbn;
```
