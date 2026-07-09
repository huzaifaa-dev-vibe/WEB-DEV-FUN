# MongoDB

> Document database. Schemaless (with validation), JSON-like, horizontal scaling.

---

## Purpose

Use MongoDB for document-oriented workloads.

## Prerequisites

- [Databases/](../Databases/), basic JSON.

## Learning Outcome

You can design schemas, write aggregation pipelines, and scale MongoDB.

## Dependencies

- MongoDB 7+.

## Related Files

- [Databases/](../Databases/) · [PostgreSQL/](../PostgreSQL/) · [Redis/](../Redis/)

## AI Instructions

When using MongoDB:
1. Use MongoDB 7+.
2. Use schema validation (not truly schemaless).
3. Use indexes (compound, text, geospatial).
4. Use aggregation pipeline for analytics.
5. Use replica sets (not single instance) in prod.
6. Use sharding for write scale.
7. Use transactions (multi-doc ACID since 4.0).

## Human Notes

### When to use MongoDB
- Document-shaped data with variation.
- Rapid prototyping.
- Schema evolution without migrations.
- Heavy read of denormalized data.

### When NOT to use
- Relational data (use Postgres).
- Need strict transactions everywhere.
- Need ad-hoc SQL.
- Need rich joins.

### Document model
```json
{
  "_id": ObjectId("..."),
  "name": "Alice",
  "email": "a@b.com",
  "addresses": [
    { "type": "home", "city": "NYC" },
    { "type": "work", "city": "SF" }
  ],
  "created_at": ISODate("2025-01-15")
}
```

### Schema design
- Embed for 1:few (e.g., user + addresses).
- Reference for 1:many (e.g., user + thousands of orders).
- Many:many via reference + join collection.

Denormalize for read performance. Normalize for write integrity.

### CRUD
```js
db.users.insertOne({ name: 'Alice', email: 'a@b.com' });
db.users.find({ name: 'Alice' });
db.users.updateOne({ _id: ... }, { $set: { name: 'Bob' } });
db.users.deleteOne({ _id: ... });
```

### Indexes
```js
db.users.createIndex({ email: 1 }, { unique: true });
db.users.createIndex({ name: 1, age: -1 });  // compound
db.users.createIndex({ '$**': 'text' });     // text
db.users.createIndex({ location: '2dsphere' }); // geo
```

### Aggregation pipeline
```js
db.orders.aggregate([
  { $match: { status: 'completed' } },
  { $group: { _id: '$user_id', total: { $sum: '$amount' } } },
  { $sort: { total: -1 } },
  { $limit: 10 }
]);
```

### Transactions (4.0+)
```js
const session = db.getMongo().startSession();
session.startTransaction();
try {
  db.accounts.updateOne({ _id: 1 }, { $inc: { balance: -50 } }, { session });
  db.accounts.updateOne({ _id: 2 }, { $inc: { balance: 50 } }, { session });
  session.commitTransaction();
} catch (e) {
  session.abortTransaction();
}
```

### Replication
- Replica set (3+ nodes).
- Primary + secondaries.
- Automatic failover.

### Sharding
- Horizontal scale.
- Shard key matters (choose carefully).
- Once chosen, hard to change.

### Schema validation
```js
db.createCollection('users', {
  validator: {
    jsonSchema: {
      bsonType: 'object',
      required: ['name', 'email'],
      properties: {
        name: { bsonType: 'string' },
        email: { bsonType: 'string', pattern: '^.+@.+$' },
      }
    }
  }
});
```

### Mongoose (Node ODM)
```js
const userSchema = new Schema({ name: String, email: String });
const User = mongoose.model('User', userSchema);
const user = new User({ name: 'Alice', email: 'a@b.com' });
await user.save();
```

### Common mistakes
- ❌ No indexes (collection scans).
- ❌ Unbounded array growth (document size limit 16MB).
- ❌ Bad shard key (hot shards).
- ❌ Treating as truly schemaless.
- ❌ No validation.
- ❌ Storing relational data.

## Tools

- MongoDB docs: https://www.mongodb.com/docs/
- Compass: https://www.mongodb.com/products/compass
- Mongoose: https://mongoosejs.com/
- MongoDB Atlas: managed MongoDB.

## Further Reading

- *MongoDB: The Definitive Guide* — Kristina Chodorow

## Exercises

1. Build a blog with MongoDB.
2. Add indexes + aggregation pipeline.
3. Set up replica set.

## Projects

- Build a real-time analytics dashboard with MongoDB aggregation.

---

**Previous:** [MySQL/](../MySQL/) · **Next:** [Redis/](../Redis/) · **Related:** [Databases/](../Databases/)
