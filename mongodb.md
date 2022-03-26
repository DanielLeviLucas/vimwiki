### Import and export JSON in mongoDB

#### To import JSON

```
mongoimport "path/to/file" -d <databaseName> -c <collectionName> --jsonArray
```

#### To export JSON

```
mongoexport --db <databaseName> --collection <collectionName> --type json --jsonArray --out "path/to/file"
```

## Commands

- To check the performance of a query

```
db.collectionName.explain("executionStats").find();
```
