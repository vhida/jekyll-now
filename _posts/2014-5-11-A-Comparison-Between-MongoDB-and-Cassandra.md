---
layout: post
title: Blogging Like a Hacker
---

MngoDB can be a great alternative to MySQL, but it’s not really 
appropriate for the scale-out applications targeted by Cassandra. Still, as 
early members of the NoSQL category, the two do draw comparisons.

One important limitation in MongoDB is database-level locking. That is, only
one writer may modify a given database at a time. Support for collection-
level (a set of documents, analogous to a relational table) locking is 
planned. With either database- or collection-level locking, other writers or
readers are locked out. Even a small number of writes can produce stalls in
read performance.

Cassandra uses advanced concurrent structures to provide row-level isolation
without locking. Cassandra even eliminated the need for row-level locks for
index updates in the recent 1.2 release.

A more subtle MongoDB limitation is that when adding or updating a field in 
a document, the entire document must be re-written. If you pre-allocate 
space for each document, you can avoid the associated fragmentation, but 
even with pre-allocation updating your document gets slower as it grows.

Cassandra’s storage engine only appends updated data, it never has to re-
write or re-read existing data. Thus, updates to a Cassandra row or 
partition stay fast as your dataset grows

Source :
http://www.datastax.com/dev/blog/2012-in-review-performance

