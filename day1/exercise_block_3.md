## Exercise Block #3: Snapshot & Restore

## Exercise 1:Create a snapshot repository using:

``` json
PUT /_snapshot/first_backup
{
  "type": "fs",
  "settings": {
    "location": "first_backup_location",
    "compress": true
  }
}
```

## Exercise 2:Take a snapshot of the movies index.
``` json
PUT /_snapshot/first_backup/snapshot_1
{
  "indices": "movies",
  "ignore_unavailable": true,
  "include_global_state": false
}
```

## Exercise 3:Delete the movies index and restore it from the snapshot.

``` json
DELETE /movies
```

Check that the index is deleted:
```json
GET /movies
```

``` json
POST /_snapshot/first_backup/snapshot_1/_restore
{
  "indices": "movies",
  "ignore_unavailable": true,
  "include_global_state": false
}
```
