# Spring Hibernate Notes

##### Roadmap:
1. Set up development environment
2. Applying Spring Inversion of COntrol and Dependency Injection
3. Perform object to relational mapping with Hybernate
4. Leverage the Hybernate API to develop CRUD apps

##### Why should we use Spring? (will use S for short)

* S is a popular framework for building enterprise Java applications
* Learn both Java EE and Spring


##### Spring Core Framework Overview 

www.spring.io (documentation, tutorials, etc)

##### Goals of Spring

* Lightweight development with Java POJOs(plain old java objects)
* Dependency injection to promote loose coupling by making use dependency of injection. So instead of hardwiring your objects to get 
you simply specify the wiring via configurations or annotations. 
* Declarative programming with Aspect-Oriented Programming - add some application-wide services to given objects
* Minimazie boilerplate Java code 

##### Spring Projects 

* Spring projects are additional S modules built on top of the core S Framework. Only use what you need
* Examples: Spring social, Spring boot 

##### Dev Environment Setup Overview 

1. You must have JDK installed 
2. You need Java Application Server (for S MVC development) - Tomcat
* Installing Tomcat
  * Verify installation http://localhost:8080
  * Connect Tomcat to Eclipse: click on the tab Servers in Eclipse, click on the link, window opens and in Apache folder, find Tomcat
3. Eclipse IDE 
4. Downloading Spring JAR files 
  * Create Eclipse Project
  * Change perspective in Eclipse from Java EE: Windows -> Perspective -> Open Perspective -> Java
  * File -> New -> Java Project - name: spring-demo-one
  * Download from www.love2code.com/downloadspring (this is spring repository of different versions of S)- > download the latest 
  * In the folder that was just downloaded, find libs folder, select all JAR files and copy them
  * Inside the project in Eclipse create a new folder named lib 
  

* Download Commons Logging JAR file
* Add JAR files to Eclipse Project ... Buld Path


What about Maven? - Istead of downloading, you can use a tool like Maven. Maven will be covered at the end of the course as we
focus on Spring now. 








