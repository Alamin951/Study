# AOP
AOP is a programming paradigm that aims to increase modularity by allowing the separation of cross-cutting concerns.
It does this by adding additional behavior to existing code without modifying the code itself.



### AspectJ
AspectJ provides an implementation of AOP and has three core concepts:

1. Join Point: A point during the execution of a script, such as the execution of a method or property access. A Join point is a point during the execution of a program, such as the execution of a method or the handling of an exception.

2. Pointcut: A regular expression that matches join points. An advice is associated with a pointcut expression, and runs at any join point that matches the pointcut.

3. Advice: Action taken by an aspect at a particular join point

**Aspect:** A modularization of a concern that cuts across multiple objects. Each aspect focuses on a specific crosscutting functionality.

public aspect AccountAspect {...} -> aspect word to define the class


### Join Point:
A JoinPoint is a point during the execution of a program, such as the execution of a method or the handling of an exception.

In Spring AOP, a JoinPoint always represents a method execution.

### Pointcut:
A Pointcut is a predicate that helps match an Advice to be applied by an Aspect at a particular JoinPoint. We often associate the Advice
with a Pointcut expression, and it runs at any Join point matched by the Pointcut.
	
### Advice: 
An Advice is an action taken by an aspect at a particular Join point. Different types of advice include “around,” “before,” and “after.”
	
	
#### Pointcut: 
A predicate that matches with any join point. Advice is also associated with pointcut and runs at any join point matched by pointcut.
The concept of join point as matched by pointcut expression is central to AOP, and Spring uses the AspectJ pointcut expression language by default.

#### Introduction: 
Declaring additional methods or fields on behalf of a type. Spring AOP allows you to introduce new interfaces
(and a corresponding implementation) to any advised object.

#### Weaving: 
Linking aspects with other application types or objects to create an advised object. This can be done at compile time (using 
the AspectJ compiler, for example), load time, or at runtime. Spring AOP, like other pure Java AOP frameworks, performs weaving at runtime
#### Target object: 
Object being advised by one or more aspects. Also referred to as the advised object. Since Spring AOP is implemented using runtime proxies, this object will always be a proxy object.

### Types of advice:
	
**Before advice:** Advice that executes before a join point, but which does not have the ability to prevent execution flow proceeding 
	to the join point (unless it throws an exception).

**After returning advice:** Advice to be executed after a join point completes normally: for example, if a method returns without throwing an
	exception.

**After throwing advice:** Advice to be executed if a method exits by throwing an exception.

**After (finally) advice:** Advice to be executed regardless of the means by which a join point exits (normal or exceptional return).

**Around advice:** Advice that surrounds a join point such as a method invocation. This is the most powerful kind of advice. Around advice can perform custom behavior before and after the method invocation. It is also responsible for choosing whether to proceed to the join point or to shortcut the advised method execution by returning its own return value or throwing an exception.


### Steps of AOP

- write aspect
- configure where the aspect will be applied
Spring AOP and AspectJ both support Method Execution but

|Joinpoint|	Spring AOP Supported|AspectJ Supported|
| -------- | ------- | ------- |
Method Call	| No | Yes|
Method Execution | Yes | Yes|
Constructor Call|No|Yes|
Constructor Execution|No|Yes|
Static initializer execution |No | Yes|
Object initialization|No|Yes|
Field reference	| No | Yes |
Field assignment | No | Yes |
Handler execution | No | Yes |
Advice execution | No |	Yes

### AOP pointcut @execution vs @within

The Spring documentation explains the difference:

execution: for matching method execution join points, this is the primary pointcut designator you will use when working with Spring AOP

	@Pointcut("execution(public String com.baeldung.pointcutAdvice.dao.FooDao.findById(Long))")
	@Pointcut("execution (* com.denka.uniDenka..*(..))")

within: limits matching to join points within certain types (simply the execution of a method declared within a matching type when using Spring AOP)
	In other words, execution matches a method and within matches a type.

	@Pointcut("within(@org.springframework.stereotype.Service *)")

In this case, your pointcuts are pretty much equivalent. Your within matches any type in the package my.app.dao.impl and your execution matches all 
the public methods of any type in the package my.app.dao.impl.

However, execution is implemented, I think, with an interceptor for each matched method (a lot of objects), which within only needs one interceptor
since it matches the entire type (very little objects).

@annotation: used for matching a join point which is annotated with the specified annotation on pointcut.



### Ref link: 
<https://medium.com/@257ramanrb/aspect-oriented-programming-in-spring-804dbd05cb61><br>
https://www.javaguides.net/2019/05/spring-boot-spring-aop-logging-example-tutorial.html

youtube:<br>
<https://www.youtube.com/watch?v=SdXYlnpR_2Q>
https://www.youtube.com/watch?v=6kxpkcEqssw
https://www.youtube.com/watch?v=8u0CavOouo8&t=0s

Official documentation:<br>
https://docs.spring.io/spring-framework/docs/4.3.15.RELEASE/spring-framework-reference/html/aop.html
