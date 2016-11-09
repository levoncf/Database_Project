# Additional Entities
## RATING
* Retrieve all book and it's rating
``` SQL
SELECT B.isbn, B.title, R.RATING
FROM BOOK AS B, RATING AS R
WHERE B.isbn == R.isbn;
```
* check all the book with rating above 3
```SQL
SELECT B.isbn, B.title, R.RATING
FROM BOOK AS B, RATING AS R
WHERE B.isbn == R.isbn AND
R.RATING >= 3;
```
## INVENTORY
