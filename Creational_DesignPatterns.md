Creational Design Patterns

1. Singleton: Ensures a class has only one instance and provides a global point of access to it.
2. Factory Method: Provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.
3. Abstract Factory: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.
4. Builder: Separates the construction of a complex object from its representation so that the same construction process can create different representations.
5. Prototype: Creates new objects by copying an existing object, known as the prototype.

''' Java
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

