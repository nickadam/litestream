# litestream
Getting to know litestream

The MinIO deployment starts using default root credentials `minioadmin:minioadmin`.

Login to minio and create the bucket, app.

Exec into the app container and create a database.
```
sqlite3 -header -csv /data/db.sqlite3 'CREATE TABLE IF NOT EXISTS kv (k TEXT PRIMARY KEY, v TEXT, timestamp DATETIME DEFAULT CURRENT_TIMESTAMP)'
```

Add some data
```
sqlite3 -header -csv /data/db.sqlite3 "INSERT INTO kv(k, v) VALUES('a_key', 'This is a test')"
sqlite3 -header -csv /data/db.sqlite3 "SELECT * FROM kv"
```

Shut everything down and delete the data volume

Start it back up, go into the litestream container and run `litestream restore /data/db.sqlite3`

Now verify your data is there by going back into the app container and running

```
sqlite3 -header -csv /data/db.sqlite3 "SELECT * FROM kv"
```
