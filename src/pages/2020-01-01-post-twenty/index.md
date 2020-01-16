---
path: "/post-twenty"
date: "2020-01-01"
title: "Microservices"
author: "Tom Spencer"
---

Microservices represent a change of paradigm in computing. All the examples we have looked at so far involve monolithic algorithms. All the components work together to create the overarching application but they cannot be separated. In a monolithic application all the parts are intricately connected. Amazon or Facebook need to have solutions which include flexibility and this involves microservices. Microservices means breaking code into small pieces which are all independent. We are not using divide and conquer. We want the features to be separate. If we create web connection to a database we need the styles and the data to be separate. 

If you have a software which requires access to information and this information involves designs data or whatever we need all those requirements to be independent. 

We need to modify the logic in our software to make independence possible. We have to write our software as micro service deployable software. This requires coding and semantics. The good point about microservices is that each application is separate. We can write each service with different languages. We can potentiate the power of software in general. The second good point is that the information shared between microservices is shared in JSON format ie plain text. This can encode a lot of information. This is a way of transmitting heavy packs of information in a lightweight format. 

Microservices can also be exported to the cloud. This means that we can use other services or computers to execute the services we need. We can add logic and requests to databases. Also microservices are usually small meaning that if we have a problem we want to divide this into small enough pieces. This can save resources.

We want each application to run independently in the cloud. What is the cloud exactly? The cloud is a platform that allows you to execute your code in a network. It is not accessing information from a network but executing code in the network. 3 ways of using the cloud in our software.

1. Infrastructure as a Service
IaaS - This means that we execute the infrastructure of the code in the cloud but the rest of the software - data, logic is created by you.

2. SaaS - Software as a Service - Gives you all the software in the cloud and only gives you results you need to know about. 

3. Platform as a Service - PaaS - means you require the infrastructure with the database connections.  

Suppose you want to prepare dinner. There are several ways of doing this. If 1. infrastructure as service: 
Go to the supermarket - buy a preheated food and then put it in the microwave. 
2. Software as a service - getting a complete dish in a restaurant - do nothing and make requirement.
3. Go to a restaurant ask for food - take own dishes and wash them before - create own ways of deploying the code. 

#### Springboot

We will now talk about the concept of dependency injection as it relates to micro services. The idea is that whenever we want to create several services working together as in a microservices framework most of the time we need one particular service to gather information from other services. This is called wiring in general. For example, if we have several services gathering information from one service as if it were the server and the others were the client it is imperative that the service does not create an instance for every request because this would use too much memory. So suppose you have a server and 1 million clients getting to the server. If the server creates an object to control every client we will have 1 million instances of the class. This is a problem for memory and also the processor that is running the server. The solution for this problem is the concept of dependency injection. The external service has to provide the server with an object that it has to use. The clients are injecting the dependency the server has to use. Every client creates the object and the object is in the machine of the client and not the server. These objects could be used to control name, clock. Let's look at an example of Microservices with a small Springboot application:

```
package com.example.controller;

import com.example.entity.Programmer;
import com.example.service.ProgrammerService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.MediaType;
import org.springframework.web.bind.annotation.*;

import java.io.IOException;
import java.util.Collection;

@RestController
@RequestMapping("/programmers")
public class Controller {
    @Autowired
    private ProgrammerService service;

    @RequestMapping(value = "/{id}", method = RequestMethod.GET)
    public Programmer getProgrammerById(@PathVariable("id") int id){

        return this.service.getProgrammerById(id);
    }

    @RequestMapping(method = RequestMethod.GET)
    public Collection<Programmer> getProgrammers(){

        return this.service.getProgrammers();
    }

    @RequestMapping(method = RequestMethod.POST, consumes = MediaType.APPLICATION_JSON_VALUE)
    public void PutProgrammer(@RequestBody Programmer ProgrammerObject) throws IOException {
        this.service.PutProgrammer(ProgrammerObject);
    }

    @RequestMapping(value = "/{id}", method = RequestMethod.DELETE)
    public void deleteProgrammerById(@PathVariable("id") int id) throws IOException {
        this.service.deleteProgrammerById(id);
    }
}
```
We start with the controller. Into the controller we inherit the Programmer class and Programmer Service which constitute the business logic of the application. 

Spring Beans are objects managed by the Spring container. By using Java configuration this helps to achieve decoupling.

The controller also inherits 3 parts of the Spring framework for its running:
```
import org.springframework.beans.factory.annotation.Autowired;
...
@Autowired
private ProgrammerService service;
```
This allows us to skip configuration for using the ProgrammerService Bean class. 

```
import org.springframework.http.MediaType;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/programmers")
public class Controller {
...
    @RequestMapping(value = "/{id}", method = RequestMethod.GET)

```

Simply put, the @RequestMapping annotation is used to map web requests to Spring Controller methods. This gives us the controller functionality enabling us to call these methods in the url.

In this controller we have a GET and a DELETE action for in the controller and also a POST action:

```
    @RequestMapping(method = RequestMethod.POST, consumes = MediaType.APPLICATION_JSON_VALUE)
```
The POST action consumes MediaType.APPLICATION_JSON_VALUE meaning that you can send information to this request method in JSON format. This specification is essential because Java is statically typed.

As seen above the Controller class calls methods in: 
```
private ProgrammerService service;
```
The methods called on the ProgrammerService are the following:

```
...
return this.service.getProgrammers();
...
this.service.PutProgrammer(ProgrammerObject);
...
this.service.deleteProgrammerById(id);
```
We can now look at how the ProgrammerService class works:
```
package com.example.service;

import com.example.database.Database;
import com.example.entity.Programmer;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.io.IOException;
import java.util.Collection;

@Service
public class ProgrammerService {
    @Autowired
    private Database database;

    public Programmer getProgrammerById(int id){
        return this.database.getProgrammerById(id);
    }
    public void deleteProgrammerById(int id) throws IOException {
        this.database.deleteProgrammerById(id);
    }

    public Collection<Programmer> getProgrammers(){
        return this.database.getProgrammers();
    }
    public void PutProgrammer(Programmer ProgrammerObject) throws IOException {
        this.database.PutProgrammer(ProgrammerObject);
    }
}
```
This class imports Programmer from the entity folder in the project and also the Database class from the database folder. Here the ProgrammerService also uses:
```
import org.springframework.stereotype.Service;
...
@Service
```
Spring @Service annotation is a specialization of @Component annotation. Spring Service annotation can be applied only to classes. It is used to mark the class as a service provider. Spring @Service annotation is used with classes that provide some business functionalities. Spring context will autodetect these classes when annotation-based configuration and classpath scanning is used.

This class then calls three methods from Database to fetch, change and delete Programmer objects:
```
this.database.getProgrammerById(id);
...
this.database.deleteProgrammerById(id);
...
this.database.PutProgrammer(ProgrammerObject);
```
We then use a Database.java class to store information sent to the server:

```
package com.example.database;

import com.example.entity.Programmer;
import org.springframework.stereotype.Repository;

import java.io.IOException;
import java.util.Collection;
import java.util.HashMap;
import java.util.Map;

@Repository
public class Database {
//    private static final Map<Integer, Programmer> programmers = new HashMap<Integer, Programmer>();
//    static {
//        programmers.put(1, new Programmer("Tom", 1));
//        programmers.put(2, new Programmer("Alex", 2));
//        programmers.put(3, new Programmer("Joe", 3));
//        programmers.put(4, new Programmer("David", 4));
//        programmers.put(5, new Programmer("James", 5));
//    }
    private static Map<Integer, Programmer> programmers;

    static {
        TextDatabase.retrieveData();
        programmers = TextDatabase.getProgrammers();
    }

    public Programmer getProgrammerById(int id){
        return programmers.get(id);
    }

    public void PutProgrammer(Programmer ProgrammerObject) throws IOException {
//        programmers.put(ProgrammerObject.getId(), ProgrammerObject);
        TextDatabase.putData(ProgrammerObject);
        programmers = TextDatabase.getProgrammers();
    }

    public void deleteProgrammerById(int id) throws IOException {
//        return programmers.remove(id);
        TextDatabase.deleteDataById(id);
        programmers = TextDatabase.getProgrammers();
    }


    public Collection<Programmer> getProgrammers(){
        return programmers.values();
    }

}
```

This class imports the Programmer class for each of its objects and also imports the Repository class:
```
import com.example.entity.Programmer;
import org.springframework.stereotype.Repository;
```
@Repository is a Spring annotation that indicates that the decorated class is a repository. A repository is a mechanism for encapsulating storage, retrieval, and search behavior which emulates a collection of objects. It is a specialization of the @Component annotation allowing for implementation classes to be autodetected through classpath scanning.

We can see the palimpsest of two different implementations for our 'database'. The first was a simple HashMap to store a preliminary list of Programmer instances which we then changed with Hash methods such as put, remove and get. The second iteration of this model involves the use of TextDatabase. This class:
```
package com.example.database;

import com.example.entity.Programmer;

import java.io.*;
import java.nio.file.Paths;
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

public class TextDatabase {
    private static Map<Integer, Programmer> programmers = new HashMap<Integer, Programmer>();

    public static FileInputStream textData;
    static File file;
    static {
        try {
            file = new File("src/main/java/com/example/database/database.txt");
            textData = new FileInputStream(file.getPath());
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
    }

    public static void putData(Programmer ProgrammerObject) throws IOException {
        programmers.put(ProgrammerObject.getId(), ProgrammerObject);
        storeData();
    }

    public static void deleteDataById(int id) throws IOException {
        programmers.remove(id);
        storeData();
    }

    public static void retrieveData(){
        Scanner scanner = new Scanner(textData);
        String [] splitLine;

        while(scanner.hasNextLine()){
            splitLine = scanner.nextLine().split("\\s+");
            programmers.put(Integer.parseInt(splitLine[0]),
                            new Programmer(splitLine[2],
                            Integer.parseInt(splitLine[1])));
        }
        scanner.close();

    }

    public static void storeData() throws IOException {
        try (FileWriter fr = new FileWriter(file, false)) {
            BufferedWriter br = new BufferedWriter(fr);
            PrintWriter pr = new PrintWriter(br);
            for(Map.Entry<Integer, Programmer> entry: programmers.entrySet()){
                pr.println(entry.getValue().getId() + " " + entry.getValue().getId() + " " + entry.getValue().getName());
            }
            pr.close();
            br.close();
        }

    }

    public static Map<Integer, Programmer> getProgrammers(){
        return programmers;
    }
}
```
This class uses imports the Scanner class to read and write data to a txt file (acting as a kind of database). Scanner is a class in java.util package used for obtaining the input of the primitive types like int, double, etc. and strings. It is the easiest way to read input in a Java program. Methods in this file use IOExceptions to protect against information not being available in the file. We can then access the data on port 8080 when we run the files and go to localhost:8080/programmers:

![run-port:8080](https://user-images.githubusercontent.com/27693622/72207911-eb8e5800-3494-11ea-95db-9045c86896a9.png)

The above, of course, is a GET request. We can also use postman to make post requests and update requests. First post:

![post](https://user-images.githubusercontent.com/27693622/72208091-cb5f9880-3496-11ea-82cd-d8fecfb5a4e5.png)

This adds an entry to the txt file in /src/main/java/com/example/database/database.txt:

![txt](https://user-images.githubusercontent.com/27693622/72208113-0661cc00-3497-11ea-9d93-3e25ca82360c.png)

We can also make a delete request:

![Screenshot 2020-01-11 at 17 25 02](https://user-images.githubusercontent.com/27693622/72208141-53de3900-3497-11ea-8198-4be1e8df3bce.png)

This deletes Tim from the text file:

![Screenshot 2020-01-11 at 17 25 53](https://user-images.githubusercontent.com/27693622/72208152-74a68e80-3497-11ea-8e51-6fb488e922e5.png)
