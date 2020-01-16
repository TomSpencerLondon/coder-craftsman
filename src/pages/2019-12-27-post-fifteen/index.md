---
path: "/post-fifteen"
date: "2019-12-27"
title: "The Well Grounded Rubyist by David A Black"
author: "Tom Spencer"
---

#### About the book

The Well-Grounded Rubyist, Second Edition consists of 15 chapters and is divided into 3 parts:
* Part 1: Ruby foundations
* Part 2: Built-in classes and modules
* Part 3: Ruby dynamics

Part 1 (chapters 1 through 6) introduces you to the syntax of Ruby and to a number of the key concepts and semantics on which Ruby programming builds: objects, methods, classes and modules, identifiers, and more.

Part 2 (chapters 7 through 12) surveys the major built-in classes—including strings, arrays, hashes, numerics, ranges, dates and times, and regular expressions— and provides you with insight into what the various built-ins are for, as well as the nuts and bolts of how to use them.

Part 3 (chapters 13 through 15) addresses the area of Ruby dynamics. Under this heading you’ll find a number of subtopics—among them some metaprogramming techniques—including Ruby’s facilities for runtime reflection and object introspection; ways to endow objects with individualized behaviors; and the handling of functions, threads, and other runnable and executable objects. 

#### Chapter 1 Bootstrapping your Ruby literacy

Ruby can tell you where its installation files are located. To get the information while in an irb session, you need to preload a Ruby library package called rbconfig into your irb session. rbconfig is an interface to a lot of compiled-in configuration infor- mation about your Ruby installation, and you can get irb to load it by using irb’s -r command-line flag and the name of the package:
```
$ irb --simple-prompt -rrbconfig
```
Now you can request information. For example, you can find out where the Ruby exe- cutable files (including ruby and irb) have been installed:
```
RbConfig::CONFIG["bindir"]
```

This command tells you where the Ruby versions are kept:
```
ruby -e 'puts $:'
```

When you install Ruby, you get a handful of important command-line tools, which are installed in whatever directory is configured as bindir—usually /usr/local/bin, /usr/bin, or the /opt equivalents. (You can require "rbconfig" and examine RbConfig::CONFIG["bindir"] to check.) These tools are
* ruby—The interpreter
* irb—The interactive Ruby interpreter
* rdoc and ri—Ruby documentation tools
* rake—Ruby make, a task-management utility
* gem—A Ruby library and application package-management utility
* erb—A templating system
* testrb—A high-level tool for use with the Ruby test framework

#### Chapter 2 Objects, methods, and local variables

We define an object in the following manner:
```
obj = Object.new
```
Here’s how to define the method talk for the object obj:
```
def obj.talk
  puts "I am an object."
  puts "(Do you object?)"
end
```


#### Chapter 3

Here is how we define a class:
```
class Ticket
  def initialize(venue, date)
    @venue = venue
    @date = date
  end

  def set_price=(amount)
    @price = amount
  end

  def price
    @price
  end
end
```
this returns:
```
ticket = Ticket.new("Town Hall", "11/12/13")
ticket.set_price = 63.00
puts "The ticket costs $#{"%.2f" % ticket.price}."
ticket.set_price = 72.50
puts "Whoops -- it just went up. It now costs $#{"%.2f" % ticket.price}."
```
We can also  use constants in classes:
```
class Ticket
  attr_reader :venue
  VENUES = ["Convention Center", "Fairgrounds", "Town Hall"]
  def initialize(venue, date)
    if VENUES.include?(venue)
      @venue = venue
    else
      raise ArgumentError, "Unknown venue #{venue}"
    end  
    @date = date
  end
  def price=(amount)
    if (amount * 100).to_i == amount * 100
      @price = amount
    else
      puts "The price seems to be malformed"
    end
  end

  def price
    @price
  end
end
```

#### Chapter 4

We can use modules in order to mix behaviours into classes:
```
module MyFirstModule
   def say_hello
    puts "Hello"
   end
end
```
This allows us to use the module within a class:
```
class ModuleTester
  include
  MyFirstModule
end
mt = ModuleTester.new
mt.say_hello

```
Every class that doesn’t have an explicit super-
class is a subclass of Object. You can see evidence of this default in irb:
```
>> class C
>> end
=> nil
>> C.superclass
=> Object
```

We can also use prepend as well as include on modules.
Every time you include a module in a class, you’re affecting what happens when instances of that class have to resolve messages into method names. The same is true of prepend. The difference is that if you prepend a module to a class, the object looks in that module first, before it looks in the class.

#### Chapter 5 The default object (self), scope, and visibility
Chapter 5 focuses on
self and scope. self is the current or default object. scope governs the visibility of variables. It is important to know
what scope you're in so you can tell what the variables refer to and not confuse them with variables from different scopes that have the same name. The third point of chapter is method access.

We can see what self is by using puts:

```
class C
  puts "Just started class C:"
  puts self
  module M
    puts "Nested module C::M:"
    puts self
  end
  puts "Back in the outer level of C:"
  puts self
end
```
As soon as you cross a class or module keyword boundary, the class or module whose definition block you’ve entered—the Class or Module object—becomes self. List- ing 5.1 shows two cases: entering C, and then entering C::M. When you leave C::M but are still in C, self is once again C.

#### Scope

**Global scope** is scope that covers the entire program. Global scope is enjoyed by global variables, which are recognizable by their initial dollar-sign ($) character. They’re available everywhere.

We can define global variables with $:
```
$gvar = "I'm a global!"
class C
  def examine_global
    puts $gvar
end end
c = C.new
c.examine_global
```
**Local scope** is a basic layer of the fabric of every Ruby program. At any given moment, your program is in a particular local scope.

#### Chapter 6 Control Flow technique

THE UNLESS KEYWORD
The unless keyword provides a more natural-sounding way to express the same semantics as if not or if !:
```
unless x == 1
```
But take “natural-sounding” with a grain of salt. Ruby programs are written in Ruby, not English, and you should aim for good Ruby style without worrying unduly about how your code reads as English prose. Not that English can’t occasionally guide you; for instance, the unless/else sequence, which does a flip back from a negative to a positive not normally associated with the use of the word unless, can be a bit hard to follow:
```
unless x > 100
  puts "Small number!"
else
  puts "Big number!"
end
```

We can also use rescue statements for error handling:
```
begin
  fussy_method(20)
rescue ArgumentError => e
  puts "That was not an acceptable number!"
  puts "Here's the backtrace for this exception:"
  puts e.backtrace
  puts "And here's the exception object's message:"
  puts e.message
end
```
Chapter 7 Built-in essentials 

#### Array role-playing with to_ary

Objects can masquerade as arrays if they have a to_ary method. If such a method is present, it’s called on the object in cases where an array, and only an array, will do— for example, in an array-concatenation operation.
Here’s another Person implementation, where the array role is played by an array containing three person attributes:
```
class Person
  attr_accessor :name, :age, :email
  def to_ary
    [name, age, email]
  end
end
```
This allows us to concat an instance of the Person class to an array:
```
david = Person.new
david.name = "David"
david.age = 55
david.email = "david@wherever"
array = []
array.concat(david)
p array
```
#### Comparison module
For classes that do need full comparison functionality, Ruby provides a convenient way to get it. If you want objects of class MyClass to have the full suite of comparison methods, all you have to do is the following:
1 Mix a module called Comparable (which comes with Ruby) into MyClass.
2 Define a comparison method with the name <=> as an instance method in
MyClass.
```
class Bid
  include Comparable
  attr_accessor :estimate
  def <=>(other_bid)
    if self.estimate < other_bid.estimate
      -1
    elsif self.estimate > other_bid.estimate
      1
    else
      0
    end
  end
end
```
We can then compare instances of bid:
```
>> bid1 = Bid.new
=> #<Bid:0x000001011d5d60>
>> bid2 = Bid.new
=> #<Bid:0x000001011d4320>
>> bid1.estimate = 100
=> 100
>> bid2.estimate = 105
=> 105
>> bid1 < bid2
=> true
```
#### Chapter 8 Strings, symbols, and other scalar objects

#### String comparison and ordering

The String class mixes in the Comparable module and defines a <=> method. Strings are therefore good to go when it comes to comparisons based on character code (ASCII or otherwise) order:
```
>> "a" <=> "b"
=> -1
>> "b" > "a"
=> true
>> "a" > "A"
=> true
>> "." > ","
=> true
```

#### Chapter 9 Collection and container objects

Arrays and hashes are closely connected. An array is, in a sense, a hash, where the keys happen to be consecutive integers. Hashes are, in a sense, arrays, where the indexes are allowed to be anything, not just integers. If you do use consecutive integers as hash keys, arrays and hashes start behaving similarly when you do lookups:
```
array = ["ruby", "diamond", "emerald"]
hash = { 0 => "ruby", 1 => "diamond", 2 => "emerald" }
puts array[0]    # ruby
puts hash[0]     # ruby
```
#### Sets

To create a **set**, you use the **Set.new** constructor. You can create an empty set, or you can pass in a collection object (defined as an object that responds to each or each_entry). In the latter case, all the elements of the collection are placed individu- ally in the set.  For example, here’s a way to initialize a set to a list of uppercased strings:
```
>> names = ["David", "Yukihiro", "Chad", "Amy"]
=> ["David", "Yukihiro", "Chad", "Amy"]
>> name_set = Set.new(names) {|name| name.upcase }
=> #<Set: {"AMY", "YUKIHIRO", "CHAD", "DAVID"}>
```
To add a single object to a set, you can use the << operator/method:
```
 >> tri_state = Set.new(["New Jersey", "New York"])
=> #<Set: {"New Jersey", "New York"}>
>> tri_state << "Connecticut"
=> #<Set: {"New Jersey", "New York", "Connecticut"}>
```
The << method is also available as add. There’s also a method called add?, which differs from add in that it returns nil (rather than returning the set itself) if the set is unchanged after the operation:
```
>> tri_state.add?("Pennsylvania")
=> nil
```

#### Chapter 10 Collections central: Enumerable and Enumerator
You can get a good sense of how Enumerable works by writing a small, proof-of- concept class that uses it. The following listing shows such a class: Rainbow. This class has an each method that yields one color at a time. Because the class mixes in Enumerable, its instances are automatically endowed with the instance methods defined in that module.
```
class Rainbow
  include Enumerable
  def each
    yield "red"
    yield "orange"
    yield "yellow"
    yield "green"
    yield "blue"
    yield "indigo"
    yield "violet"
  end
end
```
Every instance of Rainbow will know how to iterate through the colors. In the simplest case, we can use the each method:
```
r = Rainbow.new
r.each do |color|
  puts "Next color: #{color}"
end
```
The output of this simple iteration is as follows:
```
Next color: red
Next color: orange
Next color: yellow
Next color: green
Next color: blue
Next color: indigo
Next color: violet
```
But that’s just the beginning. Because Rainbow mixed in the Enumerable module, rainbows are automatically endowed with a whole slew of methods built on top of the each method.
Here’s an example: find, which returns the first element in an enumerable object for which the code block provided returns true. Let’s say we want to find the first color that begins with the letter y. We can do it with find, like this:
```
r = Rainbow.new
y_color = r.find {|color| color.start_with?('y') }
puts "First color starting with 'y' is #{y_color}."
```

#### Group_by

A **group_by** operation on an enumerable object takes a block and returns a hash. The block is executed for each object. For each unique block return value, the result hash gets a key; the value for that key is an array of all the elements of the enumerable for which the block returned that value.

#### Cycle method

You can use cycle to decide dynamically how many times you want to iterate through a collection—essentially, how many each-like runs you want to perform con- secutively. Here’s an example involving a deck of playing cards:
```
class PlayingCard
  SUITS = %w{ clubs diamonds hearts spades }
  RANKS = %w{ 2 3 4 5 6 7 8 9 10 J Q K A }
  class Deck
    attr_reader :cards
    def initialize(n=1)
      @cards = []
      SUITS.cycle(n) do |s|
        RANKS.cycle(1) do |r|
          @cards << "#{r} of #{s}"
        end
      end
    end
  end
end
```
The class PlayingCard defines constants representing suits and ranks, whereas the PlayingCard::Deck class models the deck. The cards are stored in an array in the deck’s @cards instance variable, available also as a reader attribute. Thanks to **cycle**, it’s easy to arrange for the possibility of combining two or more decks. **Deck.new** takes an argument, defaulting to 1. If you override the default, the process by which the @cards array is populated is augmented.
For example, this command produces a double deck of cards containing two of each card for a total of 104:
```
deck = PlayingCard::Deck.new(2)
```
That’s because the method cycles through the suits twice, cycling through the ranks once per suit iteration. The ranks cycle is always done only once; cycle(1) is, in effect, another way of saying each. For each permutation, a new card, represented by a descriptive string, is inserted into the deck.
What if someone gets hold of the @cards array through the cards reader attribute and alters it?
```
deck = PlayingCard::Deck.new
deck.cards << "JOKER!!"
```
Ideally, we’d like to be able to read from the cards array but not alter it. (We could freeze it with the freeze method, which prevents further changes to objects, but we’ll need to change the deck inside the Deck class when it’s dealt from.) Enumerators provide a solution. Instead of a reader attribute, let’s make the cards method return an enumerator:
```
class PlayingCard
  SUITS = %w{ clubs diamonds hearts spades }
  RANKS = %w{ 2 3 4 5 6 7 8 9 10 J Q K A }
  class Deck
    def cards
      @cards.to_enum
    end
    def initialize(n=1)
      @cards = []
      SUITS.cycle(n) do |s|
        RANKS.cycle(1) do |r|
          @cards << "#{r} of #{s}"
        end
      end
    end
  end
end
```
It’s still possible to pry into the @cards array and mess it up if you’re determined. But
the enumerator provides a significant amount of protection.

Enumerators maintain state: they keep track of where they are in their enumeration. Several methods make direct use of this information. Consider this example:
```
names = %w{ David Yukihiro }
e = names.to_enum
puts e.next
puts e.next
e.rewind
puts e.next
```

The output from these commands is
```
David
Yukihiro
David
```
The enumerator allows you to move in slow motion, so to speak, through the enumer- ation of the array, stopping and restarting at will. In this respect, it’s like one of those editing tables where a film editor cranks the film manually. 

You can use a lazy enumerator to write a version of FizzBuzz that can handle any
range of numbers. Here’s what it might look like:
```
def fb_calc(i)
  case 0
  when i % 15
    "FizzBuzz"
  when i % 3
    "Fizz"
  when i % 5
    "Buzz"
  else
    i.to_s
  end
end

def fb(n)
  (1..Float::INFINITY).lazy.map {|i| fb_calc(i) }.first(n)
end
```
Now you can examine, say, the FizzBuzz output for the first 15 positive integers like this:
```
p fb(15)
The output will be
["1", "2", "Fizz", "4", "Buzz", "Fizz", "7", "8", "Fizz", "Buzz", "11",
     "Fizz", "13", "14", "FizzBuzz"]
```
Without creating a lazy enumerator on the range, the map operation would go on forever. Instead, the lazy enumeration ensures that the whole process will stop once we’ve got what we want.

#### Chapter 11 Regular expressions and regexp-based string operations

Regular expressions are instances of the Regexp class, which is one of the Ruby classes that has a literal constructor for easy instantiation. The regexp literal constructor is a pair of forward slashes:
```
//
```
The match method and the =~ operator are equally useful when you’re after a simple yes/no answer to the question of whether there’s a match between a string and a pattern. If there’s no match, you get back nil. That’s handy for conditionals; all four of the previous examples test the results of their match operations with an if test. Where match and =~ differ from each other chiefly is in what they return when there is a match: =~ returns the numerical index of the character in the string where the match started, whereas match returns an instance of the class MatchData:
```
"The alphabet starts with abc" =~ /abc/
=> 25
/abc/.match("The alphabet starts with abc.")
=> #<MatchData "abc">
```
#### Character classes

Inside a character class, you can also insert a range of characters. A common case is this, for lowercase letters:
```
/[a-z]/
```

#### Common methods using regular expressions

The payoff for gaining facility with regular expressions in Ruby is the ability to use the methods that take regular expressions as arguments and do something with them.
To begin with, you can always use a match operation as a test in, say, a find or find_all operation on a collection. For example, to find all strings longer than 10 characters and containing at least 1 digit, from an array of strings called array, you can do this:
```
array.find_all {|e| e.size > 10 and /\d/.match(e) }
```
#### String#scan

For example, if you want to harvest all the digits in a string, you can do this:
```
>> "testing 1 2 3 testing 4 5 6".scan(/\d/)
=> ["1", "2", "3", "4", "5", "6"]
```

#### Chapter 12 File and I/O operations

The following examples involve a file called ticket2.rb that contains the code in listing 3.2 and that’s stored in a directory called code:
```
>> f = File.new("code/ticket2.rb")
=> #<File:code/ticket2.rb>
```
This example performs some simple write and append operations, pausing along the way to use the mighty File.read to check the contents of the file:
```
>> f = File.new("data.out", "w")
=> #<File:data.out>
>> f.puts "David A. Black, Rubyist"
=> nil
>> f.close
=> nil
>> puts File.read("data.out")
David A. Black, Rubyist
=> nil
>> f = File.new("data.out", "a")
=> #<File:data.out>
>> f.puts "Yukihiro Matsumoto, Ruby creator"
=> nil
>> f.close
=> nil
>> puts File.read("data.out")
David A. Black, Rubyist
Yukihiro Matsumoto, Ruby creator
```
#### The open-uri library
The open-uri standard library package lets you retrieve information from the net- work using the HTTP and HTTPS protocols as easily as if you were reading local files. All you do is require the library (require 'open-uri') and use the Kernel#open method with a URI as the argument. You get back a StringIO object containing the results of your request:
```
require 'open-uri'
rubypage = open("http://rubycentral.org")
puts rubypage.gets
```
You get the doctype declaration from the Ruby Central homepage—not the most scintillating reading, but it demonstrates the ease with which open-uri lets you import networked materials.

#### Part 3 Ruby dynamics

#### Chapter 13 Object individuation

#### Defining class methods with class <<
Here’s an idiom you’ll see often:
```
class Ticket
  class << self
    def most_expensive(*tickets)
      tickets.max_by(&:price)
    end
  end
end
```
This code results in the creation of the class method Ticket.most_expensive—much
the same method as the one defined in section 3.6.3, but that time around we did this:
```
def Ticket.most_expensive(*tickets)  # etc.
```
Here’s how the Person example would look, using extend instead of explicitly open- ing up the singleton class of the ruby object. Let’s also use extend for david (instead of the singleton method definition with def):
```
module Secretive
  def name
    "[not available]"
  end
end
class Person
  attr_accessor :name
end
david = Person.new
david.name = "David"
matz = Person.new
matz.name = "Matz"
ruby = Person.new
ruby.name = "Ruby"
david.extend(Secretive)
ruby.extend(Secretive)
puts "We've got one person named #{matz.name}, " +
     "one named #{david.name}, "                 +
     "and one named #{ruby.name}."
```

#### Chapter 14 Callable and runnable objects

Let’s start with the basic callable object: an instance of Proc, created with Proc.new. You create a Proc object by instantiating the Proc class, including a code block:
```
pr = Proc.new { puts "Inside a Proc's block" }
```
The code block becomes the body of the proc; when you call the proc, the block you
provided is executed. Thus if you call pr 
```
pr.call
```
it reports as follows:
```
Inside a Proc's block
```
An important and often misunderstood fact is that a Ruby code block is not an object. This familiar trivial example has a receiver, a dot operator, a method name, and a code block:
```
[1,2,3].each {|x| puts x * 10 }
```
The receiver is an object, but the code block isn’t. Rather, the code block is part of the syntax of the method call.

Like Proc.new, the lambda method returns a Proc object, using the provided code block as the function body:
```
>> lam = lambda { puts "A lambda!" }
=> #<Proc:0x0000010299a1d0@(irb):2 (lambda)>
>> lam.call
A lambda!
```
As the inspect string suggests, the object returned from lambda is of class Proc. But note the (lambda) notation. There’s no Lambda class, but there is a distinct lambda flavor of the Proc class. And lambda-flavored procs are a little different from their vanilla cousins, in three ways.
First, lambdas require explicit creation. Wherever Ruby creates Proc objects implicitly, they’re regular procs and not lambdas. That means chiefly that when you grab a code block in a method, like this
```
def m(&block)
```
the Proc object you’ve grabbed is a regular proc, not a lambda.

Second, lambdas differ from procs in how they treat the return keyword. return
inside a lambda triggers an exit from the body of the lambda to the code context immediately containing the lambda. return inside a proc triggers a return from the method in which the proc is being executed.

Finally, and most important, lambda-flavored procs don’t like being called with the wrong number of arguments. They’re fussy:
```
>> lam = lambda {|x| p x }
=> #<Proc:0x000001029901f8@(irb):3 (lambda)>
>> lam.call(1)
1
=> 1
>> lam.call
ArgumentError: wrong number of arguments (0 for 1)
>> lam.call(1,2,3)
ArgumentError: wrong number of arguments (3 for 1)
```
#### Threads

Ruby’s threads allow you to do more than one thing at once in your program, through a form of time sharing: one thread executes one or more instructions and then passes control to the next thread, and so forth. Exactly how the simultaneity of threads plays out depends on your system and your Ruby implementation.

Creating threads in Ruby is easy: you instantiate the Thread class. A new thread starts executing immediately, but the execution of the code around the thread doesn’t stop. If the program ends while one or more threads are running, those threads are killed.

Here is a threaded date server:
The date server we’ll write depends on a Ruby facility that we haven’t looked at yet: TCPServer. TCPServer is a socket-based class that allows you to start up a server almost unbelievably easily: you instantiate the class and pass in a port number. Here’s a simple example of TCPServer in action, serving the current date to the first person who
connects to it:
```
require 'socket'
s = TCPServer.new(3939)
conn = s.accept
conn.puts "Hi. Here's the date."
conn.puts `date`
conn.close
s.close
```
Put this example in a file called dateserver.rb, and run it from the command line. (If port 3939 isn’t available, change the number to something else.) Now, from a different console, connect to the server:
```
telnet localhost 3939
```
You’ll see output similar to the following:
```
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
Hi. Here's the date.
Sat Jan 18 07:29:11 EST 2014
Connection closed by foreign host.
```
We can use threads to create a simple chat server using TCPServer:
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
First we load the socket library. Then we define some needed helper methods. We start the program in earnest with the instantiation of the TCPServer and the initialization of the array of chatters.

The server goes into a while loop similar to the loop we saw with the date server. When a chatter connects, the server welcomes it (or him or her). The welcome process involves the welcome mehthod which takes a chatter (a socket object) as its argument prints a welcome message and returns a line of client input. It is now time to notify all the current chatters that a new chatter has arrived. This involvs the broadcast method which is the heart of the chat funcitonality of the program. The broadcast method is responsible for going through the array of chatters and sending a message to each one. In this case the message states that the new client has joined the chat.

After being announced the new chatter is added to the chatters array. That means it will be included in future message broadcasts.

Next we continue with the chatting aspect of the application. The chatting functionality consists of an infinite loop wrapped in a begin/rescue clause. The goal is to accept messages from the client forever but to take action if the client socket reports end of file. Messages to the chat are accepted via readline which raises an exception on end-of-file. If the chatter leaves the chat, then the next next attempt to read a line from that chatter raises EOFError. When that happens, control goes to the rescue block where the departed chatter is removed from the chatters array and an announcement is broadcast to the effect that the chatter has left. If there is no EOFError the chatters message is broadcast to all chatters.

When using threads it is important to know how the rules of variable scoping and visibility play out inside threads.

Here we have an Rock Paper Scissors game which we will later use in a thread:
```
module Games
  class RPS
    include Comparable
    WINS = [%w{ rock scissors },
            %w{ scissors paper },
            %w{ paper rock }]
    attr_accessor :move
    def initialize(move)
      @move = move.to_s
    end
    def <=>(other)
      if move == other.move
        0
      elsif WINS.include?([move, other.move])
        1
      elsif WINS.include?([other.move, move])
        -1
      else
        raise ArgumentError, "Something's wrong"
      end
    end
    def play(other)
      if self > other
        self
      elsif other > self
        other
      else
        false
      end
    end
  end
end
```
The RPS class includes the Comparable module. This allows us to determine who wins the game. The WINS constant contains all the possible winning combinations in three arrays. The first element in each array beats the second element. There is also a move attribute which stores the move for the instance of RPS. The initialize method stores the move as a string.

RPS has a spaceship operator (<=>) method definition which specifies what happens when the instance of RPS is compared to another instance. If the two have equal moves the result is 0. This signifies that the two terms are equal. The rest of the logic looks for winning combinations and then returns -1 for lose and 1 for win. If it doesn't find any match and the result isn't a tie then the program raises an exception. We then use the play method to show who has won.

We can now incorporate the RPS class to use threads:
```
require 'socket' 
require_relative 'rps' 
s = TCPServer.new(3939)
threads = []
2.times do |n|
  conn = s.accept
  threads << Thread.new(conn) do |c|
    Thread.current[:number] = n + 1
    Thread.current[:player] = c
    c.puts "Welcome, player #{n+1}!"
    c.print "Your move? (rock, paper, scissors) "
    Thread.current[:move] = c.gets.chomp
    c.puts "Thanks... hang on."
  end
end
a,b = threads
a.join
b.join
rps1, rps2 = Games::RPS.new(a[:move]), Games::RPS.new(b[:move])
winner = rps1.play(rps2)
if winner
  result = winner.move
else
  result = "TIE!"
end

threads.each do |t|
  t[:player].puts "The winner is #{result}!" i
end
```
As in the chat-server example, we start with a server along with an array in which threads are stored. Rather than a continuous loop, however, we gather only two threads courtesy of the 2.times loop and the server's accept method. For each of the two connections we create a thread.

Next we store some values in the thread's keys. We take a number for the player based on the loop and add 1 so that there is no player 0. We then welcome the player and store the move in the :move key of the thread.

After both players have played, we grab the two threads in the convenience variables a and b and join both threads. Next we put the moves of the two thread objects into the RPS objects. The winner is determined by playing one thread against the other. The final result is either the winner or if the game returns false a tie. Finally, we show the results to both players. 

 In this chapter, we’ve looked at a number of ways in which the general notion of callable and runnable objects plays out. We looked at Proc objects and lambdas, the anonymous functions that lie at the heart of Ruby’s block syntax. We also discussed methods as objects and ways of unbinding and binding methods and treating them separately from the objects that call them. The eval family of methods took us into the realm of executing arbitrary strings and also showed some powerful and elegant techniques for runtime manipulation of the program’s object and class landscape, using not only eval but, even more, class_eval and instance_eval with their block-wise operations.

 #### Chapter 15 Callbacks, hooks, and runtime introspection

 #### Callbacks and hooks

 The use of callbacks and hooks is a fairly common meta-programming technique. These methods are called when a particular event takes place during the run of a Ruby pro- gram. An event is something like
* A nonexistent method being called on an object
* A module being mixed in to a class or another module
* An object being extended with a module
* A class being subclassed (inherited from)
* A reference being made to a nonexistent constant
* An instance method being added to a class
* A singleton method being added to an object

For every event in that list, you can (if you choose) write a callback method that will be executed when the event happens. 

When you send a message to an object, the object executes the first method it finds on its method-lookup path with the same name as the message. If it fails to find any such method, it raises a NoMethodError exception—unless you’ve provided the object with a method called method_missing. Method_missing is arguably the most commonly used runtime hook in Ruby.

You can use method_missing to bring about an automatic extension of the way your object behaves.

We can add method_missing to automatically extend the way an object behaves. For instance if we have a Cookbook class we can use the method to add more array methods:
```
class Cookbook
  attr_accessor :title, :author
  def initialize
    @recipes = []
  end
  def method_missing(m,*args,&block)
    @recipes.send(m,*args,&block)
  end
end
```

Now we can perform manipulations on the collection of recipes, taking advantage of any array methods we wish. Let’s assume there’s a Recipe class, separate from the Cookbook class, and we’ve already created some Recipe objects:
```
cb = Cookbook.new
cb << recipe_for_cake
cb << recipe_for_chicken
beef_dishes = cb.select {|recipes| recipe.main_ingredient == "beef" }
```
In this method_missing example, we’ve delegated the processing of messages (the unknown ones) to the array @recipes.
This use of method_missing is very straightforward (though you can mix and match it with some of the bells and whistles from chapter 4) but very powerful; it adds a great deal of intelligence to a class in return for little effort.

An oft-cited problem with method_missing is that it doesn’t align with respond_to?. Consider this example. In the Person class, we intercept messages that start with set_, and transform them into setter methods: set_age(n) becomes age=n and so forth. For example:
```
class Person
  attr_accessor :name, :age
  def initialize(name, age)
    @name, @age = name, age
  end
  def method_missing(m, *args, &block)
    if /set_(.*)/.match(m)
      self.send("#{$1}=", *args)
    else
      super
    end
  end
end
```

So does a person object have a set_age method, or not? Well, you can call that method, but the person object claims it doesn’t respond to it:
```
person = Person.new("David", 54)
person.set_age(55)
p person.age
p person.respond_to?(:set_age)
```
The way to get method_missing and respond_to? to line up with each other is by defining the special method respond_to_missing?. Here’s a definition you can add to the preceding Person class:
```
  def respond_to_missing?(m, include_private = false)
    /set_/.match(m) || super
  end
```
Now the new person object will respond differently given the same queries:
```
55
true
```

You can also use included and extended as callback methods on include and extend to add extra methods or messages:

```
module M
  def self.included(c)
    puts "#{self} included by #{c}."
  end
  def self.extended(obj)
    puts "#{self} extended by #{obj}."
  end 
end
obj = Object.new
puts "Including M in object's singleton class:"
class << obj
 include M
end

obj = Object.new
puts "Extending object with M:"
obj.extend(M)
```
Both callbacks are defined in the module M: included B and extended. Each callback prints out a report of what it’s doing. Starting with a freshly minted, generic object, we include M in the object’s singleton class and then repeat the process, using another new object and extending the object with M directly.

The output from this listing is
Including M in object's singleton class:
```
M included by #<Class:#<Object:0x0000010193c978>>.
Extending object with M:
M extended by #<Object:0x0000010193c310>.
```
Sure enough, the include triggers the included callback, and the extend triggers extended.

#### Intercepting inheritance with Class#inherited

Here’s a simple example, where the class C reports on the fact that it has been subclassed:
```
class C
  def self.inherited(subclass)
    puts "#{self} just got subclassed by #{subclass}."
  end
end

class D < C
end
```
The subclassing of C by D automatically triggers a call to inherited and produces the following output:
```
C just got subclassed by D.
```

#### The Module#const_missing method

As the name implies, this method is called whenever an unidentifiable constant is referred to inside a given module or class:
```
class C
  def self.const_missing(const)
     puts "#{const} is undefined—setting it to 1."
     const_set(const,1)
  end
end
puts C::A
puts C::A
```
The output of this code is
```
A is undefined—setting it to 1.
1
1
```

Thanks to the callback, C::A is defined automatically when you use it without defin- ing it. This is taken care of in such a way that puts can print the value of the con- stant; puts never has to know that the constant wasn’t defined in the first place. Then, on the second call to puts, the constant is already defined, and const_missing isn’t called.

There are four min method querying methods. The four methods work as follows:
■ instance_methods returns all public and protected instance methods.
■ public_instance_methods returns all public instance methods.
■ protected_instance_methods and private_instance_methods return all pro-
tected and private instance methods, respectively.

Once you get some practice using the various methods methods, you’ll find them use- ful for studying and exploring how and where methods are defined. For example, you can use method queries to examine how the class methods of File are composed. To start with, find out which class methods File inherits from its ancestors, as opposed to those it defines itself:
```
>> File.singleton_methods - File.singleton_methods(false)
=> [:new, :open, :sysopen, :for_fd, :popen, :foreach, :readlines,
:read, :select, :pipe, :try_convert, :copy_stream]
```
The call to singleton_methods(false) provides only the singleton methods defined on File. The call without the false argument provides all the singleton methods defined on File and its ancestors. The difference is the ones defined by the ancestors. The superclass of File is IO. Interestingly, although not surprisingly, all 12 of the ancestral singleton methods available to File are defined in IO.

Here’s another rendition of a simple Person class, which illustrates what’s involved in an instance-variable query:
```
class Person
  attr_accessor :name, :age
  def initialize(name)
    @name = name
  end
end

david = Person.new("David")
david.age = 55
p david.instance_variables
The output is
[:@name, :@age]
```

The object david has two instance variables initialized at the time of the query. One of them, @name, was assigned a value at the time of the object’s creation. The other, @age, is present because of the accessor attribute age.

#### Caller

The caller method provides an array of strings. Each string represents one step in the stack trace: a description of a single method call along the way to where you are now. The strings contain information about the file or program where the method call was made, the line on which the method call occurred, and the method from which the current method was called, if any.
Here’s an example. Put these lines in a file called tracedemo.rb:
```
def x y
end 

def y
 z
end

def z
  puts "Stacktrace: "
  p caller
end
x
```
Here is the output:
```
Stacktrace:
["tracedemo.rb:6:in `y'", "tracedemo.rb:2:in `x'", "tracedemo.rb:14:in
        `<main>'"]
```

#### Writing a tool for parsing stack traces

CallerTools::Call will have three reader attributes: program, line, and meth. (It’s better to use meth than method as the name of the third attribute because classes already have a method called method and we don’t want to override it.) Upon initialization, an object of this class will parse a stack trace string and save the rele- vant substrings to the appropriate instance variables for later retrieval via the attri- bute-reader methods.
CallerTools::Stack will store one or more Call objects in an array, which in turn will be stored in the instance variable @backtrace. We’ll also write a report method, which will produce a (reasonably) pretty printable representation of all the informa- tion in this particular stack of calls.

The following is the Call class:
```
module CallerTools
  class Call b
    CALL_RE = /(.*):(\d+):in `(.*)'/
    attr_reader :program, :line, :meth
    def initialize(string)
      @program, @line, @meth = CALL_RE.match(string).captures
    end

    def to_s
      "%30s%5s%15s" % [program, line, meth] e
    end 
  end
```

Here is the Stack class:
```
  class Stack
    def initialize
      stack = caller
      stack.shift
      @backtrace = stack.map do |call|
        Call.new(call)
      end
    end
    def report
      @backtrace.map do |call|
        call.to_s
      end 
    end
    def find(&block)
      @backtrace.find(&block)
    end 
  end
end
```

Now we can put this code in a file called callertest.rb:
```
require_relative 'callertools'
def x
  y
end
def y
  z
end 
def z
  stack = CallerTools::Stack.new
  puts stack.report
end
x
```
When you run the program, you’ll see this output:
```
                 callertest.rb   12              z
                 callertest.rb    8              y
                 callertest.rb    4              x
                 callertest.rb   16         <main>
```
Next we will implement a MicroTest framework. We start with the Deck class that we wish to test:

```
module PlayingCards
  RANKS = %w{ 2 3 4 5 6 7 8 9 10 J Q K A }
  SUITS = %w{ clubs diamonds hearts spades }
  class Deck
    def initialize
      @cards = []
      RANKS.each do |r|
        SUITS.each do |s|
          @cards << "#{r} of #{s}"
        end
      end
      @cards.shuffle!
    end
    def deal(n=1)
      @cards.pop(n)
    end
    def size
      @cards.size
    end
  end
end
```
Creating a new deck involves initializing @cards, inserting 52 strings into it, and shuffling the array. Each string takes the form “rank of suit,” where rank is one of the ranks in the constant array RANKS and suit is one of SUITS. In dealing from the deck, we return an array of n cards, where n is the number of cards being dealt and defaults to 1.

Here we test the class using MiniTest:
```
require 'minitest/unit'
require 'minitest/autorun'
require_relative 'cards'
class CardTest < MiniTest::Unit::TestCase
  def setup
    @deck = PlayingCards::Deck.new
  end
  def test_deal_one
    @deck.deal
    assert_equal(51, @deck.size)
  end
  def test_deal_many
    @deck.deal(5)
    assert_equal(47, @deck.size)
  end
end
```
Execute cardtest.rb from the command line. Here’s what you’ll see (probably with a different seed and different time measurements):
```
$ ruby cardtest.rb
Run options: --seed 39562
# Running tests:
..
Finished tests in 0.000784s, 2551.0204 tests/s, 2551.0204 assertions/s.
2 tests, 2 assertions, 0 failures, 0 errors, 0 skips
```
The last line tells you that there were two methods whose names began with test (2 tests) and a total of two assertions (the two calls to assert_equal). It tells you fur- ther that both assertions passed (no failures) and that nothing went drastically wrong (no errors; an error is something unrecoverable like a reference to an unknown variable, whereas a failure is an incorrect assertion). It also reports that no tests were skipped (skipping a test is something you can do explicitly with a call to the skip method).

The most striking thing about running this test file is that at no point do you have to instantiate the CardTest class or explicitly call the test methods or the setup method. Thanks to the loading of the autorun feature, MiniTest figures out that it’s supposed to run all the methods whose names begin with test, running the setup method before each of them. This automatic execution—or at least a subset of it—is what we’ll implement in our exercise.

Here’s a more detailed description of the steps needed to implement MicroTest:
1 Define the class MicroTest.
2 Define MicroTest.inherited.
3 Inside inherited, the inheriting class should...
4 Define its own method_added callback, which should...
5 Instantiate the class and execute the new method if it starts with test, but
first...
6 Execute the setup method, if there is one.

Here is the class MicroTest with the inherited method:

```
require_relative 'callertools'
class MicroTest
  def self.inherited(c)
    c.class_eval do
      def self.method_added(m)
        if m =~ /^test/
          obj = self.new
          if self.instance_methods.include?(:setup)
            obj.setup
          end
          obj.send(m)
        end
      end
    end
  end

  def assert(assertion)
    if assertion
      puts "Assertion passed"
      true 
    else
      puts "Assertion failed:"
      stack = CallerTools::Stack.new
      failure = stack.find {|call| call.meth !~ /assert/ }
      puts failure
      false
    end
  end
  def assert_equal(expected, actual)
    result = assert(expected == actual)
    puts "(#{actual} is not #{expected})" unless result
    result
  end
end
```
Inside the class definition (class_eval) scope of the new subclass, we define method_added, and that’s where most of the action is. If the method being defined starts with test, we create a new instance of the class. If a setup method is defined, we call it on that instance. Then (whether or not there was a setup method; that’s optional), we call the newly added method using send because we don’t know the method’s name.

The assert method tests the truth of its single argument. If the argument is true (in the Boolean sense; it doesn’t have to be the actual object true), a message is printed out, indicating success. If the assertion fails, the message printing gets a lit- tle more intricate. We create a CallerTools::Stack object and pinpoint the first Call object in that stack whose method name doesn’t contain the string assert. The purpose is to make sure we don’t report the failure as having occurred in the assert method nor in the assert_equal method. It’s not robust; you might have a method with assert in it that you did want an error reported from. But it illustrates the kind of manipulation that the find method of CallerTools::Stack allows.

The second assertion method, assert_equal, tests for equality between its two arguments. It does this by calling assert on a comparison. If the result isn’t true, an error message showing the two compared objects is displayed. Either way—success or failure—the result of the assert call is returned from assert_equal.