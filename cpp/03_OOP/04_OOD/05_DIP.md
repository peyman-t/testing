### Dependency Inversion Principle (DIP)
The Dependency Inversion Principle (DIP) is a principle of object-oriented design that states that high-level modules should not depend on low-level modules, but rather both should depend on abstractions. In other words, instead of directly depending on concrete implementations of low-level modules, high-level modules should depend on interfaces or abstract classes, allowing for more flexibility and maintainability.

Assume the following code:
```cpp
class MySQLDatabase {
public:
    bool connect() {
        // connect to MySQL database
    }
    bool queryData() {
        // query data from MySQL database
    }
    bool disconnect() {
        // disconnect from MySQL database
    }
};

class OracleDatabase {
public:
    bool connect() {
        // connect to Oracle database
    }
    bool queryData() {
        // query data from Oracle database
    }
    bool disconnect() {
        // disconnect from Oracle database
    }
};

class SQLServerDatabase {
public:
    bool connect() {
        // connect to SQL Server database
    }
    bool queryData() {
        // query data from SQL Server database
    }
    bool disconnect() {
        // disconnect from SQL Server database
    }
};

class DataAnalyzer {
public:
    void analyzeMySQLData(MySQLDatabase& mysql) {
        if (mysql.connect()) {
            mysql.queryData();
            mysql.disconnect();
        }
    }

    void analyzeOracleData(OracleDatabase& oracle) {
        if (oracle.connect()) {
            oracle.queryData();
            oracle.disconnect();
        }
    }

    void analyzeSQLServerData(SQLServerDatabase& sqlServer) {
        if (sqlServer.connect()) {
            sqlServer.queryData();
            sqlServer.disconnect();
        }
    }
};

int main() {
    MySQLDatabase mysql;
    OracleDatabase oracle;
    SQLServerDatabase sqlServer;

    DataAnalyzer analyzer;
    analyzer.analyzeMySQLData(mysql);
    analyzer.analyzeOracleData(oracle);
    analyzer.analyzeSQLServerData(sqlServer);

    return 0;
}
```
The code defines three database classes - `MySQLDatabase`, `OracleDatabase`, and `SQLServerDatabase` - which implement the same set of methods: `connect`, `queryData`, and `disconnect`. Then, there is a `DataAnalyzer` class, which has three methods - `analyzeMySQLData`, `analyzeOracleData`, and `analyzeSQLServerData` - that take an instance of the corresponding database class and perform a simple analysis of its data by calling the `connect`, `queryData`, and `disconnect` methods in sequence.

In the above code, the `DataAnalyzer` class depends on the concrete classes `MySQLDatabase`, `OracleDatabase`, and `SQLServerDatabase`. This makes the code harder to maintain and less flexible, as we cannot easily swap out different types of databases without modifying the `DataAnalyzer` class.

In C++, we can implement DIP using abstract classes, interfaces (pure virtual functions), or templates. For example, consider a class hierarchy for different types of databases. We can define a base class `Database` with pure virtual functions for connecting to the database, querying data, and disconnecting from the database. We can then define derived classes for specific types of databases, such as `MySQLDatabase`, `OracleDatabase`, and `SQLServerDatabase`, each with their own implementation of these virtual functions.

To implement DIP, we can define a high-level module that depends on the abstract Database class rather than on the concrete implementations of the derived classes. For example, we can define a class `DataAnalyzer` that takes a `Database` object as a constructor parameter and uses its virtual functions to query data for analysis. This way, we can easily switch between different types of databases without having to modify the `DataAnalyzer` class.

Here's an example implementation:
```cpp
class Database {
public:
    virtual bool connect() = 0;
    virtual bool queryData() = 0;
    virtual bool disconnect() = 0;
};

class MySQLDatabase : public Database {
public:
    bool connect() override {
        // connect to MySQL database
    }
    bool queryData() override {
        // query data from MySQL database
    }
    bool disconnect() override {
        // disconnect from MySQL database
    }
};

class OracleDatabase : public Database {
public:
    bool connect() override {
        // connect to Oracle database
    }
    bool queryData() override {
        // query data from Oracle database
    }
    bool disconnect() override {
        // disconnect from Oracle database
    }
};

class SQLServerDatabase : public Database {
public:
    bool connect() override {
        // connect to SQL Server database
    }
    bool queryData() override {
        // query data from SQL Server database
    }
    bool disconnect() override {
        // disconnect from SQL Server database
    }
};

class DataAnalyzer {
public:
    DataAnalyzer(Database* db) : m_db(db) {}

    void analyzeData() {
        if (m_db->connect()) {
            m_db->queryData();
            m_db->disconnect();
        }
    }
private:
    Database* m_db;
};

int main() {
    MySQLDatabase mysql;
    OracleDatabase oracle;
    SQLServerDatabase sqlServer;

    DataAnalyzer analyzer1(&mysql);
    analyzer1.analyzeData();

    DataAnalyzer analyzer2(&oracle);
    analyzer2.analyzeData();

    DataAnalyzer analyzer3(&sqlServer);
    analyzer3.analyzeData();

    return 0;
}
```
In this example, we have defined an abstract class `Database` with pure virtual functions for connecting to the database, querying data, and disconnecting from the database. We have then defined derived classes `MySQLDatabase`, `OracleDatabase`, and `SQLServerDatabase` with their own implementations of these virtual functions.

To implement DIP, we have defined a high-level module `DataAnalyzer` that takes a `Database` object as a constructor parameter and uses its virtual functions to query data for analysis. We have then created instances of `DataAnalyzer` with different types of databases, demonstrating how we can easily switch between different types of databases without having to modify the `DataAnalyzer` class.

The consequence of violating DIP is that changes to low-level modules can have a ripple effect on high-level modules that depend on them, leading to a tightly coupled system that is difficult to maintain and modify.