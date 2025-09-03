## Types of Advice

An advice is a definition that determines when a pointcut should be triggered.

- Before Advice: it triggers the pointcut before the associated join point is executed  
  ```
  @Aspect
  public class BeforeExample {
  
  	@Before("execution(* com.xyz.dao.*.*(..))")
  	public void doAccessCheck() {
  		// ...
  	}
  }
  ```

- After Returning Advice : it triggers the pointcut when joinpoint returns a value ( it musnt throw an exception )
  ```
  @Aspect
  public class AfterReturningExample {
  
  	@AfterReturning("execution(* com.xyz.dao.*.*(..))")
  	public void doAccessCheck() {
  		// ...
  	}
  }

   // if we need the body that returns from method, we can take a parameter as "Object retVal".
   // The name we give to the parameter must match the parameter we give to 'returning' inside of the @AfterReturning annotation
    @AfterReturning( 
      pointcut="execution(* com.xyz.dao.*.*(..))", 
      returning="retVal")
    public void doAccessCheck(Object retVal) { // ... }
  ```

- After Throwing Advice : It triggers when pointcut method throws an exception
```
    @Aspect
  public class AfterThrowingExample {
  
  	@AfterThrowing("execution(* com.xyz.dao.*.*(..))")
  	public void doRecoveryActions() {
  		// ...
  	}
  }

  //In some cases, we want to trigger advice for specific exception classes
  @Aspect
  public class AfterThrowingExample {
  
  	@AfterThrowing(
  		pointcut="execution(* com.xyz.dao.*.*(..))",
  		throwing="ex")
  	public void doRecoveryActions(DataAccessException ex) {
  		// ...
  	}
  }
```
- After ( Finally ) Advice : It triggers when the method defined with pointcut ends. This method either returns a value or throws an exception. This is usually used to handle releasing resources.
```
  @Aspect
  public class AfterFinallyExample {
  	@After("execution(* com.xyz.dao.*.*(..))")
  	public void doReleaseLock() {
  		// ...
  	}
  }
```
- Around Advice : It is basically used to perform some operations either before or after method calls. It is a strong advice but we have to handle if method returns a normal value or throw exception.
  ```
  @Aspect
  public class AroundExample {
  
  	@Around("execution(* com.xyz..service.*.*(..))")
  	public Object doBasicProfiling(ProceedingJoinPoint pjp) throws Throwable {
  		// start stopwatch
  		Object retVal = pjp.proceed();
  		// stop stopwatch
  		return retVal;
  	}
  
  }
  ```
  --------------------------------------------------
  ## Advice Parameters

  ❗First parameter must be JoinPoint type for any advice ( excluding around advice ). If type is **around** parameter must be ProceedingJoinPoint type. (But I can use it without a JoinPoint-type parameter. I guess I understood the docs differently.)
  ❗ We can use **args** for pass the method parameters to the advice method.
  ```
  @Before("execution(* com.xyz.dao.*.*(..)) && args(account,..)")
  public void validateAccount(Account account) {
  	// ...
  }
  
  @Before("com.xyz.Pointcuts.publicMethod() && @annotation(auditable)")
  public void audit(Auditable auditable) {
  	AuditCode code = auditable.value();
  	// ...
  }

  ```
  ❗ We can change the advice parameters name using **argNames** inside of the Advice Annotations.
  ```
  @Before(
  	value = "com.xyz.Pointcuts.publicMethod() && target(bean) && @annotation(auditable)",
  	argNames = "watermelon,peach")
  public void audit(Object watermelon, Auditable peach) {
  	AuditCode code = auditable.value();
  }
  ```
❗ If multiple advices want to trigger at the same time, their priority determines which one will execute


<img width="1193" height="367" alt="image" src="https://github.com/user-attachments/assets/7f3ebc2a-e448-41d2-98f9-36bc1d76dee7" />
