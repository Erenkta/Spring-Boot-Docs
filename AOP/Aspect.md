## Defining an Aspect

You can define a simple **Aspect** using the following code.

```
@Configuration  
@EnableAspectJAutoProxy  
public class ApplicationConfiguration {
	@Bean  
	public NotVeryUsefulAspect myAspect() {  
		NotVeryUsefulAspect myAspect = new NotVeryUsefulAspect();  
		// Configure properties of the aspect here  
		return myAspect;  
	}
}
```

