# Graph Data Modeling Fundamentals
<img src="img/course_icon.png" alt="course icon" width="250"/>


## Table of Contents
1. [Getting Started](#chapter-1---getting-started)
2. [Modeling Nodes](#chapter-2---modeling-nodes)
3. [Modeling Relationships](#chapter-3---modeling-relationships)
4. [Testing the Model](#chapter-4---testing-the-model)
5. [Refactoring the Graph](#chapter-5---refactoring-the-graph)
6. [Eliminate Duplicate Data](#chapter-6---eliminate-duplicate-data)
7. [Using Specific Relationships](#chapter-7---using-specific-relationships)
8. [Adding Intermediate Nodes](#chapter-8---adding-intermediate-nodes)


## Chapter 1 - Getting Started <a name="chapter_1"></a>

### What is Graph Data Modeling?

#### Why model?

If you use Neo4j to support part or all of your application, you must collaboratively work with you stakeholders to design a graph that will
- Answer the key use cases for the application
- Provide the best Cypher statement perfomance for the key use cases

#### Components of a Noe4j graph

The componenets used to define the graph data model are
- Nodes
- Labels
- Relationships
- Properties

#### Data modeling process

Here are the steps to create a graph data model
1. Understand the **domain** and define specific **use cases** (questions) for the application
2. Develop the **initial graph model**
    - Model the nodes (entities)
    - Model the relationships between nodes
3. **Test** the use cases against the initial data model
4. Create the graph (**instance model**) with test data using Cypher
5. Test the use cases including **performance** against the graph
6. **Refactor** (improve) the graph data model due to a change in the key use cases or for performance reasons
7. Refactor and retest

Being an iterative process, the schema flexibility helps.

### The Domain

Before you begin the data processing model you must 
- Identify the stakeholders and developers of the application
- With them
    - Describe the application in detail
    - Identify the users of the application (people, systems)
- Agree upon the use cases for the application
- Rank the importance of the use cases

#### Movie domain

The domain we will use in the examples includes movies, people who acted or directed movies, and users who rated movies.

What makes this domain interesting are the connections or relationships between nodes in the graph.

#### Use cases

1. What people acted in a movie?
2. What person directed a movie?
3. What movies did a person acted in?
4. How many users rated a movie?
5. Who was the youngest actor in a movie?
6. What role did a person play in a movie?
7. What's the highest rated movie in a particular year according to IMDB?
8. What drama movies did an actor act in?
9. What users give a rating of 5 to a movie?

### Purpose of the model

#### Type of models

When performing the data modeling process for an application, you will need at least two types of models:
- Data model
- Instance model

##### Data Model

The data model describes
- Labels
- Relationships
- Properties

for the graph.

Below, an example:

<img src="img/data_model.png" alt="data model" width="550"/>

##### Style guidelines for modeling

The names of the entities listed below are **case sensitive**. For each of them, the naming best practices are reported.
- Label -> TitleCase
- Relationship -> UPPER_CASE
- Property key -> camelCase

##### Instance model

Sample data to test whether the use cases can be answered with the model.


## Chapter 2 - Modeling Nodes <a name="chapter_2"></a>

### Defining Labels

**Entities** are the domain **nouns** in your application use cases.

The entities of your use cases will be the labeled nodes in the graph data model.

Labels are defined by nouns in TitleCase.

### Node Properties

Node properties are used to:
- Uniquely identify a node
- Answer specific details of the use cases of the application
- Return data

### Unique identifiers in the movie graph

- Person.tmdbId
- Movie.tmdbId

### Properties for nodes

Below is a list of specific use cases to person and movie nodes.

These use cases inform us about the data we need in person and movie nodes.

| Use Case | Steps Required |
|-|-|
| What people acted in a movie? | <ul><li>Retrieve the movie by its title</li><li>Return the name of the actors in the movie</li></ul> | 
| What person directed a movie? | <ul><li>Retrieve the movie by its title</li><li>Return the name of the director of the movie</li></ul> |
| What movies did a person act in? | <ul><li>Retrieve a person by its name</li><li>Return the titles of the movies</li></ul> |
| Who was the youngest person who acted in a movie? | <ul><li>Retrieve the movie by its title</li><li>Evaluate the ages of the actors</li><li>Return the name of the actor</li></ul> |
| What is the highest rated movie in a particolar year? | <ul><li>Retrieve all the movies for that year</li><li>Evaluate the imdb ratings</li><li>Return the movie title</li></ul> |
| What drama movies did an actor act in? | <ul><li>Retrieve the actor by name</li><li>Evaluate the genres for the movies the actor acted in</li><li>Return the movie title</li></ul> |
|

Given the details of the steps of these use cases, below are the properties that needs to be defined

- Movie
    - title (String)
    - released (Date)
    - imdbRating (Decimal 0-10)
    - genres (List of Strings)
- Person
    - name (String)
    - born (Date)
    - died (Date)


## Chapter 3 - Modeling Relationships <a name="chapter_3"></a>

### Relationships are Connections between Entities

**Connections** are the **verbs** in your use cases
- What ingredients are **used** in a recipe?
- Who is **married** to this person?

Using "connections are verbs" is a fine shorthand to get started, but there are other important considerations...

### Naming Relationships

Choosing the god names (types) for the relationships in the group is important.

Relationship types should be intuitive to stakeholders and developer alikes.

Relationship types cannot be confused with entity names (also because they are written in uppercase)
- USES
- MARRIED

### Relationships in the Movie Graph

Use cases
- What people **acted** in a movie?
- What person **directed** a movie?
- What movie did a person **act** in?

Given these use cases, we name the relationships as follows
- ACTED_IN
- DIRECTED

### Properties for Relationships

Properties for a relationship are used to enrich how two nodes are related.

When you define a property for a relationship, it is because your use case asks specific questions about how two nodes are related, not just that they are related.

### Relationship Properties in the Movie Graph

Here is the use case

6. What role did a person play in a movie?

Operations
- Retrieve the name of the person
- Follow the ACTED_IN relationship to movies
- Filter movies by title
- Return the role from the ACTED_IN relationship by the two nodes


## Chapter 4 - Testing the Model <a name="chapter_4"></a>

### Why Test?

To ensure that the graph can satisfy every use case

### Example

"What people acted in a movie?"

```
MATCH (p:Person)-[:ACTED_IN]->(m:Movie)
WHERE m.title = 'Sleepless in Seattle'
RETURN p.name AS actor
```

In the description of the use cases, you may even specify what the expected result should be.

### More Testing ?

If and when the graph is refactored (next module), the Cypher code for these use cases may be modified to improve performance.

The basic testing to ensure that the use cases can be answered by the data model is the first step of testing.

A really important factor with testing the graph is **scalability**: how will these queries perform if the graph has millions of nodes or relationships?


## Chapter 5 - Refactoring the Graph <a name="chapter_5"></a>

### Labels at Runtime

Node labels serve as an anchor point for a query.

By specifying a label, we are specifying a subset of one or more nodes with which to start a query.

Using a label helps to reduce the amount of data that is retreived.

Your goal in modeling should be to **reduce the size of the graph that is touched by a query**.

In order you can produce a query plan that shows the sequence of operations
```
PROFILE <query>
```

In Cypher you cannot parametrize labels so keeping e.g. the counter as a property makes the Cypher code more flexible
```
MATCH (n:Person)
WHERE n.country = 'US'
RETURN n
```

### Do Not Overuse Labels

You should use labels wisely in your data model.

They should be used if it will help with most of the use cases.

A best practice is to **limit the number of labels for a node to 4**.

### New Use Case

Here is an example where adding a label will help our queries at runtime

10. Which actors where born before 1950?

Here is the Cypher statement to test this use case
```
MATCH (p:Person)-[:ACTED_IN]->()
WHERE p.born < 1950
RETURN p.name
```

### Profiling a Query

```
PROFILE <query>
```

Because the cache is automatically populated, it is sometimes hard to measure performance with a small dataset.

That is, DB Hits and elapsed time may not be comparable.

What you can see, however, is the number of rows that are retrieved in the query and this number can be compared.

One way you can optimize the retriever is to change the data model to include a Actor label for a Person node.

### Refactor (Update) the Graph

With Cypher, you can easily transform the graph.

We can set a label for actors like below
```
MATCH (p:Person)
WHERE exists ( (p)-[:ACTED_IN]-() )
SET p:Actor
```

### Retesting after Refactoring

After you have refactored the graph, you should revisit all the queries for your use cases.

You should first determine if any query needs to be rewritten to take advantage of the refactoring.

You should also profile your queries to check for possible performance changes.

1. What person acted in a movie?

Original query
```
MATCH (p:Person)-[:ACTED_IN]->(m:Movie)
WHERE m.title = '...'
RETURN p.name AS actor
```
After refactoring
```
MATCH (p:Actor)-[:ACTED_IN]->(m:Movie)
WHERE m.title = '...'
RETURN p.name AS actor
```

### Avoid these Labels

#### Semantically Orthogonal Labels 

Labels should have nothing to do with one another.

You should be careful not to use the same type of labels in different contexts.

#### Represent Class Hierarchies

You also want to avoid labeling your nodes to represent hierarchies.

Avoid the IS_A relationship.


## Chapter 6 - Eliminate Duplicate Data <a name="chapter_6"></a> 

You should take care of avoid duplicating data in your graph.

### New Use Case

11. What movies are available for a particular language?

### Refactoring Duplicate Data

Example: the following query findds all movies in italian
```
MATCH (m:Movie)
WHERE 'italian' IN m.languages
RETURN m.title
```

What this query does is retrieving all movie nodes and test whether the languages property contains italian.

There are two issues with the data model, especially if the graph scales
- The name of the language is duplicated in many movie nodes
- In order to perform the query, all nodes must be retrieved

### Refactoring Properties as Nodes

Here are the steps we use to refactor

1. We take the property values for each movie node and create a language node
2. Then we create the IN_LANGUAGE relatioship between that movie node and the language node
3. Finally, we remove the languages property from the movie node

```
MATCH (m:Movie)
UNWIND m.languages AS language
WITH language, collect(m) AS movies
MERGE (l:Language {name: language})
WITH l, movies
UNWIND movies as m
MERGE m-[:IN_LANGUAGE]->(l)
MATCH (m: Movie)
SET m.languages = null
```

### Eliminating Complex Data Nodes

*Example*

Since nodes are used to store data about specific entities, you may have initially modeled, for example, a production node to contain the details of the address for the production company.

<img src="img/graph_example.png" alt="graph example" width="550"/>

Storing complex data nodes like this may not be beneficial for a couple of reasons:
- Duplicate data (location-related data)
- Queries related to the information in the node requires all nodes to be retrieved

#### Refactoring Complex Data 

If there is a high amount of duplicate data in the nodes or if the key nodes of your use cases would perform better if all nodes need not to be retrieved to get at the complex data, then you might consider refactoring the graph as shown below.

<img src="img/graph_example_2.png" alt="graph example 2" width="550"/>

In this refactoring, if there are queries that need to filter production companies by their state, then it will be faster to query based upon the state.name value, rather than evaluatingall of the state properties for the production nodes.

Perfomance (main queries) => refactoring


## Chapter 7 - Using Specific Relationships <a name="chapter_7"></a> 

### Relatioships in the Graph

Neo4j as a native graph database is implemented to traverse relationships quickly.

**In some cases, it is more performant to query the graph based upon relationship types rather than properties in the nodes.**

- What movies did an actor act for a particular year?

```
MATCH (p:Actor)-[:ACTED_IN]->(m:Movie)
WHERE p.name = 'Tom Hanks' 
      AND m.released STARTS WITH '1995'
RETURN m.title as movie
```

What if Tom Hanks acted in 50 movies in the year 1995?

The query would need to retrieve all movies that Tom Hanks acted in and then check the value of the released properties.

- What actors or directors worked in a particular year?

```
MATCH (p:Person)--(m:Movie)
WHERE m.released STARTS WITH '1995'
RETURN DISTINCT p.name AS 'actor or director'
```

This query is even worse for performance because in order to return results it must retrieve all nodes.

### Refactoring to Specialize Relationships

Relationships are fast to traverse and they do not take up a lot of space in the graph.

In the previous two queries, the data model would benefit from having specialized relationships between nodes.

e.g.
- ACTED_IN_1995
- DIRECTED_IN_1995

At first, it seems like a lot of relationships for a large, scaled movie graph. But if the latest two queries are important use cases, it is worth it.

In most cases, where we specialize relationships, we keep the original generic relationships as existing queries still need to use them.


## Chapter 8 - Adding Intermediate Nodes <a name="chapter_8"></a> 

### Intermediate Nodes

You sometimes find cases where you need to connect more data to a relationship that can be fully captured in the properties.

In other words, you want a **relationship that connects more than two nodes**.

Mathematics allows this with the concept of hyper edge.

This is impossible in Neo4j => Intermediate nodes

You can create intermediate nodes when you need to
- Connect more than two nodes in a single context
- Relating something to a relationship
- Share data in the graph between entities

### Example: Need for an Intermediate Node

Consider the following instance model with an hyper edge.

<img src="img/hyper_edge.png" alt="hyper edge" width="550"/>

It could be refactored adding intermediate node.

<img src="img/intermediate_node.png" alt="intermediate node" width="550"/>

### Example: Intermediate Nodes for Sharing Data

Here is what the graph looks like before we refactor it:

<img src="img/many_edges.png" alt="many edges" width="550"/>

Intermediate nodes also allow you to deduplicate information.

<img src="img/shared_info.png" alt="shared info" width="550"/>

