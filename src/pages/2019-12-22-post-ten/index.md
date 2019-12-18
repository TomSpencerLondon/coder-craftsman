---
path: "/post-ten"
date: "2019-12-22"
title: "SOLID design principles"
author: "Tom Spencer"
---

The **SOLID** design principles were originally conceived to address three main tendencies of legacy software. These were **rigidity**, **fragility** and **immobility**. **Rigidity** means that any change to your code base can affect many other parts. **Fragility** is when things can break in unrelated places and **immobility** is the problem that we cannot reuse code outside of its original context. 

### S  = Single Responsibility

Instead we want applications that are cohesive. This means that we would expect to see a well organised folder/file structure and Object Hierarchy structure. Each class / piece of functionality should be name so that its functionality is very obvious and should only contain logic to perform that task. If you saw huge manager classes with lots of code that would be a sign that responsibility isn’t being followed. 

### O = Open/ closed Principle

This means that new functionality should be added through new classes that have a minimum of impact on / require modification of existing functionality.

Here we would expect to see lots of use of object inheritance, sub-typing, interfaces and abstract classes to separate out the design of functionality from the implementation. This would allow others to implement other versions without affecting the original. 


### L = Liskov substitution principle

We are thinking about the ability to treat sub-types as their parent type. In Ruby we see this with proper object hierarchy. For this quality we would expect to see code treating common objects are their base type and calling methods on the base/ abstract classes rather than instantiating and working on the sub-types themselves.

![Liskov](https://madewithlove.be/wp-content/uploads/2019/04/liskovlsp.jpg)

Barbara Liskov was the computer pioneer after whom the Liskov substitution principle is named. One of the many notable achievements Liskov developed was the first high-level language to support implementation of distributed programs and to demonstrate the technique of promise pipelining. In 2008 Turing Award for her work in the design of programming languages and software methodology that led to the development of object-oriented programming.

![Barbara Liskov](https://d2r55xnwy6nx47.cloudfront.net/uploads/2019/11/Liskov_2880x1800_Lede_v03.jpg)


### I = Interface Segregation Principle

Interface segregation is similar in many ways to Single Responsibility Principle. You define smaller subsets of functionality as interfaces and work with those to keep you system decoupled. For example a FileManager might have the responsibility of dealing with File input and output. The responsibilities of IFileReader and IFileWriter would be clearly separated from the FileManager and their method definitions would be focused respectively on Reading and Writing files.

### D = Dependency Inversion Principle

Instead of a high-level module depending on a low-level module both should depend on an abstraction. This image might clarify this idea further:

![dependency inversion](https://springframework.guru/wp-content/uploads/2015/06/DIP_Img01.png)

Without Dependency Inversion Principle. The code for Object A in Package A refers directly Object B in Package B. With Dependency Inversion Principle Interface A is introduced as an abstraction in Package A. This means that Object A now refers to Interface A and Object B inherits form Interace A. We can now summarise the benefits of this new set up:
1. Both Object A and Object B now depend on Interface A, the abstraction.
2. This has now inverted the dependency that existed from Object A to Object B. Now Object B is dependent on the abstraction from Interface A.

### My own experience with SOLID and its anti patterns

To some extent rigidity has presented itself in my work code base when we have used themes for several agents on our front end application which then require lots of logic to stop them affecting each other’s site presentation. We have resolved this to some extent with changes to our newer version of the CMS system. We have added theme config settings that users can use to change the configurations for their sites.

## Revisiting the principles

### Single Responsibility Principle

The Single Responsibility Principle means that a class should have only one reason to change. The reason to change relates to the responsibility of the class. Each responsibility is an axis for change. The principle is similar to designing classes which are highly cohesive.

We can relate the “reason to change” to “the responsibility of the class”. So each responsibility would be an axis for change. This principle is similar to designing classes which are highly cohesive. So the idea is to design a class which has one responsibility or in other words caters to implementing a functionality. Of course one responsibility does not mean that the class has only **ONE** method. A responsibility can be implemented by means of different methods in the class.

Let's now look at an example of code that violates this principle:

```
class User
{
    void CreatePost(Database db, string postMessage)
    {
        try
        {
            db.Add(postMessage);
        }
        catch (Exception ex)
        {
            db.LogError("An error occured: ", ex.ToString());
            File.WriteAllText("\LocalErrors.txt", ex.ToString());
        }
    }
}
```
Here the CreatePost method is responsible for adding the post to the database, logging an error in the database and also logging the error in a local file. This code clearly violates the **single responsibility principle**.

Here we have an improved version of the code:

```
class Post
{
    private ErrorLogger errorLogger = new ErrorLogger();

    void CreatePost(Database db, string postMessage)
    {
        try
        {
            db.Add(postMessage);
        }
        catch (Exception ex)
        {
            errorLogger.log(ex.ToString())
        }
    }
}

class ErrorLogger
{
    void log(string error)
    {
      db.LogError("An error occured: ", error);
      File.WriteAllText("\LocalErrors.txt", error);
    }
}
```

Here we have added a separate logger class to handle error logging. This abstracts the double resonsibilities that were in the User class in our earlier code. Now we have two abstracted classes from the User class. The Post class and the ErrorLogger class.

### Open/ closed principle

The open/closed principle states that software entities (classes, modules and functions for example) should be open for extension but closed for modification.
That means that ideally we would be able to extend the behavoiur of classes without modifying their source code.

In object-oriented programming, the term **polymorphism** refers to objects' ability to change their behaviour depending on the data types which are fed to them. More specifically, it is the ability to redefine methods for derived classes. So if we had a base class shape we would be able to define different area methods for any number of derived classes such as circles, rectangles and triangles. No matter what the shape was the area method would return the correct result.

Lets look at the violation of the Open/Closed principle in order to get a clearer idea of the principle itself and the advantages of **polymorphism**:

```
class Post
{
    void CreatePost(Database db, string postMessage)
    {
        if (postMessage.StartsWith("#"))
        {
            db.AddAsTag(postMessage);
        }
        else
        {
            db.Add(postMessage);
        }
    }
}
```
Here the method CreatePost inside the class Post is written to do something different whenever the post starts with the character '#'. This violates the open/closed principle because we are setting ourselves on a path of adding to this if statement. For instance, if we wanted to handle mentions starting with @ we would then have to create an extra 'else if' and so on...

We can use inheritance in order to make our code more compliant to the open/closed principle:

```
class Post
{
    void CreatePost(Database db, string postMessage)
    {
        db.Add(postMessage);
    }
}

class TagPost : Post
{
    override void CreatePost(Database db, string postMessage)
    {
        db.AddAsTag(postMessage);
    }
}
```

Here, by using inheritance we are able to extend the behaviour to the CreatePost() method in Post by using the TagPost class and its version of CreatePost that overrides the original method in Post. We could then use a yaml file or similar to instantiate each of the tag logic after also abstracting the tags into separate classes. In any case the evaluation of the '#' or '@' logic will be handled elsewhere and we will be able to change the code there without affecting the underlying behaviour of Post class.

### Liskov Substitution Principle

The main point here, as discussed above, is that objects in a program should be replaceable with instances of their subtypes without altering the correctness of the program.

Lets see some code breaks this principle:

```
class Post
{
    void CreatePost(Database db, string postMessage)
    {
        db.Add(postMessage);
    }
}

class TagPost : Post
{
    override void CreatePost(Database db, string postMessage)
    {
        db.AddAsTag(postMessage);
    }
}

class MentionPost : Post
{
    void CreateMentionPost(Database db, string postMessage)
    {
        string user = postMessage.parseUser();

        db.NotifyUser(user);
        db.OverrideExistingMention(user, postMessage);
        base.CreatePost(db, postMessage);
    }
}

class PostHandler
{
    private database = new Database();

    void HandleNewPosts() {
        List<string> newPosts = database.getUnhandledPostsMessages();

        foreach (string postMessage in newPosts)
        {
            Post post;

            if (postMessage.StartsWith("#"))
            {
                post = new TagPost();
            }
            else if (postMessage.StartsWith("@"))
            {
                post = new MentionPost();
            }
            else {
                post = new Post();
            }

            post.CreatePost(database, postMessage);
        }
    }
}
```

Here, whereas the TagPost does override the CreatePost method in Post, MentionPost does not. The CreateMentionPost uses the CreatePost method from Post. In fact the CreateMentionPost is not used and the CreatePost method call in the forEach loop of the HandleNewPosts() method in PostHandler will just bubble up to Post. Let's now see a corrected version of MentionPost:

```
class MentionPost : Post
{
    override void CreatePost(Database db, string postMessage)
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

    private void OverrideExistingMention(string user, string postMessage)
    {
        db.OverrideExistingMention(_user, postMessage);
    }
}
```
Here we override the CreatePost() method and call the private NotifyUser OverrideExistingMention methods in the CreatePost method.

### Interface segregation principle

This principle means that no client should be forced to depend on methods it does not use. The headline here is that you should not add additional functionality to an existing interface by adding new methods.

Instead we should create a new interface and let our subclasses implement multiple interfaces if necessary. Here is a violation o fthe interface segregation principle:

```
interface IPost
{
    void CreatePost();
}

interface IPostNew
{
    void CreatePost();
    void ReadPost();
}
```
Say we see the IPostNew interface and are asked to implement ReadPost for IPost. The naive approach would be to add ReadPost() so that is like the IPostNew Interface. A better solution would be the following:
```
interface IPostCreate
{
    void CreatePost();
}

interface IPostRead
{
    void ReadPost();
}
```
If our subclasses need both the CreatePost() and the ReadPost() methods then they can implement both interfaces.

### Dependency inversion principle

The dependency inversion principle enables us to decouple software modules. The principle is that:
* High level modules should not depend on low-level modules. Both should depend on abstractions.

* Abstractions should not depend on details. Details should depend on abstractions.

We can use dependency injection in order to comply with this principle. Dependency injection simply means injecting the dependencies of a class through the class' constructor as an input parameter. An example of violation of the principle is useful here:

```
class Post
{
    private ErrorLogger errorLogger = new ErrorLogger();

    void CreatePost(Database db, string postMessage)
    {
        try
        {
            db.Add(postMessage);
        }
        catch (Exception ex)
        {
            errorLogger.log(ex.ToString())
        }
    }
}
```
Here create the ErrorLogger class in the Post class. This violates the dependency inversion principle. If we wanted to use a different kind of logger we would have to modify the Post class directly.

We can use dependency inversion in order to correct this:

```
class Post
{
    private Logger _logger;

    public Post(Logger injectedLogger)
    {
        _logger = injectedLogger;
    }

    void CreatePost(Database db, string postMessage)
    {
        try
        {
            db.Add(postMessage);
        }
        catch (Exception ex)
        {
            logger.log(ex.ToString())
        }
    }
}
```

Here we inject the Logger that we want to use when we instantiate the Post class. This frees us to define logger needed at run-time.

The aim of these principles is to improve our codebase so that we can achieve code that is **reusable**, **scalable** and easily **testable**.