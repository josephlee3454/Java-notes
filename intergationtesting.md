## Intergation testing 
* intergration testing plays a important role in the app dev cycle by verifying the end to end behavior of a system 


## preperation
* we'll need the latest junit-jupiter-engine, junit-jupiter-api, and Spring test dependencies:

 
# 
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-engine</artifactId>
        <version>5.7.0</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.7.0</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-test</artifactId>
        <version>5.3.3</version>
        <scope>test</scope>
    </dependency> 
#


* we also need hamcrest json
#   
    <dependency>
        <groupId>org.hamcrest</groupId>
        <artifactId>hamcrest-library</artifactId>
        <version>2.2</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>com.jayway.jsonpath</groupId>
        <artifactId>json-path</artifactId>
        <version>2.5.0</version>
        <scope>test</scope>
    </dependency> 

#

## spring mvc test config
* JUnit 5 defines an extension interface through which classes can integrate with the JUnit test.
We can enable this extension by adding the @ExtendWith annotation to our test classes and specifying the extension class to load. To run the Spring test, we use SpringExtension.class.


# 

    @ExtendWith(SpringExtension.class)
    @ContextConfiguration(classes = { ApplicationConfig.class })
    @WebAppConfiguration
    public class GreetControllerIntegrationTest {
        ....
    }   


#


* we use this java class to specify the context config
# 

    @ContextConfiguration(locations={""})

# 

* By default, it looks for the root web application at path src/main/webapp. We can override this location by simply passing the value attribute:

#
   @WebAppConfiguration(value = "")

#

* We'll now  wire the web application context right into the test
#

    @Autowired
    private WebApplicationContext webApplicationContext;
#

* MockMvc provides support for Spring MVC testing. It encapsulates all web application beans and makes them available for testing.



# 
    private MockMvc mockMvc;
    @BeforeEach
    public void setup() throws Exception {
        this.mockMvc = MockMvcBuilders.webAppContextSetup(this.webApplicationContext).build();
    }
    
#


* Let's verify that we're loading the WebApplicationContext object (webApplicationContext) properly. We'll also check that the right servletContext is being attached:
# 

    @Test
    public void givenWac_whenServletContext_thenItProvidesGreetController() {
        ServletContext servletContext = webApplicationContext.getServletContext();
        
        Assert.assertNotNull(servletContext);
        Assert.assertTrue(servletContext instanceof MockServletContext);
        Assert.assertNotNull(webApplicationContext.getBean("greetController"));
    }
#

* We can invoke the /homePage endpoint from our test as:


# 
    http://localhost:8080/spring-mvc-test/

                or
    
    http://localhost:8080/spring-mvc-test/homePage



    test code

    @Test
    public void givenHomePageURI_whenMockMVC_thenReturnsIndexJSPViewName() {
        this.mockMvc.perform(get("/homePage")).andDo(print())
        .andExpect(view().name("index"));
    }

#


## lets break down what we just did 

* perform() method will call a GET request method, which returns the ResultActions. Using this result, we can have assertion expectations about the response, like its content, HTTP status, or header

* andDo(print()) will print the request and response. This is helpful to get a detailed view in case of an error

* andExpect() will expect the provided argument. In our case, we're expecting “index” to be returned via MockMvcResultMatchers.view()


# send get request 

# 
    http://localhost:8080/spring-mvc-test/greetWithPathVariable/John
    The expected output will be:

    {
        "id": 1,
        "message": "Hello World John!!!"
    }
    Let's see the test code:

    @Test
    public void givenGreetURIWithPathVariable_whenMockMVC_thenResponseOK() {
        this.mockMvc
        .perform(get("/greetWithPathVariable/{name}", "John"))
        .andDo(print()).andExpect(status().isOk())
        
        .andExpect(content().contentType("application/json;charset=UTF-8"))
        .andExpect(jsonPath("$.message").value("Hello World John!!!"));
    }
        

#


# send get request with query parameters

#

    We'll invoke the /greetWithQueryVariable?name={name} endpoint from our test as:

    http://localhost:8080/spring-mvc-test/greetWithQueryVariable?name=John%20Doe
    In this case, the expected output will be:

    {
        "id": 1,
        "message": "Hello World John Doe!!!"
    }
    Now, let's see the test code:

    @Test
    public void givenGreetURIWithQueryParameter_whenMockMVC_thenResponseOK() {
        this.mockMvc.perform(get("/greetWithQueryVariable")
        .param("name", "John Doe")).andDo(print()).andExpect(status().isOk())
        .andExpect(content().contentType("application/json;charset=UTF-8"))
        .andExpect(jsonPath("$.message").value("Hello World John Doe!!!"));
    }
    param(“name”, “John Doe”) will append the query parameter in the GET request. This is similar to “/greetWithQueryVariable?name=John%20Doe“.

    The query parameter can also be implemented using the URI template style:

    this.mockMvc.perform(
    get("/greetWithQueryVariable?name={name}", "John Doe"));

#


# send post request 

#
    We'll invoke the /greetWithPost endpoint from our test as:

    http://localhost:8080/spring-mvc-test/greetWithPost
    We should obtain as output:

    {
        "id": 1,
        "message": "Hello World!!!"
    }
    And our test code is:

    @Test
    public void givenGreetURIWithPost_whenMockMVC_thenVerifyResponse() {
        this.mockMvc.perform(post("/greetWithPost")).andDo(print())
        .andExpect(status().isOk()).andExpect(content()
        .contentType("application/json;charset=UTF-8"))
        .andExpect(jsonPath("$.message").value("Hello World!!!"));
    }
    MockMvcRequestBuilders.post(“/greetWithPost”) will send the POST request. We can set path variables and query parameters in a similar way as before, whereas form data can be set only via the param() method, similar to query parameters as:

    http://localhost:8080/spring-mvc-test/greetWithPostAndFormData

    freestar
    Then, the data will be:

    id=1;name=John%20Doe
    So, we should get:

    {
        "id": 1,
        "message": "Hello World John Doe!!!"
    }
    Let's see our test:

    @Test
    public void givenGreetURI_whenMockMVC_thenVerifyResponse() throws Exception {
        MvcResult mvcResult = this.mockMvc.perform(MockMvcRequestBuilders.get("/greet"))
        .andDo(print())
        .andExpect(MockMvcResultMatchers.status().isOk())
        .andExpect(MockMvcResultMatchers.jsonPath("$.message").value("Hello World!!!"))
        .andReturn();
    
    assertEquals("application/json;charset=UTF-8", mvcResult.getResponse().getContentType());
    }
#
        