# Authentication Module
There are many type of authorization method and protocols. One popular protocol is ***OAuth***. OAuth is open protocol that allows third party application or web site to access restricted resources on another web site or service. By using the access token strategy a user's login credentials are never stored within an application and only used or required when authenticating a service for the application or user.

The SQLiteConnectionRepository class implements the ConnectionRepository Interface from Spring Social. 


### Set up Spring Security
If Spring Security is on the class path then Spring Boot automatically secures all HTTP endpoints with basic authentication. 

With Gradle we need to add 3 Lines in build.gradle
~~~
implementation 'org.springframework.boot:spring-boot-starter-security'
//  Temporary explicit version to fix Thymeleaf bug
implementation 'org.thymeleaf.extras:thymeleaf-extras-springsecurity6:3.1.1.RELEASE'
implementation 'org.springframework.security:spring-security-test'
~~~

In Maven need to add two extra entries (one for application and one for testing) in the pom.xml.

~~~
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-security</artifactId>
</dependency>
<dependency>
	<groupId>org.thymeleaf.extras</groupId>
	<artifactId>thymeleaf-extras-springsecurity6</artifactId>
	<!-- Temporary explicit version to fix Thymeleaf bug -->
	<version>3.1.1.RELEASE</version>
</dependency>
<dependency>
	<groupId>org.springframework.security</groupId>
	<artifactId>spring-security-test</artifactId>
	<scope>test</scope>
</dependency>
~~~

#### Basic WebSecurityConfig.java
~~~
package com.example.securingweb;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
@EnableWebSecurity
public class WebSecurityConfig {

	@Bean
	public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
		http
			.authorizeHttpRequests((requests) -> requests
				.requestMatchers("/", "/home").permitAll()
				.anyRequest().authenticated()
			)
			.formLogin((form) -> form
				.loginPage("/login")
				.permitAll()
			)
			.logout((logout) -> logout.permitAll());

		return http.build();
	}

	@Bean
	public UserDetailsService userDetailsService() {
		UserDetails user =
			 User.withDefaultPasswordEncoder()
				.username("user")
				.password("password")
				.roles("USER")
				.build();

		return new InMemoryUserDetailsManager(user);
	}
}
~~~

The ***WebSecurityConfig*** class is annotated with ***@EnableWebSecurity*** to enable Spring Security’s web security support and provide the Spring MVC integration. It also exposes two beans to set some specifics for the web security configuration:

The ***SecurityFilterChain*** bean defines which URL paths should be secured and which should not. Specifically, the / and */home* paths are configured to not require any authentication. All other paths must be authenticated.

When a user successfully logs in, they are redirected to the previously requested page that required authentication. There is a custom */login* page (which is specified by *loginPage()*), and everyone is allowed to view it.

The ***UserDetailsService*** bean sets up an in-memory user store with a single user. That user is given a user name of user, a password of password, and a role of USER.


> HTTP Request > JwtAuthFilter > JwtService > update the SecurityContextHolder > DispatcherServlet





## Authorisation in Spring Security
Spring Security defines the notion of a principal which is currently logged in user. After user's successful authentication, the principal is stored in Spring's security context. It is thread-bound. This makes it available to the rest of service. 
*Security context does not propagate by default in child threads.*

In order to provide authorisation functionality, Spring Security uses the ***AccessDecisionManager*** , which is responsible for delegating authorisation decisions to one or more ***AccessDecisionVoter*** instances.



### Core
***spring-security-core.jar*** contains core authentication and access-control classes and interfaces, remote support and basic provisioning APIs. It Contains the package:
- org.springframework.security.core
- org.springframework.security.access
- org.springframework.security.authentication
- org.springframework.security.provisioning



## Java Configuration
### Hello Web Security Java Configuration
The First step is to create a Spring Security Java Configuration. 
THe configuration creates a servlet Filter Known as the ***SpringSecurityFilterChain***, which is responsible for all the security of the application. 

~~~
@Configuration
@EnableWebSecurity
public class WebSecurityConfig {

	@Bean
	public UserDetailsService userDetailsService() {
		InMemoryUserDetailsManager manager = new InMemoryUserDetailsManager();
		manager.createUser(User.withDefaultPasswordEncoder().username("user").password("password").roles("USER").build());
		return manager;
	}
}
~~~

This configuration is not complex or extensive, but it does a lot:

- Require authentication to every URL in your application

- Generate a login form for you

- Let the user with a Username of user and a Password of password authenticate with form based authentication

- Let the user logout

- CSRF attack prevention

- Session Fixation protection

- Security Header integration:

	- HTTP Strict Transport Security for secure requests

	- X-Content-Type-Options integration

	- Cache Control (which you can override later in your application to allow caching of your static resources)

	- X-XSS-Protection integration

	- X-Frame-Options integration to help prevent Clickjacking

- Integration with the following Servlet API methods:

	- HttpServletRequest#getRemoteUser()

	- HttpServletRequest#getUserPrincipal()

	- HttpServletRequest#isUserInRole(java.lang.String)

	- HttpServletRequest#login(java.lang.String, java.lang.String)

	- HttpServletRequest#logout()

### AbstractSecurityWebApplicationInitializer
Next step is to register the ***springSecurityFilterChain*** with the war file.
We can do so in Java configuration with Spring’s *WebApplicationInitializer* support in a Servlet 3.0+ environment. Not surprisingly, Spring Security provides a base class (*AbstractSecurityWebApplicationInitializer*) to ensure that the springSecurityFilterChain gets registered for you. The way in which we use *AbstractSecurityWebApplicationInitializer* differs depending on if we are already using Spring or if Spring Security is the only Spring component in our application.



### HttpSecurity

~~~
@Bean
public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
	http
		.authorizeRequests(authorize -> authorize
			.anyRequest().authenticated()
		)
		.formLogin(withDefaults())
		.httpBasic(withDefaults());
	return http.build();
}
~~~

This default configuration consists:
- Ensures that any request requires the user to be authenticated
- authenticate with form based login
- Let user authenticate with HTTP Basic authentication


