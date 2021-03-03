
pgstart
psql
CREATE DATABASE lab14;  


\q
psql -f data/schema.sql -d lab14;
psql -f data/seed.sql -d lab14;


\c lab14 ; 

SELECT COUNT(*) FROM books;

CREATE DATABASE lab14_normal WITH TEMPLATE lab14;

\c lab14_normal 
SELECT COUNT(*) FROM books;

CREATE TABLE AUTHORS (id SERIAL PRIMARY KEY, name VARCHAR(255));
\d authors 

INSERT INTO authors(name) SELECT DISTINCT author FROM books; 
SELECT COUNT(*) FROM authors;

ALTER TABLE books ADD COLUMN author_id INT; 
\d books


UPDATE books SET author_id=author.id FROM (SELECT * FROM authors) AS author WHERE books.author = author.name;
SELECT author_id FROM books;

ALTER TABLE books DROP COLUMN author;
\d books

query6 :  ALTER TABLE books ADD CONSTRAINT fk_authors FOREIGN KEY (author_id) REFERENCES authors(id);
\d books