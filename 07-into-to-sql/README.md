Intro to SQL
============

### Persistence


### Things we can do to data:



1. Install the SQLite Browser if you haven't already [here](http://sqlitebrowser.org/)
2. Open the SQLite Browser and click 'File -> Open DataBase'
3. Choose the `chinook.db` file from this repo. This database is open source and maintained by Microsoft (SQL is no fun if you don't have any data)
4. Click the tab that says 'Execute SQL'. Type SQL queries in the box above. Press the play button. See the results of that query in the box below

## Challenges

1. Write the SQL to return all of the rows in the artists table?

Which part of CRUD?

```SQL
SELECT * FROM artists;
```

2. Write the SQL to select the artist with the name "Black Sabbath"

```SQL
SELECT * FROM artists WHERE name="Black Sabbath";
```

3. Write the SQL to create a table named 'fans' with an autoincrementing ID that's a primary key and a name field of type text

```sql
CREATE TABLE fans (id INTEGER PRIMARY KEY, name TEXT);
```

4. Write the SQL to alter the fans table to have a artist_id column type integer?

```sql
ALTER TABLE fans ADD artist_id INTEGER;
```

5. Write the SQL to add yourself as a fan of the Black Eyed Peas? artists.id **169**
CRUD?

```sql
INSERT INTO fans (name, artist_id) VALUES ("Rishi", 169);
```

```sql
INSERT INTO fans (name, artist_id) VALUES ("Duke",
  (SELECT id from artists WHERE name="Black Eyed Peas")
);
```

6. Check out the [Faker gem](https://github.com/stympy/faker). `gem install faker`, open up irb, run `require 'faker'` and then generate a fake name for yourself using `Faker::Name.name`. How would you update your name in the fans table to be your new name?

```sql
UPDATE fans SET name="Rishikesh" WHERE name="Rishi";
```

7. Write the SQL to return fans that are not fans of the black eyed peas.

```sql
SELECT * FROM fans WHERE artist_id!=169;
```

8. Write the SQL to display an artists name next to their album title


```sql
SELECT artists.name, albums.title FROM artists INNER JOIN albums ON artists.id=albums.artist_id;
```

we can choose not to specify that the album belongs to an artist, but unfortunately that gives us a solution where every artist and every album are connected
```sql

SELECT artists.name, albums.title FROM artists, albums;
```

9. Write the SQL to display artist name, album name and number of tracks on that album

```sql
SELECT artists.name AS Artist, albums.title AS Album, COUNT(tracks.id) AS "Track Count" FROM artists INNER JOIN albums ON artists.id=albums.artist_id INNER JOIN tracks ON albums.id=tracks.album_id GROUP BY tracks.album_id;
```

10. Write the SQL to return the name of all of the artists in the 'Pop' Genre

```sql
SELECT DISTINCT artists.name AS Artist FROM artists INNER JOIN albums ON  artists.id=albums.artist_id INNER JOIN tracks ON albums.id=tracks.album_id INNER JOIN genres ON genres.id=tracks.genre_id WHERE genres.name="Pop";
```

## BONUS (very hard)

11. I want to return the names of the artists and their number of rock tracks
    who play Rock music
    and have move than 30 tracks
    in order of the number of rock tracks that they have
    from greatest to least

```sql

```