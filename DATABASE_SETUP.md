# Database Configuration and Migration Guide

This guide explains the default database configuration and provides instructions for migrating the project to persistent relational databases like PostgreSQL or MySQL.

---

## Default Configuration (H2 In-Memory)

The project is configured by default with an in-memory H2 database. All data resides in RAM and resets when the backend server stops.

### application.properties Settings

```properties
spring.application.name=ecom-project

spring.datasource.url=jdbc:h2:mem:testDB
spring.datasource.driverClassName=org.h2.Driver

spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=update

spring.jpa.defer-datasource-initialization=true

spring.jackson.deserialization.fail-on-null-for-primitives=false
```

### Accessing the H2 Web Console
1. Start the Spring Boot application.
2. Open a browser and navigate to: `http://localhost:8080/h2-console`
3. Enter the connection settings:
   - **Saved Settings**: Generic H2 (Embedded)
   - **Driver Class**: `org.h2.Driver`
   - **JDBC URL**: `jdbc:h2:mem:testDB`
   - **User Name**: `sa`
   - **Password**: *(leave blank)*
4. Click **Connect**.

---

## Switching to Persistent H2 File Database

If you want to keep using H2 without installing external database software while persisting your data across restarts:

1. Update `spring.datasource.url` in `src/main/resources/application.properties`:
   ```properties
   spring.datasource.url=jdbc:h2:file:./data/ecomdb;DB_CLOSE_ON_EXIT=FALSE;AUTO_RECONNECT=TRUE
   ```
2. H2 will automatically store database files in a `./data` folder in the backend working directory.

---

## Switching to PostgreSQL

1. Add the PostgreSQL driver dependency to `pom.xml`:
   ```xml
   <dependency>
       <groupId>org.postgresql</groupId>
       <artifactId>postgresql</artifactId>
       <scope>runtime</scope>
   </dependency>
   ```

2. Create a database in PostgreSQL:
   ```sql
   CREATE DATABASE ecom_db;
   ```

3. Update `application.properties`:
   ```properties
   spring.datasource.url=jdbc:postgresql://localhost:5432/ecom_db
   spring.datasource.username=your_postgres_username
   spring.datasource.password=your_postgres_password
   spring.datasource.driver-class-name=org.postgresql.Driver

   spring.jpa.hibernate.ddl-auto=update
   spring.jpa.show-sql=true
   spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
   ```

---

## Switching to MySQL

1. Add the MySQL connector dependency to `pom.xml`:
   ```xml
   <dependency>
       <groupId>com.mysql</groupId>
       <artifactId>mysql-connector-j</artifactId>
       <scope>runtime</scope>
   </dependency>
   ```

2. Create a database in MySQL:
   ```sql
   CREATE DATABASE ecom_db;
   ```

3. Update `application.properties`:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/ecom_db?useSSL=false&serverTimezone=UTC
   spring.datasource.username=your_mysql_username
   spring.datasource.password=your_mysql_password
   spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

   spring.jpa.hibernate.ddl-auto=update
   spring.jpa.show-sql=true
   ```
