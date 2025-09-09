## Spring Core Annotations  
Spring Core annotations can be divided into two categories :  
1- Dependency Injection ( DI ) Related Annotations  
2- Context Configuration Annotations  

### Depencendy Injection Related Annotations
## @Autowired : 
This annotations is applied to setters,constructors or fields to tell Spring Container to  inject object dependency.  

❗ **Spring docs says it is a good rule of thumb to use constructors for mandatory dependencies and setter method for optional dependenies.**  

## @Bean : 
This annotations defines a Spring Bean in a configuration class.  

## @Primary: 
This annotation marks a bean as the default one to inject when multiple candidates are present.  
### Example 

If both debit and credit payments service beans are available, we want to use the Debit Payment. So we mark the Debit Payment bean with @Primary.  
```
  @Component
  @Primary
  public class DebitPayment implements Payment {
      // implementation
  }
  
  @Component
  public class CreditPayment implements Payment {
      // implementation
  }

```


## @Qualifier: 
This annotation specifies which bean to inject when multiple beans of the same type are available.  
### Example  

We want to use the debit payment service for food purchases and the credit payment service for clothes. We mark both the debit and credit payment services with @Qualifier and can use them wherever needed.
```
// Using @Qualifier to select the correct payment service
@Autowired
@Qualifier("debitPayment")
private PaymentService debitPayment;

@Autowired
@Qualifier("creditPayment")
private PaymentService creditPayment;
```
## @Scope: 
This annotation specifies the scope of a Spring bean ( We will talk in more detail in Bean Scopes section )  

## @Value: 
This annotation injects values into fields from property files.
### Example

Suppose you have the following property defined in your `.properties` file:

```properties
logger.LogLevel=Verbose
````
We can inject this property's value like following :   
```
@Value("${logger.LogLevel}")
String logLevet;
```

## @DependsOn
We can use this annotation to make Spring initialize other beans before the annotated one. It specifies that a Spring bean depends on one or more other beans.

### Example

```
@Component
@DependsOn("databaseInitializer")
public class UserService {
    private final DatabaseInitializer databaseInitializer;

    public UserService() {
        databaseInitializer.checkUserTable(); // We get an error if DatabaseInitialized doesnt initialize before the User Service Bean
    }
}

```
## @Lazy
As a default behavior, Application Context ( Spring Container ) wants to instantiate and configures all beans immediately.  
This behavior is generally preferred because it allows errors to be detected immediately.  

If we dont want to use this behavior , we have to mark our bean with `@Lazy`. With this annotation our bean will be instantiated and configured upon the first request.  

### Example
This annotation can be used if there is a heavy dependency that slows our initialization. We can defer its instantiation, so our application will be initialized faster.


