# Chapter 1: MongoDB Comparison to SQL

In this chapter, we will compare MongoDB, a NoSQL database, with SQL databases. This comparison will help you understand the fundamental differences and similarities between the two, and why you might choose one over the other.

---
## SQL vs NoSQL

SQL databases are relational, meaning they organize data in tables and rows. They use structured query language (SQL) for defining and manipulating the data.

On the other hand, NoSQL databases like MongoDB are non-relational and store data in a different format. MongoDB, for instance, uses a flexible, JSON-like document model. This means that data can be stored in complex, nested structures.

---
## Key Comparisons

Here are some key comparisons between SQL (Relational Databases) and MongoDB (NoSQL):

| SQL | MongoDB |
| --- | ------- |
| Table | Collection |
| Row | Document |
| Column | Field |
| Table Join | Embedded Documents |
| Primary Key | Primary Key (_id) |

---
### Table vs Collection

In SQL, data is stored in tables, whereas in MongoDB, data is stored in collections. A collection in MongoDB is equivalent to a table in SQL.

---
### Row vs Document

In SQL, each entry in a table is called a row. In MongoDB, the equivalent of a row is a document. Each document is a set of key-value pairs.

---
### Column vs Field

In SQL, each attribute of a data entity (like a user's name or age) is stored in a column. In MongoDB, these are stored as fields within a document.

---
### Table Join vs Embedded Documents

SQL databases use table joins to link tables together. MongoDB, on the other hand, uses two methods to establish relationships between data: embedding and linking.

#### Embedding

Embedding is the process of including one document inside another. This is a natural way to store related data in MongoDB, especially when the related data is frequently accessed together.

Here's an example of an embedded document:
```json
{
  "_id": ObjectId("507f191e810c19729de860ea"),
  "name": "John Doe",
  "address": {
    "street": "123 Main St",
    "city": "Springfield",
    "state": "IL",
    "zip": "62701"
  }
}
```
In this example, the address field is an embedded document containing related data.

#### Linking

Linking is the process of including a reference from one document to another. This is similar to how foreign keys work in SQL.

Here's an example of linking documents:

```json
// User document
{
  "_id": ObjectId("507f191e810c19729de860ea"),
  "name": "John Doe"
}

// Order document
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "product": "Apple iPhone",
  "price": 699,
  "user_id": ObjectId("507f191e810c19729de860ea")
}
```
In this example, the user_id field in the Order document is a reference to the _id field in the User document. 

This is how you establish a relationship between the two documents.  When to use embedding vs linking depends on the specific use case and data access patterns. If the related data is frequently accessed together, embedding can be a good choice. If the related data is large or frequently updated, linking might be a better choice

---
### Primary Key

Both SQL and MongoDB use primary keys to uniquely identify records. In MongoDB, every document has a unique `_id` field that acts as a primary key.

---
### Indexes in MongoDB

Indexes are a powerful feature in MongoDB that allow for efficient querying of data. However, they should be used with caution as they can slow down write operations (inserts, updates, and deletes).

An index in MongoDB is a special data structure that holds a small portion of the collection’s data set in an easy-to-traverse form. The index stores the value of a specific field or set of fields, ordered by the value of the field as specified in the index.

#### Impact on Write Operations

While indexes can significantly speed up read operations, they come with a cost on write operations. Every time a document is inserted or a field indexed is updated, the index must be updated as well. This can slow down write operations, which is something MongoDB is typically very good at. Therefore, it's important to find a balance between the number of indexes and the speed of write operations.

#### Indexing Best Practices

When it comes to indexing, not all fields are good candidates for indexing. For example, fields with boolean values or enums with very few distinct values (like a status field with 'active', 'inactive', 'deleted') are typically poor candidates for indexing. This is because there are so few distinct values that the database ends up scanning almost the entire collection anyway.

On the other hand, fields with a high number of distinct values (like email addresses or usernames) can be good candidates for indexing.


## Notes
- When modeling data in MongoDB, it can be helpful to think of it as coding in an Object-Oriented Programming (OOP) language like Java. In this context, each embedded entity or document in MongoDB can be thought of as an object in Java. This analogy can be particularly useful if you're familiar with using Hibernate for SQL databases, where each entity corresponds to a table. In MongoDB, each of these entities would be a document. This mindset can help you transition your thinking when swapping between SQL and MongoDB.
- MongoDb Document size limit is up to 20MB you have to be really careful with it because it may cause you troubles later.
