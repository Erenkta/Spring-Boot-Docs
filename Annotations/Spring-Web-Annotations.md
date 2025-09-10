# Spring Web Annotations
This section includes most commonly used Spring Web Annotations. You generally come across with this topic inside of a `Controller`  

## @RequestMapping  
This annotation maps HTTP requests to handler methods in the controller.
**Note** : It is better to use `@GetMapping`, `@PostMapping`, `@PutMapping`, `@PatchMapping`, `@DeleteMapping`
### Example
```
@Controller
public class MyController {

    @RequestMapping("/hello")
    public String sayHello() {
        return "hello";
    }
}
```
---
## @RequestBody  
This annotation binds the body of the HTTP request (usually it is a JSON due to Rest API) to a Java object.
### Example
```
@PostMapping("/addUser")
public String addUser(@RequestBody User user) {
    return "User added: " + user.getName();
}
```
---
## @PathVariable  
This annotation extracts values from the URI template.
### Example
```
@GetMapping("/user/{id}")
public String getUser(@PathVariable("id") int id) {
    return "User ID: " + id;
}
```
---
## @RequestParam  
This annotation extracts query parameters from the URL.  
### Example
```
@GetMapping("/search")
public String search(@RequestParam("q") String query) {
    return "Search query: " + query;
}
```
---
## @ResponseBody  
This annotation indicates that the return value of the method should be used as the response body.
### Example
```
@GetMapping("/user")
@ResponseBody
public User getUser() {
    return new User("John Doe", 25);
}
// This endpoint returns a json as follows :
{
  "name": "John Doe",
  "age": 25
}
```
---
## @ExceptionHandler  
This annotation is used to handle exceptions thrown by request-handling methods.
**Note** : It is only available for methods in same controller. So you better use Global Exception Handler with `@ControllerAdvice`
### Example
```
@Controller
public class MyController {

    @ExceptionHandler(ArithmeticException.class)
    public String handleError(Exception ex) {
        return "Error occurred: " + ex.getMessage();
    }
}
```
---
## @ResponseStatus  
This annotation specifies the HTTP status code for the response. We use this annotation with Exception classes.
### Example
```
@ResponseStatus(HttpStatus.NOT_FOUND)
public class UserNotFoundException extends RuntimeException {
    public UserNotFoundException(String msg) {
        super(msg);
    }
}
```
---
## @RestController  
This annotation is a combination of @Controller and @ResponseBody, used for RESTful web services.
### Example
```
@RestController
public class MyRestController {

    @GetMapping("/greet")
    public String greet() {
        return "Hello, REST!";
    }
}
```
---
## @CrossOrigin  
This annotation enables cross-origin resource sharing (CORS) for specific handler methods or controller classes
### Example
```
@RestController
@CrossOrigin(origins = "http://example.com")
public class MyRestController {

    @GetMapping("/data")
    public String getData() {
        return "Some data";
    }
}
```
---
