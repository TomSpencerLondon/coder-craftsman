# Interface Segregation

This is the fourth in a series of five blogs on the SOLID Design Principles. Read the blog on the previous principle, the Liskov substitution principle here.

The Interface Segregation principle states that no client should be forced to depend on methods it does not use.

![interface segregation](https://user-images.githubusercontent.com/63193195/79233735-28d1ff80-7e61-11ea-9900-afafd74e7799.jpg)

Robert C. Martin (Uncle Bob) defined the interface-segregation principle (ISP) whilst working with Xerox to improve the software for their new printers. He stated it as:

A client should never be forced to implement an interface that it doesn't use. Nor should clients be forced to depend on methods they do not use.

The motivation behind this principle is to move towards a codebase that relies on thin abstract interfaces It splits interfaces that are very large into smaller and more specific ones so that clients will only have to know about the methods that are of interest to them. It means clients have less dependent factors between modules, thus reducing coupling, increasing cohesion and improving the maintainabilty of the code.

This makes it similar to the Single Responsibility Principle - your abstractions should be small, individual units of business logic so that your clients implement the slice of the pie they need, rather than the whole pie.
