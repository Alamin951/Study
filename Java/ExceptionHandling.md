# GlobalExceptionHandler
create a class and with @ControllerAdvice annotation 

Exception Handler:
The @ExceptionHandler is an annotation used to handle the specific exceptions and sending the custom responses to the client
	
Any class annotated with @ControllerAdvice will become a controller-advice class which will be responsible for handling exceptions. Under 
this class we make use of annotations provided as @ExceptionHandler, @ModelAttribute, @InitBinder.

ResponseEntityExceptionHandler is a convenient base class for @ControllerAdvice classes that wish to provide centralized exception handling 
across all @RequestMapping methods through @ExceptionHandler methods.

ResponseEntityExceptionHandler is a convenient base class for @ControllerAdvice classes that wish to provide centralized exception handling 
across all @RequestMapping methods through @ExceptionHandler methods. It provides methods for handling internal Spring MVC exceptions. It 
returns a ResponseEntity in contrast to DefaultHandlerExceptionResolver which returns a ModelAndView

By default @ControllerAdvice will scan and handle all the classes in your application. we can also control this:

1) annotations — Controllers that are annotated with the mentioned annotations will be assisted by the @ControllerAdvice annotated class and 
	are eligible for exception of those classes

	eg. @ControllerAdvice(annotations = RestController.class)

2) basePackages — By Specifying the packages which we want to scan and handling exceptions for the same.

	eg. @ControllerAdvice(basePackages = “org.example.controllers”) 

3) assignableTypes — This arguments will make sure to scan and handle the exceptions from the mentioned classes

	eg. @ControllerAdvice(assignableTypes = {ControllerInterface.class, AbstractController.class})


## Basic structure
	@ControllerAdvice
	public class GlobalExceptionHandler {
		@ExceptionHandler({myExceptionClass.class})
		public ResponseEntity<Object> handleSomethingNotFoundException(myExceptionClass exception) {
			return ResponseEntity
					.status(HttpStatus.INTERNAL_SERVER_ERROR)
					.body(exception.getMessage());
		}
	}
	
	
### For non Rest controller 
	we can use spring AOP to handle Exception and can also create that specific type to exception class to make it more effective
	we can also pass message or specific data or throw cause for that exception.