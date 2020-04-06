# Single Responsibility Principle

This is the first in a series of five blogs on the SOLID Design Principles. These five principles apply to object-orientated programme and form a subset of the many principles promoted by American software engineer and instructor Robert C. Martin (Uncle Bob), first set out in a paper in 2000. The aim of the principles is to make a codebase for software designs which is more understandable, flexible and maintainable. 

### SOLID is a mnemonic  which stands for:

- Single Responsibility Principle
- Open/Closed Principle
-	Liskov Substitution Principle
- Interface Segregation Principle
- Dependency Inversion Principle

#### We will start by looking at the Single Responsibility Principle. 

![image](https://user-images.githubusercontent.com/63193195/78601077-0716be00-784c-11ea-8ec6-492f259b0891.png)


This principle states that every module or class should have responsibility over one part of the functionality the software provides, and that this should be completely encapsulated by the class, module or function. As such it helps to limit the impact of future changes. 

This is a main file for Single Responsibility Principle in code:
```
package SPR;

class Spr {
    public static void main(String[] args) throws Exception {
        Note note = new Note();
        note.addComment("First note");
        note.addComment("Second note");

        Persistence persistence = new Persistence();
        String filename = "notes.txt";
        persistence.saveToFile(note, filename);

        System.out.println(note);
        Runtime.getRuntime().exec("gedit " + filename);
    }
}
```
We need classes to have their own single responsibility. So we'll create two classes. We create a note and also a persistence instance. We then call persistence.saveToFile(note, filename) on persistence. 

This is the Note class:
```
package SPR;

import java.util.ArrayList;
import java.util.List;

class Note {
    private final List<String> comments = new ArrayList<>();
    private static int count = 0;

    void addComment(String text) {
        comments.add("" + (++count) + ": " + text);
    }

    @Override
    public String toString() {
        return String.join(System.lineSeparator(), comments);
    }
}s
```
It has responsibility for addComment and a toString method. Nothing else. 

Our Persistence() class also only does one thing:
```
package SPR;

import java.io.PrintStream;

class Persistence {
    void saveToFile(Note note, String filename) throws Exception {
        try (PrintStream out = new PrintStream(filename)) {
            out.println(note.toString());
        }
    }
}
```
Its role here here is to saveToFile. 

As we can see, in each of these cases each class has a single responsibility. As such the code is easier to maintain. If we needed to change some of the formatting at a future point, we would not need to change the class as the responsibilities are separated out.

In the next blog we will look at the Open/Closed Principle.
