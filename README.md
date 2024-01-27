# Eclipselink-4.0.2-and-JPA
How to use Eclipselink in 2024 when programming in JAVA.

# pom.xml file

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.example</groupId>
    <artifactId>hibernate6</artifactId>
    <version>1.0-SNAPSHOT</version>
    <parent>
        <groupId>com.example</groupId>
        <artifactId>jakartaee10-sandbox-parent</artifactId>
        <version>1.0-SNAPSHOT</version>
        <relativePath>..</relativePath>
    </parent>    <name>hibernate6</name>
    <description>Jakarta EE 10 Sandbox: Hibernate 6/JPA 3.1 example</description>    <properties>
        <maven.compiler.release>17</maven.compiler.release>        <!-- requires 6.1.2.Final or higher -->
        <hibernate.version>6.1.4.Final</hibernate.version>
        <h2.version>2.1.214</h2.version>        <!-- test deps -->
        <junit-jupiter.version>5.9.1</junit-jupiter.version>
        <assertj-core.version>3.23.1</assertj-core.version>        <slf4j.version>2.0.3</slf4j.version>
        <logback.version>1.4.4</logback.version>
    </properties>    <dependencies>
        <dependency>
            <groupId>org.hibernate.orm</groupId>
            <artifactId>hibernate-core</artifactId>
            <version>${hibernate.version}</version>
        </dependency>
        <dependency>
            <groupId>jakarta.persistence</groupId>
            <artifactId>jakarta.persistence-api</artifactId>
            <version>3.1.0</version>
        </dependency>        <!-- H2 Database -->
        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
            <version>${h2.version}</version>
        </dependency>        <!-- logging with logback -->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>${slf4j.version}</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>jcl-over-slf4j</artifactId>
            <version>${slf4j.version}</version>
        </dependency>
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-core</artifactId>
            <version>${logback.version}</version>
        </dependency>
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>${logback.version}</version>
        </dependency>        <!-- test dependencies -->
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>${junit-jupiter.version}</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.assertj</groupId>
            <artifactId>assertj-core</artifactId>
            <version>${assertj-core.version}</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.hibernate.orm</groupId>
            <artifactId>hibernate-testing</artifactId>
            <version>${hibernate.version}</version>
            <scope>test</scope>
            <exclusions>
                <exclusion>
                    <groupId>junit</groupId>
                    <artifactId>junit</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
    </dependencies>    
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.10.1</version>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.0.0-M7</version>
            </plugin>
        </plugins>
    </build>
</project>
```

# Outils de base de données

## ObjectDB
 - [https://www.objectdb.com/download](https://www.objectdb.com/download)

 ```
     <repositories>
            ...
        <repository>
            <id>objectdb</id>
            <name>ObjectDB Repository</name>
            <url>https://m2.objectdb.com</url>
        </repository>
            ...
    </repositories>
            ...
    <dependencies>
            ...
        <dependency>
            <groupId>com.objectdb</groupId>
            <artifactId>objectdb</artifactId>
            <version>2.8.9</version>
        </dependency>
            ...
    </dependencies>

```

## MysqlDB

## SQLite

## DuckDB

## EclipseLink and JPA

## TopLink


## TopLink


## TopLink


## TopLink


## TopLink

## persistence unit

 Based on the search results you provided, it seems like you are having trouble getting your Java SE application to recognize the `persistence.xml` file when using EclipseLink 4.0.2 and JPA 2.1.0 to connect to a database. Here are some steps you can take to troubleshoot the issue:

1. Verify the Location of the `persistence.xml` File: According to the EclipseLink documentation, the `persistence.xml` file must be located in the `META-INF` directory of the jar file that contains your entities. So, if your entities are in a package named `entities`, then the `persistence.xml` file should be located in `src/main/resources/META-INF/persistence.xml`.
2. Set the Persistence Unit Name Correctly: Ensure that the name specified in the `persistence-unit` tag in the `persistence.xml` file matches the name specified in the `@PersistenceUnit` annotation in your Java code.
3. Use the Right Provider Class: In the `persistence.xml` file, ensure that the `provider` property is set to `org.eclipse.persistence.jpa.PersistenceProvider`.
4. Enable Debugging: Add the following line to your VM arguments in the Run Configuration in Eclipse to enable debug logging: `-Djavax.persistence.loglevel=ALL`. This will output verbose log messages during runtime and help identify any issues.
5. Check the Content of the `persistence.xml` File: Ensure that the `persistence.xml` file includes the necessary configurations for the persistence unit, such as the JDBC driver URL, username, password, and dialect. Here's an example `persistence.xml` file:

```xml
<persistence version="2.1" xmlns="http://xmlns.jcp.org/xml/ns/persistence" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence http://xmlns.jcp.org/xml/ns/persistence/persistence_2_1.xsd">
    <persistence-unit name="MyPU" transaction-type="RESOURCE_LOCAL">
        <class>com.example.entity.MyEntity</class>
        <exclude-unlisted-classes>true</exclude-unlisted-classes>
        <properties>
            <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/mydatabase"/>
            <property name="javax.persistence.jdbc.user" value="root"/>
            <property name="javax.persistence.jdbc.password" value="mypassword"/>
            <property name="javax.persistence.jdbc.driver" value="com.mysql.cj.jdbc.Driver"/>
            <property name="eclipselink.logging.level" value="FINEST"/>
            <property name="eclipselink.session-customizer" value="com.example.config.SessionCustomizer"/>
        </properties>
    </persistence-unit>
</persistence>
```

Replace the values in the `<properties>` section with the appropriate settings for your database.

6. Try Upgrading to a More Recent Version of EclipseLink: Consider upgrading to a newer version of EclipseLink, such as 4.0.3 or later, to benefit from bug fixes and improvements.

By following these steps, you should be able to resolve the issue with EclipseLink recognizing the `persistence.xml` file in your Java SE application. Good luck!

### JPA 3.0 ou 3.1 compatible avec Eclipselink 4.0.2 (voir site [https://eclipse.dev/eclipselink/releases/tck-summary.java](https://eclipse.dev/eclipselink/releases/tck-summary.java))

**REMARQUE** : Tous  les détails importants sur le contenu du fichier **persistence.xml** en fonction de la version de Eclipselink et JPA sont disponibles ici : [https://jakarta.ee/xml/ns/persistence/](https://jakarta.ee/xml/ns/persistence/)

```xml
<persistence xmlns="https://jakarta.ee/xml/ns/persistence"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://jakarta.ee/xml/ns/persistence/orm https://jakarta.ee/xml/ns/persistence/orm/orm_3_1.xsd" 
             version="3.1">             

    <persistence-unit name="MyPU" transaction-type="RESOURCE_LOCAL">
        <class>com.example.entity.MyEntity</class>
        <exclude-unlisted-classes>true</exclude-unlisted-classes>
        <properties>
            <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/mydatabase"/>
            <property name="javax.persistence.jdbc.user" value="root"/>
            <property name="javax.persistence.jdbc.password" value="mypassword"/>
            <property name="javax.persistence.jdbc.driver" value="com.mysql.cj.jdbc.Driver"/>
            <property name="eclipselink.logging.level" value="FINEST"/>
            <property name="eclipselink.session-customizer" value="com.example.config.SessionCustomizer"/>
        </properties>
    </persistence-unit>
</persistence>
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--

    Copyright (c) 2018, 2021 Oracle and/or its affiliates. All rights reserved.

    This program and the accompanying materials are made available under the
    terms of the Eclipse Distribution License v. 1.0, which is available at
    http://www.eclipse.org/org/documents/edl-v10.java.

    SPDX-License-Identifier: BSD-3-Clause

-->

<persistence xmlns="https://jakarta.ee/xml/ns/persistence"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://jakarta.ee/xml/ns/persistence https://jakarta.ee/xml/ns/persistence/persistence_3_0.xsd"
             version="3.0">
    <persistence-unit name="firstcupPU" transaction-type="JTA">
        <provider>org.eclipse.persistence.jpa.PersistenceProvider</provider>
        <jta-data-source>java:comp/DefaultDataSource</jta-data-source>
        <properties>
            <property name="eclipselink.ddl-generation" value="drop-and-create-tables"/>
        </properties>
    </persistence-unit>
</persistence>
```


### Connecteurs pour les autres types de moteurs de BD

The properties for connecting to different databases would vary depending on the database vendor being used. Here are examples of properties for SQLite, ObjectDB, DuckDB, Oracle, and PostgreSQL:

**SQLite:**
```java
<properties>
    <property name="javax.persistence.jdbc.url" value="jdbc:sqlite::resource:yourDatabaseFileName.db"/>
</properties>
```
**ObjectDB:**
```java
<properties>
    <property name="javax.persistence.jdbc.url" value="jdbc:objectdb:~/databases/yourDatabaseFileName"/>
    <property name="javax.persistence.jdbc.user" value="admin"/>
    <property name="javax.persistence.jdbc.password" value="admin"/>
</properties>
```
**DuckDB:**
Please note that DuckDB doesn't currently support JDBC connections. Therefore, you won't be able to use it with JPA. Instead, you can use the DuckDB-Java library to access DuckDB databases.

source : [https://duckdb.org/docs/archive/0.9.2/api/java](https://duckdb.org/docs/archive/0.9.2/api/java)

```java
Properties ro_prop = new Properties();
ro_prop.setProperty("duckdb.read_only", "true");
Connection conn_ro = DriverManager.getConnection("jdbc:duckdb:/tmp/my_database", ro_prop);
```

 Installation

The DuckDB Java JDBC API can be installed from Maven Central. Please see the installation page for details.
Basic API Usage

DuckDB’s JDBC API implements the main parts of the standard Java Database Connectivity (JDBC) API, version 4.1. Describing JDBC is beyond the scope of this page, see the official documentation for details. Below we focus on the DuckDB-specific parts.

Refer to the externally hosted API Reference for more information about our extensions to the JDBC specification, or the below Arrow Methods
Startup & Shutdown

In JDBC, database connections are created through the standard java.sql.DriverManager class. The driver should auto-register in the DriverManager, if that does not work for some reason, you can enforce registration like so:
```
Class.forName("org.duckdb.DuckDBDriver");
```
To create a DuckDB connection, call DriverManager with the jdbc:duckdb: JDBC URL prefix, like so:
```
Connection conn = DriverManager.getConnection("jdbc:duckdb:");
```
When using the `jdbc:duckdb:` URL alone, an in-memory database is created. Note that for an in-memory database no data is persisted to disk (i.e., all data is lost when you exit the Java program). If you would like to access or create a persistent database, append its file name after the path. **For example**, if your database is stored in `/tmp/my_database`, use the JDBC URL `jdbc:duckdb:/tmp/my_database` to create a connection to it.

It is possible to open a DuckDB database file in read-only mode. This is for example useful if multiple Java processes want to read the same database file at the same time. To open an existing database file in read-only mode, set the connection property duckdb.read_only like so:
```java
Properties ro_prop = new Properties();
ro_prop.setProperty("duckdb.read_only", "true");
Connection conn_ro = DriverManager.getConnection("jdbc:duckdb:/tmp/my_database", ro_prop);
```
Additional connections can be created using the DriverManager. A more efficient mechanism is to call the DuckDBConnecttion#duplicate() method like so:
```java
Connection conn2 = ((DuckDBConnection) conn).duplicate();
```
Multiple connections are allowed, but mixing read-write and read-only connections is unsupported.
Querying

DuckDB supports the standard JDBC methods to send queries and retrieve result sets. First a Statement object has to be created from the Connection, this object can then be used to send queries using execute and executeQuery. execute() is meant for queries where no results are expected like CREATE TABLE or UPDATE etc. and executeQuery() is meant to be used for queries that produce results (e.g., SELECT). Below two examples. See also the JDBC Statement and ResultSet documentations.
```sql
// create a table
Statement stmt = conn.createStatement();
stmt.execute("CREATE TABLE items (item VARCHAR, value DECIMAL(10, 2), count INTEGER)");
// insert two items into the table
stmt.execute("INSERT INTO items VALUES ('jeans', 20.0, 1), ('hammer', 42.2, 2)");

try (ResultSet rs = stmt.executeQuery("SELECT * FROM items")) {
    while (rs.next()) {
        System.out.println(rs.getString(1));
        System.out.println(rs.getInt(3));
    }
}

-- >>> // jeans
-- >>> // 1
-- >>> // hammer
-- >>> // 2
```

DuckDB also supports prepared statements as per the JDBC API:
```java
try (PreparedStatement p_stmt = conn.prepareStatement("INSERT INTO items VALUES (?, ?, ?);")) {
    p_stmt.setString(1, "chainsaw");
    p_stmt.setDouble(2, 500.0);
    p_stmt.setInt(3, 42);
    p_stmt.execute();
    
    // more calls to execute() possible
}
```


**Oracle:**
```java
<properties>
    <property name="javax.persistence.jdbc.url" value="jdbc:oracle:thin:@//hostname:portnumber/servicename"/>
    <property name="javax.persistence.jdbc.user" value="username"/>
    <property name="javax.persistence.jdbc.password" value="password"/>
    <property name="javax.persistence.jdbc.driver" value="oracle.jdbc.OracleDriver"/>
</properties>
```
**PostgreSQL:**
```java
<properties>
    <property name="javax.persistence.jdbc.url" value="jdbc:postgresql://hostname:portnumber/databasename"/>
    <property name="javax.persistence.jdbc.user" value="username"/>
    <property name="javax.persistence.jdbc.password" value="password"/>
    <property name="javax.persistence.jdbc.driver" value="org.postgresql.Driver"/>
</properties>
```
**H2:**
To use H2 in EclipseLink, use the platform class `org.eclipse.persistence.platform.database.H2Platform`. If this platform is not available in your version of EclipseLink, you can use the OraclePlatform instead in many case. See also H2Platform. 

```java
<properties>
    <property name="javax.persistence.jdbc.url" value="jdbc:postgresql://hostname:portnumber/databasename"/>
    <property name="javax.persistence.jdbc.user" value="username"/>
    <property name="javax.persistence.jdbc.password" value="password"/>
    <property name="javax.persistence.jdbc.driver" value="org.postgresql.Driver"/>
</properties>
```

# Hibernate 6.*

## Drivers for hibernate

JDBC driver dependencies Database

```
PostgreSQL or CockroachDB ===> org.postgresql:postgresql:{version}

MySQL or TiDB ===> com.mysql:mysql-connector-j:{version}

MariaDB ===> org.mariadb.jdbc:mariadb-java-client:{version}

DB2 ===> com.ibm.db2:jcc:{version}

SQL Server ===> com.microsoft.sqlserver:mssql-jdbc:${version}

Oracle ===> com.oracle.database.jdbc:ojdbc11:${version}

H2 ===> com.h2database:h2:{version}

HSQLDB ===> org.hsqldb:hsqldb:{version}

```

## hibernate persistence xml

```xml

<persistence xmlns="http://java.sun.com/xml/ns/persistence"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://java.sun.com/xml/ns/persistence https://jakarta.ee/xml/ns/persistence/persistence_3_0.xsd"
             version="2.0">

    <persistence-unit name="org.hibernate.example">

        <class>org.hibernate.example.Book</class>
        <class>org.hibernate.example.Author</class>

        <properties>
            <!-- PostgreSQL -->
            <property name="jakarta.persistence.jdbc.url"
                      value="jdbc:postgresql://localhost/example"/>

            <!-- Credentials -->
            <property name="jakarta.persistence.jdbc.user"
                      value="gavin"/>
            <property name="jakarta.persistence.jdbc.password"
                      value="hibernate"/>

            <!-- Automatic schema export -->
            <property name="jakarta.persistence.schema-generation.database.action"
                      value="drop-and-create"/>

            <!-- SQL statement logging -->
            <property name="hibernate.show_sql" value="true"/>
            <property name="hibernate.format_sql" value="true"/>
            <property name="hibernate.highlight_sql" value="true"/>

        </properties>

    </persistence-unit>

</persistence>


```










