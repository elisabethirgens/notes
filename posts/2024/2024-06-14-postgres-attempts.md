---
layout: post
title: "Import more data into Postgres"
date: 2024-06-14
---

…continuing from [postgres with data]({{ '/2024/06/more-postgres/' | url }}) yesterday. Current status is that I have used `psql` to import data from a CSV to a table named `checkins`. That first stab was a stripped down CSV with only 3 columns and 30 rows, so now I want to learn how to expand with more data in both directions.

## Add venue and city to my table

My project [github.com/elisabethirgens/wanderlust](https://github.com/elisabethirgens/wanderlust) is primarily about travel and less about the beer, so for example venue and city from the checkin is relevant.

```sql
ALTER TABLE checkins
ADD venue_city VARCHAR(100);
```

## Failed attempt

The raw export from Untappd contains a lot more columns than I am interested in. I made a new `untappd-test-2.csv` that is still limited to 30 rows, but now with all 33 columns of the original data. I&nbsp;only want these 5 columns, here is an extract with random rows and only 5 columns:

| checkinid | beer_name      | brewery_name          | venue_name            | venue_city |
| :-------- | :------------- | :-------------------- | :-------------------- | :--------- |
| 1         | Dead Pony Club | BrewDog               | BrewDog Nottingham    | Nottingham |
| 7         | Tiger Tripel   | Nøgne Ø               |                       |            |
| 26        | Old Mephisto   | Bryggeriet Djævlebryg | Henrik Øl- & Vinstove | Bergen     |

Perhaps `psql` will only import data from the columns that I send into the command? 🙏

Lets try:

```sql
\copy checkins (checkinid, beer_name, brewery_name, venue_name, venue_city)
    FROM '~/proj/hello-postgres/untappd-test-2.csv'
    WITH DELIMITER ';' CSV HEADER;
```

Nope, that did not work. Worth a shot! And also now I see that naively copying the same data that I had previously copied, yeah that means I have now duplicated those rows of data. This is why experimenting with only 30 rows first is a good idea.

## Try again

I have now landed on wanting to first clean up the CSV, to first make a file that contains only the columns I am interested in and not the columns of data that I don‘t want for my database. I’m sure there are alternative approaches here, that in many real life projects it would make sense to keep any data available in the raw data export. But for me right now, it seems removing unwanted columns in the CSV first will make it easier for me to continue with learning how to `psql` with my data from Untappd.

---

## Commands to remember

- `which postgres` shows me that I have a brew installed postgresql@16
- `brew services` can confirm if postgresql@16 has started
- `psql -U your_username -d your_database` will open the database admin
  - `\h` for help with SQL commands
  - `\?` for help with psql commands
