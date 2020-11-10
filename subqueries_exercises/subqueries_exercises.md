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

### Exercise 2

```SQL
auction=# SELECT name AS "Bid on items" FROM items WHERE id 
IN (SELECT bids.item_id FROM bids);
 Bid on items  
---------------
 Video Game
 Outdoor Grill
 Painting
 Tent
 Vase
(5 rows)

```

### Exercise 3

```SQL
auction=# SELECT name AS "Not Bid On" FROM items WHERE id 
NOT IN (SELECT bids.item_id FROM bids);
 Not Bid On 
------------
 Television
(1 row)
```

### Exercise 4

```SQL
auction=# SELECT bidders.name FROM bidders
auction-# WHERE EXISTS (SELECT bidder_id FROM bids WHERE bidder_id = bidders.id);

      name       
-----------------
 Alison Walker
 James Quinn
 Taylor Williams
 Alexis Jones
 Gwen Miller
 Alan Parker
(6 rows)



auction=# SELECT DISTINCT bidders.name FROM bidders
INNER JOIN bids
ON bidder_id = bidders.id;
      name       
-----------------
 James Quinn
 Alexis Jones
 Taylor Williams
 Gwen Miller
 Alison Walker
 Alan Parker
```


### Exercise 5
```SQL
auction=# SELECT MAX(count) FROM 
(SELECT COUNT(bidder_id) FROM bids GROUP BY bidder_id) AS max;
 max 
-----
  9
```

### Exercise 6 
```SQL
auction=# SELECT items.name, (SELECT COUNT(bids.item_id) FROM bids WHERE items.id = bids.item_id) FROM items; 
     name      | count 
---------------+-------
 Video Game    |     4
 Outdoor Grill |     1
 Painting      |     8
 Tent          |     4
 Vase          |     9
 Television    |     0
(6 rows)

auction=# SELECT items.name, COUNT(bids.item_id) FROM items
LEFT JOIN bids
ON items.id = bids.item_id
GROUP BY items.name, items.id
ORDER BY items.id;
     name      | count 
---------------+-------
 Video Game    |     4
 Outdoor Grill |     1
 Painting      |     8
 Tent          |     4
 Vase          |     9
 Television    |     0
(6 rows)
```

### Exercise 7

```SQL
auction=# SELECT id FROM items WHERE
auction-# ROW('Painting', 100.00, 250.00) = ROW(name, initial_price, sales_price);
 id 
----
  3
(1 row)

``` 

### Exercise 8 

```SQL
auction=# EXPLAIN SELECT name FROM bidders
WHERE EXISTS (SELECT 1 FROM bids WHERE bids.bidder_id = bidders.id)
auction-# ;
                                QUERY PLAN                                
--------------------------------------------------------------------------
 Hash Join  (cost=33.38..66.47 rows=635 width=32)
   Hash Cond: (bidders.id = bids.bidder_id)
   ->  Seq Scan on bidders  (cost=0.00..22.70 rows=1270 width=36)
   ->  Hash  (cost=30.88..30.88 rows=200 width=4)
         ->  HashAggregate  (cost=28.88..30.88 rows=200 width=4)
               Group Key: bids.bidder_id
               ->  Seq Scan on bids  (cost=0.00..25.10 rows=1510 width=4)
(7 rows)
```

In the example above, the `EXPLAIN` keyword is used which parses the query, without executing it, and returns the estimated processing cost by evaluating each expression in the query and totaling the cost. It is important to note that this only an estimated guess by PostgreSQL. This function should be used to weight up optimization choices when designing with databases in mind.



```SQL
auction=# EXPLAIN ANALYZE SELECT name FROM bidders
WHERE EXISTS (SELECT 1 FROM bids WHERE bids.bidder_id = bidders.id);
 
---------------------------------------------------------------------------------------------------------------------
 Hash Join  (cost=33.38..66.47 rows=635 width=32) (actual time=0.115..0.123 rows=6 loops=1)
   Hash Cond: (bidders.id = bids.bidder_id)
   ->  Seq Scan on bidders  (cost=0.00..22.70 rows=1270 width=36) (actual time=0.017..0.019 rows=7 loops=1)
   ->  Hash  (cost=30.88..30.88 rows=200 width=4) (actual time=0.086..0.087 rows=6 loops=1)
         Buckets: 1024  Batches: 1  Memory Usage: 9kB
         ->  HashAggregate  (cost=28.88..30.88 rows=200 width=4) (actual time=0.038..0.041 rows=6 loops=1)
               Group Key: bids.bidder_id
               ->  Seq Scan on bids  (cost=0.00..25.10 rows=1510 width=4) (actual time=0.008..0.016 rows=26 loops=1)
 Planning time: 0.315 ms
 Execution time: 0.193 ms
(10 rows)
```

In the query above, the `ANALYZE` keyword is added in addition to the `EXPLAIN` keyword. This actually runs the query and gives you accurate information in terms of performance cost it takes to run the query. Moreover, in the query plan it provides additional information like the planning time and execution time in miliseconds.


### Exercise 9

```SQL
EXPLAIN ANALYSE SELECT MAX(bid_counts.count) FROM
  (SELECT COUNT(bidder_id) FROM bids GROUP BY bidder_id) AS bid_counts;
---------------------------------------------------------------------------------------------------------------
 Aggregate  (cost=37.15..37.16 rows=1 width=8) (actual time=0.054..0.056 rows=1 loops=1)
   ->  HashAggregate  (cost=32.65..34.65 rows=200 width=12) (actual time=0.046..0.050 rows=6 loops=1)
         Group Key: bids.bidder_id
         ->  Seq Scan on bids  (cost=0.00..25.10 rows=1510 width=4) (actual time=0.014..0.020 rows=26 loops=1)
 Planning time: 0.154 ms
 Execution time: 0.129 ms
(6 rows)

```

```SQL
auction=# EXPLAIN ANALYZE SELECT COUNT(bidder_id) AS max_bid FROM bids
  GROUP BY bidder_id
  ORDER BY max_bid DESC
  LIMIT 1;

---------------------------------------------------------------------------------------------------------------------
 Limit  (cost=35.65..35.65 rows=1 width=12) (actual time=0.063..0.065 rows=1 loops=1)
   ->  Sort  (cost=35.65..36.15 rows=200 width=12) (actual time=0.062..0.063 rows=1 loops=1)
         Sort Key: (count(bidder_id)) DESC
         Sort Method: top-N heapsort  Memory: 25kB
         ->  HashAggregate  (cost=32.65..34.65 rows=200 width=12) (actual time=0.045..0.049 rows=6 loops=1)
               Group Key: bidder_id
               ->  Seq Scan on bids  (cost=0.00..25.10 rows=1510 width=4) (actual time=0.015..0.021 rows=26 loops=1)
 Planning time: 0.174 ms
 Execution time: 0.125 ms
(9 rows)

```

It would appear from a comparison of the two querires that the subquery statement has a larger performance cost than the JOIN query. However, it's execution time is actually faster than the the JOIN table when both its planning and execution time are adding together. This would suggest that even if a query has a larger performance cost it may still be the more efficient solution if it's total time is quicker. 