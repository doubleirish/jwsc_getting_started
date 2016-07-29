# jwsc   Environment Setup
java web services in the cloud . Getting your environment setup. e.g vagrant, sdkman etc 

A Commmon Environment 
In previous labs a lot of time was spent by students on setting up their environment before they could write a single line of code. 
Depending on their Operating System , Mac, PC, Unix they might have to  use  sligtly different configuration or software versions and might also encounter issues local to a specific OS.  
To Simplify the setup we're using Vagrant and VirtualBox to create a Linux environment which is perconfigured with most of the tools you'll nee

This attached Vagrantfile provides a standard predefined java environment to help you get started faster.



##sdkman!
The included [sdkman](http://sdkman.io/) tool makes it easy to install and manage tools like maven, gradle and springboot-cli without worrying about PATHS and environmental variables.
In the old days to install a tool like maven or gradle you would have to do the following :-
 * find the tool on the web and download it
 * extract it into a directory 
 * possibly fix file permissions
 * add a XYZ_HOME environmental variable
 * add the XYZ_HOME\bin directory to your PATH variable

The sdkman utility simplfies all of the above
  and also makes it easy to have multiple versions of tools like maven and gradle
   and easily switch between versions. This tool is already included in the attached Vagrantfile .

To install sdkman on a fresh system just paste the following in a linux terminal

```
curl -s "https://get.sdkman.io" | bash
```

This will install the sdk tool.
To use the tool create a new terminal window to activate the entry the installation
added to your ~/.bashrc file

To see all the candidate softwarre you can install type
```
sdk list
```

to install the latest version
```
sdk install candidate
```
e.g
sd install maven

Examples of commonly used command are below. The  full usage guide is at http://sdkman.io/usage.html

| sdk cmd  |  example | description  |
|---|---|---|
| sdk ls                             | sdk list                | show all candidate software you can install |
| sdk ls <candidate>                 | sdk ls maven            | show all versions of candidate software |
| sdk install <candidate>            | sdk install maven       | install the latest version  |
| sdk install <candidate>  [version] | sdk install maven 3.3.3 | install a specific verion of software    |
| sdk current                        |                         | show all software installed by sdk    |
| sdk use <candidate> <version>      | sdk use gradle 2.8      | switch to a differnt version of installed software  |


the following is the list of software automatically installed by sdkman in the vagrant file
```
sdk install maven
sdk install springboot
sdk install gradle
```

vagrant@vagrant-ubuntu-trusty-64:/vagrant$ sdk current
Using:
gradle: 2.8
maven: 3.3.9
springboot: 1.3.6.RELEASE

## spring init
The Spring boot Command Line Interface  can be accessed by entering
```
spring
```

entering spring with out arguments by default   returns  the help message showing all the commands you can pass into the spring CLI

to see more information on a particualr command  enter

spring help <command>

e.g
spring help init

the init command allows skeleton applications to be created very easily
this is somewhat similar to the old maven archetype feature but it is much more flexible.
Think of an application as containing facets or dependencies, you decide what facets will be included
e.g a web facet if it has a web frontend or a JPA facet if it has a JPA based interface with a datastore.
You include the facets you're interested in and it builds a zip containing the source code of a skeleton application.

to see a list of all avaialble dependencies
```
spring init --list
```
or  visit the following website and enable the advanced search to see all available dependencies
```
http://start.spring.io/
```

the following command will create a simple web appicalition skelton in a new "hello" directory
```
spring init -d=web,actuator,actuator-docs,hateoas  hello
```

```
cd hello
/vagrant/hello$ ls
mvnw  mvnw.cmd  pom.xml  src
```
and it's created a standard maven subdirectory structure to store the application files
```
/vagrant/hello$ du
49      ./.mvn/wrapper
49      ./.mvn
1       ./src/main/java/com/example
1       ./src/main/java/com
1       ./src/main/java
0       ./src/main/resources/static
0       ./src/main/resources/templates
0       ./src/main/resources
1       ./src/main
1       ./src/test/java/com/example
1       ./src/test/java/com
1       ./src/test/java
1       ./src/test
1       ./src
```


At this point we're good to run the webapp

$ mvn spring-boot:run

in your browser navigate to

localhost:8080/

this doesn't doo much right now

 in your IDE select File->Open and double click on the hello/pom.xml file to create a new project

 open up the src/main/java/com/example/DemoApplication

 this file is the entry point of the application.

 we can add a simple rest controller mapping  so the class looks like the following

 package com.example;

 import org.springframework.boot.SpringApplication;
 import org.springframework.boot.autoconfigure.SpringBootApplication;
 import org.springframework.web.bind.annotation.RequestMapping;
 import org.springframework.web.bind.annotation.RestController;

 @SpringBootApplication
 @RestController
 public class DemoApplication {

 	@RequestMapping("/")
 	public String helloWorld() {
 		return "Hello World";
 	}

 	public static void main(String[] args) {
 		SpringApplication.run(DemoApplication.class, args);
 	}
 }


 save the file, use [CTRL-C] to kill your existin running webapp and restart it with the following command made from the hello directory

 $ mvn spring-boot:run

 refreshing your browser at the following location
 localhost:8080/
 should now return a simple hello page

 by adding the actuator dependency when we called spring init
 we also automatically added a simple admin console set of pages to our webapp.

  localhost:8080/actuator

Most of this actuator related information is returned in JSON format.
to make it easier to read There's a JSON formatter chrome extension you can add if you're using the chrome browser

https://chrome.google.com/webstore/detail/bcjindcccaagfpapjjmafapmmgkkhgoa


## Spring Tool Suite
there are some special spring boot wizards built into the Spring Tool Suite (STS) IDE
This IDE can be downloaded from spring at
https://spring.io/tools/sts/all

On Runing the IDE for the first time
select a workspace location of "/vagrant/workspace"
After installation completes select the following menu items

File -> New -> Spring Starter Project
use the defaults and select next
select the web dependency

Add the @RequestCOntroller and @requestMapping annotations as before

select the Run -> Run As menu item
Select "Spring Boot" App as the Run-as configuration

run the app , you should see the output in  the log pane.
conect a browser to localhost:8080
or
curl localhost:8080 to see the output.

to see how to use properties
https://spring.io/blog/2015/03/18/spring-boot-support-in-spring-tool-suite-3-6-4

TODO spring init -d=web,data-jpa,thymeleaf,actuator,actuator-docs,hsql  hello

## Deploying to cloud foundry from eclipse
https://blog.pivotal.io/pivotal-cloud-foundry/products/service-management-through-cloud-foundry-eclipse
