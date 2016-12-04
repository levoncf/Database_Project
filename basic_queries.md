# Basic Queries

- Retrieve all book and list author name

  ```sql
  SELECT BOOK.isbn, title, N.fname, N.fname
  FROM BOOK, PUBLISHERS, NAMES AS  N, AUTHOR AS  A
  WHERE BOOK.pid == PUBLISHERS.pid AND
  N.id == A.name_id AND
  BOOK.isbn == A.isbn;
  ```

- Retrieve all the book published by publisher named 'McGraw-Hill Osborne Media'

  ```sql
  SELECT title,isbn
  FROM BOOK, PUBLISHERS
  WHERE BOOK.pid == PUBLISHERS.pid AND
  PUBLISHERS.publisher == 'McGraw-Hill Osborne Media';
  ```

- Retrieve all the book written by author name 'Chip Dawes'

  ```sql
  SELECT B.isbn, B.title
  FROM BOOK AS B, AUTHOR AS A , NAMES AS N
  WHERE B.isbn == A.isbn AND
  N.id == A.name_id AND
  N.fname == 'Chip' AND
  N.lname == 'Dawes';
  ```

- Retrieve all customer information

  ```sql
  SELECT C.entity_id, N.fname, N.lname,phone ,email
  FROM ENTITY AS E , NAMES AS  N, CUSTOMER AS  C
  WHERE E.name_id == N.id AND
  C.entity_id == E.id;
  ```

- Retrieve a customer's order information

  ```sql
  SELECT C.entity_id, N.fname, N.lname, B.isbn, B.title, O.quantity
  FROM BOOK AS B, ORDERITEM AS O, "ORDER",CUSTOMER AS C,ENTITY AS E, NAMES AS N
  WHERE C.entity_id == E.id AND
  E.name_id == N.id AND
  C.entity_id == "ORDER".customer_id AND
  "ORDER".order_id == O.order_id AND
  O.product_id == B.isbn AND
  N.fname == 'Jane' AND N.lname == 'Gonzalez';
  ```

  # Queries from Checkpoint 2

- Find the titles of all books by Pratchett that cost less than $10.

  ```sql
  SELECT B.isbn, B.title
  FROM BOOK AS B
  WHERE (SELECT A.isbn
       FROM AUTHOR AS A, NAMES AS N
       WHERE A.name_id == N.id AND
       N.lname LIKE 'Pratchett%' AND
       A.isbn == B.isbn) == B.isbn AND
      B.price <= 10;
  ```

- Give all the titles and their dates of purchase made by a single customer (you choose how to designate the customer).

  ```sql
  SELECT OIT.product_id, B.title, OIT.timestamp, OIT.quantity
  FROM BOOK AS B, 'ORDER' AS O, ORDERITEM AS OIT
  WHERE
  (SELECT C.entity_id
  FROM CUSTOMER AS C, ENTITY AS E, NAMES AS N
  WHERE E.name_id == N.id AND
  C.entity_id == E.id AND
  N.fname == 'Jane' AND
  N.lname == 'Gonzalez') == O.customer_id AND
  O.order_id == OIT.order_id AND
  OIT.product_id == B.isbn;
  ```

- Find the titles and ISBNs for all books with less than 5 copies in stock. (CHECKED)

  ```sql
  SELECT B.title, I.ISBN
  FROM BOOK AS B, ISBN AS I, INVENTORY AS IV
  WHERE
  ( B.b_id == I.b_id AND IV.bid == I.b_id AND IV.quantity < 5
  );
```
- Give all the customers who purchased a book by Pratchett and the titles of Pratchett books they purchased.
- Find the total number of books purchased by a single customer (you choose how to designate the customer). (CHECKED
  
  ```sql
  SELECT N.fname, SUM(OIT.quantity)
  FROM BOOK AS B, 'ORDERS' AS O, ORDERITEM AS OIT, NAMES AS N
  WHERE
  (SELECT C.entity_id
  FROM CUSTOMER AS C, ENTITY AS E
  WHERE E.name_id == N.id AND
  C.entity_id == E.id AND
  N.fname == 'Jane' AND
  N.lname == 'Gonzalez') == O.customer_id AND
  O.order_id == OIT.order_id AND
  OIT.bid == B.b_id;

- Find the customer who has purchased the most books and the total number of books they have purchased.
- Three more Additional Queries (include joins and at least one include aggregate function and at least one Queries use 'extra' Entities from Checkpoint 1).

# Queries from Checkpoint 3

- Provide a list of customer names, along with the total dollar amount each customer has spent.
- Provide a list of customer names and e-mail addresses for customers who have spent more than the average customer.
- Provide a list of the titles in the database and associated total copies sold to customers, sorted from the title that has sold the most individual copies to the title that has sold the least.
- Provide a list of the titles in the database and associated dollar totals for copies sold to customers, sorted from the title that has sold the highest dollar amount to the title that has sold the smallest.
- Find the most popular author in the database (i.e. the one who has sold the most books).
- Find the most profitable author in the database for this store (i.e. the one who has brought in the most money).
- Provide a list of customer information for customers who purchased anything written by the most profitable author in the database.
- Provide the list of authors who wrote the books purchased by the customers who have spent more than the average customer.
