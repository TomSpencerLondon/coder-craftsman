---
path: "/post-eighteen"
date: "2019-12-31"
title: "Java Network Programming"
author: "Tom Spencer"
---

Networking means to connect several systems via a network. Most examples refer to connecting computers. In general you can connect anything. We will focus here on computers. In order to make this connection possible we need to focus on some design patterns or architectures. Here we need to focus **tcp/ip** connections. 

When we have a computer in general and want to design a network application the most common idea is to focus on a four layer concept.

The first layer is the application layer. It gets the information from the user. For example if you are using a chat. It gets your message or use the graphics interface to get some information from you. Just to be clear these layers show how networks work.

The second layer is the transport layer or TCP layer. It takes the information you already have and transforms it to packages to send. This uses Transformation, Control Protocol which is similar to HTTP only that we are not connecting to the internet.

After this we have the internet layer. This is not connecting to google. This the remote connection to connect computers separated by space. This layer takes the packages produced by the transport layer and makes them into packages that are ready to be transported to the other computer.

Finally we have the host to network layer. This is the layer that transforms the layer in the internet layer to information that is encoded. This has more to do with hardware than software. It has to do with optic lines, cable infra red etc.

Suppose two people are chatting. The person sends a chat message which is prepared for transportation. The host to network layer connects between the two servers and after this the other computer receives the message through the internet layer and then transports it.

The most important point about layers is that every layer can only communicate with the previous and next layer in the same exact order. We have to focus on these connections when we work on our projects. 

Lets look at the application layer and understand how a message is sent from the application layer. Before we send a message we need to create a connection to the computer we want to connect with. This connection is formed through an abstract concept called the socket and uses a model called the Client Server model. 

Let’s start with the client server model. In theory when connecting two computers one computer takes the role of client ie it asks for information. The other one is the server and waits for the client to ask for information and sends the information if it finds it. This is the basic setting for a client server relationship. You never usually have this simple role relationship as the roles can change depending on the problem. Sometimes one computer can be at the same time a client and a server. This is what we do when we create the first versions of our websites. In these versions the computer is playing the role of both client and server because in the first version we test our connections as a server and use our own computer as a server.

Lets look a bit further into how the connection works. Every computer has a direction. This direction is most of the time the IP direction: 198.12.1.2 is just a simplified version. The IP direction is much more complicated and describes every possible computer.

95.144.100.150 means your computer if it is IPv4 it says your location. This number is an identifier to a whole package of information regarding my IP direction. 
IPv6 is more secure it doesn’t give information for location. 

Once I identify the computer I want to connect to I have to choose a port to connect to. We can think of this in the following way two computers, two IP addresses, once I have identified the two ports we create a path between the two ports. If from A to B it is called an output stream for A and input stream for B. If we want to connect two computers we want to make two connections. One connection is one way. Two way path needs two ports and two connections. 

ssh connection is asynchronous version of this process it is connecting two computers with single screen. The difference with two connections. This connection is more organised.

Finally, the abstraction of this concept of port is the concept of a socket in Java. And the abstraction of input and output connections is the concept of InputStream and OutputStream classes in Java.
We must keep in mind that servers and clients have independent algorithms, files and scripts. One script is for the client eg. Client socket. 

For the server we create another script which is different from the client. A few notes about programming with networks in Java is that most of the cases we want to work with error control. Why do we need to do this? Network connections are volatile. It is easy to lose the connection. If we try to make connections without error control this can lead to break down of the project. In Java in an IDE if you create any object from the JavaNet package without a try catch statement or exception handling then Java won’t let you even execute the program. There will be a syntax error. 

We can now summarise some of the chapters in **Java Network Programming** by Eliotte Rusty Harold

**Chapter 1**: is the basic concept of connections.
Here we get some introduction to layers and ports and how the client server model works.

**Chapter 2**: is about **streams**. This is nothing to do with the streams data structures in Java. These are streams to connect computers to other computers. How to filter them and make them more secure.

**Chapter 8 + 9** are about sockets for the client and servers.

We are going to create an example involving both threads and networking. This example consists of a server that will accept requests from server.client. It will communicate between them in a three way format. 

Here I have made a socket connection in Ruby:

```
 require 'socket'
def welcome(chatter)
  chatter.print "Welcome! Please enter your name: "
  chatter.readline.chomp
end

def broadcast(message, chatters)
  chatters.each do |chatter|
    chatter.puts message
  end
end

s = TCPServer.new(3939)
   chatters = []
while (chatter = s.accept)
  Thread.new(chatter) do |c|
    name = welcome(chatter)
broadcast("#{name} has joined", chatters)
chatters << chatter
    begin
      loop do
        line = c.readline
        broadcast("#{name}: #{line}", chatters)
      end
    rescue EOFError
      c.close
      chatters.delete(c)
      broadcast("#{name} has left", chatters)
    end
  end
end
```

The first point to note is that whenever we create a single server connection. This connection cannot be shared with other clients. If we want several clients to connect to our server we need to make the connections in separate threads. This is only for TCP (transmission control protocol) connections. Every TCP connection has to be through threads.

We have another model called the UDP (universal datagram protocol). Datagrams are similar to packages of information. TCP makes writing reading directly whereas UDP presents packages of information. UDP is much faster than TCP because UDP does not need to create a connection. It just sends the data. The concept of being connected does not exist here because there is no continuous transmission. In UDP is discrete connections. Also with UDP there is no way of knowing that the request is transmitted unless you ask the server. We will focus on TCP because we never lose the connection. We have no control with UDP. UDP is useful for servers that return single packets of data such as the time or similar just sends the file and then that’s it.