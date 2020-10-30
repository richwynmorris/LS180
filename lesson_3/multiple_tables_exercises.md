
### Exercise 1
Import this file into an empty PostgreSQL database. Note: the file contains a lot of data and may take a while to run; your terminal should return to the command prompt once the import is complete.

**Answer:**
```SQL
psql -d examples < Documents/SQL/lesson_3/theatre_full.SQL
```

### Exercise 2
Write a query that determines how many tickets have been sold.

Expected Output
```SQL
count
-------
3783
(1 row)
```
**Answer:**
```SQL
examples=# SELECT count(id) FROM tickets;
 count 
-------
  3783
(1 row)
```

### Exercise 3
Write a query that determines how many different customers purchased tickets to at least one event.

```SQL
Expected Output

  count
-------
  1652
(1 row)
```
**Answer:**
```SQL
examples=# SELECT COUNT(DISTINCT customer_id) FROM tickets;
 count 
-------
  1652
(1 row)
```

### Exercise 4
Write a query that determines what percentage of the customers in the database have purchased a ticket to one or more of the events.

Expected Output

```SQL
  percent
----------
    16.52
(1 row)
```

**Answer:**
```SQL
examples=# SELECT COUNT(DISTINCT tickets.customer_id) / COUNT (DISTINCT customers.id)::float * 100 AS percent FROM customers
LEFT JOIN tickets ON customers.id = tickets.customer_id;
 percent 
---------
   16.52
(1 row)

```

### Exercise 5

Write a query that returns the name of each event and how many tickets were sold for it, in order from most popular to least popular.

Expected Output

```SQL

            name            | popularity
----------------------------+------------
  A-Bomb                     |        555
  Captain Deadshot Wolf      |        541
  Illustrious Firestorm      |        521
  Siren I                    |        457
  Kool-Aid Man               |        439
  Green Husk Strange         |        414
  Ultra Archangel IX         |        359
  Red Hope Summers the Fated |        307
  Magnificent Stardust       |        134
  Red Magus                  |         56
(10 rows)

```

**Answer:**

```SQL
examples=# SELECT events.name AS name, COUNT(tickets.event_id) AS popularity FROM events 
LEFT JOIN tickets ON events.id = tickets.event_id
GROUP BY name
examples-# ORDER BY popularity DESC;
            name            | popularity 
----------------------------+------------
 A-Bomb                     |        555
 Captain Deadshot Wolf      |        541
 Illustrious Firestorm      |        521
 Siren I                    |        457
 Kool-Aid Man               |        439
 Green Husk Strange         |        414
 Ultra Archangel IX         |        359
 Red Hope Summers the Fated |        307
 Magnificent Stardust       |        134
 Red Magus                  |         56
(10 rows)
```


### Exercise 6

Write a query that returns the user id, email address, and number of events for all customers that have purchased tickets to three events.

```SQL
Expected Output

  id   |                email                 | count
-------+--------------------------------------+-------
  141  | isac.hayes@herzog.net                |     3
  326  | tatum.mraz@schinner.org              |     3
  624  | adelbert.yost@kleinwisozk.io         |     3
  1719 | lionel.feeney@metzquitzon.biz        |     3
  2058 | angela.ruecker@reichert.co           |     3
  3173 | audra.moore@beierlowe.biz            |     3
  4365 | ephraim.rath@rosenbaum.org           |     3
  6193 | gennaro.rath@mcdermott.co            |     3
  7175 | yolanda.hintz@binskshlerin.com       |     3
  7344 | amaya.goldner@stoltenberg.org        |     3
  7975 | ellen.swaniawski@schultzemmerich.net |     3
  9978 | dayana.kessler@dickinson.io          |     3
(12 rows)
```

**Answer:**

```SQL
examples=# SELECT customers.id as id, customers.email as email, COUNT(DISTINCT tickets.event_id)                                                                                          FROM customers INNER JOIN tickets ON tickets.customer_id = customers.id GROUP BY customers.id                                            
HAVING COUNT(DISTINCT tickets.event_ID) = 3;
  id  |                email                 | count 
------+--------------------------------------+-------
  141 | isac.hayes@herzog.net                |     3
  326 | tatum.mraz@schinner.org              |     3
  624 | adelbert.yost@kleinwisozk.io         |     3
 1719 | lionel.feeney@metzquitzon.biz        |     3
 2058 | angela.ruecker@reichert.co           |     3
 3173 | audra.moore@beierlowe.biz            |     3
 4365 | ephraim.rath@rosenbaum.org           |     3
 6193 | gennaro.rath@mcdermott.co            |     3
 7175 | yolanda.hintz@binskshlerin.com       |     3
 7344 | amaya.goldner@stoltenberg.org        |     3
 7975 | ellen.swaniawski@schultzemmerich.net |     3
 9978 | dayana.kessler@dickinson.io          |     3
(12 rows)

```

### Exercise 7

Write a query to print out a report of all tickets purchased by the customer with the email address 'gennaro.rath@mcdermott.co'. The report should include the event name and starts_at and the seat's section name, row, and seat number.

```SQL
Expected Output

        event        |      starts_at      |    section    | row | seat
--------------------+---------------------+---------------+-----+------
  Kool-Aid Man       | 2016-06-14 20:00:00 | Lower Balcony | H   |   10
  Kool-Aid Man       | 2016-06-14 20:00:00 | Lower Balcony | H   |   11
  Green Husk Strange | 2016-02-28 18:00:00 | Orchestra     | O   |   14
  Green Husk Strange | 2016-02-28 18:00:00 | Orchestra     | O   |   15
  Green Husk Strange | 2016-02-28 18:00:00 | Orchestra     | O   |   16
  Ultra Archangel IX | 2016-05-23 18:00:00 | Upper Balcony | G   |    7
  Ultra Archangel IX | 2016-05-23 18:00:00 | Upper Balcony | G   |    8
(7 rows)
```

```SQL
examples=# SELECT events.name AS event, events.starts_at, sections.name AS section, seats.row, seats.number AS seat FROM tickets  
INNER JOIN events
ON tickets.event_id = events.id
INNER JOIN customers
ON tickets.customer_id = customers.id
INNER JOIN seats
ON tickets.seat_id = seats.id
INNER JOIN sections
ON seats.section_id = sections.id
WHERE customers.email = 'gennaro.rath@mcdermott.co';
       event        |      starts_at      |    section    | row | seat 
--------------------+---------------------+---------------+-----+------
 Kool-Aid Man       | 2016-06-14 20:00:00 | Lower Balcony | H   |   10
 Kool-Aid Man       | 2016-06-14 20:00:00 | Lower Balcony | H   |   11
 Green Husk Strange | 2016-02-28 18:00:00 | Orchestra     | O   |   14
 Green Husk Strange | 2016-02-28 18:00:00 | Orchestra     | O   |   15
 Green Husk Strange | 2016-02-28 18:00:00 | Orchestra     | O   |   16
 Ultra Archangel IX | 2016-05-23 18:00:00 | Upper Balcony | G   |    7
 Ultra Archangel IX | 2016-05-23 18:00:00 | Upper Balcony | G   |    8
(7 rows)
```