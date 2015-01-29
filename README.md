# Demo for RelEng-2015

This repository contains a simple application which demonstrates the difference in applying database schema operations to a database under active use. It works as followed:

1. It creates a sample database with 50 million records.
2. It runs a sample application within the JVM on the created database.
3. After some time it will apply the user-specified method of applying database schema operations.
4. Start a newer sample application within the JVM which operates on the new schema.
5. Terminates the first sample application.
6. The migration has completed. The second application is terminated and the database is cleared.

In this demo the user can specify to use one of two methods of applying these schema operations:

1. **with-downtime** which is the regular way to alter the database schema using _Data Definition Language_ (DDL) statements such as: `ALTER TABLE ...`, `CREATE INDEX ...`, etc.
2. **quantumdb** which uses ghost tables to alter the database schema. If this method is specified, the sample applications will use a custom JDBC driver which wraps the PostgreSQL JDBC driver, and rewrites queries to use select the appropriate table name (original or ghost table name) according to what version of the schema the sample application operates on.

## Running the demo
You can fetch the JAR file from [the releases page of this project](https://github.com/quantumdb/releng-demo/releases). Ensure you have Java 8 installed on your machine and PostgreSQL 9.3 (other versions have not been tested). To run this demo open up the terminal for your OS, navigate to the folder where the JAR file is located, and execute one of the following commands: 

#### Regular method
```
java -jar releng-demo-0.1.0.jar with-downtime <jdbc url> <username> <password>
```

#### QuantumDB method
```
java -jar releng-demo-0.1.0.jar quantumdb <jdbc url> <username> <password>
```
