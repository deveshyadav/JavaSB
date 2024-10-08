Creational Design Patterns

1. Singleton: Ensures a class has only one instance and provides a global point of access to it.
2. Factory Method: Provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.
3. Abstract Factory: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.
4. Builder: Separates the construction of a complex object from its representation so that the same construction process can create different representations.
5. Prototype: Creates new objects by copying an existing object, known as the prototype.

``` Java
/*Singleton Pattern*/
public class Singleton {
    /*// Private static instance of the class*/
    private static Singleton instance;

    /*// Private constructor to prevent instantiation*/
    private Singleton() {}

    /*// Public method to provide access to the instance*/
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }

    public void showMessage() {
        System.out.println("Hello from Singleton!");
    }
}

public class SingletonDemo {
    public static void main(String[] args) {
        Singleton singleton = Singleton.getInstance();
        singleton.showMessage();
    }
}


/*//Factorty Method // Abstract Product*/

public interface Animal {
    void speak();
}

/*// Concrete Product A*/
public class Dog implements Animal {
    @Override
    public void speak() {
        System.out.println("Woof!");
    }
}

/*// Concrete Product B*/
public class Cat implements Animal {
    @Override
    public void speak() {
        System.out.println("Meow!");
    }
}

/*// Creator*/
abstract class AnimalFactory {
    abstract Animal createAnimal();
}

/*// Concrete Creator A*/
class DogFactory extends AnimalFactory {
    @Override
    Animal createAnimal() {
        return new Dog();
    }
}

/*// Concrete Creator B*/
class CatFactory extends AnimalFactory {
    @Override
    Animal createAnimal() {
        return new Cat();
    }
}

public class FactoryMethodDemo {
    public static void main(String[] args) {
        AnimalFactory factory = new DogFactory();
        Animal animal = factory.createAnimal();
        animal.speak();  // Output: Woof!

        factory = new CatFactory();
        animal = factory.createAnimal();
        animal.speak();  // Output: Meow!
    }
}

/*//Abstract Factory Pattern // Abstract Products*/
interface Chair {
    void sitOn();
}

interface Table {
    void use();
}

/*// Concrete Product A1*/
class VictorianChair implements Chair {
    @Override
    public void sitOn() {
        System.out.println("Sitting on a Victorian chair.");
    }
}

/*// Concrete Product A2*/
class ModernChair implements Chair {
    @Override
    public void sitOn() {
        System.out.println("Sitting on a modern chair.");
    }
}

/*// Concrete Product B1*/
class VictorianTable implements Table {
    @Override
    public void use() {
        System.out.println("Using a Victorian table.");
    }
}

/*// Concrete Product B2*/
class ModernTable implements Table {
    @Override
    public void use() {
        System.out.println("Using a modern table.");
    }
}

/*// Abstract Factory*/
interface FurnitureFactory {
    Chair createChair();
    Table createTable();
}

/*// Concrete Factory A*/
class VictorianFurnitureFactory implements FurnitureFactory {
    @Override
    public Chair createChair() {
        return new VictorianChair();
    }

    @Override
    public Table createTable() {
        return new VictorianTable();
    }
}

/*// Concrete Factory B*/
class ModernFurnitureFactory implements FurnitureFactory {
    @Override
    public Chair createChair() {
        return new ModernChair();
    }

    @Override
    public Table createTable() {
        return new ModernTable();
    }
}

public class AbstractFactoryDemo {
    public static void main(String[] args) {
        FurnitureFactory factory = new VictorianFurnitureFactory();
        Chair chair = factory.createChair();
        Table table = factory.createTable();
        chair.sitOn();  /*// Output: Sitting on a Victorian chair.*/
        table.use();   /* // Output: Using a Victorian table.*/

        factory = new ModernFurnitureFactory();
        chair = factory.createChair();
        table = factory.createTable();
        chair.sitOn();  /*// Output: Sitting on a modern chair.*/
        table.use();    /*// Output: Using a modern table.*/
    }
}


/*//Builder Pattern // Product*/
class House {
    private String walls;
    private String roof;
    private String garden;

    public void setWalls(String walls) {
        this.walls = walls;
    }

    public void setRoof(String roof) {
        this.roof = roof;
    }

    public void setGarden(String garden) {
        this.garden = garden;
    }

    @Override
    public String toString() {
        return "House [walls=" + walls + ", roof=" + roof + ", garden=" + garden + "]";
    }
}

/*// Builder*/
abstract class HouseBuilder {
    protected House house = new House();

    abstract void buildWalls();
    abstract void buildRoof();
    abstract void buildGarden();

    House getHouse() {
        return house;
    }
}

/*// Concrete Builder*/
class ConcreteHouseBuilder extends HouseBuilder {
    @Override
    void buildWalls() {
        house.setWalls("Concrete Walls");
    }

    @Override
    void buildRoof() {
        house.setRoof("Concrete Roof");
    }

    @Override
    void buildGarden() {
        house.setGarden("Beautiful Garden");
    }
}

/*// Director*/
class HouseDirector {
    private HouseBuilder builder;

    public HouseDirector(HouseBuilder builder) {
        this.builder = builder;
    }

    public House constructHouse() {
        builder.buildWalls();
        builder.buildRoof();
        builder.buildGarden();
        return builder.getHouse();
    }
}

public class BuilderPatternDemo {
    public static void main(String[] args) {
        HouseBuilder builder = new ConcreteHouseBuilder();
        HouseDirector director = new HouseDirector(builder);
        House house = director.constructHouse();
        System.out.println(house); // Output: House [walls=Concrete Walls, roof=Concrete Roof, garden=Beautiful Garden]
    }
}


/*//Prototype Pattern // Prototype*/
abstract class Shape implements Cloneable {
    private String id;
    String type;

    abstract void draw();

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    @Override
    protected Object clone() {
        Object clone = null;
        try {
            clone = super.clone();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        return clone;
    }
}

/*// Concrete Prototype A*/
class Circle extends Shape {
    public Circle() {
        type = "Circle";
    }

    @Override
    void draw() {
        System.out.println("Drawing a Circle");
    }
}

/*// Concrete Prototype B*/
class Square extends Shape {
    public Square() {
        type = "Square";
    }

    @Override
    void draw() {
        System.out.println("Drawing a Square");
    }
}

/*// Prototype Registry*/
class ShapeCache {
    private static Map<String, Shape> shapeMap = new HashMap<>();

    public static Shape getShape(String shapeId) {
        Shape cachedShape = shapeMap.get(shapeId);
        return (Shape) cachedShape.clone();
    }

    public static void loadCache() {
        Circle circle = new Circle();
        circle.setId("1");
        shapeMap.put(circle.getId(), circle);

        Square square = new Square();
        square.setId("2");
        shapeMap.put(square.getId(), square);
    }
}

public class PrototypePatternDemo {
    public static void main(String[] args) {
        ShapeCache.loadCache();

        Shape clonedShape1 = ShapeCache.getShape("1");
        System.out.println("Shape : " + clonedShape1.type);
        clonedShape1.draw(); /*// Output: Drawing a Circle*/

        Shape clonedShape2 = ShapeCache.getShape("2");
        System.out.println("Shape : " + clonedShape2.type);
        clonedShape2.draw(); /*// Output: Drawing a Square*/
    }
}
```

## Structural patterns

Adapter Pattern

Purpose: Converts one interface to another that the client expects.
Use Case: When you need to use an existing class but its interface doesn't match the one you need.

```java
// Target interface
interface MediaPlayer {
    void play(String audioType, String fileName);
}

// Adaptee class (Existing class)
class VLCPlayer {
    public void playVLC(String fileName) {
        System.out.println("Playing VLC file. Name: " + fileName);
    }
}

// Adapter class
class MediaAdapter implements MediaPlayer {
    private VLCPlayer vlcPlayer;

    public MediaAdapter(String audioType) {
        if(audioType.equalsIgnoreCase("vlc")) {
            vlcPlayer = new VLCPlayer();
        }
    }

    @Override
    public void play(String audioType, String fileName) {
        if(audioType.equalsIgnoreCase("vlc")) {
            vlcPlayer.playVLC(fileName);
        }
    }
}

// Client class
class AudioPlayer implements MediaPlayer {
    private MediaAdapter mediaAdapter;

    @Override
    public void play(String audioType, String fileName) {
        if(audioType.equalsIgnoreCase("vlc")) {
            mediaAdapter = new MediaAdapter(audioType);
            mediaAdapter.play(audioType, fileName);
        } else {
            System.out.println("Invalid media. " + audioType + " format not supported");
        }
    }
}

public class AdapterPatternDemo {
    public static void main(String[] args) {
        AudioPlayer audioPlayer = new AudioPlayer();
        audioPlayer.play("vlc", "song.vlc");
    }
}

```

Bridge Pattern

Purpose: Separates the abstraction from the implementation, allowing both to vary independently.
Use Case: When you want to avoid a permanent binding between abstraction and its implementation.

```java
// Implementor
interface DrawAPI {
    void drawCircle(int radius, int x, int y);
}

// Concrete Implementor
class RedCircle implements DrawAPI {
    public void drawCircle(int radius, int x, int y) {
        System.out.println("Drawing Circle [color: red, radius: " + radius + ", x: " + x + ", y: " + y + "]");
    }
}

// Abstraction
abstract class Shape {
    protected DrawAPI drawAPI;

    protected Shape(DrawAPI drawAPI) {
        this.drawAPI = drawAPI;
    }

    public abstract void draw();
}

// Refined Abstraction
class Circle extends Shape {
    private int x, y, radius;

    public Circle(int x, int y, int radius, DrawAPI drawAPI) {
        super(drawAPI);
        this.x = x;
        this.y = y;
        this.radius = radius;
    }

    public void draw() {
        drawAPI.drawCircle(radius, x, y);
    }
}

public class BridgePatternDemo {
    public static void main(String[] args) {
        Shape redCircle = new Circle(100, 100, 10, new RedCircle());
        redCircle.draw();
    }
}

```

Composite Pattern

Purpose: Compose objects into tree-like structures to represent part-whole hierarchies.
Use Case: When clients need to treat individual objects and compositions uniformly.

```java
import java.util.ArrayList;
import java.util.List;

// Component
interface Employee {
    void showDetails();
}

// Leaf
class Developer implements Employee {
    private String name;
    private long empId;
    private String position;

    public Developer(String name, long empId, String position) {
        this.name = name;
        this.empId = empId;
        this.position = position;
    }

    @Override
    public void showDetails() {
        System.out.println(empId + " " + name);
    }
}

// Composite
class Manager implements Employee {
    private String name;
    private long empId;
    private String position;
    private List<Employee> subordinates;

    public Manager(String name, long empId, String position) {
        this.name = name;
        this.empId = empId;
        this.position = position;
        subordinates = new ArrayList<>();
    }

    public void addEmployee(Employee emp) {
        subordinates.add(emp);
    }

    @Override
    public void showDetails() {
        System.out.println(empId + " " + name);
        for (Employee emp : subordinates) {
            emp.showDetails();
        }
    }
}

public class CompositePatternDemo {
    public static void main(String[] args) {
        Employee dev1 = new Developer("John", 1001, "Developer");
        Employee dev2 = new Developer("Doe", 1002, "Developer");

        Manager manager = new Manager("Alice", 1003, "Manager");
        manager.addEmployee(dev1);
        manager.addEmployee(dev2);

        manager.showDetails();
    }
}

```

Decorator Pattern

Purpose: Adds additional functionality to objects dynamically.
Use Case: When you need to extend functionality of a class at runtime.

```java
// Component interface
interface Shape {
    void draw();
}

// Concrete component
class Circle implements Shape {
    public void draw() {
        System.out.println("Drawing Circle");
    }
}

// Decorator class
abstract class ShapeDecorator implements Shape {
    protected Shape decoratedShape;

    public ShapeDecorator(Shape decoratedShape) {
        this.decoratedShape = decoratedShape;
    }

    public void draw() {
        decoratedShape.draw();
    }
}

// Concrete decorator
class RedShapeDecorator extends ShapeDecorator {

    public RedShapeDecorator(Shape decoratedShape) {
        super(decoratedShape);
    }

    @Override
    public void draw() {
        decoratedShape.draw();
        setRedBorder(decoratedShape);
    }

    private void setRedBorder(Shape decoratedShape) {
        System.out.println("Border Color: Red");
    }
}

public class DecoratorPatternDemo {
    public static void main(String[] args) {
        Shape circle = new Circle();
        Shape redCircle = new RedShapeDecorator(circle);
        redCircle.draw();
    }
}

```

Facade Pattern

Purpose: Provides a simplified interface to a complex subsystem.
Use Case: When you need to make a complex system easier to use.

```java
// Subsystem classes
class CPU {
    public void start() {
        System.out.println("CPU started");
    }
}

class Memory {
    public void load() {
        System.out.println("Memory loaded");
    }
}

class HardDrive {
    public void read() {
        System.out.println("Hard Drive reading");
    }
}

// Facade class
class Computer {
    private CPU cpu;
    private Memory memory;
    private HardDrive hardDrive;

    public Computer() {
        cpu = new CPU();
        memory = new Memory();
        hardDrive = new HardDrive();
    }

    public void startComputer() {
        cpu.start();
        memory.load();
        hardDrive.read();
    }
}

public class FacadePatternDemo {
    public static void main(String[] args) {
        Computer computer = new Computer();
        computer.startComputer();
    }
}

```

Flyweight Pattern

Purpose: Reduces the cost of creating large numbers of similar objects by sharing as much data as possible.
Use Case: When you need to create a large number of objects, and want to reduce memory usage by sharing common state.

```java
import java.util.HashMap;

// Flyweight interface
interface Shape {
    void draw();
}

// Concrete Flyweight
class Circle implements Shape {
    private String color;
    private int x, y, radius;

    public Circle(String color) {
        this.color = color;
    }

    public void setX(int x) { this.x = x; }
    public void setY(int y) { this.y = y; }
    public void setRadius(int radius) { this.radius = radius; }

    @Override
    public void draw() {
        System.out.println("Drawing Circle [color: " + color + ", x: " + x + ", y: " + y + ", radius: " + radius + "]");
    }
}

// Flyweight Factory
class ShapeFactory {
    private static final HashMap<String, Shape> circleMap = new HashMap<>();

    public static Shape getCircle(String color) {
        Circle circle = (Circle) circleMap.get(color);

        if(circle == null) {
            circle = new Circle(color);
            circleMap.put(color, circle);
            System.out.println("Creating circle of color: " + color);
        }
        return circle;
    }
}

public class FlyweightPatternDemo {
    public static void main(String[] args) {
        Shape circle1 = ShapeFactory.getCircle("Red");
        circle1.draw();

        Shape circle2 = ShapeFactory.getCircle("Red");
        circle2.draw();
    }
}

```

Proxy Pattern

Purpose: Provides a surrogate or placeholder for another object to control access to it.
Use Case: When you want to control access to an object, like in lazy initialization or access control.

```java
// Subject interface
interface Image {
    void display();
}

// Real subject
class RealImage implements Image {
    private String fileName;

    public RealImage(String fileName) {
        this.fileName = fileName;
        loadFromDisk(fileName);
    }

    private void loadFromDisk(String fileName) {
        System.out.println("Loading " + fileName);
    }

    @Override
    public void display() {
        System.out.println("Displaying " + fileName);
    }
}

// Proxy class
class ProxyImage implements Image {
    private RealImage realImage;
    private String fileName;

    public ProxyImage(String fileName) {
        this.fileName = fileName;
    }

    @Override
    public void display() {
        if(realImage == null) {
            realImage = new RealImage(fileName);
        }
        realImage.display();
    }
}

public class ProxyPatternDemo {
    public static void main(String[] args) {
        Image image = new ProxyImage("test.jpg");
        image.display(); // First time loading
        image.display(); // Second time, no loading
    }
}

```

### Summary of Structural Patterns:
### Pattern ->	Purpose
Adapter	-> Converts one interface to another.  
Bridge	-> Separates abstraction from implementation.  
Composite	-> Composes objects into tree structures.  
Decorator	-> Adds behavior to objects dynamically.  
Facade	-> Provides a unified interface to a set of interfaces in a system.  
Flyweight	-> Reduces memory use by sharing as much data as possible.  
Proxy	-> Controls access to another object.  



## Behavioral Design Patterns in Java with Code Samples

Chain of Responsibility Pattern

Purpose: Passes a request along a chain of handlers where each handler decides either to process the request or pass it on.
Use Case: When multiple objects can handle a request, and the handler is determined at runtime.

```java
abstract class Logger {
    public static int INFO = 1;
    public static int DEBUG = 2;
    public static int ERROR = 3;

    protected int level;
    protected Logger nextLogger;

    public void setNextLogger(Logger nextLogger) {
        this.nextLogger = nextLogger;
    }

    public void logMessage(int level, String message) {
        if (this.level <= level) {
            write(message);
        }
        if (nextLogger != null) {
            nextLogger.logMessage(level, message);
        }
    }

    abstract protected void write(String message);
}

class ConsoleLogger extends Logger {
    public ConsoleLogger(int level) {
        this.level = level;
    }

    @Override
    protected void write(String message) {
        System.out.println("Console Logger: " + message);
    }
}

class FileLogger extends Logger {
    public FileLogger(int level) {
        this.level = level;
    }

    @Override
    protected void write(String message) {
        System.out.println("File Logger: " + message);
    }
}

public class ChainPatternDemo {
    private static Logger getChainOfLoggers() {
        Logger consoleLogger = new ConsoleLogger(Logger.INFO);
        Logger fileLogger = new FileLogger(Logger.DEBUG);

        consoleLogger.setNextLogger(fileLogger);
        return consoleLogger;
    }

    public static void main(String[] args) {
        Logger loggerChain = getChainOfLoggers();
        loggerChain.logMessage(Logger.INFO, "This is an informational message.");
        loggerChain.logMessage(Logger.DEBUG, "This is a debug message.");
    }
}

```

Command Pattern

Purpose: Encapsulates a request as an object, thereby allowing for parameterization of clients with different requests.
Use Case: When you need to issue requests to objects without knowing about the operation being requested.

```java
interface Command {
    void execute();
}

class Light {
    public void turnOn() {
        System.out.println("Light is ON");
    }

    public void turnOff() {
        System.out.println("Light is OFF");
    }
}

class TurnOnLightCommand implements Command {
    private Light light;

    public TurnOnLightCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.turnOn();
    }
}

class TurnOffLightCommand implements Command {
    private Light light;

    public TurnOffLightCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.turnOff();
    }
}

class RemoteControl {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void pressButton() {
        command.execute();
    }
}

public class CommandPatternDemo {
    public static void main(String[] args) {
        Light light = new Light();
        Command turnOn = new TurnOnLightCommand(light);
        Command turnOff = new TurnOffLightCommand(light);

        RemoteControl remote = new RemoteControl();
        remote.setCommand(turnOn);
        remote.pressButton();
        remote.setCommand(turnOff);
        remote.pressButton();
    }
}

```

Interpreter Pattern

Purpose: Provides a way to evaluate language grammar or expressions.
Use Case: When you need to interpret a specific language or notation.

```java
interface Expression {
    boolean interpret(String context);
}

class TerminalExpression implements Expression {
    private String data;

    public TerminalExpression(String data) {
        this.data = data;
    }

    @Override
    public boolean interpret(String context) {
        return context.contains(data);
    }
}

class OrExpression implements Expression {
    private Expression expr1;
    private Expression expr2;

    public OrExpression(Expression expr1, Expression expr2) {
        this.expr1 = expr1;
        this.expr2 = expr2;
    }

    @Override
    public boolean interpret(String context) {
        return expr1.interpret(context) || expr2.interpret(context);
    }
}

public class InterpreterPatternDemo {
    public static void main(String[] args) {
        Expression isJava = new TerminalExpression("Java");
        Expression isPython = new TerminalExpression("Python");

        Expression isProgrammingLanguage = new OrExpression(isJava, isPython);
        System.out.println("Does context contain Java or Python? " + isProgrammingLanguage.interpret("I love Java"));
    }
}

```


Iterator Pattern

Purpose: Provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
Use Case: When you need to traverse a collection without exposing its internal structure.

```java
interface Iterator {
    boolean hasNext();
    Object next();
}

interface Container {
    Iterator getIterator();
}

class NameRepository implements Container {
    public String names[] = {"John", "Jane", "Julie", "Jack"};

    @Override
    public Iterator getIterator() {
        return new NameIterator();
    }

    private class NameIterator implements Iterator {
        int index;

        @Override
        public boolean hasNext() {
            return index < names.length;
        }

        @Override
        public Object next() {
            if (this.hasNext()) {
                return names[index++];
            }
            return null;
        }
    }
}

public class IteratorPatternDemo {
    public static void main(String[] args) {
        NameRepository namesRepository = new NameRepository();
        Iterator iterator = namesRepository.getIterator();

        while (iterator.hasNext()) {
            String name = (String) iterator.next();
            System.out.println("Name: " + name);
        }
    }
}

```

Mediator Pattern

Purpose: Defines an object that encapsulates how a set of objects interact, promoting loose coupling.
Use Case: When you want to reduce communication complexity between objects.

```java
class ChatRoom {
    public static void showMessage(User user, String message) {
        System.out.println(user.getName() + ": " + message);
    }
}

class User {
    private String name;

    public User(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void sendMessage(String message) {
        ChatRoom.showMessage(this, message);
    }
}

public class MediatorPatternDemo {
    public static void main(String[] args) {
        User john = new User("John");
        User jane = new User("Jane");

        john.sendMessage("Hello Jane!");
        jane.sendMessage("Hi John!");
    }
}

```

Memento Pattern

Purpose: Captures the state of an object without exposing its internal structure, allowing it to be restored later.
Use Case: When you need to rollback to a previous state.
```java
class Memento {
    private String state;

    public Memento(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }
}

class Originator {
    private String state;

    public void setState(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }

    public Memento saveStateToMemento() {
        return new Memento(state);
    }

    public void getStateFromMemento(Memento memento) {
        state = memento.getState();
    }
}

class Caretaker {
    private List<Memento> mementoList = new ArrayList<>();

    public void add(Memento state) {
        mementoList.add(state);
    }

    public Memento get(int index) {
        return mementoList.get(index);
    }
}

public class MementoPatternDemo {
    public static void main(String[] args) {
        Originator originator = new Originator();
        Caretaker caretaker = new Caretaker();

        originator.setState("State #1");
        caretaker.add(originator.saveStateToMemento());

        originator.setState("State #2");
        caretaker.add(originator.saveStateToMemento());

        originator.getStateFromMemento(caretaker.get(0));
        System.out.println("First saved state: " + originator.getState());

        originator.getStateFromMemento(caretaker.get(1));
        System.out.println("Second saved state: " + originator.getState());
    }
}

```

Observer Pattern

Purpose: Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
Use Case: When an object should notify other objects without being tightly coupled to them.
```java
import java.util.ArrayList;
import java.util.List;

interface Observer {
    void update();
}

class Subject {
    private List<Observer> observers = new ArrayList<>();
    private int state;

    public int getState() {
        return state;
    }

    public void setState(int state) {
        this.state = state;
        notifyAllObservers();
    }

    public void attach(Observer observer) {
        observers.add(observer);
    }

    public void notifyAllObservers() {
        for (Observer observer : observers) {
            observer.update();
        }
    }
}

class ConcreteObserver implements Observer {
    private Subject subject;

    public ConcreteObserver(Subject subject) {
        this.subject = subject;
        this.subject.attach(this);
    }

    @Override
    public void update() {
        System.out.println("State changed to: " + subject.getState());
    }
}

public class ObserverPatternDemo {
    public static void main(String[] args) {
        Subject subject = new Subject();

        new ConcreteObserver(subject);
        new ConcreteObserver(subject);

        subject.setState(5);
        subject.setState(10);
    }
}

```


Behavioral Design Patterns in Java with Code Samples
Chain of Responsibility Pattern

Purpose: Passes a request along a chain of handlers where each handler decides either to process the request or pass it on.
Use Case: When multiple objects can handle a request, and the handler is determined at runtime.
java
Copy code
abstract class Logger {
    public static int INFO = 1;
    public static int DEBUG = 2;
    public static int ERROR = 3;

    protected int level;
    protected Logger nextLogger;

    public void setNextLogger(Logger nextLogger) {
        this.nextLogger = nextLogger;
    }

    public void logMessage(int level, String message) {
        if (this.level <= level) {
            write(message);
        }
        if (nextLogger != null) {
            nextLogger.logMessage(level, message);
        }
    }

    abstract protected void write(String message);
}

class ConsoleLogger extends Logger {
    public ConsoleLogger(int level) {
        this.level = level;
    }

    @Override
    protected void write(String message) {
        System.out.println("Console Logger: " + message);
    }
}

class FileLogger extends Logger {
    public FileLogger(int level) {
        this.level = level;
    }

    @Override
    protected void write(String message) {
        System.out.println("File Logger: " + message);
    }
}

public class ChainPatternDemo {
    private static Logger getChainOfLoggers() {
        Logger consoleLogger = new ConsoleLogger(Logger.INFO);
        Logger fileLogger = new FileLogger(Logger.DEBUG);

        consoleLogger.setNextLogger(fileLogger);
        return consoleLogger;
    }

    public static void main(String[] args) {
        Logger loggerChain = getChainOfLoggers();
        loggerChain.logMessage(Logger.INFO, "This is an informational message.");
        loggerChain.logMessage(Logger.DEBUG, "This is a debug message.");
    }
}
Command Pattern

Purpose: Encapsulates a request as an object, thereby allowing for parameterization of clients with different requests.
Use Case: When you need to issue requests to objects without knowing about the operation being requested.
java
Copy code
interface Command {
    void execute();
}

class Light {
    public void turnOn() {
        System.out.println("Light is ON");
    }

    public void turnOff() {
        System.out.println("Light is OFF");
    }
}

class TurnOnLightCommand implements Command {
    private Light light;

    public TurnOnLightCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.turnOn();
    }
}

class TurnOffLightCommand implements Command {
    private Light light;

    public TurnOffLightCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.turnOff();
    }
}

class RemoteControl {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void pressButton() {
        command.execute();
    }
}

public class CommandPatternDemo {
    public static void main(String[] args) {
        Light light = new Light();
        Command turnOn = new TurnOnLightCommand(light);
        Command turnOff = new TurnOffLightCommand(light);

        RemoteControl remote = new RemoteControl();
        remote.setCommand(turnOn);
        remote.pressButton();
        remote.setCommand(turnOff);
        remote.pressButton();
    }
}
Interpreter Pattern

Purpose: Provides a way to evaluate language grammar or expressions.
Use Case: When you need to interpret a specific language or notation.
java
Copy code
interface Expression {
    boolean interpret(String context);
}

class TerminalExpression implements Expression {
    private String data;

    public TerminalExpression(String data) {
        this.data = data;
    }

    @Override
    public boolean interpret(String context) {
        return context.contains(data);
    }
}

class OrExpression implements Expression {
    private Expression expr1;
    private Expression expr2;

    public OrExpression(Expression expr1, Expression expr2) {
        this.expr1 = expr1;
        this.expr2 = expr2;
    }

    @Override
    public boolean interpret(String context) {
        return expr1.interpret(context) || expr2.interpret(context);
    }
}

public class InterpreterPatternDemo {
    public static void main(String[] args) {
        Expression isJava = new TerminalExpression("Java");
        Expression isPython = new TerminalExpression("Python");

        Expression isProgrammingLanguage = new OrExpression(isJava, isPython);
        System.out.println("Does context contain Java or Python? " + isProgrammingLanguage.interpret("I love Java"));
    }
}
Iterator Pattern

Purpose: Provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
Use Case: When you need to traverse a collection without exposing its internal structure.
java
Copy code
interface Iterator {
    boolean hasNext();
    Object next();
}

interface Container {
    Iterator getIterator();
}

class NameRepository implements Container {
    public String names[] = {"John", "Jane", "Julie", "Jack"};

    @Override
    public Iterator getIterator() {
        return new NameIterator();
    }

    private class NameIterator implements Iterator {
        int index;

        @Override
        public boolean hasNext() {
            return index < names.length;
        }

        @Override
        public Object next() {
            if (this.hasNext()) {
                return names[index++];
            }
            return null;
        }
    }
}

public class IteratorPatternDemo {
    public static void main(String[] args) {
        NameRepository namesRepository = new NameRepository();
        Iterator iterator = namesRepository.getIterator();

        while (iterator.hasNext()) {
            String name = (String) iterator.next();
            System.out.println("Name: " + name);
        }
    }
}
Mediator Pattern

Purpose: Defines an object that encapsulates how a set of objects interact, promoting loose coupling.
Use Case: When you want to reduce communication complexity between objects.
java
Copy code
class ChatRoom {
    public static void showMessage(User user, String message) {
        System.out.println(user.getName() + ": " + message);
    }
}

class User {
    private String name;

    public User(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void sendMessage(String message) {
        ChatRoom.showMessage(this, message);
    }
}

public class MediatorPatternDemo {
    public static void main(String[] args) {
        User john = new User("John");
        User jane = new User("Jane");

        john.sendMessage("Hello Jane!");
        jane.sendMessage("Hi John!");
    }
}
Memento Pattern

Purpose: Captures the state of an object without exposing its internal structure, allowing it to be restored later.
Use Case: When you need to rollback to a previous state.
java
Copy code
class Memento {
    private String state;

    public Memento(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }
}

class Originator {
    private String state;

    public void setState(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }

    public Memento saveStateToMemento() {
        return new Memento(state);
    }

    public void getStateFromMemento(Memento memento) {
        state = memento.getState();
    }
}

class Caretaker {
    private List<Memento> mementoList = new ArrayList<>();

    public void add(Memento state) {
        mementoList.add(state);
    }

    public Memento get(int index) {
        return mementoList.get(index);
    }
}

public class MementoPatternDemo {
    public static void main(String[] args) {
        Originator originator = new Originator();
        Caretaker caretaker = new Caretaker();

        originator.setState("State #1");
        caretaker.add(originator.saveStateToMemento());

        originator.setState("State #2");
        caretaker.add(originator.saveStateToMemento());

        originator.getStateFromMemento(caretaker.get(0));
        System.out.println("First saved state: " + originator.getState());

        originator.getStateFromMemento(caretaker.get(1));
        System.out.println("Second saved state: " + originator.getState());
    }
}
Observer Pattern

Purpose: Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
Use Case: When an object should notify other objects without being tightly coupled to them.
java
Copy code
import java.util.ArrayList;
import java.util.List;

interface Observer {
    void update();
}

class Subject {
    private List<Observer> observers = new ArrayList<>();
    private int state;

    public int getState() {
        return state;
    }

    public void setState(int state) {
        this.state = state;
        notifyAllObservers();
    }

    public void attach(Observer observer) {
        observers.add(observer);
    }

    public void notifyAllObservers() {
        for (Observer observer : observers) {
            observer.update();
        }
    }
}

class ConcreteObserver implements Observer {
    private Subject subject;

    public ConcreteObserver(Subject subject) {
        this.subject = subject;
        this.subject.attach(this);
    }

    @Override
    public void update() {
        System.out.println("State changed to: " + subject.getState());
    }
}

public class ObserverPatternDemo {
    public static void main(String[] args) {
        Subject subject = new Subject();

        new ConcreteObserver(subject);
        new ConcreteObserver(subject);

        subject.setState(5);
        subject.setState(10);
    }
}
### Summary of Behavioral Patterns:
### Pattern	->Purpose
Chain of Responsibility -> 	Passes a request along a chain of handlers.  
Command ->	Encapsulates a request as an object.  
Interpreter ->	Defines a grammar and an interpreter for the language.    
Iterator	->Provides a way to access elements of a collection.  
Mediator	->Defines an object that coordinates interactions between peers.  
Memento	->Captures and restores an object's internal state.  
Observer	->Notifies dependent objects of state changes.  
State	->Allows an object to change its behavior when its state changes  
Strategy	->Encapsulates algorithms for interchangeability.  
Template ->Method	Defines a skeleton of an algorithm, deferring some steps.  
Visitor	->Separates algorithm from object structure.  

