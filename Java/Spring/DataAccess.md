# Data Access


## Transaction Management

### Advantages of the Spring Framework’s Transaction Support Model
Traditionally, EE application developers have had two choices for transaction management: global or local transactions, both of which have profound limitations.

#### Global Transactions
Global transactions let you work with multiple transactional resources, typically relational databases and message queues. The application server manages global transactions through the JTA, which is a cumbersome API (partly due to its exception model). Furthermore, a JTA UserTransaction normally needs to be sourced from JNDI, meaning that you also need to use JNDI in order to use JTA. The use of global transactions limits any potential reuse of application code, as JTA is normally only available in an application server environment.

#### Local Transactions
Local transactions are resource-specific, such as a transaction associated with a JDBC connection. Local transactions may be easier to use but have a significant disadvantage: They cannot work across multiple transactional resources. For example, code that manages transactions by using a JDBC connection cannot run within a global JTA transaction. Because the application server is not involved in transaction management, it cannot help ensure correctness across multiple resources. (It is worth noting that most applications use a single transaction resource.) Another downside is that local transactions are invasive to the programming model.

#### Spring Framework’s Consistent Programming Model
Spring resolves the disadvantages of global and local transactions. It lets application developers use a consistent programming model in any environment. You write your code once, and it can benefit from different transaction management strategies in different environments. The Spring Framework provides both declarative and programmatic transaction management. Most users prefer declarative transaction management, which we recommend in most cases.





## DAO Support


## Data Access with JDBC

## Data Access with R2DBC

## Object Relational Mapping (ORM) Data Access

## Marshalling ZML by Using Object-XML Mappers