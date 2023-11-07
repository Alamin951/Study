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








### Core
***spring-security-core.jar*** contains core authentication and access-control classes and interfaces, remote support and basic provisioning APIs. It Contains the package:
- org.springframework.security.core
- org.springframework.security.access
- org.springframework.security.authentication
- org.springframework.security.provisioning


