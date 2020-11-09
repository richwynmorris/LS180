### Exercise 1 

```SQL
auction=# CREATE TABLE bidders (
auction(# id serial PRIMARY KEY,
auction(# name text NOT NULL );
CREATE TABLE

auction=# CREATE TABLE items (
id serial PRIMARY KEY,
name text NOT NULL,
initial_price numeric(6,2) NOT NULL,
sales_price numeric(6,2) );
CREATE TABLE

auction=# CREATE TABLE bids (
id serial PRIMARY KEY,
bidder_id int NOT NULL REFERENCES bidders(id) ON DELETE CASCADE,
item_id int NOT NULL REFERENCES items(id) ON DELETE CASCADE,
amount numeric(6,2));
CREATE TABLE

auction=# CREATE INDEX bid_bidder_item ON bids (bidder_id, item_id);
CREATE INDEX

\copy bidders FROM 'Documents/SQL/subqueries_exercises/bidders.csv' WITH HEADER CSV;
COPY 7

\copy items FROM 'Documents/SQL/subqueries_exercises/items.csv' WITH HEADER CSV;
COPY 6

\copy bids FROM 'Documents/SQL/subqueries_exercises/bids.csv' WITH HEADER CSV;
COPY 26
```
