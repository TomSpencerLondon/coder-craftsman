# Single Responsibility Principle

This is the first in a series of five blogs on the SOLID Design Principles. These five principles apply to object-orientated programme and form a subset of the many principles promoted by American software engineer and instructor Robert C. Martin (Uncle Bob), first set out in a paper in 2000. The aim of the principles is to make a codebase for software designs which is more understandable, flexible and maintainable. 

### SOLID is a mnemonic  which stands for:

- Single Responsibility Principle
- Open/Closed Principle
-	Liskov Substitution Principle
- Interface Segregation Principle
- Dependency Inversion Principle

We will start by looking at the Single Responsibility Principle. 

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
