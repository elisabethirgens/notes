---
layout: post
title: "Select all the things with SQL"
date: 2024-11-08
---

We have enjoyed a full week devoted to learning at work, and in between teaching Git, I also managed to [pick up Postgres again]({{ '/2024/06/pick-up-postgres/' | url }}) yesterday. I now have a database with the data I want, and the next step is to practice writing queries to explore the data…

```sql
-- Show me the last 50 rows of checkins from before I quit Untappd

SELECT * FROM checkins ORDER BY created_at DESC LIMIT 50;
```

```sql
-- Show all rows from a specific year

SELECT * FROM checkins WHERE EXTRACT(YEAR FROM created_at) = 2015;
```

```sql
-- Show me rows from my fake birthday date

SELECT * FROM checkins
WHERE EXTRACT(MONTH FROM created_at) = 01
  AND EXTRACT(DAY FROM created_at) = 01;
```

```sql
-- Show all rows from cities where I have not lived, but travelled to!

SELECT * FROM checkins
WHERE venue_city IS NOT NULL
  AND venue_city <> ''
  AND venue_city <> 'Bergen'
  AND venue_city <> 'Oslo';
```

```sql
-- List every city in alphabetical order without any other data

SELECT DISTINCT venue_city FROM checkins ORDER BY venue_city;
```

Aaah yes, this is what problems with data quality can look like… 😅

```
       venue_city
------------------------
 Copenhagen N
 Copenhagen V
 København
 København K
 København N
 København V
```

Counties should be interesting, too!

```sql
-- List every country in alphabetical order without any other data

SELECT DISTINCT venue_country FROM checkins ORDER BY venue_country;
```

```
 venue_country
----------------
 Danmark
 Deutschland
 Espanya
 España
 France
 Ireland
 Italia
 Magyarország
 Nederland
 Norge
 Sverige
 United Kingdom
 United States
 Ísland
 ประเทศไทย
 日本
 臺灣
 香港

(19 rows)
```

```sql
-- Show me all rows from Taiwan

SELECT * FROM checkins WHERE venue_country = '臺灣';

```

All right, that is enough for now, but this was fun! 🎉
