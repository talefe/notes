## 1. Java Database Connectivity

&nbsp;

## 2.1. JDBC

The jdbc is the standard API for java programs to interact with Database Management Systems.

&nbsp;

## 2.2. Functionality of JDBC

By making use of JDBC, we are able to:

-   Connect to data sources, like databases
-   Perform queries and update statements on the data
-   Retrieve information and process the received results

&nbsp;

## 2.3. Connecting to a database

In order to connect to a database we will need:

-   a [DriverManager][drivermanager-java-docs], which will connect the application to the data
    source
-   a Database URL (in the form of a String), which will have the information pertaining as to where
    to search for the database, the name of the database to connect to and some configuration
    properties (more on that in a second)

&nbsp;

## 2.4. Database URL

A database URL string should have the following format:  
`jdbc:mysql://[host][,failoverhost...][:port]/[database][?propertyName1][=propertyValue1]`

It is comprised of the following:

-   `host:port` - the hostname and port of the machine hosting the database. Will default to IP
    127.0.0.1 and port 3306.

*   `database` - the name of the specific database to which the connection should be made
*   `failoverhost` - the hostname of a secondary or alternative database to which to connect in case
    the first desired one fails (MySQL Connector/J supports failover) - more on this?
*   `propertyName=propertyValue` - optional properties, separated by ampersands in case there's more
    than one youw wish to specify.

&nbsp;

## 2.5. Example snippet of connecting to a Database

```Java
public class ConnectionManager {

    private Connection connection = null;

    public Connection getConnection() {

            try {
                if (connection == null) {
                    connection = DriverManager.getConnection(dbUrl, user, pass);
                }
            } catch (SQLException ex) {
                System.out.println("Failure to connect to database : " + ex.getMessage());
            }
            return connection;
        }

    public void close() {
        try {
            if (connection != null) {
                connection.close();
            }
        } catch (SQLException ex) {
            System.out.println("Failure to close database connections: " + ex.getMessage());
        }
    }
}
```

&nbsp;

## 2.6. Statement

A [Statement][statement-java-docs] is an interface provided by the java.sql package, that represents
an SQL statement. They can be executed and doing so generates a [ResultSet][resultset-java-docs],
which is an object representing the database's result set.

&nbsp;

## 2.7. Executing queries using Statements

There are several ways that you can ask your [Statement][statement-java-docs] to perform a given
query (I counted at least 10), but the slide shows the 3 that the cadets will most probably be
using.

-   `execute(String sql)` - will return a boolean in case if retrieved at least one
    [ResultSet][resultset-java-docs]. It's used when the query might return several
    [ResultSet][resultset-java-docs] and you can access those by calling the `getResultSet()` on the
    [Statement][statement-java-docs].

*   `executeQuery(String sql)` - will return a single [ResultSet][resultset-java-docs], which is the
    result of executing the given SQL statement.
*   `executeUpdate(String sql)` - will return an `int` value which represents the number of records
    affected by performing the given SQL statement. It is intended to be used with `INSERT`,
    `UPDATE`, `DELETE`

&nbsp;

## 2.8. An example of what we just saw

```Java
public class JdbcUserService implements UserService {

    private Connection dbConnection;

    @Override
    public int count() {

        int result = 0;

        // create a new statement
        Statement statement = dbConnection.createStatement();

        // create a query
        String query = "SELECT COUNT(*) FROM user";

        // execute the query
        ResultSet resultSet = statement.executeQuery(query);

        // get the results
        if (resultSet.next()) {
            result = resultSet.getInt(1);
        }

        return result;
    }
}
```

&nbsp;

## 2.9. How about explaining what the hell a ResultSet object is?!

These [ResultSet][resultset-java-docs] objects represent the set of results that I would get from querying the database as we are used to seeing if we did it using for example MySQL in our CLI's.  
So you can think of these objects as a representation of a table in java.

We can access the data contained in a [ResultSet][resultset-java-docs] by using a cursor that points to what would be a row in the results table, representing a record.  
In order to move this cursor to the next avaliable record we can call the method `next()` from the [ResultSet][resultset-java-docs], which will move the cursor to the next tuple. In case there are no more avaliable rows the method will return false. (Not that distant from some [iterators][iterator-java-doc] that we've seen in the past, right?)

The [ResultSet][resultset-java-docs] in turn presents a huge API of getter methods that allow us to retrieve the data from the current row in a myriad of ways.


[drivermanager-java-docs]: https://docs.oracle.com/javase/7/docs/api/java/sql/DriverManager.html
[statement-java-docs]: https://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html
[resultset-java-docs]: https://docs.oracle.com/javase/7/docs/api/java/sql/ResultSet.html
[iterator-java-doc]:https://docs.oracle.com/javase/7/docs/api/java/util/Iterator.html
