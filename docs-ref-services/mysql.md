---
title: Azure Database for MySQL libraries for Java
description: Reference documentation for the Java client libraries for Azure Database for MySQL
keywords: Azure, Java, SDK, API, SQL, database, PostGres, MySQL 
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: mysql
---

# Azure Database for MySQL libraries for Java

## Overview

[Azure Database for MySQL](/azure/sql-database/sql-database-technical-overview) is a relational database service based on the open source [MySQL](https://www.mysql.com/) Server engine. 

[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the [MySQL JDBC driver](https://dev.mysql.com/downloads/connector/j/) in your project.  

```XML
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.45</version>
</dependency>
```   

To get started with Azure Database for MySQL, review [the connect and query quickstart](/azure/mysql/connect-java) or jump in using a   [connection string](https://docs.microsoft.com/en-us/azure/mysql/howto-connection-string) with the [example code for the JDBC driver](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-examples.html).

## Connect to Azure Database for MySQL

Connect to Azure Database for MySQL host `fabrikamysql.mysql.database.azure.com` and database name `fabrikamdb`.

```java

import java.sql.*;
import java.util.Properties;

String url = String.format("jdbc:mysql://fabrikamysql.mysql.database.azure.com/fabrikamdb");
            
// Set connection properties.
Properties properties = new Properties();
properties.setProperty("user", user);
properties.setProperty("password", password);
properties.setProperty("useSSL", "true");
properties.setProperty("verifyServerCertificate", "true");
properties.setProperty("requireSSL", "false");

try {
    Connection conn = DriverManager.getConnection(url, properties);
}
catch (SQLException e) {
    throw new SQLException("Failed to create connection to database.", e);
}
```

## Execute a simple query 

Use an initialized [Connection](https://docs.oracle.com/javase/8/docs/api/java/sql/Connection.html) object to create a table and insert some records.

```java

import java.sql.*;

Statement statement = connection.createStatement();
try {
    // Create table.
    statement.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");

    // Insert some data into table.
    int nRowsInserted = 0;
    PreparedStatement preparedStatement = connection.prepareStatement("INSERT INTO inventory (name, quantity) VALUES (?, ?);");
    preparedStatement.setString(1, "banana");
    preparedStatement.setInt(2, 150);
    nRowsInserted += preparedStatement.executeUpdate();

    preparedStatement.setString(1, "orange");
    preparedStatement.setInt(2, 154);
    nRowsInserted += preparedStatement.executeUpdate();

    preparedStatement.setString(1, "apple");
    preparedStatement.setInt(2, 100);
    nRowsInserted += preparedStatement.executeUpdate();
    System.out.println(String.format("Inserted %d row(s) of data.", nRowsInserted));
}
catch (SQLException e) {
    throw new SQLException("Encountered an error when executing given sql statement.", e);
}    
```

> [!div class="nextstepaction"]
> [Find more sample code](https://azure.microsoft.com/resources/samples/?platform=java&term=mysql)

## Next steps

[Build a Java and MySQL web app](/azure/app-service-web/app-service-web-tutorial-java-mysql)   
[Design a MySQL database using the Azure CLI](/azure/mysql/tutorial-design-database-using-cli)