# Single Sign on with github 


* First, you need to create a Spring Boot application, which can be done in a number of ways. The easiest is to go to https://start.spring.io and generate an empty project (choosing the "Web" dependency as a starting point). Equivalently, do this on the command line:
##
    $ mkdir ui && cd ui
    $ curl https://start.spring.io/starter.tgz -d style=web -d name=simple | tar -xzvf -


##

* Add a Home Page
#### In your new project, create index.html in the src/main/resources/static folder. You should add some stylesheets and JavaScript links so the result looks like this:



##

        <!doctype html>
    <html lang="en">
    <head>
        <meta charset="utf-8"/>
        <meta http-equiv="X-UA-Compatible" content="IE=edge"/>
        <title>Demo</title>
        <meta name="description" content=""/>
        <meta name="viewport" content="width=device-width"/>
        <base href="/"/>
        <link rel="stylesheet" type="text/css" href="/webjars/bootstrap/css/bootstrap.min.css"/>
        <script type="text/javascript" src="/webjars/jquery/jquery.min.js"></script>
        <script type="text/javascript" src="/webjars/bootstrap/js/bootstrap.min.js"></script>
    </head>
    <body>
        <h1>Demo</h1>
        <div class="container"></div>
    </body>
    </html>    




##

* None of this is necessary to demonstrate the OAuth 2.0 login features, but it’ll be nice to have a pleasant UI in the end, so you might as well start with some basic stuff in the home page.

## 
    <dependency>
	<groupId>org.webjars</groupId>
	<artifactId>jquery</artifactId>
	<version>3.4.1</version>
    </dependency>
    <dependency>
        <groupId>org.webjars</groupId>
        <artifactId>bootstrap</artifactId>
        <version>4.3.1</version>
    </dependency>
    <dependency>
        <groupId>org.webjars</groupId>
        <artifactId>webjars-locator-core</artifactId>
    </dependency>
##

*To make the application secure, you can simply add Spring Security as a dependency. Since you’re wanting to do a "social" login (delegate to GitHub), you should include the Spring Security OAuth 2.0 Client starter:


##
    <dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-oauth2-client</artifactId>
    </dependency>
##