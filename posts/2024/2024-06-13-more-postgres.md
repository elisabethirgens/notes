---
layout: post
title: 'Postgres with data'
date: 2024-06-13
---

…continuing from my first steps to [poke at postgres]({{ '/2024/06/poke-at-postgres/' | url }}) yesterday! And since I need some data to play around with, this is a perfect opportunity to pick up my [Untappd project]({{ '/2023/11/free-my-photos/' | url }}) again.

## Open the database admin

```
psql -U your_username -d your_database
```

Ah. Right. This will… open a portal into the database administration thingy where I will actually be running these commands. This is the choice I made when selecting `psql` over a GUI. Excellent. When I was running a couple of commands yesterday, those were not against the PostgreSQL server because I hadn’t actually connected to it yet. Now I can start to do things like:

## Create a table

```sql
CREATE TABLE checkins (
    id INTEGER,
    beer_name VARCHAR(100),
    brewery_name VARCHAR(100)
);
```

Changed my mind about the `id` name. No worries, I can rename:

```sql
ALTER TABLE checkins
RENAME COLUMN id TO checkinid;
```

## Import the CSV Data

I made a limited `untappd-test-1.csv` with 3 columns and 30 rows. Extract with random rows:

| checkinid | beer_name      | brewery_name          |
| :-------- | :------------- | :-------------------- |
| 1         | Dead Pony Club | BrewDog               |
| 7         | Tiger Tripel   | Nøgne Ø               |
| 26        | Old Mephisto   | Bryggeriet Djævlebryg |

So the command I can now use looks like this:

```sql
\copy checkins (checkinid, beer_name, brewery_name) FROM '/Users/katla/proj/hello-postgres/untappd-test-1.csv' DELIMITER ';' CSV HEADER;
```

Hm. What exactly is `\copy` here? 🤔 <br>
Okay! That is a `psql` command.

- `\h` gives me help with sql
- `\?` helps with `psql` commands and can for example describe that:

```
Input/Output
  \copy ...              perform SQL COPY with data stream to the client host
```

Did importing the data work? 🥁

## Verify

```
SELECT * FROM checkins;
```

Yesssssss!! I can now see data from the CSV has been imported into my `checkins` database. 🥳

---

TIL to remember the semicolon! I am so used to my editor being rigged to add semicolons for me in JavaScript, that when I first started out using `psql` I kept forgetting to terminate my query. Which in turn made me confused about why a thing I tried didn‘t work as I expected. I realise now that I hadn’t executed the query, and then tried running another one, but getting syntax errors.

Also: it’s really cool to see after just a tiny bit of experience with `psql`, I can scroll up in my terminal to re-read all of the initial errors and now understand for each of them why I got the error. It becomes easier to _read_ the errors and understand that “No, there is not a super complicated concept I have missed here, it really is just a case of double checking my query and making sure I am not referring to a name that does not exist in that table” and so on.
