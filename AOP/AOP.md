This file includes key information, highlights, and important notes on Spring AOP, compiled from the official Spring Boot documentation.
Document Link : 🔗 https://docs.spring.io/spring-framework/reference/core/aop.html

❗ These notes are written by me and might include incorrect information or sentences that are hard to understand. I’m a junior developer trying to learn Spring Boot and the Spring Framework properly. Please let me know if you notice any mistakes.

## AOP with Spring

In a short term, AOP complements OOP by providing another way of thinking about program structure. The key of modularity is aspect. AOP complements Spring IoC to provide a very capable middleware solution.  

There is 2 way to use Spring AOP. Either a schema-based approach or the @AspectJ annotation style. I will cover the @AspectJ approach in this section. 

❗ Spring AOP supports only method execution. So if you need interceptor for fields, you should consider a language such as AspectJ.

## AOP Concepts and explanations 
- Aspect : A modular unit written for cross-cutting concerns.Transaction management is a good example of a cross-cutting concern. An ascept usually includes **advices** and **point cut**.
- Join Point : A point during execution of a program. In Spring AOP,a join point always represents a method execution.
- Advice : Is an action taken by an **aspect** at a particular **join point**. In many AOP Frameworks, advice can be thought of as an interceptor.
- PointCut: A predicate that matches **join point**. **Advice** is associated with a pointcut expression and runs at any **join point** matched by the pointcut.
- AOP proxy : An object created by the AOP framework in order to implement the aspect contracts. (This is important. Make sure you understand what a proxy is and what it is used for in Spring Boot.)  
  [**Proxy** : is a wrapper of a class. Spring AOP uses proxies and makes method calls which can perform additional operations before passing method call to the actual object.]
