# how_to_use_Neo4j

Neo4j is a new way of extract information using graphical sql. The structure and syntax that Neo4j uses is totally different compare with classic SQL structure. In fact, it is not even similar. In this repository I will add new commands and I will explain more in detail how to extract that using.


To understand the schema and visualize it. You can use **CALL db.schema.visualization**

# Writing Queries 

In order to select 10 actors from the table. We can use:
- **MATCH (actor:Person) RETURN actor LIMIT 10**
- **MATCH (Person) RETURN Person LIMIT 10**. In this case, we are not using **actor:**
- *If we read this sintax in a SQL classic way. This is like SELECT Person as actor. In this case we need to add RETURN actor.*

Example:

**MATCH (:Person {name: 'Tom Hanks'})-[:DIRECTED]->(movie:Movie) RETURN movie**.

Find a movie Tom Hanks has directed. Return only the title of the movie. However if I want to return the attribute **movie** and **Person**, I should write:

**MATCH (person:Person {name: 'Tom Hanks'})-[:DIRECTED]->(movie:Movie) RETURN movie,person**

If we do not want to see the node **movie** (or title). We can add an extension using the syntax *variable.property* to return the name value.

**MATCH (:Person {name: 'Tom Hanks'})-[:DIRECTED]->(movie:Movie) RETURN movie.title**

If want to add more information, using this example, of Tom Hanks. We can use the number syntax *varible.property* and return the information like a table.

**MATCH (person:Person {name: 'Tom Hanks'})-[:DIRECTED]->(movie:Movie) RETURN person.name, person.born, movie.title, movie.released**

We can also use the *AS* keyword to change the name of the variables.

**MATCH (person:Person {name: 'Tom Hanks'})-[:DIRECTED]-> (movie:Movie) RETURN person.name AS name,person.born  AS 'year born', movie.title AS 'movie title', movie.released AS 'Year Released'**

# Updating with Cypher

In this seccion we will show you how to add data. Cyphers works very similarly to any other data access language's. To do this, we normally use the *INSERT* keywoed. However in Cypher we use *CREATE*. You can use this keyword to insert nodes, relationships, and patters into Neo4j.

Let's image that we want to add a new friend to graph. We can add a new person using the following statement

**CREATE (friend: Person {name: 'Mark'}) RETURN friend**. 

Great! but what happend if we made a mistake and we want to delete this node. We can do it by the following syntax:

**MATCH (friend:Person {name: 'Mark'} DELETE friend**

Now, let's add a new friend call Jennifer. If we add Jennifer, she will not have any relationship with mark. However we can establish a relationship between them.

**CREATE (friend: Person {name: 'Jennifer'}) RETURN friend**. 

Now, we establish the relationship between both nodes.

**MATCH (jennifer:Person {name: 'Jennifer'})
MATCH (mark:Person {name: 'Mark'})
CREATE (jennifer)-[rel:IS_FRIENDS_WITH]->(mark)** 

With our current nodes, we can add more information about both friends. Let's update Jennifer's node to add her birthday. We can do this using this statement:

**MATCH (p:Person {name: 'Jennifer'}) SET p.birthdate = date('1980-01-01') RETURN p**.
Note that if we want to change or upde her birthday, we just have to change the date in the set clause. 

Imagine that we are trying to delete the relationship between both nodes. In Neo4j it is possible to do that using

**MATCH (j:Person {name:'Jennifer'})-[r:IS_FRIENDS_WITH]->(m:Person {name:'Mark}) DELETE r**

# Exercise 

Let's practice with a real using the same data set provided in the sandbox.

## Simple Patterns
Find all actors that directed a movie they also acted in and return actor and movie nodes.
**MATCH (p:Person)-[:ACTED_IN]->(m:Movie) MATCH (p:Person)-[:DIRECTED]->(m2:Movie) WHERE m = m2 RETURN p.name, m.title,m2.title**
*To see the nodes, just change Return p,m,m2*
