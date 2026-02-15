# MongoDB Design Patterns

This document outlines best-practice MongoDB data modeling patterns, each suited for different data access and scalability needs.

---

## 🪣 1. Bucket Pattern

### Use Case:

High-frequency time-series or event data (e.g., logs, IoT readings).

### Description:

Group many related records into a single document "bucket" based on time or metadata.

### Example:

```json
{
  "_id": "device_123_2025-07",
  "deviceId": "device_123",
  "month": "2025-07",
  "readings": [
    { "timestamp": "2025-07-01T10:00:00Z", "value": 23 },
    { "timestamp": "2025-07-01T10:01:00Z", "value": 24 }
  ]
}
```

### Pros:

* Reduces number of documents.
* Improves read performance on time-ranged queries.

### Cons:

* Buckets can grow too large (MongoDB 16MB limit).
* Updates to arrays may be inefficient.

---

## 🧩 2. Extended Reference Pattern

### Use Case:

Optimizing queries that require frequently accessed reference data.

### Description:

Stores both a reference ID and duplicate (denormalized) fields.

### Example:

```json
{
  "orderId": 123,
  "userId": "u456",
  "userName": "Alice",  // duplicated field
  "items": [...]
}
```

### Pros:

* Minimizes lookups.
* Improves read speed.

### Cons:

* Requires handling data consistency during writes/updates.

---

## 🔸 3. Subset Pattern

### Use Case:

Large embedded arrays where only part is often queried.

### Description:

Split document: frequently accessed subset in the main doc, rest in another collection.

### Example:

```json
{
  "_id": 1,
  "name": "Product A",
  "topReviews": [ ... ],
  "allReviewsRef": "reviews_1"
}
```

### Pros:

* Improves performance for common reads.

### Cons:

* More complexity on full reads.

---

## 🔀 4. Polymorphic Pattern

### Use Case:

Entities with shared and type-specific fields.

### Description:

Single collection with a `type` field to distinguish structures.

### Example:

```json
{
  "_id": 1,
  "type": "car",
  "make": "Toyota",
  "model": "Corolla"
},
{
  "_id": 2,
  "type": "bike",
  "brand": "Giant",
  "gearCount": 21
}
```

### Pros:

* Query flexibility.
* Shared index usage.

### Cons:

* Sparse fields and type-dependent logic.

---

## 🚩 5. Outlier Pattern

### Use Case:

When a few documents are significantly larger than others.

### Description:

Move large fields out of the main document to avoid bloating.

### Example:

```json
// articles collection
{
  "_id": 1,
  "title": "Intro to AI",
  "bodyRef": "articleBody_1"
}

// article_bodies collection
{
  "_id": "articleBody_1",
  "body": "Full article content..."
}
```

### Pros:

* Better index performance.

### Cons:

* Requires additional read.

---

## 🧮 6. Computed Pattern

### Use Case:

Frequently queried values that require calculation.

### Description:

Store pre-computed values inside documents.

### Example:

```json
{
  "_id": 1,
  "items": [ ... ],
  "totalPrice": 143.75
}
```

### Pros:

* Fast retrieval.

### Cons:

* Must maintain data consistency on updates.

---

## 🌲 7. Tree and Graph Patterns

### Use Case:

Modeling hierarchical or graph-like data.

### Variants:

#### a. Parent Reference

```json
{
  "_id": 2,
  "name": "Electronics",
  "parent": 1
}
```

#### b. Child References

```json
{
  "_id": 1,
  "name": "Root",
  "children": [2, 3]
}
```

#### c. Materialized Path

```json
{
  "_id": 5,
  "name": "Laptops",
  "path": "1/2/5"
}
```

### Pros:

* Suitable for various tree traversal operations.

### Cons:

* Updating paths can be complex.

---

## 🧾 8. Schema Versioning Pattern

### Use Case:

When schema changes over time but backward compatibility is needed.

### Description:

Add a `schemaVersion` field and migrate docs as needed.

### Example:

```json
{
  "_id": 1,
  "name": "Alice",
  "schemaVersion": 2,
  "email": "alice@example.com"
}
```

### Pros:

* Smooth migration.
* Backward support.

---

## ✅ Best Practices Summary

* **Keep documents < 16MB.**
* **Embed for read-heavy operations**, reference for write-heavy or frequently updated relationships.
* **Index frequently used fields.**
* **Avoid unnecessary joins** — denormalize when practical.
* **Use aggregation pipelines** for in-place data transformation.

---

## 🔗 References

* [MongoDB Schema Design Best Practices](https://www.mongodb.com/blog/post/6-rules-of-thumb-for-mongodb-schema-design-part-1)
* [MongoDB Docs: Data Modeling Patterns](https://www.mongodb.com/docs/manual/core/data-model-design/)

---

> Keep this file as a reference when designing collections and schemas for performance, scalability, and maintainability.
