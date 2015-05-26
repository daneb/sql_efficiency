## SQL Efficiency: 
This is not an attempt to provide a definitive answer, but only to provide a **guide** to coming to a right one. This is how I did that given my situation. Perhaps the logic flow will be a reference point to me in the future.

#### Problem Statement:
Is it more efficient to run a single query in chunks to return 30 000 of those records, or to run 30 000 individual selects from an application? We have a single table with 60 000 rows.

##### Benchmarks

##### Considerations
1. Is it over a local or wide-area network? A 2ms network response is negligle.
2. Is the table indexed? At first consideration this sounds plausible but it's not as, whether it's a single query or a chunked subset of 100, both will result in full table scans.
3. Oppurtunity Cost
 * The cost of chunking results in complexity pushed to the developers code, instead of allowing the database to do what it does best.
 * The cost of single individual queries is the expense of creating and closing the connection, but also that query optimization is lost given it's a new query every time
4. Does the SQL query have considerable complexity in regards to unions and intersections? (joins)
5. How large a table is it?

##### Conclusion
1.