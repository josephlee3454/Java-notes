# Spring Security Archetecture 

## Aithentication and Access control 
* the security of a application boils down to two more or less independent problems Authentication and authorization 

* some people use the term access control but that is for some real jabronies lets not make you confused so we will stick to what we said above 

* spring security has an architecture that is designed to sperate authentication and authorization 


# Authentication 
* The main strategy fot the inteface of the authentication managaer has only one methods 

##
    public interface AuthenticationManager {

    Authentication authenticate(Authentication authentication)
        throws AuthenticationException;
    }



## 

### This authentication manager can do one of 3 things in its authenticate() method
* return a authentication (with having authenticated=true) if it can verify that the input represents a valid principal
* throw a exception if it belives that the input is a invalid principal 
* return null if i cant decide 

### AuthenticationException is a runtime exception. It is usually handled by an application in a generic way, depending on the style or purpose of the application. In other words, user code is not normally expected to catch and handle it. For example, a web UI might render a page that says that the authentication failed, and a backend HTTP service might send a 401 response, with or without a WWW-Authenticate header depending on the context.

## the most commonly used implementation of the AuthenticationManager is a ProviderManager delegates to a chain of authenticationprovider instances. 



## 

    public interface AuthenticationProvider {

	Authentication authenticate(Authentication authentication)
			throws AuthenticationException;

	boolean supports(Class<?> authentication);
    }

##


# Customizing Atuhentication Managers 
* Spring Security provides some configuration helpers to quickly get common authentication manager features set up in your application. The most commonly used helper is the AuthenticationManagerBuilder, which is great for setting up in-memory, JDBC, or LDAP user details or for adding a custom UserDetailsService. The following example shows an application that configures the global (parent) AuthenticationManager:


##
            @Configuration
        public class ApplicationSecurity extends WebSecurityConfigurerAdapter {

        ... // web stuff here

        @Autowired
        public void initialize(AuthenticationManagerBuilder builder, DataSource dataSource) {
            builder.jdbcAuthentication().dataSource(dataSource).withUser("dave")
            .password("secret").roles("USER");
        }

        }

##

* This example relates to a web application, but the usage of AuthenticationManagerBuilder is more widely applicable (see Web Security for more detail on how web application security is implemented). Note that the AuthenticationManagerBuilder is @Autowired into a method in a @Bean — that is what makes it build the global (parent) AuthenticationManager. In contrast, consider the following example:

##
    @Configuration
    public class ApplicationSecurity extends WebSecurityConfigurerAdapter {

    @Autowired
    DataSource dataSource;

    ... // web stuff here

    @Override
    public void configure(AuthenticationManagerBuilder builder) {
        builder.jdbcAuthentication().dataSource(dataSource).withUser("dave")
        .password("secret").roles("USER");
    }

    }

##




