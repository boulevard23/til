# Denormalization

**Denormalization** is the process of attempting to optimize the read performance of a database by adding redundant data or by grouping data.

Most of the time it is used to address some performance issue.

For example, you have a big join query you have to run every time, the query is really slow. You can denormalize it by creating a table to store the result from that complex query, and then write a simple `SELECT *` from this table.