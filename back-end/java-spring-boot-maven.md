# Create a simple RESTful API using Spring-boot maven

- Goals:
  - call HTTP method GET to http://localhost:8080/greeting would get response:
  ```JSON
  { "id": 1, "content": "Hello World!" }
  ```
### Using Itellij IDEA
#### 1.Open Intellj IDEA - New project
#### 2.Maven (*Project Java SDK: 10.0.2)
#### 3.GroupId (/*Argument1/)
#### 4.ArtifactId (/*Argument2/)
#### 5.Version (/*1.0-SNAPSHOT/)
#### 6.Project name: /*Project Name/
#### 7.Directory: (/*~/Directory You Want to Use//)
#### 8.Set up the ***`POM.XML`***
```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		 xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.2.2.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>/*Argument1/</groupId>
	<artifactId>/*Argument2/</artifactId>
	<version>0.0.1-SNAPSHOT</version>
<!--============================= ABOVE is Generated content! ============================-->
	<properties>
		<java.version>1.8</java.version>
	</properties>
 <!--============================ This tag<java.version> defines the version of JAVA =========================-->
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
			<exclusions>
				<exclusion>
					<groupId>org.junit.vintage</groupId>
					<artifactId>junit-vintage-engine</artifactId>
				</exclusion>
			</exclusions>
		</dependency>
	</dependencies>
  
  <!--================================<dependencies>tag includes all individual<denpendency>tag==============-->

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>
<1--=============================<build> tag definces the <plugins> to use to build the project=============-->
</project>
```


#### 9.create ~/src/main/java/*Wherever-You-Want/*Entry-You-Name-It.java
```Java
public class *Entry-You-Name-It {
    public static void main(String[] args) {
    }
}
```

#### 10. Right click ***`pom.xml`*** file -> Run Maven -> install (This step is to download and install all needed dependencies)
If success you should be able to see information similar to below
```powershell
...
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 4.617 s
[INFO] Finished at: 2020-03-31T00:14:56+11:00
[INFO] Final Memory: 26M/94M
[INFO] ------------------------------------------------------------------------
```
#### 11.Create ~/src/main/java/*Wherever-You-Want/Example.java as below:
```Java
// * This class is to store the data class you want to send

public class Example {
    private final long id; // * Notice here the name of the variable
    private final String content; // * Notice this too

    public Example(long id, String content) {
        this.id = id;
        this.content = content;
    }

    public long getId() { // * The getter should strictly written like get + Captalized Initial Letter + remaining letter
        return id;
    }

    public String getContent() { // * Same as getId, get + content => getContent()
        return content;
    }
}

```
#### 12.Create ~/src/main/java/*Wherever-You-Want/ExampleController.java as below:
```Java


import java.util.concurrent.atomic.AtomicLong; // a very large incrementable number just for simple Id

import org.springframework.web.bind.annotation.GetMapping; // Here maps the url call to the coresponding method
import org.springframework.web.bind.annotation.RequestParam; // Here retrieves the url parameters (i.e. ~url/?Parameter=thevalue)
import org.springframework.web.bind.annotation.RestController; // Here defines where the rest controller is

@RestController
public class ExampleController {
    private static final String template = "Hello, %s!"; // Here writes the simplest template for the content.
    private final AtomicLong counter = new AtomicLong(); // generate an instance of the id object

    @GetMapping("/greeting") // maps this method to relative url :/greeting , **the base url could be http://localhost:8080 which host by tomcat
    public Example greeting(@RequestParam(value = "name", defaultValue = "World") String name) { // this line means if no parameter like "name=???"exists, the name value would be 'World'
        return new Example(counter.incrementAndGet(), String.format(template, name)); // Here returns JSON.parse(new Example(bla bla))
    }
}
```
***If the import shows error message there, just click it and hover your mouse to "Add Maven Dependency..."

#### 13.Edit ~/src/main/java/*Wherever-You-Want/*Entry-You-Name-It.java as below:
```Java
import org.springframework.boot.SpringApplication; // Import Java Spring Framework
import org.springframework.boot.autoconfigure.SpringBootApplication; // Import the Sprint Boot application with default configurations

@SpringBootApplication // Tells where the entry class of springBootApplication is
public class *Entry-You-Name-It {

	public static void main(String[] args) {
		SpringApplication.run(*Entry-You-Name-It.class, args); // here runs the Spring Application with default configurated Spring Boot Application
	}

```
#### 14. Run ~/src/main/java/*Wherever-You-Want/*Entry-You-Name-It.java
if you see information as below, this means you have succeed.
```powershell
2020-03-31 00:44:22.627  INFO 14128 --- [           main] *Wherever-You-Want/*Entry-You-Name-It    : No active profile set, falling back to default profiles: default
2020-03-31 00:44:24.731  INFO 14128 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2020-03-31 00:44:24.746  INFO 14128 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2020-03-31 00:44:24.746  INFO 14128 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.29]
2020-03-31 00:44:24.747  INFO 14128 --- [           main] o.a.catalina.core.AprLifecycleListener   : Loaded APR based Apache Tomcat Native library [1.2.23] using APR version [1.7.0].
2020-03-31 00:44:24.747  INFO 14128 --- [           main] o.a.catalina.core.AprLifecycleListener   : APR capabilities: IPv6 [true], sendfile [true], accept filters [false], random [true].
2020-03-31 00:44:24.748  INFO 14128 --- [           main] o.a.catalina.core.AprLifecycleListener   : APR/OpenSSL configuration: useAprConnector [false], useOpenSSL [true]
2020-03-31 00:44:24.751  INFO 14128 --- [           main] o.a.catalina.core.AprLifecycleListener   : OpenSSL successfully initialized [OpenSSL 1.1.1c  28 May 2019]
2020-03-31 00:44:24.874  INFO 14128 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2020-03-31 00:44:24.874  INFO 14128 --- [           main] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 2160 ms
2020-03-31 00:44:25.089  INFO 14128 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2020-03-31 00:44:25.255  INFO 14128 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2020-03-31 00:44:25.258  INFO 14128 --- [           main] *Wherever-You-Want/*Entry-You-Name-It    : Started Entry in 3.157 seconds (JVM running for 3.866)
```
#### 15.Open your browser and go to ***`http://localhost:8080/greeting`*** the output should be as below
```powershell
{"id":1,"content":"Hello, World!"}
```
if you go ***`http://localhost:8080/greeting?name=yourname`*** the output could be
```powershell
{"id":2,"content":"Hello, yourname!"}
```
