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
  * Inside the project in Eclipse create a new folder named lib and paste the JAR files
  * There is one more file that we need. It is Apache Commons Logging (luv2code.com/downloadlogging) - download from here 
  * Open the downloaded folder and copy JAR file: commons-logging-1.2.jar and paste into lib folder in Eclipse 
  * Now we need to add it to the path of our project - right click on project name and choose Properties - > select Java Build Path - Libraries tab -> Add JARS -> expand lib folder for spring-demo-one -> shift click and highlight all the jar files - click ok -> now inside the project there should be a new item called Referenced Libraries
  

* Download Commons Logging JAR file
* Add JAR files to Eclipse Project ... Buld Path


What about Maven? - Istead of downloading, you can use a tool like Maven. Maven will be covered at the end of the course as we
focus on Spring now. 

##### What is Inversion Control? 

* It is the design process of externalizing the construction and management of your objects
* You outsource obect creation to an object factory - the big idea of inversion of control




###### Coding Scenario 

* We will have an app that will make use of a coach, Baseball coach. 
* Our app will say: "Hey coach, give me a daily workout"
* The requirement is also that the app is configurable for another sport (hockey, cricket, tennis, etc) and work with any type of coach

We are about to create a prototype and it will have 4 key players:
* myApp.java - main method
* BaseballCoach.java
* Coach.java - interface after refactoring 
* TrackCoach.java


We start with myApp.java - it just has the main method. 
BaseballCoach.java - will have implementation.
THEN AFTER REFACTORING, we will introduce an interface Coach.java 
and then we will also have another implementation TrackCoach.java - introducing another coach and seeing of our application continues to work. 


ROUGH PROTOTYPE 

* Create a new package (com.luv2code.springdemo)
* Now, we create a simple pojo - BaseballCoach.java 
* We create one method there 
```
public class BaseballCoach{
 public String getDailyWorkout() {
  return "Spend 30 minutes on batting practice";
 }
}

```

* Now create new class MyApp.java

```
MyApp.java

public class MyApp {

 public static void main(String[] args) {
 
  //create the object 
  BaseballCoach theCoach = new BaseballCoach();
  
  
  // use the object 
  System.out.println(theCoach.getDailyWorkout());
 }
}

```

* Now we have the requirement that this app should would with any type of Coach. We will take advantage of the Software Engineering Best Practice - Code to Interface which means instead of coding directly into BaseballCoach implementation (MyApp.java), we will make use of a well defined interface that all coaches will support.

* Every coach will have a method getDailyWorkout();

* Right click on project and create a new interface - name: Coach and add one method getDailyWorkout(); Interface specified what and not how. Implementations will provide the details. 

```
public interface Coach {
 
 public String getDailyWorkout();
}

```

* We need to re-factor BaseballCoach.java by adding "implements Coach" and add @Override - this is the method that we override 

```
public class BaseballCoach implements Coach {
 
 @Override 
 public String getDailyWorkout() {
  
  return "Spend 30 minutes on batting practice.";
 }
}

```

* Inside MyApp.java, we need to change " BaseballCoach theCoach = new BaseballCoach();" to Coach theCoach = new BaseballCoach();





