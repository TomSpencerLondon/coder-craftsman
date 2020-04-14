# Interface Segregation

Robert C. Martin (Uncle Bob) defined the interface-segregation principle (ISP) whilst working with Xerox to improve the software for their new printers. He stated it as:

A client should never be forced to implement an interface that it doesn't use. Nor should clients be forced to depend on methods they do not use.

The motivation behind this principle is to move towards a codebase that relies on thin abstract interfaces. It makes it easier for clients to have less dependent factors between modules them, thus reducing coupling, increasing cohesion and improving the maintainabilty of the code.

This is in a similar vain to the Single Responsibility Principle. Your abstractions should be small, individual units of business logic so that your clients implement the slice of the pie they need not the whole pie (nor the ice cream, cherry or sprinkles).
