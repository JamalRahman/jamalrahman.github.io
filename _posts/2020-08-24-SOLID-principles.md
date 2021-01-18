---
layout: article
title: The SOLID Principles
show_edit_on_github: false
tags: OOP interview-prep

---

The SOLID principles are the five textbook principles that any programmer worth their salt should adhere to. The principles were first proposed by Robert C. Martin in his eminent handbook, Clean Code (2008).

Although written for OOP, the principles also apply towards functions & other smaller segments of code.

----------

**S**ingle Responsibility Principle

- Code does one job

**O**pen-Closed Principle (Open to extension, Closed to mod)

- Extend code, don’t change code

**L**iskov Substitution

- Interchangeable subclasses

**I**nterface Segregation Principle

- Split up interfaces into atomic parts

**D**ependency Inversion

- Don’t hard-link modules, abstract & inject dependencies at runtime

---

## **S**ingle Responsibility principle

**A class/function should have one reason to change, because the class/function should only have one job.**
 
 
 
 
Here is one example, we create a Book class which manages properties of a Book.

```java
    public class Book {
    
      private String name;
      private String author;
      private String text;
      
      //constructor, getters and setters ommitted for brevity
      
      // methods that directly relate to the book properties
      public String replaceWordInText(String word){
          return text.replaceAll(word, text);
      }
      
      public boolean isWordInText(String word){
          return text.contains(word);
      }
    }
```
Now suppose we want a method to print the Book to the console. Naively, we add the method to Book:

```java
    public class Book {
        //...
     
        void printTextToConsole(){
            // our code for formatting and printing the text
        }
    }
```

This addition we've just made violates the SRP. We now have the Book class handling the Book logic and handling output logic. What if we next wanted a method to stream the data through a non-disk method, such as writing to console or to some other stream? We would have to edit ‘Book’ to add more non-Book logic.

To solve this, we can create a second class whose sole purpose is to output to various forms:

```java
    public class BookPrinter {
     
      // methods for outputting text
      void printTextToConsole(String text){
          //our code for formatting and printing the text
      }
    
      void printTextToAnotherMedium(String text){
          // code for writing to any other location..
      }
    }
```


----------
## **O**pen - Closed Principle

“Open for extension. Closed for Modification.”

**The OC principle puts that code should be written in a way that you don’t go back and change old code, but if you wanted to make an addition the structure allows you to extend prior functionality.**

******This basically means, use implementation and extension properly.**




Here we have a lovely Twitter Post class, complete with any property we would ever want a Post to have.

```java
    public class Post{
    
      void CreatePost(Database db, String postMessage){
        if (postMessage.StartsWith("#")){
          db.AddAsTag(postMessage);
        }
        else{
          db.Add(postMessage);
        }
      }
    }
```
If, in the future, we realise we want to add another property to the Post and handle it differently (e.g. store an @ post accordingly), we would have to edit the Post class.

So let’s rewrite what we have to make it more Open-Closed: 

```java
    public class Post{
      public void CreatePost(Database db, String postMessage){
        db.Add(postMessage);
      }
    }
    
    public class TagPost extends Post{
      public void CreatePost(Database db, String postMessage){
        db.AddAsTag(postMessage);
      }
    }
```
Now the code is open to extension but closed to modification. Extending Post logic by handling # posts or @ posts needs only addressing the specific code


----------


## **L**iskov Substitution

Let q(x) be a property provable about objects of x of type T. Then q(y) should be provable for objects y of type S where S is a subtype of T.

**What this means is that a subclass should be substitutable for their parent class, and code will not break.**

This can be a tricky one. We’ll supply a trivial example, but it may involved redefining your concepts of the superclass / interface.

Suppose we add a MentionPost (@) class, and want to write logic for mentioning another user when someone creates a MentionPost. Naively we write CreateMentionPost().

```java
    class MentionPost extends Post
    {
        void CreateMentionPost(Database db, string postMessage)
        {
            String user = postMessage.parseUser();
    
            db.NotifyUser(user);
            super.CreatePost(db, postMessage);
        }
    }
```

This is an obvious violation of Liskov substitution because we didn’t actually overwrite CreatePost(). We wrote our own new CreateMentionPost(). Any code that wanted to call Post.CreatePost() would break for mention posts.

We should instead design MentionPost to be replaceable with TagPost or Post:

```java
    class MentionPost : Post{
      public void CreatePost(Database db, string postMessage)
      {
        string user = postMessage.parseUser();
    
        NotifyUser(user);
        OverrideExistingMention(user, postMessage)
        base.CreatePost(db, postMessage);
      }
    
      private void NotifyUser(string user)
      {
        db.NotifyUser(user);
      }
    }
```

----------


## Interface Segregation

**Larger interfaces should be split into smaller ones. Implementing classes only need to implement relevant methods.**

This one is quite trivial. Suppose we define a job role of a Data Scientist:


```java
    public interface DataScientist{
      void manageDatabase();
      void buildSQLPipelines();
      void runStatisticalTests();
      void buildVisualisations();
      void buildSoftware();
      void buildMachineLearningModel();
    }
```
The DataScientist interface just has too many job roles to be a useful thing to implement. There is too much baggage here.

Let’s split these up into smaller interfaces:

```java
    public interface DataEngineer{
      void manageDatabase();
      void buildSQLPipelines();
    }
    
    public interface Analyst{
      void runStatisticalTests();
      void buildVisualisations();
    }
    
    public interface Engineer{
      void buildSoftware();
    }
    
    public interface ML{
      void buildMachineLearningModel();
    }
```
Thanks to interface segregation, we can build a Machine Learning Engineer class that specialises:

```java
    public class MLE implements ML, Engineer{
      public void buildSoftware(){
      }
      public void buildMachineLearningModel(){
      }
    }
```

----------


## **D**ependency Inversion Principle

This principle decouples software modules. High level modules should not depend on low level modules. Both should depend on abstractions.

We use dependency injection to solve this principle. The most common form of dependency injection is injecting dependencies through an object’s constructor.

First, an incorrect example:

```java
    public class Post{
      private ErrorLogger errorLogger = new ErrorLogger();
      // ...
    }
```
The Post object is strongly coupled with the ErrorLogger object. This violates the principle.

```java
    public class Post{
      private Logger logger;
      
      public post(Logger logger){
        this.logger = logger;
      }
    }
```

Not only have we allowed a logger to be injected, but we have abstracted the **type** of logger, so *any* logger can be used. 

