# Interface Segregation

This is the fourth in a series of five blogs on the SOLID Design Principles. Read the blog on the previous principle, the Liskov substitution principle here.

The Interface Segregation principle states that no client should be forced to depend on methods it does not use.

![interface segregation](https://user-images.githubusercontent.com/63193195/79233735-28d1ff80-7e61-11ea-9900-afafd74e7799.jpg)

Robert C. Martin (Uncle Bob) defined the interface-segregation principle (ISP) whilst working with Xerox to improve the software for their new printers. He stated it as:

A client should never be forced to implement an interface that it doesn't use. Nor should clients be forced to depend on methods they do not use.

The motivation behind this principle is to move towards a codebase that relies on thin abstract interfaces It splits interfaces that are very large into smaller and more specific ones so that clients will only have to know about the methods that are of interest to them. It means clients have less dependent factors between modules, thus reducing coupling, increasing cohesion and improving the maintainabilty of the code.

This makes it similar to the Single Responsibility Principle - your abstractions should be small, individual units of business logic so that your clients implement the slice of the pie they need, rather than the whole pie.

Let's take a look at the ISP using a printer:
```
package ISP;

public class Isp {
    public static void main(String[] args) throws Exception {

        Document document = new Document();
        document.addDocument("Offer");
        document.addDocument("Invoice");

        PrinterHP printerHP = new PrinterHP();
        printerHP.Print(document);

        ScannerSony scannerSony = new ScannerSony();
        scannerSony.Scan(document);

        PhotocopierHP photocopierHP = new PhotocopierHP();
        photocopierHP.Print(document);

        FaxPanasonic faxPanasonic = new FaxPanasonic();

        MultiFunctionMachine multiFunctionMachine = new MultiFunctionMachine(printerHP, scannerSony, faxPanasonic);
        multiFunctionMachine.InternetFax(document);
    }
}
```
Here we have a simple document class:
```
package ISP;

import java.util.ArrayList;
import java.util.List;

public class Document {
    private final List<String> documents = new ArrayList<>();

    void addDocument(String text) {
        documents.add(text);
    }

    @Override
    public String toString() {
        return String.join(", ", documents);
    }
}
```
We have a Multifunction device interface:
```
package ISP;

public interface MultiFunctionDevice extends Printer, Scanner, Fax {
}
```
and a Multifunction Machine that implements the device interface:
```
package ISP;

public class MultiFunctionMachine implements MultiFunctionDevice {
    private Printer printer;
    private Scanner scanner;
    private Fax fax;

    MultiFunctionMachine(Printer printer, Scanner scanner, Fax fax) {
        this.printer = printer;
        this.scanner = scanner;
        this.fax = fax;
    }

    public void Print(Document d) throws Exception {
        printer.Print(d);
    }

    public void Scan(Document d) throws Exception {
        scanner.Scan(d);
    }

    public void InternetFax(Document d) throws Exception {
        fax.InternetFax(d);
    }
}
```
We then have different interfaces which can interact as this device:
```
package ISP;

public interface Printer {
    void Print(Document d) throws Exception;
}
```
and:
```
package ISP;

public class PrinterHP implements Printer {
    public void Print(Document d) {
        System.out.println("Print the text from the document: " + d);
    }
}
```
Scanner:
```
  
package ISP;

public interface Scanner {
    void Scan(Document d) throws Exception;
}
```
and:
```
  
package ISP;

public class ScannerSony implements Scanner {
    public void Scan(Document d) {
        System.out.println("Scan the text from the document: " + d);
    }
}
```
and photocopier:
```
package ISP;

class PhotocopierHP implements Printer, Scanner {
    public void Print(Document d) {
        System.out.println("Print the text from the document: " + d);
    }

    public void Scan(Document d) {
        System.out.println("Scan the text of the document: " + d);
    }
}
```
and fax:
```
package ISP;

public interface Fax {
    void InternetFax(Document d) throws Exception;
}
```
and here:
```
package ISP;

public class FaxPanasonic implements Fax {

    public void InternetFax(Document d) {
        System.out.println("Fax the text from the document: " + d);
    }
}
```
We then look again at the ISP class:
```
package ISP;

public class Isp {
    public static void main(String[] args) throws Exception {

        Document document = new Document();
        document.addDocument("Offer");
        document.addDocument("Invoice");

        PrinterHP printerHP = new PrinterHP();
        printerHP.Print(document);

        ScannerSony scannerSony = new ScannerSony();
        scannerSony.Scan(document);

        PhotocopierHP photocopierHP = new PhotocopierHP();
        photocopierHP.Print(document);

        FaxPanasonic faxPanasonic = new FaxPanasonic();

        MultiFunctionMachine multiFunctionMachine = new MultiFunctionMachine(printerHP, scannerSony, faxPanasonic);
        multiFunctionMachine.InternetFax(document);
    }
}
```
We can now see that we have a document and all the different devices. We can then use Print on each class or alternatively use the MultiFunctionMachine to call InternetFax to feed in all the classes and then print the document how we want.

The next blog is on the Dependency Inversion, the final SOLID principle. 
