# Refactoring
- the purpose of refactoring the code is to take an existing code base and make it better
- as project grows the application needs changes as well
- previous solutions needs to be rewritter so they can meet the current and future needs of the project
## purpose of refactoring
- its to take an existing code base and make it better
- Refactoring helps software development teams restructure and clean up code by making incremental changes that do not affect overall project behaviour
## What Refactoring DOES:
- Improves code readability and simplicity
- removes unnecessary duplicate code
## What Refactoring DOES NOT:
- Alter function of program
- change purpose of the code
- change output of system
## How does Agile facilitate code refactoring?
- since agile framework does not follow any rigid or detailed working structure
- they can improvise on the go
- agile practices encourages experimentation and light solutions
## Benefits of Agile Development
- Agile improves refactoring process by breaking down development into bite-size pieces and allows teams to focus on weeks long sprints instead of looking at the whole project all at once
- Agile offers
	- Flexibility
		- rewriting code allows you to switch between task according to user feedback
		- solve problems based on their priority instead of following a linear checklist
	- Improved communication
		- agile promotes open conversation between users and developers
		- customer feedback is sent through user stories
		- this helps in better refactoring
	- team cohesion
		 - agile requires teamwork and good communication within teams
		 - each member has to clearly understand what's the purpose of each re-write
		 - this close teamwork would lead to a shared feeling of code ownership
	- adaptability
		- agile refactoring focuses on small increments, so its easy to adapt
## Principles of refactoring
its important to know these so we dont compromise the project's integrity
1) Identify risks and benefits
	- when there's a code change, there's risk involved
	- know the risk-to-benefit ratio before making any changes
		- if changing the code is more risky but offers very less benefits, keep that in very low priority
2) Keep problems small
	- The larger the edit, the more riskier it is. so keep the problems small.
	- incremental refactoring breaks down a big problem into smaller manageable sections
	- it improves code health
3) stay on target
	 - its easy to get sidetracked during edit
	 - always remember the purpose of the edit, it is to modify, read and maintain.
## Agile Refactoring Techniques
- agile allows teams to easily switch directions and alter goals on the fly while delivering high quality results
here are some techniques,
1) Write unit tests
	- a popular method in agile developers is test-driven coding
	- its the "test first" approach to writing code
	- FIRST STEP: is to make a unit test that will prove or disprove the code's functionality
	- SECOND STEP: is to write the code that will pass the test
2) Know your code smells
	- there's publicly available patterns for good, sustainable code and bad code
	- there are patterns for bad code and these are called "code smells"
	- when identifying where to begin your refactor, code smells are a great place to start
3) Identify technical debt
	- Code rot occurs when you assume a problem and write code to it but later find out that your assumptions were wrong
	- this code then begins to "rot" making it a technical debt
	- identify the code's technical debt beforehand could save a great deal of wasted effort
***
# SOLID Principles
SOLID is a set of five design principles that help developers write clean, maintainable and error free code

SOLID stands for
1. S -> Single Responsibility Principle: (SIP) A Class should have only one reason to change
2. O -> Open-Closed Principle (OCP): A class should be open for extension but closed for modification
3. L -> Liskov Substitution Principle (LSP): All sub-classes should be able to replace the parent class without throwing any errors.
4. I -> Interface Segregation Principle (ISP): Don't force a class to implement methods it doesn't need.
5. D -> Dependency Inversion Principle (DIP): All high-level and low level methods should be dependent on abstractions (interfaces), and not concrete classes

# 1) Single Responsibility Principle (SRP)
A class should have only one reason to change.

This class does
- User data handling
- saving to db
- sending mail
```java
class UserService{
	public void createUser(String name){}
	public void saveToDB(String name){}
	public void sendEmail(String name){}
}
```
if any one logic changes, the whole class changes.

So, SRP says
```java
class UserService{
	public void createUser(String name){}
}
class UserRepository{
	public void save(String name){}
}
class EmailService{
	public void send(String name){}
}
```
now each class has only one responsibility and only reason to change.
***
# 2) Open-Closed Principle (OCP)
Classes should be open for extension but closed for modification. It means that,
- You should be able to add new features without editing the code
- Add new functionality by extending, not rewriting 

Example,
```java
class AreaCalculator{
	public double calculate(Object shape){
		if(shape instanceof Circle){
			//circle area calc
		}
		if(shape instanceof Rectangle){
			//rectangle area calc
		}
		return 0;
	}
}

class Circle{
	double radius;
}
class Rectangle{
	double length, width;
}
```
If we need to add in `Triangle` class, we need to make changes to the `AreaCalculator` class as well. **This Breaks OCP rule**.

So, 
```java
interface Shape{
	double area();
}

class Circle implements Shape{
	double radius;
	
	Circle(double radius){
		this.radius = radius;
	}
	
	public double area(){
		// calc
	}
}

class Rectangle implements Shape{
	double height, width;
	
	Rectangle(double height, double width){
		this.length = length;
		this.width = width;
	}
	
	public double area(){
		//calc
	}
}

class AreaCalculator{
	public double calculate(Shape shape){
		return shape.area();
	}
}
```

so, we don't have to modify `AreaCalculator` class anymore
```java
public class Main{
	public static void main(String args[]){
		AreaCalculator calc = new AreaCaluclator();
		
		Shape c = new Circle(5);
		Shape r = new Rectangle(4,2);
		
		System.out.println(calc.calulate(c));
		System.out.println(cacl.calculate(r));
	}
}
```

if we want to add `Triangle` we can just,
```java
class Traingle implements Shape{
	double base, height;
	
	Triangle(double b, double h){
		this.base = b;
		this.height = h;
	}
	
	public double area(){
		// calc
	}
}
```
we don't have to edit `AreaCalculator` again.
Therefore, **OCP is acheived.**
***
# 3) Liskov Substitution Principle (LSP)
**A Child class must be able to replace its parent without causing any errors, otherwise it breaks the LSP rule**

Example
Parent class: Vehicle
```java
class Vehicle {
    public String start() {
        return "Engine started";
    }
}
```

Child Class 1: Car ==(Valid - follows LSP)==
```java
class Car extends Vehicle {
    public String start() {
        return "Car engine started";
    }
}
```
(its valid because the structure is the same)

Child class 2: Bicycle (invalid - breaks LSP)
```java
class Bicycle extends Vehicle {
    public String start() {
        throw new Exception();
    }
}
```
(This doesn't not return a value, instead it makes an error)

Now, if a function calls these classes
```python
public class TestLSP {
    public static void main(String[] args) {
        Vehicle v1 = new Car();
        System.out.println(v1.start()); //Works

        Vehicle v2 = new Bicycle();
        System.out.println(v2.start()); //Crashes! Breaks LSP
    }
}
```
So, the Bicycle class was not able to replace the parent class fully, Therefore LSP rule is violated.
***
# 5) Dependency Inversion Principle (DIP)
**High-level and low-level code should depend on abstractions (interfaces), not concrete classes. So, this makes the system more flexible and easy to change.**

Here the High level class depends on a low-level class and there's a direct hard-coded implementation which breaks the DIP rule
```java
// low level class
class EmailService(){
	public void send(string msg){
		System.out.println("Email: " + msg);
	}
}

// high level class
class Notification{
	public void notifyUser(String msg){
		EmailService email = new EmailService(); //Direct Implementation 
		email.send(msg);
	}
}
```
Problem: for a newer class `SMService` -> need to modify `Notification` class.

Solution:
```java
interface MessageService{
	void send(String msg);
}

class SMService implements MessageService{
	public void send(String msg){
		System.out.println("SMS: " + msg);
	}
}
class EmailService implements MessageService{
	public void send(String msg){
		System.out.println("Email: " + msg);
	}
}

class Notification{
	private MessageService service;
	
	public Notification(MessageService service){
		this.service = service;
	}
	public void notifyUser(String msg){
		service.send(msg);
	}
}
```

So these can then be used like,
```java
public class Main{
	public static void main(String[] args){
		Notification n1 = new Notification(new EmailService());
		n1.notifyUser("Hello");
		
		Notification n2 = new Notification(new SMService());
		n2.notifyUser("Hello");
	}
}
```
Now we don't have to edit the `Notification` class each time when we add in a new messaging service.




***
# MODULE 5
## Agile Application Life cycle Management (ALM)
- its a structured process of 
	- planning, 
	- developing, 
	- testing, 
	- deploying. 
	- maintaining and 
	- eventually retiring an application

- it provides a unified workflow for managing people, workflows and tools throughout the software's life-cycle
- Unlike other project management which only focuses on delivery, ALM covers the entire journey from initial concept to post-deployment maintenance
- Modern agile principles adds to this framework further with 
	- iterative planning
	- cross-functional collaboration
	- continuous integration
- the result is 
	- faster delivery, 
	- higher visibility, 
	- and a closer connection between customers and product outcomes
## Key areas of ALM
- Governance
	- managing requirements
	- overseeing resources
	- ensuring data security
	- regulating user access
- Application Development
	- coding
	- designing
	- testing
- Maintenance
	- bug fixes
	- updates
	- enhancements addressing user's needs
## Importance of application lifecycle management (ALM)
- Faster development and delivery
- Improves Colloboration
- Higher quality apps (because of early defect detection)
- reduces costs (optimizes from the beginning)
- increases agility 
- end to end visibility
## Top ALM tools
- Atlassian Jira
- IBM ALM solutions
- MS Azure DevOps
- CodeBeamer
***
# Agile in Distributed Teams
- A distributed agile team is a group of software development professionals who are working together from different geographical locations and time zones, united by agile methodology
- this setup allows companies to tap into the global resource pool 
## Challenges
- Lacks face-to-face interactions
- Uneven work distribution
- Cultural and time zone differences
## Tools used
- Project management tools like Jira, Teams, Trello
- Video conferencing like Zoom, GMeet, Skype
- Paired Coding 
## Implementation
- Daily Scrums and meetings
- Sprint planning and reviews
- Continuous Delivery and feedback
***
# Continuous Integration / Continuous Deployment (CI/CD)
- a CI/CD pipeline automates the process of software delivery
- it builds code, runs tests, safely deploys the new version
- reduces manual errors, provides feedback to developers and allows for faster product iterations
## Continuous Integration
- members of the team can integrate their work at least once a day
- every integration is checked by an automated build to search for errors
## Continuous delivery and Continuous deployment
- Continuous delivery is a software engineering method where team develops a software in short cycles. It ensures that the software can be released at any time
- Continuous deployment is a software engineering process where the product functionalities are delivered using automatic deployment
## Stages
1. Source
	- triggered by a code repository
2. Build
3. Test
4. Deploy
# Key component of CD:
- Deployment pipeline
- Environment management
- Release automation
- Monitoring and rollback