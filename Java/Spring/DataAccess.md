# Data Access


## Transaction Management
# Spring Boot Transaction Management Overview

In a Spring Boot application, transactions play a crucial role in managing the consistency and integrity of data. Transactions ensure that a series of operations either complete successfully as a whole or leave the system in a consistent state if an error occurs during any part of the process. Spring Boot provides a comprehensive and flexible transaction management mechanism, building upon the Spring Framework's transaction support.

## Transaction Basics

1. **Definition:**
   - A transaction is a sequence of one or more operations treated as a single unit of work.
   - It follows the ACID properties: Atomicity, Consistency, Isolation, and Durability.

2. **Isolation Levels:**
   - Transactions operate under different isolation levels, defining how concurrent transactions interact.
   - Common isolation levels include READ_UNCOMMITTED, READ_COMMITTED, REPEATABLE_READ, and SERIALIZABLE.

## Spring Boot Transaction Management

1. **Transaction Manager:**
   - Spring Boot uses a `PlatformTransactionManager` to manage transactions.
   - Common implementations include `DataSourceTransactionManager` for JDBC and `JpaTransactionManager` for JPA.

2. **`@Transactional` Annotation:**
   - The `@Transactional` annotation is used to mark a method or class for transaction management.
   - It can be applied at the method level or at the class level.

   ```java
   @Service
   public class MyService {
       @Autowired
       private MyRepository myRepository;

       @Transactional
       public void performTransaction() {
           // Transactional operations
       }

3. **Propagation:**
    - Defines how transactions propagate when methods are called within a transactional context.
    - Options include REQUIRED, REQUIRES_NEW, SUPPORTS, NOT_SUPPORTED, and MANDATORY.
    - **REQUIRED:** If a transaction exists, the method will join it; - otherwise, a new transaction will be started.
    - **REQUIRES_NEW:** A new transaction will always be started, suspending the existing one if it exists.
    - **SUPPORTS:** If a transaction exists, the method will join it; otherwise, it will execute non-transactionally.
    - **NOT_SUPPORTED:** The method will execute non-transactionally, suspending any existing transaction.
    - **MANDATORY:** The method requires an existing transaction; otherwise, an exception is thrown.

    ```java
    @Transactional(propagation = Propagation.REQUIRED)
    public void methodWithTransaction() {
        // Transactional operations
    }
    ```
4. **Isolation:**
    - Specifies the isolation level for the transaction.
    - Common isolation levels include READ_UNCOMMITTED, READ_COMMITTED, REPEATABLE_READ, and SERIALIZABLE.
    - **READ_UNCOMMITTED:** Allows dirty reads, non-repeatable reads, and phantom reads.
    - **READ_COMMITTED:** Prevents dirty reads but allows non-repeatable reads and phantom reads.
    - **REPEATABLE_READ:** Prevents dirty reads and non-repeatable reads but allows phantom reads.
    - **SERIALIZABLE:** Prevents dirty reads, non-repeatable reads, and phantom reads

    ```java
    @Transactional(isolation = Isolation.READ_COMMITTED)
    public void methodWithTransaction() {
        // Transactional operations
    }
    ```
5. **Rollback:**

    - Determines under what conditions a transaction should be rolled back.
    - The @Transactional(rollbackFor = Exception.class) annotation explicitly specifies exceptions that trigger a rollback.
    - For example, @Transactional(rollbackFor = CustomException.class)

6. **Timeout:**

    - Specifies a timeout for the transaction in seconds.
    - If the transaction takes longer than the specified timeout, it will be automatically rolled back.
    - A timeout of 0 (the default) means no timeout.

# Programmatic Transaction Management

In addition to declarative transaction management using annotations, Spring Boot also supports programmatic transaction management. This approach allows for more fine-grained control over transactions using programming code.

## TransactionTemplate

The `TransactionTemplate` class is a key component for programmatic transaction management. It encapsulates the transactional code and is responsible for managing the transaction lifecycle. Below is an example of using `TransactionTemplate`:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.PlatformTransactionManager;
import org.springframework.transaction.TransactionStatus;
import org.springframework.transaction.support.TransactionCallbackWithoutResult;
import org.springframework.transaction.support.TransactionTemplate;

@Service
public class MyService {

    @Autowired
    private PlatformTransactionManager transactionManager;

    public void performProgrammaticTransaction() {
        // Creating a TransactionTemplate with the provided transaction manager
        TransactionTemplate transactionTemplate = new TransactionTemplate(transactionManager);

        // Executing transactional code within the template
        transactionTemplate.execute(new TransactionCallbackWithoutResult() {
            @Override
            protected void doInTransactionWithoutResult(TransactionStatus status) {
                // Transactional operations
            }
        });
    }
}
```
### Declarative vs. Programmatic Transaction Management:

#### Declarative:

- Relies on annotations or XML configuration.
- Easier to use and maintain.
- Promotes separation of concerns.

#### Programmatic:

- Uses programming code to control transactions.
- Offers more fine-grained control.
- Can be useful in complex scenarios.


## Best Practices for Programmatic Transaction Management

1. **Keep Transactions Short:**
   - Minimize the duration of transactions to reduce the likelihood of conflicts and deadlocks.

2. **Exception Handling:**
   - Properly handle exceptions to control transactional behavior.
   - Use `TransactionTemplate` within try-catch blocks for effective error handling.

3. **Fine-Grained Control:**
   - Utilize programmatic transaction management for scenarios where fine-grained control is necessary.

4. **Testing:**
   - Test programmatic transactions to ensure they behave as expected.
   - Use appropriate testing frameworks to validate transactional behavior.

By incorporating programmatic transaction management when needed, developers can achieve greater flexibility and control over transactions in their Spring Boot applications.




### Advantages of the Spring Framework’s Transaction Support Model
Traditionally, EE application developers have had two choices for transaction management: global or local transactions, both of which have profound limitations.

#### Global Transactions
Global transactions let you work with multiple transactional resources, typically relational databases and message queues. The application server manages global transactions through the JTA, which is a cumbersome API (partly due to its exception model). Furthermore, a JTA UserTransaction normally needs to be sourced from JNDI, meaning that you also need to use JNDI in order to use JTA. The use of global transactions limits any potential reuse of application code, as JTA is normally only available in an application server environment.

#### Local Transactions
Local transactions are resource-specific, such as a transaction associated with a JDBC connection. Local transactions may be easier to use but have a significant disadvantage: They cannot work across multiple transactional resources. For example, code that manages transactions by using a JDBC connection cannot run within a global JTA transaction. Because the application server is not involved in transaction management, it cannot help ensure correctness across multiple resources. (It is worth noting that most applications use a single transaction resource.) Another downside is that local transactions are invasive to the programming model.

#### Spring Framework’s Consistent Programming Model
Spring resolves the disadvantages of global and local transactions. It lets application developers use a consistent programming model in any environment. You write your code once, and it can benefit from different transaction management strategies in different environments. The Spring Framework provides both declarative and programmatic transaction management. Most users prefer declarative transaction management, which we recommend in most cases.


#### Understanding the Spring Framework’s Declarative Transaction Implementation
The most important concepts to grasp with regard to the Spring Framework’s declarative transaction support are that this support is enabled via AOP proxies and that the transactional advice is driven by metadata (currently XML- or annotation-based). The combination of AOP with transactional metadata yields an AOP proxy that uses a TransactionInterceptor in conjunction with an appropriate TransactionManager implementation to drive transactions around method invocations.

@Transactional commonly works with thread-bound transactions managed by PlatformTransactionManager, exposing a transaction to all data access operations within the current execution thread. Note: This does not propagate to newly started threads within the method.

A reactive transaction managed by ReactiveTransactionManager uses the Reactor context instead of thread-local attributes. As a consequence, all participating data access operations need to execute within the same Reactor context in the same reactive pipeline.



## DAO Support


## Data Access with JDBC

## Data Access with R2DBC

## Object Relational Mapping (ORM) Data Access

## Marshalling ZML by Using Object-XML Mappers