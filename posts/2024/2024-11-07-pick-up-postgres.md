---
layout: post
title: "Pick up Postgres again! 🐘"
date: 2024-11-07
---

Months have passed since I started [poking at postgres]({{ '/2024/06/poke-at-postgres/' | url }}) and time flies, but this week we have another study week at work — and I am ready to pick up where I left off. Thankfully I have written these notes, that was super helpful now for reminding myself what I learnt back in June and where to go next after this failed attempt to [import more data into Postgres]({{ '/2024/06/postgres-attempts/' | url }}).

The raw exported data contains many columns that I don’t want to copy into my database. I kinda thought I could write a `psql` command to only copy specific columns, but as far as I understand, the `\copy` command does not support that.

## Preprocess CSV

The complete export weights in at only 925 KB, so I am happy to use Numbers as the approach delete columns I don’t want to copy. But first a test file with 30 rows!

## Create table

```sql
CREATE TABLE checkins (
    id INTEGER,
    beer_name VARCHAR(100),
    brewery_name VARCHAR(50),
    venue_name VARCHAR(100),
    venue_city VARCHAR(50),
    venue_country VARCHAR(50),
    created_at DATE,
    checkin_id INTEGER
);
```

## Copy to database from CSV

```sql
\copy checkins (id, beer_name, brewery_name,
    venue_name, venue_city, venue_country, created_at, checkin_id)
    FROM '~/proj/hello-postgres/untappd-test-7.csv'
    WITH DELIMITER ';' CSV HEADER;
```

## Verify limited test

```sql
SELECT * FROM checkins;
```

Perfect! Now ready to repeat on a complete export.

## Repeat with full export

- I have preprocessed a CSV with all checkins, but only the 8 columns I want
- `CREATE TABLE checkins ()` like before
- `\copy checkins ()` from a CSV with 2817 rows of data

…and whoa, new fun errors!

```
ERROR:  value too long for type character varying(50)
CONTEXT:  COPY checkins, line 209, column brewery_name: "BIRRIFICIO AGRICOLO BALADIN - Baladin Indipendente Italian Farm Brewery"
```

I am so curious

```
ERROR:  value too long for type character varying(100)
CONTEXT:  COPY checkins, line 2565, column beer_name: "PATRONS PROJECT 14.07 // BLOOD YOUTH // RUDE RECORDS // VISIONS OF ANOTHER ALE // TROPICAL IMPERIAL ..."
```

Haha, okay, I will give both `beer_name` and `brewery_name` 200 characters 😅 and learn about different approaches to truncate or whatever later. But now…

```sql
CREATE TABLE
postgres=# \copy checkins (id, beer_name, brewery_name,
    venue_name, venue_city, venue_country, created_at, checkin_id)
    FROM '~/proj/hello-postgres/untappd-all-2.csv'
    WITH DELIMITER ';' CSV HEADER;
COPY 2817
```

🥳

Excellent! I can now start practicing writing queries.

### …and how long are the longest beer names anyway?!

```sql
SELECT brewery_name, beer_name, LENGTH(beer_name) AS beer_name_length
FROM checkins
ORDER BY beer_name_length DESC
LIMIT 10;
```

```
       brewery_name       |                                                            beer_name                                                            | beer_name_length
--------------------------+---------------------------------------------------------------------------------------------------------------------------------+------------------
 Evil Twin Brewing NYC    | THERE’S NOTHING BETTER THAN YOUR NON-NYC FRIENDS TELLING YOU HOW BIG OF A MORTGAGE YOU COULD TAKE WITH YOUR RENT PAYMENT        |              120
 Northern Monk            | PATRONS PROJECT 14.07 // BLOOD YOUTH // RUDE RECORDS // VISIONS OF ANOTHER ALE // TROPICAL IMPERIAL BLACK IPA                   |              109
 Yo-Ho Brewing Company    | Zenryaku Konominante Kiitenaize Sorry Session Yuzu Ale (前略 好みなんて聞いてないぜSORRY セッション柚子エール ～あら塩仕立て～)           |               96
 Northern Monk            | Patrons Project 3.01 // Coconut Black IPA // James Butler // Attack on the Bounty // Siren                                      |               90
 Evil Twin Brewing NYC    | PRETTY STOKED ABOUT EATING AT MY FAVORITE RESTAURANT I’VE ONLY HAD TAKEOUT FROM UNTIL NOW                                       |               89
 S43 Brewery              | Our Lawyers Made Us Change the Name of This Beer So We Don't Get Sued                                                           |               69
 AleSmith Brewing Company | Speedway Stout (w/ Mexican Dark Chocolate, Sea Salt & Mexican Coffee)                                                           |               69
 Brew By Numbers          | π|09 (Pi|09) - Pilot Series - Mixed Ferm Witbier (Wai-iti & Waimea)                                                             |               67
 Hoppin' Frog Brewery     | Tower Tuesday Series Infusion C Vanilla Bean Gangster Frog I.P.A.                                                               |               65
 Yo-Ho Brewing Company    | Karuizawa Beer Craft Saurus Black IPA (軽井沢ビール クラフトザウルス ブラックIPA)                                                     |               63
(10 rows)
```

Definitly need to keep those. Perhaps I can set the length to 120? I have checked in my last beer and stopped using Untappd, so no matter what new names Evil Twin come up with for me to drink, this will still be the longest name in the data set.
