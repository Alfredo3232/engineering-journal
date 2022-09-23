# Welcome to The Course

* What is a Graph?
  * Graph - a collection of “Nodes” and “Relationships”
  * Nodes - are like a thing, for example I am a thing
  * I am a node and my parents are other nodes
    * Relationships - are like what connection does each node have with each other or no connection at all
* Properties
  * Properties - Key-Value pairs on a Node or Relationship
    * The types of values that a property can have is
      * Boolean - true, false
      * String - ‘text’
      * Numbers - 123, 5.6
      * Point - 2D, 3D, Lat, Lon
      * Temporal - Date, Time, Duration
      * Lists - [‘must be’, ‘the same type’]
    * Neo4j DOES NOT SUPPORT NESTED PROPERTIES
    * Schemas are optional

---

# Getting Set Up

* Neo4j Browser Overview
  * Cypher is Neo4j’s graph query language, working with a graph is all about understanding of data which are central to Cypher queries
  * Use MATCH clauses for reading data, and CREATE or MERGE for writing data

```JS
MATCH <pattern>
WHERE <conditions>
RETURN <expressions>
```

* MATCH clause describes a pattern of graph data, Neo4j will collect all paths within the graph which match this pattern. This is often used with WHERE to filter the collection
  * The MATCH describes the structure, and WHERE specifies the content of a query

```JS
SHOW DATABASES
```

* This command will show all the databases that exist on your existing machine

```JS
CREATE DATABASE <NAME>
```

* This command will create a new database

```JS
DROP DATABASE <NAME>
```

* This command will delete the given database

```JS
SHOW ALL ROLES
```

* This command will show the security roles that exist on the current machine like admin, publisher, reader, editor, and architect

---

# Querying Basics - Node and Relationships

* MATCH - Nodes
  * To match or find nodes in more detail it's like this

```JS
MATCH (<var>: <property>) RETURN <var> LIMIT <num>
```

* MATCH - Relationships

```JS
MATCH (<var1>: <property>)-[<var2>: <RELATION>]->(<var3>: <property>)
RETURN <var1>, <var2>, <var3>
```

* This command tries to find any two nodes that have that property and relationship.

---

# Querying Basics - Filtering & Transforming

* WHERE Clause
  * WHERE is not a clause in its own right — rather, it’s part of MATCH, OPTIONAL MATCH and WITH. In the case of WITH, WHERE simply filters the results.
    * For Example:

```JS
MATCH (tom:Person)
WHERE tom.name = 'Tom Hanks' AND tom.born = 1956
RETURN tom
LIMIT 1
```

* What this does is filter Person nodes to tom hanks and born in 1956. So it will only return nodes with those two properties.

* Comparison Operators
  * &lt;
    * Less Than Operator.
  * .>
    * Greater Than Operator.
  * =
    * This operator is for comparing a property's value to the value given.
  * <>
    * This operator is not equal to. Essentially this gets anything that is not equal to whatever is given.
  * &lt;=
    * Less than or equal to Operator.
  * >=
    * Greater than or equal to Operator
  * These operators are also available on text as well, for example, say we wanted to find people whose names started with t or letter after T in the alphabet

```JS
MATCH (someone:Person)
WHERE someone.name >= 'T'
RETURN someone
LIMIT 3
```

* Boolean Operators
  * AND
    * This operator allows you to filter two different properties at the same time, but it has to include all of the different ones.
  * OR
    * This operator allows you to filter two different properties at the same time, it has to include any of the given properties, it doesn't have to include all of them
  * IN
    * This operator is when you want to include multiple ors

```JS
WHERE <var>.<prop> IN [1956, 1957, 1958, 1959, 1960]
```

* This is find any property with any of those numbers
  * Boolean Operators with paths

```JS
MATCH (person:Person)-->(movie:Movie)
WHERE movie.title = 'Unforgiven' AND NOT (person)-[:DIRECTED]->(movie)
RETURN person, movie

```

* String matching with regular expressions

```JS
MATCH (movie:Movie)
WHERE movie.title =~ 'The.*'
RETURN movie
```

* The =~ I think this is how we tell docker to find that and use regex. What this does is finds any movie that has The and any character after.
  * To make a string case insensitive.

```JS
WHERE movie.title =~ '(?i)The.*'
```

* To find any string that has The anywhere, and case insensitive.

```JS
WHERE movie.title =~ '(?i).*The.*'
```

* To find any title with The, but not at the start, but anywhere in the title.

```JS
WHERE movie.title =~ '(?i).+The.*'
```

* Transform results (ORDER BY, LIMIT, SKIP AS)

```JS
MATCH (actor:Person)-[role:ACTED_IN]->(movie:MOVIE)
WHERE movie.title = 'Top Gun'
RETURN actor.name, role.earnings
ORDER BY role.earnings
```

* What this does it returns the what is returned, but it automatically order the earning by lowest to highest
  * If you want highest to lowest, adding DESC is a descending order from highest to lowest because the default is a ascending order
    * `ORDER BY role.earnings DESC`
  * If you want to show results after first 3 given results you can use SKIP 3

```JS
MATCH (actor:Person)-[role:ACTED_IN]->(movie:MOVIE)
WHERE movie.title = 'Top Gun'
RETURN actor.name, role.earnings
ORDER BY role.earnings
SKIP 3
LIMIT 3
```

* What this does is it returns the results after the first 3 and gets limited by 3
        * NOTE - make sure you SKIP before you limit or else you will get a error
  * If you want to give a property of a label a custom name you can do this

```JS
RETURN actor.name AS Name, role.earnings
```

* What this does is essentially this `var Name actor.name`

---

# Querying basics - Aggregation, and other basic functions

* Removing Duplicates with DISTINCT
  * If you get duplicate results from RETURN, you can use DISTINCT to prevent from getting duplicate results. For example

```JS
RETURN DISTINCT actor.name
```

* Aggregation functions (COUNT, AVG, SUM, MIN, MAX)
  * COUNT
    * Its invoked after RETURN, so something like this `COUNT(&lt;VAR>)`
    * Like the name suggests this counts how many results appeared
  * SUM
    * Let's say that your return values are all number values,  you can add all the numbers together to one single sum

 ```JS
SUM(<VAR>)
```

* AVG
  * Like SUM this gives back a result as one, except this one gives you the average of all summed results

```JS
AVG(<VAR>)
```

* MIN
  * Lets say your return values are all numbers, if you want the minimum of all those numbers

```JS
MIN(<VAR>)
```

* MAX
  * Like MIN, MAX return a single value that is the highest of all the values being put in the variable

```JS
MAX(<VAR>)
```

* String Functions

```JS
toString(<EXPRESSION>)
```

* What this does converts integers, floats, boolean, string, point, duration, date, time, localtime, localdatetime, or date time value to a string

```JS
toUpper(<EXPRESSION>)
```

* What this does it returns the original string in  all uppercase

 ```JS
toLower(<EXPRESSION>)
```

* What this does it returns the original string in all lower case

```JS
trim(<EXPRESSION>)
```

* What this does it removes any spaces at the end and beginning of the given string

```JS
replace(<STRING>, "word to find", "word to replace")
```

* When given a string or variable that is a string it find and replaces whatever it is given in the string

---

# Create

* Nodes

```JS
CREATE()
```

* This alone will create a node with 0 labels and 0 properties

```JS
CREATE(:<LABEL>)
```

* This is how create a node with a label
  * You can also stack labels on top of each other

```JS
CREATE(<VAR>:<LABEL>:<LABEL>{<KEY>: <VALUE>})
RETURN <VAR>
```

* This is how you create a node with labels and properties

* Relationships

    ```

CREATE (<STUFF>)-[:<NAME>]->(<NODE_NAME>)

```

        * This is how you create a relationship to another node

            ```
CREATE (<STUFF>)-[:<NAME>{<KEY>:VALUE}]->(<NODE_NAME>)

```

        * You can also insert properties into relationships

* Adding to existing data
    *

<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image1.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image1.png "image_tooltip")

    * What this does is finds existing nodes and all their values on lines 1 & 2. Line 3 is where he creates a relationship using their variables and then returns both variables.

---

# Delete

* Deleting Nodes, Relationships
  * You can't delete node with relationships still attached, you need to also match the relationships associated with

        ```

MATCH (node)-[rel]-()
DELETE node, rel

```

    * This is to delete a node and the relationships associated with those nodes

        ```
MATCH (node)
OPTIONAL MATCH (node)-[rel]-()
DELETE node, rel

```

    * This is an extension of the other, the other only deleted nodes that had relationships, but wouldn’t delete any nodes that had no relationships, meanwhile this code does.

---

# Update

* SET properties, labels

    ```

MATCH (tom:Person{name: 'Tom Hanks'})
SET tom.sex = 'male'
RETURN tom

```

    * The SET command allows you add a new key-value property inside of any of the given nodes
        * You can also set labels on a existing node

            ```
SET tom:Handsome

```

* REMOVE properties, labels

    ```

MATCH (tom:Person{name: 'Tom Hanks'})
REMOVE tom:Handsome
RETURN tom

```

    * The REMOVE removes labels and properties in a node

* Changing Relationship Types
    *

<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image2.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image2.png "image_tooltip")

    * This is an example of setting a new relationship type

---

# Working with NULL

* NULL values explained
  * NULL values you get them when either properties that you are trying to access that don't exist
* Boolean logic with NULL
  * NULL can stand for a value that doesn’t exist or undefined.

        ```

WITH ( true OR false ) AS result
RETURN result

```

        * If you have a value that is either true or false the result is always going to be true, however

            ```
WITH ( true OR false ) AS result
RETURN result

```

        * This is going to return false

            ```
WITH ( NULL IN [1,2,3,NULL] ) AS result
RETURN result

```

    * This is going to return NULL because NULL is not the same as NULL, NULL represents a future value, those future values could be different from other future values

* NULL Gotchas

    ```

WITH (NULL IS NULL) AS result
RETURN result

```

    * This will actually return true

        ```
WITH (NULL IS NOT NULL) AS result
RETURN result

```

    * This will return false

        ```
WITH ( NULL AND false ) AS result
RETURN result

```

    * This will return false

        ```
WITH ( NULL OR false ) AS result
RETURN result

```

    * This will return NULL

        ```
WITH ( NULL + [1,2,3] ) AS result
RETURN result

```

    * Adding a list to a NULL value is undefined. The answer is therefore null.

---

# Merge

* MERGE

    ```

MERGE (<VAR>:<LABEL>{<key>: <VALUE>})
RETURN <VAR>

```

    * MERGE does what MATCH does except if it doesn’t find a match it creates that value for you.

---

# Working with paths

* Nth Degree Relationships
    *

<p id="gdcalert3" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image3.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert4">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image3.png "image_tooltip")

* Variable Length Paths
    *

<p id="gdcalert4" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image4.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert5">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image4.png "image_tooltip")

* Path Length
    *

<p id="gdcalert5" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image5.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert6">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

![alt_text](images/image5.png "image_tooltip")

* Shortest Path

    ```

MATCH path = shortestPath((<VAR>)-[:<REL>*..<NUM>]->(<VAR>))

```

    * The shortestPath “function” returns the shortest path to the second node given, the number of relationships is NECESSARY, i’m guessing it finds the shortest out of the number given.
