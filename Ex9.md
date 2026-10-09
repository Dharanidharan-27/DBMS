# Ex No: 9 - NoSQL Examples (Redis, Cassandra, MongoDB, Neo4j)

## Key-Value Store Example (Redis-style)

```
SET Name "Joe Bloggs"
SET Age 42
SET Occupation "Stunt Double"
SET Height "175cm"
SET Weight "77kg"
```

**Output:**
```
Redis> SET Name "Joe Bloggs"
OK
Redis> SET Age 42
OK
Redis> SET Occupation "Stunt Double"
OK
Redis> SET Height "175cm"
OK
Redis> SET Weight "77kg"
OK
```

## Column-based Store Example (Cassandra CQL)

```sql
CREATE TABLE ColumnFamily (
    RowKey text PRIMARY KEY,
    col1 text,
    col2 text,
    col3 text
);
```

**Output:**
```
Cassandra> CREATE TABLE ColumnFamily (...);
Query OK
```

## Document-oriented Example (MongoDB)

```javascript
db.documents.insertMany([
    { "prop1": "data", "prop2": "data", "prop3": "data", "prop4": "data" },
    { "prop1": "data", "prop2": "data", "prop3": "data", "prop4": "data" },
    { "prop1": "data", "prop2": "data", "prop3": "data", "prop4": "data" }
]);
```

**Output:**
```
MongoDB> db.documents.insertMany([...])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('...'),
    '1': ObjectId('...'),
    '2': ObjectId('...')
  }
}
```

## Graph-based Example (Cypher / Neo4j)

```cypher
CREATE (p:Person {name:"Alice"})-[:LIVES_IN]->(c:City {name:"Chennai"})
CREATE (p)-[:LIKES {rating:5}]->(r:Restaurant {name:"Spice House"})
CREATE (r)-[:LOCATED_IN]->(c)
```

**Output:**
```
Neo4j> CREATE (p:Person {name:"Alice"})-[:LIVES_IN]->(c:City {name:"Chennai"})
CREATE (p)-[:LIKES {rating:5}]->(r:Restaurant {name:"Spice House"})
CREATE (r)-[:LOCATED_IN]->(c)
```
