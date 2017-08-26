CQL, stands for Query Language for Cassandra.Compared to SQL, it’s clearly limiting in its grammar. This is largely to avoid inefficient queries for Cassandra is mainly used to store massive data in distributed systems. Data are hashed against partition key and then distributed to each node to store. Therefore one key in designing a cassandra query is to scan less as possible nodes as it can be very inefficient.    
      
We know that relational database is a set of rows. Cassandra is a set of partitions. Without cluster keys, a partition is simple a single row. A partition that consists of multiple rows are simply wide-row. It’s the hash value of partition key that cassandra use to decide which node data should be stored. It’s a hash indexing, not a range. We  need clustering key to order the data and give a range and according to which query is made possible. An example may be more illustrative.  
   
For the table below, node is the partition key, while (date,number) is the clustering key.  
  
```  
CREATE KEYSPACE test WITH REPLICATION = {  
    'class': 'SimpleStrategy',   
    'replication_factor': 1   
}
```
```
CREATE TABLE log(    
    `node text,`    
    `date text,`    
    `name text,`  
    `number int,`  
    `Primary Key(node,date,number)`  
)
```


The data would be stored in a relational database like this:  

node |  date | number | name   
n1  |   feb |  1   |    name1  
n1  |   feb |  2   |    name2
n2  |   feb |  1   |    name3
n2  |   feb |  2   |    name4  
    
In Cassandra, it looks like this:    
   
```
partition1
{
    date:feb {number:1 {name:name1}} 
             {number:2 {name:name2}}
}
```
```
partition2
{
    date:feb {number:1 {name:name3}} 
             {number:2 {name:name4}}
}
```
Note that since column order is not fixed, the name of each column has to be stored as well.   
  
#  Range Query.   
Prior to cassandra 2.2,  IN can only be used for the last column of partition key. After 2.2 it’s any column。We has said that for performance, we should reduce the number of nodes we query into. IN operation would involve multiple nodes, and replicate factor further increased by folds. Coordinate nodes then would have to store more query results from each node. Stack may be highly occupied and GC be forced to stop. Performance issue.   
From Cassandra 3.0, IN began to support columns in clustering key.   
Range query can also be done by using the toke function of partition key, for instance, `SELECT * FROM log WHERE token(node) > token('1')`    


In theory, ByteOrderedPartitioner  can support range query as its distribution is ordered. BUt usually it’s not used in practice as the distribution of data can cause load balance problem among node.   
clustering key
For single column, the query can only be done on last column and with the column before specified, like    
`SELECT *FROM log WHERE node = '1' AND date >='date1'`   

`SELECT *FROM log WHERE node = '1' AND date = 'date' AND number >=1`  


Query like this would be invalid.   
`SELECT *FROM log where node = '1' AND number >= 1`      


#  In summary    
partition key is based on hash and therefore CQL can’t support range query. IN operation is supported though.   
clustering key is ordered and supports IN, greater, less operations。It works like a combined index, which, to be useful, has to include the columns before the query column.    
With only clustering key without partition key, all nodes have to be scanned and then filtered. The execution can be inefficient. Cassandra has a ALLOW FILTERING flag. It can be efficient when most of the scanned nodes have the query results.    
   
   
#  Some notes   
“Or” is not supported in CQL where clause. “Or” is designed in SQL to reduce the number of requests to db server. However,in case of Cassandra, it’s better in performance to reduce the number of nodes that are queried into. An “Or”  operation may involve too many nodes and partition keys.    
Cassandra supports “Like” operation after release 3.4, but with many limitations.   



