# Booktown, USA

For each question below, find the approriate SQL query to obtain the information requested. Create a `.sql` file that contains all of your answers.

## Getting Started

To get started we'll need to import the booktown.sql file.

1. Fork and clone this repository
2. `cd` into the repository
3. use the command `psql -f booktown.sql`
4. type `psql` to open your psql console
5. type `\list` to ensure the booktown database was successfully completed
6. type `\c booktown` to connect to the booktown database
7. type `\d` to see a list of all the tables in the booktown database
8. type `\d [TABLE_NAME]` to see information about columns and their types for a specific table. You should see output like below:

```
booktown=# \d books
       Table "public.books"
   Column   |  Type   | Modifiers 
------------+---------+-----------
 id         | integer | not null
 title      | text    | not null
 author_id  | integer | 
 subject_id | integer | 
Indexes:
    "books_id_pkey" PRIMARY KEY, btree (id)
    "books_title_idx" btree (title)
```

## Queries

Complete the following exercises to practice using SQL.

### Order
* Find all subjects sorted by subject
	SELECT * FROM subjects ORDER BY subject;
* Find all subjects sorted by location
	SELECT * FROM subjects ORDER BY location;

### Where
* Find the book "Little Women"
SELECT title FROM books WHERE title='Little Women';
* Find all books containing the word "Python"
	SELECT * FROM books WHERE title LIKE '%Python';
* Find all subjects with the location "Main St" sort them by subject
	ELECT * FROM subjects WHERE location='Main St' ORDER BY subject;


### Joins

* Find all books about Computers and list ONLY the book titles
	SELECT books.title FROM books JOIN subjects ON books.subject_id = subjects.id WHERE subjects.id = 4;

* Find all books and display a result table with ONLY the following columns
	* Book title
	* Author's first name
	* Author's last name
	* Book subject

	SELECT books.title, authors.first_name, authors.last_name, subjects.subject FROM subjects JOIN books ON books.subject_id = subjects.id JOIN authors ON books.author_id = authors.id;

* Find all books that are listed in the stock table
	* Sort them by retail price (most expensive first)
	* Display ONLY: title and price
SELECT stock.retail, books.title FROM books JOIN editions ON books.id = editions.book_id JOIN stock ON editions.isbn = stock.isbn ORDER BY stock.retail DESC;
\
* Find the book "Dune" and display ONLY the following columns
	* Book title
	* ISBN number
	* Publisher name
	* Retail price
Select books.title, editions.isbn, publishers.name, stock.retail FROM books JOIN editions ON books.id = editions.book_id JOIN publishers ON publishers.id = editions.publisher_id JOIN stock ON stock.isbn = editions.isbn 

Find all shipments sorted by ship date display a result table with ONLY the following columns:
	* Customer first name
	* Customer last name
	* ship date
	* book title
SELECT customers.first_name, customers.last_name, shipments.ship_date, books.title FROM customers JOIN shipments ON customers.id = shipments.customer_id JOIN editions ON shipments.isbn = editions.isbn JOIN books ON editions.book_id = books.id;

### Grouping and Counting

* Get the COUNT of all books
	SELECT count(*) FROM books;
* Get the COUNT of all Locations
	SELECT count(subjects.location) FROM subjects;
* Get the COUNT of each unique location in the subjects table. Display the count and the location name. (hint: requires GROUP BY).
	SELECT location, COUNT(location) FROM subjects GROUP BY location;
* List all books. Display the book_id, title, and a count of how many editions each book has. (hint: requires GROUP BY and JOIN)
 
#### YAY! You're done!!

---

## Licensing
1. All content is licensed under a CC-BY-NC-SA 4.0 license.
2. All software code is licensed under GNU GPLv3. For commercial use or alternative licensing, please contact legal@ga.co.
