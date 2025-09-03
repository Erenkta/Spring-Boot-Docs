## Defining a PointCut

You can define a simple **PointCut** using the following code : 
```
@Pointcut("execution(* transfer(..))") // the pointcut expression
private void anyOldTransfer() {}  // the pointcut signature
```

Pointcuts basically consist of two structures : 
1- pointcut expression : Defining a pointcut with the @Pointcut annotation. It shows which method we are interested in and defines the join point where the advice will be applied.(That means anyOldTransfer is going to invoke when transfer method executed)
2- pointcut signature : It has the same purpose with method signatures. But we have to set the return type as **void**.

❗ Only public interface method calls on the proxy can be intercepted.  

❗ Spring AOP also provides a special identifier named **bean** for pointcuts. With **bean** identifier we can create pointcut for a specific bean with bean id or bean name.  

❗ We can use **&&**,**||**,**!** inside of a pointcut expression to create complex pointcuts. And it is best practice to create complex bean with using smaller pointcuts. In example :   
```
 @Pointcut("publicMethod() && inTrading()")  //inTrading and publicMethod are named pointcuts
 public void tradingOperation() {}
```  
❗If we are going to define pointcuts for different packages but same functional area ( it described like this in docs) like com.xyz.service and com.xyz.def.service we can define pointcut like below :   
```@Pointcut("execution(* com.xyz..service.*.*(..))")```
❗We usually use **execution** to define a pointcut. A **execution** is structured as follows : 
```
execution(modifier-pattern?
          ret-type-pattern
          declaring-type-pattern?name-pattern(param-pattern)
          throws-pattern?
```
ret-type-pattern,name-pattern and parameters-pattern are mandatory. We usually use wildcard (*) for ret-type-pattern. For param-pattern : 
() => takes no parameter
(..) => takes any number of parameter ( includes zero )
(*) => takes 1 parameter of any type
(*,String) => takes 2 parameter.

--------------------------------------------------------
## Pointcut identifiers

<img width="929" height="688" alt="image" src="https://github.com/user-attachments/assets/a9a75cbc-1e8b-4f64-8870-ed2473d5d72a" />  
<img width="891" height="134" alt="image" src="https://github.com/user-attachments/assets/77bb9ab0-fc5c-4aa9-87f0-f10cf53ea061" />

------------------------------------------------------
## Pointcut Usage Scenarios

- We can use **execution** identifier for method logger. For example we can define a pointcut for a method and log the start/finish time of the method.
- We can use **within** to log only controllers. It is using for filtering ( kinda )
- We can use **args** for validation. For example we can use Authentication body to check if its valid or not.
- 
