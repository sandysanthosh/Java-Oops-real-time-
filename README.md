
To design a system for a car dealership where cars can have different engines (e.g., petrol engine, electric engine), the goal is to ensure that engines can be swapped or replaced without modifying the car class. This scenario can be handled effectively using Object-Oriented Principles like Abstraction, Inheritance, and Polymorphism.

Here’s a breakdown of how to implement this system:

Key OOP Concepts

1. Abstraction: Abstract the concept of an engine, so we can have multiple types of engines.


2. Interface (or Abstract Class): Define an interface for engines that different types of engines will implement.


3. Dependency Injection: Inject the engine dependency into the car, allowing flexibility in changing the engine type.


4. Composition over Inheritance: A car "has an" engine, so we use composition to model this relationship, making the engine replaceable.



Design Steps

1. Define an Engine Interface

Create an Engine interface to represent the general behavior that all types of engines should have. This will allow you to define multiple engine types without changing the Car class.
```
// The Engine interface defines the contract for all types of engines
public interface Engine {
    void start();
    void stop();
    String getType();
}
```
2. Implement Different Engine Types

Now, create different concrete classes that implement the Engine interface, representing specific types of engines like PetrolEngine and ElectricEngine.
```
// A PetrolEngine class implementing the Engine interface
public class PetrolEngine implements Engine {
    @Override
    public void start() {
        System.out.println("Petrol engine is starting...");
    }

    @Override
    public void stop() {
        System.out.println("Petrol engine is stopping...");
    }

    @Override
    public String getType() {
        return "Petrol Engine";
    }
}

// An ElectricEngine class implementing the Engine interface
public class ElectricEngine implements Engine {
    @Override
    public void start() {
        System.out.println("Electric engine is starting...");
    }

    @Override
    public void stop() {
        System.out.println("Electric engine is stopping...");
    }

    @Override
    public String getType() {
        return "Electric Engine";
    }
}
```
3. Define the Car Class with an Engine Dependency

The Car class will have a reference to an Engine object. This allows the car to have any engine type without modifying the Car class itself.
```
// The Car class that contains a reference to an Engine
public class Car {
    private Engine engine; // The car "has an" engine

    // Constructor that accepts an Engine object (Dependency Injection)
    public Car(Engine engine) {
        this.engine = engine;
    }

    // Start the car using the current engine
    public void startCar() {
        System.out.println("Car is starting with " + engine.getType());
        engine.start();
    }

    // Stop the car using the current engine
    public void stopCar() {
        System.out.println("Car is stopping with " + engine.getType());
        engine.stop();
    }

    // Replace the car's engine with a different engine
    public void setEngine(Engine engine) {
        this.engine = engine;
        System.out.println("Engine replaced with: " + engine.getType());
    }
}
```
4. Using the Car and Engine Classes

You can now create Car objects with different types of engines, and swap the engine at runtime if needed:
```
public class CarDealershipApp {
    public static void main(String[] args) {
        // Create a car with a PetrolEngine
        Engine petrolEngine = new PetrolEngine();
        Car car = new Car(petrolEngine);

        // Start and stop the car
        car.startCar();
        car.stopCar();

        // Replace the car's engine with an ElectricEngine
        Engine electricEngine = new ElectricEngine();
        car.setEngine(electricEngine);

        // Start and stop the car with the new engine
        car.startCar();
        car.stopCar();
    }
}
```
Output:

```
Car is starting with Petrol Engine
Petrol engine is starting...
Car is stopping with Petrol Engine
Petrol engine is stopping...
Engine replaced with: Electric Engine
Car is starting with Electric Engine
Electric engine is starting...
Car is stopping with Electric Engine
Electric engine is stopping...
```
5. Extending the System

If you need to add more engine types, such as a HybridEngine or a DieselEngine, you just create a new class that implements the Engine interface:
```
// A HybridEngine class implementing the Engine interface
public class HybridEngine implements Engine {
    @Override
    public void start() {
        System.out.println("Hybrid engine is starting...");
    }

    @Override
    public void stop() {
        System.out.println("Hybrid engine is stopping...");
    }

    @Override
    public String getType() {
        return "Hybrid Engine";
    }
}
```
With this design, you do not need to modify the Car class to support new engines—just create a new engine class that implements the Engine interface.

Advantages of This Design

1. Loose Coupling: The Car class is not tightly coupled to any specific engine type. It only relies on the Engine interface.


2. Open/Closed Principle: You can extend the system by adding new engine types without modifying existing code.


3. Dependency Injection: The Engine is injected into the Car, making it easy to change the engine at runtime.


4. Reusability: The Engine implementations are reusable and can be plugged into any car that uses the Engine interface.



Possible Enhancements

1. Factory Pattern: Use a factory pattern to create engine instances if you have complex creation logic.


2. Strategy Pattern: The current implementation follows a strategy pattern because it allows switching the engine (strategy) at runtime.


3. Decorator Pattern: If you want to add more features to engines (like turbo mode), you can implement a decorator.



This modular design makes the system adaptable, maintainable, and easy to extend, following core OOP principles effectively.

