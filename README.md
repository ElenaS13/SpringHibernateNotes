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

```
MyApp.java

public class MyApp {

 public static void main(String[] args) {
 
  //create the object 
  Coach theCoach = new BaseballCoach();
  
  
  // use the object 
  System.out.println(theCoach.getDailyWorkout());
  
 }
 
}
```

* Now we need to add the requirement of working with a different type of coach. Inside MyApp.java, change "Coach theCoach = new BaseballCoach();" to "Coach theCoach = new TrackCoach();"


```
MyApp.java

public class MyApp {

 public static void main(String[] args) {
 
  //create the object 
  Coach theCoach = new TrackCoach();
  
  
  // use the object 
  System.out.println(theCoach.getDailyWorkout());
  
 }
 
}
```

* But we do not have a TrackCoach class yet so we get an error. Click on the error that will create TrackCoach class. The interface will be included. 

```
public class TrackCoach implements Coach {
 
  @Override 
  public String getDailyWorkout(){
   
   return "Run a hard 5k.";
   
  }
}
```

* The other requirement is that Coach implementaiton should be configurable. Right now it is hard-coded: Coach theCoach = new TrackCoach();

* Ideally we would read the implementation from the config file so we could easily swap by changing a config file instead of having to change the source code. **Spring was designed to addess this exact problem**.



##### Spring Inversion of Control

We did not have support for configuration up to this point. We will make use of **object factory**. Spring provides and object factory so that our application could talk to Spring, say "give me an object". Based on the config file or annotation, Spring will give you an appropriate implementation. 

Spring Container

Primary Funcions: create and manage objects(Inversion of Control) and Inject object's dependancies (Dependancy Injection)

There are 3 ways to configure Spring Container:
1. XML config file (legacy, but most legacy apps still use this )
2. Java Annotations 
3. Java Source Code


##### Spring Development Process

* Configure your Spring Beans
This is done in xml file. In our case, applicationContext.xml. 

<bean id="myCoach"
      class="com.luv2code.springdemo.BaseballCoach">
</bean>

id is what will be used by Java app to retrieve bean from S container.
Class is actual class that you will use for your application. 



* Create Spring Container 

Generally known as application context. 

ClassPAthXmlApplicatonContext context = new ClassPathXmlApplicationContext("applicationContext.xml");


* Retrieve Beans from Spring Container 

Your application will tell the S container to give Coach object and based on the information in the config file, it will give you an implementation of that given interface. 

So here is the code to retrieve bean from S container 

Coach theCoach = context.getBean("myCoach", Coach.class);  //myCoach has to match whats in xml file for id. 



NEXT STEP
We are adding .xml file and configuring S beans. 
WE define a bean with id and class. 

Now we are going to make use of a Java class and we name it HelloSpringApp.java

```
public class HelloSpringApp {

 public static void main(String[] args) {
 
  //load the spring config file 
  
  ClassPAthXmlApplicatonContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
  
  //retrieve beans from S container 
  
  Coach theCoach = context.getBean("myCoach", Coach.class);
  
  
  //now that we have the bean, we can call methods on it 
  
  System.out.println(theCoach.getDailyWorkout());
  
  //close the app context 
  context.close();
  
 }
}

```
* Create and manage objects(Inversion of Control)
* Inject object's dependencies (Dependency Injection)

Demo Example:
Our Coach already provides daily workouts. Now will also provide daily fortunes. 
* New helper: Fortune Service 
* This is dependency
* dependency = helper (coach depends on the fortuneService to serve daily fortune)

There are many types of Injection in Spring:
Common ones are Constructor Injection and Setter Injection

DEVELOPMENT PROCESS - Constructor Injection 

1. Define the dependency interface and class 
We create an interface FortuneService and it will return a string 

```
FortuneService.java

public interface FortuneService {

 public String getFortune();    //returns a string 
}

```
NOW we create a class that implements the interface FortuneService 

```
HappyFortuneService.java

public class HappyFortuneService implements FortuneService {
 
  public String getFortune() {
   return "Today is your lucky day!";
  }
}
```

Move to Coach interface Coach.java which right now provides daily workout and add fortuneService. 

```
public interface Coach {
 
 public String getDailyWorkout();
 
 public String getDailyFortune();
 
}

```

Now we add the getDailyFortune() to BaseballCoach.java and same for TrackCoach.java 

```
public class BaseballCoach implements Coach {
 
 @Override 
 public String getDailyWorkut() {
  return "Spend 30 minutes on batting practice";
  
 }
 
 @Override 
 public String getDailyFortune() {
 
  return "Have a lucky day";
 }
}

```




2. Create a constructor in your class for injections 
Inject dependencies here calling a constructor. Create a constructor that will accept a dependency. 

```
BaseballCoach.java

public class BaseballCoach implements Coach {

 private FortuneService fortuneService;  //private field for dependency
 
 public BaseballCoach(FortuneService theFortuneService){
   
   fortuneService = theFortuneService;
 
 }
 
 @Override 
 public String getDailyWorkout() {
  return "Spend 30 minutes on batting practice";
 }
 
 @Override 
 public String getDailyFortune() {
 
 //use the Fortune Service
  return fortuneService.getFortune();
 }
}

```


3. Configure the dependency injection in Spring config file 
Define a bean inside xml file and then inject that dependency into the class. 



>>>>>>>>>>

NOW we will move into main class (HelloSpringApp.java) and make use of the beans from spring and call some methods on it. 


##### Setter Injection
1. Create a setter method in your class for injections 

```
package com.love2code.springdemo;

public class CricketCoach implements Coach {
	
	private FortuneService fortuneService;
	
	public CricketCoach() {
		
		
	}
	//setter method will be called by S to injects dependency
	public void setFortuneService(FortuneService fortuneService) {
		
		this.fortuneService = fortuneService;
	}

	@Override
	public String getDailyWorkout() {
		// TODO Auto-generated method stub
		return null;
	}

	@Override
	public String getDailyFortune() {
		// TODO Auto-generated method stub
		return null;
	}

}

```



2. Configure dependency injection in config file 

When you use 'property' in config file, S will attempt to call a setter method.



SPRING CONFIG WITH ANNOTATIONS

Anntotations - meta-data about the class. 



Spring will scan a package and it will register al @Components 


SETTER INJECTION
Inject dependancies by calling setter methods on your class. 
Default constructor - no args constructor. 



