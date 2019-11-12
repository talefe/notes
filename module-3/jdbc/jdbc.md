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
-   a Database URL (in the form of a String with a few rules that we'll see in the following slide),
    which will have the information pertaining as to where to search for the database, the name of
    the database to connect to and some configuration properties.

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

The slides don't manage to be very explicit about this, but the [Connection][connection-java-docs]
object that we are receiving from the [DriverManager][drivermanager-java-docs], represents the
connection to the database itself, and has a bunch of functionality, including being able to create
[Statement][statement-java-docs] objects, something that we will be using in a moment.

&nbsp;

## 2.6. Statement

A [Statement][statement-java-docs] is an interface provided by the java.sql package (we will take a
look at implementing classes later), that represents an SQL statement. They can be executed and
doing so generates a [ResultSet][resultset-java-docs], which is an object representing the resulting
table that you would receive upon performing the given query on the database.

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

These [ResultSet][resultset-java-docs] objects represent the set of results that I would get from
querying the database as we are used to seeing if we did it using for example MySQL in our CLI's.  
So you can think of these objects as a representation of a table in java.

We can access the data contained in a [ResultSet][resultset-java-docs] by using a cursor that points
to what would be a row in the results table, representing a record.  
In order to move this cursor to the next avaliable record we can call the method `next()` from the
[ResultSet][resultset-java-docs], which will move the cursor to the next tuple. In case there are no
more avaliable rows the method will return false. Also, keep in mind that before calling the
`next()`, your cursor is not yet pointing to the first record in case there is one. Think of it as
having you cursor start out by pointing to the header of the table, or to the HEAD of a linked list
for example. (Not that distant from some [iterators][iterator-java-doc] that we've seen in the past,
right?)

The [ResultSet][resultset-java-docs] in turn presents a huge API of getter methods that allow us to
retrieve the data from the current row in a myriad of ways.

&nbsp;

## 2.10. An example on how interacting with ResultSet objects is performed

```Java
@Override
public User findByName(String username) {

      // ... connection and statements....

      // execute the query
      ResultSet resultSet = statement.executeQuery(query);

      // user exists
      if(resultSet.next()) {

          String usernameValue = resultSet.getString("username");
          String passwordValue = resultSet.getString("password");
          String emailValue = resultSet.getString("email");

          user = new User(usernameValue, passwordValue, emailValue);
      }

      // ....
}
```

&nbsp;

## 2.11. Closing connections

As in whenever we were talking about streams or similar objects, closing them when we were done
using them was always an integral part of interacting with those. Same thing applies to JDBC's
[Connections][connection-java-docs], as we don't want to keep a connection established to a database
if we are not currently or about to use it in the immediate future.

```Java
@Override
public User findByName(String username) {

    try {

        ...

        if(statement != null) {
            statement.close();
        }

    } catch (SQLException e) {
        e.printStackTrace();
    }
}
```

&nbsp;

## 2.12. {Exercise} Introduce JDBC in a service layer!

#### Objectives

-   Have the cadets implement their first iteration of a service layer that provides real
    persistence, and first contact with JDBC.
-   Have the cadets deal with the (relatively) low-level of interaction with a database that JDBC
    provides, in order for them to later on understand (and appreciate) all that the frameworks are
    taking care of for us.

#### Flow

-   Provide the cadets with the skeleton
-   They will have to download the required java SQL connector and include it as a dependency  
    _**(you must use the correct version of the connector. The one included in the solution is
    outdated and should be replaced by [8.0.18][jdbc-connector-download](at the time of
    writing))**_  
    (simply download the platform independent version, unzip it, and in there you will find your
    `.jar`)
-   Show them that there is a mock implementation in place, which doesn't really persist users, and
    there's an interface for the service they are supposed to implement and replace
-   Hint them at separating the managing of the connection from the Service itself
-   Remember the cadets that they are required to create the database beforehand, as JDBC will only
    attempt to connect to a given one, not create it if it doesn't exist, as well as the tables.
    Luckily for them we have provided them a small SQL script to take care of that, contained in the
    resources folder of the project.  
    (remember them how to run said script `mysql -u root < db.sql` if inside the directory)

&nbsp;

## 2.13. Statement types

_**Might be cool to first perform an SQL injection a cadet's application to show them the danger of
those, and then coming back to explain these**_

As previously stated, [Statement][statement-java-docs] is just an Interface and
the[Connection][connection-java-docs] is able to provide you with an implementation of it.

But there are in fact two concrete implementations: [PreparedStatement][preparedstatement-java-docs]
and [CallableStatement][callablestatement-java-docs].

The [PreparedStatement][preparedstatement-java-docs] are used for precompiling SQL statements that
might contain input parameters, while the [CallableStatement][callablestatement-java-docs] is meant
to execute stored procedures, that might contain both input and output parameters.

&nbsp;

## 2.14. PreparedStatement

These prepared statements are a both more performing and safer way to create your queries to the
database.

-   you need to provide an SQL statement at the moment of creation (in the form of a String)
-   The given statement is sent to the DBMS, where it is compiled
-   The execution time of performing one of these several times is improved over performing "normal"
    statements over and over
-   It covers your ass from SQL injection attacks!

The following slide exemplifies the usage of one of these.

&nbsp;

## 2.15. How do we create one o' those?

```Java
public User getUser(int id, String name) {
	...

	// create a query
	String query = "SELECT * FROM table WHERE id=? AND name=?";
	PreparedStatement statement = dbConnection.prepareStatement(query);

	// set values for the placeholders
	statement.setInt(1, id);
	statement.setString(2, name);

	// execute the query
	ResultSet resultSet = statement.executeQuery();

	//...

}
```

## 2.16. Injections, bewaaare!

An injection of SQL attack consists simply of inserting malicious SQL via the data that the client
is sending to the application.

&nbsp;

## 2.17. {Hands-On} Your password means nothing to me!

#### Objectives

-   Show the cadets that the current implementation is vulnerable to SQL injections

#### Flow

-   Either try this out against a cadet's program or against the `prompt-jdbc`(without
    prepared-statements)
-   When prompted for the username, insert `batata' OR 1=1; --` exactly as writtten in this snippet.
    (the `--` comments out the rest of the line in SQL, and needs to be followed by a space)

*   You must have been able to login despite whatever password you might have input.

&nbsp;

## 2.18. {Exercise} Let's cover that...

#### Objectives

-   Have the cadets protect their JdbcUserService from such injections

#### Flow

-   Ask the cadets to replace their current [Statements][statement-java-docs] with
    [PreparedStatement][preparedstatement-java-docs]

[drivermanager-java-docs]: https://docs.oracle.com/javase/7/docs/api/java/sql/DriverManager.html
[statement-java-docs]: https://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html
[resultset-java-docs]: https://docs.oracle.com/javase/7/docs/api/java/sql/ResultSet.html
[iterator-java-doc]: https://docs.oracle.com/javase/7/docs/api/java/util/Iterator.html
[connection-java-docs]: https://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html
[jdbc-connector-download]: https://dev.mysql.com/downloads/connector/j/
[preparedstatement-java-docs]:
    https://docs.oracle.com/javase/7/docs/api/java/sql/PreparedStatement.html
[callablestatement-java-docs]:
    https://docs.oracle.com/javase/7/docs/api/java/sql/CallableStatement.html
