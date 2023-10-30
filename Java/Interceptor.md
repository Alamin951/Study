
Dispatcher Servlet is the entry point for all the incoming request.

tomcat -> Filter -> Interceptor -> Controller -> ......


In Spring boot application we have 2 options either we use filter or Interceptor.

	Before writing an Interceptor class we need to register the interceptor class to the WebConfig. 

	On the webConfig we need to  override the addInterceptors for register.

On  webConfig addInterceptors we can also assign the pathPatterns
	registry.addInterceptors(...).addPathPatterns("") -> specify any url.

Spring Interceptor is similar to a Filter, which is used to intercept the request and process them. Spring MVC allows you to intercept web requests for pre-handling 
and post-handling through Handler Interceptors.

- Spring Interceptor works like the filter which intercepts the request and process them.
	
	1. preHandle(): The preHandle() method will be called before the actual handler is executed. This method returns a boolean value which can be used to continue or break the control flowing to the DispatcherServlet.
		
	2. postHandle(): The postHandle() method will be called after the handler is executed but before the view being rendered. So, you can add more model objects to the view but you can not change the HttpServletResponse.
		
	3. afterCompletion(): The afterCompletion() method will be called after the request has completed and the view is rendered.
	
	
### Spring Interceptor using HandlerInterceptor:
	
	public class HelloInterceptor implements HandlerInterceptor
	{
		@Override
		public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object obj) throws Exception
		{
			System.out.println("Inside preHandle!!");
			return true;
		}
		
		@Override
		public void postHandle(HttpServletRequest request, HttpServletResponse response, Object obj, ModelAndView mav)
				throws Exception
		{
			System.out.println("Inside postHandle!!");
		}
		
		@Override
		public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object obj, Exception exception)
				throws Exception
		{
			System.out.println("Inside afterCompletion!!");
		}
	}
	
### Ref link:
https://www.youtube.com/watch?v=DuMf8Nwb-9w
https://medium.com/@aedemirsen/what-is-spring-boot-request-interceptor-and-how-to-use-it-7fd85f3df7f7
	