# springboot-swagger
Swagger Implementation with Spring Boot


This sample provides the implementation of Swagger in a Spring Boot Project

A class named SwaggerConfig.java enables the configuration for Swagger. Also I have provided a test endpoint at HelloController.java

Example of implementation:

**1. Create a new project (For the creation I have used IntelliJ -> Spring initializr)**

First thing we need to do is adding some dependencies at your pom.xml configuration
```
<dependency>
  <groupId>io.springfox</groupId>
  <artifactId>springfox-swagger2</artifactId>
  <version>2.7.0</version>
</dependency>

<dependency>
  <groupId>io.springfox</groupId>
  <artifactId>springfox-swagger-ui</artifactId>
  <version>2.7.0</version>
</dependency>
```

Next step is about implementing the swagger at our project

**2. Create a new package called "config"**

**3. Create a new class inside config package SwaggerConfig.java**

  Add the following code below:
  
  ```
  @Bean
    public Docket api() {
        return new Docket(DocumentationType.SWAGGER_2)
                .select()
                .apis(RequestHandlerSelectors.any())
                .paths(Predicates.not(PathSelectors.regex("/error")))
                .build()
                .apiInfo(apiInfo())
                .useDefaultResponseMessages(false)
                .securitySchemes(new ArrayList<>(Arrays.asList(new ApiKey("Bearer %token", "Authorization", "Header"))))
                .genericModelSubstitutes(Optional.class);
    }

    private ApiInfo apiInfo() {
        return new ApiInfoBuilder().title("Your API")
                .description("Swagger Implementation")
                .build();
    }
  ```
The main part of implementation is done by implementing those steps

##### If you want to test the swagger with any endpoints (you can add yours)

**4. Create a new package "controller" and Add a new class HelloController.java**

Add the following code below:

```
@RestController
public class HelloController {

    @PostMapping("/hello")
    public String sayHello(){
        return "Hello!";
    }
}
```

To have an access at our Swagger Implementation
Run the project and go to: http://localhost:8080/swagger-ui.html




