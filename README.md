# how_to_use_Neo4j

Neo4j is a new way of extract information using graphical sql. The structure and syntax that Neo4j uses is totally different compare with classic SQL structure. In fact, it is not even similar. In this repository I will add new commands and I will explain more in detail how to extract that using.


To understand the schema and visualize it. You can use CALL db.schema.visualization


In order to select 10 actors from the table. We can use:
- **MATCH (actor:Person) RETURN actor LIMIT 10**
- *If we read this sintax in a SQL clasic way. This is like SELECT Person as actor. In this case we need to add RETURN actor.*




