# Concepts of Programming Languages

This document explores key programming language concepts such as Object-Oriented Programming (OOP) and Functional Programming, using code examples from a series of practical Flutter / Dart, C++ and JavaScript projects. Each section breaks down fundamental principles and demonstrates how they are applied in real-world scenarios. 

## Featured Projects
- **Node.js Movie API** ([GitHub Repository](https://github.com/ohalukkarakaya/node-movie-api)): A RESTful API for managing a movie database.
- **Flutter Weather Forecast App** ([GitHub Repository](https://github.com/ohalukkarakaya/flutter-weather-forecast/tree/master)): A responsive app for weather forecasting.
- **C++ Mongoose Library** ([GitHub Repository](https://github.com/ohalukkarakaya/cpp-mongoose)): A MongoDB schema manager built in C++.
- **Enigma Machine Simulation** ([GitHub Repository](https://github.com/ohalukkarakaya/Enigma-cpp)): A simulation of the Enigma encryption machine in C++.
- **CLI Slot Game** ([GitHub Repository](https://github.com/ohalukkarakaya/cli-slot-game)): A command-line slot machine game demonstrating functional programming concepts in C++.

## 📋 Table of Contents
- [<code>🧩 Fundamentals</code>](#-fundamentals)
- [<code>🏛️ Object-Oriented Programming</code>](#%EF%B8%8F-object-oriented-programming)
- [<code>🧑‍💻 Functional Programming</code>](#-functional-programming)

---

## 🧩 Fundamentals

### 1. Variables and Scoping

Variables in programming are fundamental for storing data, and their scope determines accessibility within various parts of the program.

- **Example in Node.js**: In the [Node Movie API](https://github.com/ohalukkarakaya/node-movie-api) project, local variables declared with `let` or `const` within routes (e.g., `routes/movies.js`) are accessible only within that function scope, preventing unintended access.
- **Example in Flutter**: In the [Flutter Weather Forecast App](https://github.com/ohalukkarakaya/flutter-weather-forecast/tree/master), variables like `weatherData` in `lib/screens/home.dart` are scoped to the widget, ensuring that each widget manages its own state independently.

### 2. Typing Systems (Static/Dynamic)

Typing systems define when and how variable types are checked.

- **Node.js (Dynamic Typing)**: JavaScript’s typing is dynamic, so variables can change types at runtime. For example, in the Node Movie API project, `let genre = 'Action';` could later be reassigned to a number if needed.
- **Flutter (Static Typing)**: Dart, used in Flutter, is statically typed, so types are determined at compile-time. In `lib/models/weather.dart`, fields like `final String description` ensure that `description` can only be a string, providing additional safety.

### 3. Type Inference

Type inference allows the compiler or interpreter to deduce variable types automatically.

- **Flutter**: Dart supports type inference, as seen in `var temperature = 23;` within the Weather Forecast project, where Dart infers `temperature` as an `int`.

## 🏛️ Object-Oriented Programming

### 1. Classes and Objects

Classes and objects are the core building blocks of OOP. Classes define data structure and behavior, while objects are instances of these classes.

#### Examples
- **C++ Mongoose Library**: In the [cpp-mongoose](https://github.com/ohalukkarakaya/cpp-mongoose) project, the `MongoSchema` class encapsulates the schema definition and operations for MongoDB collections. It manages CRUD operations, data validation, and index creation, providing a structured approach to interact with the database.
- **Enigma Machine Simulation**: The [Enigma-cpp](https://github.com/ohalukkarakaya/Enigma-cpp) project includes classes such as `Rotor`, `Reflector`, and `EnigmaMachine`. Each class represents a component of the Enigma machine, encapsulating specific behaviors and data, and working together to simulate the encryption and decryption processes.

### 2. Inheritance

Inheritance allows a class to inherit properties and behaviors from another class, promoting code reuse and establishing a hierarchical relationship between classes.

#### 1. Single and Multiple Inheritance
   - **Single Inheritance**: A class inherits from a single parent class, extending its functionality.
   - **Multiple Inheritance**: A class inherits from multiple parent classes, which is supported in C++ but can introduce complexity due to the "diamond problem."

#### Examples
- **Enigma Machine Simulation**: While the current implementation focuses on composition, an example of single inheritance could involve creating a base class `MachineComponent` with common attributes and methods, and then deriving `Rotor` and `Reflector` classes from it. This would allow shared functionality to be defined in the base class and specialized behaviors in the derived classes.
- **C++ Mongoose Library**: The [cpp-mongoose](https://github.com/ohalukkarakaya/cpp-mongoose) project is structured as a library with a base class `MongoSchema` that can be extended to define specific schemas. By inheriting from `MongoSchema`, users can create specialized schemas and override the `initializeSchema` and `validation` methods to tailor the schema to their needs.

   For example, let's say you want to create a `UserSchema` to manage user-related data. By inheriting from `MongoSchema`, you can create this specialized schema as follows:

   ```cpp
   #include "MongoSchema.h"

   class UserSchema : public MongoSchema {
   public:
       UserSchema() : MongoSchema("users") {
           // Custom constructor logic if needed
       }

   protected:
       // Initialize schema-specific configuration, like indexes or default values
       void initializeSchema(bsoncxx::document::view document) override {
           // Logic to initialize document-specific schema configurations
           // This could involve setting default values, creating additional fields, etc.
       }

       // Define validation logic specific to "User"
       bool validation() const override {
           // Define validation logic for User schema
           return true;  // Replace with actual validation checks
       }
   };
   ```
  In this example:
  
  *   `UserSchema` inherits from `MongoSchema`, passing `"users"` as the collection name.
  *   `initializeSchema` is overridden to allow schema-specific initialization, such as setting default values or custom configuration.
  *   `validation` is overridden to define validation rules specific to the `UserSchema`.

#### 2. Interface Inheritance and Abstract Classes

- **Abstract Classes**: These are classes that cannot be instantiated directly and are intended to be extended. They often contain pure virtual functions, providing a template for derived classes to implement specific behaviors.
- **Interface Inheritance**: In C++, abstract classes can serve as interfaces when they include only pure virtual methods. 

**Examples**
- **Enigma Machine Simulation**: In this project, an abstract class like `Encryptable` could represent an interface with methods for encryption and decryption. `Rotor` and `Reflector` classes could implement this interface, ensuring that all components in the machine follow a consistent interface for encryption.
- **C++ Mongoose Library**: In the **cpp-mongoose** project, `MongoSchema` acts as a base class with virtual methods like `initializeSchema` and `validation` that derived classes can override. This enables each schema, such as a hypothetical `UserSchema`, to define its specific initialization and validation rules, providing flexibility for various database models.

##### 3. Prototype-Based vs. Class-Based Inheritance

- **Class-Based Inheritance**: C++ uses class-based inheritance, with hierarchies defined explicitly in class relationships. 
- **Prototype-Based Inheritance**: While C++ doesn’t use prototype-based inheritance, you can use patterns like object cloning or factory functions to create reusable and dynamic object types.

**Examples**
- **Enigma Machine Simulation**: The project is inherently class-based, with `EnigmaMachine` composed of different components, such as `Rotor` and `Reflector`. This modular design allows specific machine configurations.
- **C++ Mongoose Library**: The class-based structure in `MongoSchema` allows for explicit inheritance, enabling new schemas to build upon and customize the generic database handling capabilities offered by the library.

#### 3. Polymorphism

Polymorphism allows for accessing different types through a common interface, enabling behaviors to vary depending on the object type at runtime.

##### Dynamic Dispatch and Late Binding
- **Dynamic Dispatch**: C++ uses virtual functions to achieve dynamic dispatch, where the function called on an object is determined at runtime.
- **Late Binding**: C++ virtual functions also implement late binding, where method implementation details are resolved at runtime.

**Examples**
- **Enigma Machine Simulation**: Polymorphism could be applied here by defining a base class `MachineComponent` with a virtual method like `processSignal`. Derived classes like `Rotor` and `Reflector` would override this method, allowing `EnigmaMachine` to process each component polymorphically based on its type.
- **C++ Mongoose Library**: The `MongoSchema` base class in **cpp-mongoose** includes virtual functions such as `validation` and `initializeSchema`. Derived classes can override these methods to customize their behavior, enabling polymorphic behavior for different schema types while ensuring a consistent API for MongoDB interactions.

## 🧑‍💻 Functional Programming 

The [`cli-slot-game`](https://github.com/ohalukkarakaya/cli-slot-game) repository demonstrates several functional programming concepts in C++.

### Pure Functions and Referential Transparency

Pure functions are those that, given the same input, always produce the same output without causing any side effects. In the [`cli-slot-game`](https://github.com/ohalukkarakaya/cli-slot-game), functions responsible for generating the slot machine's symbols and determining the outcome of a spin are designed to be pure. They rely solely on their input parameters and do not modify any external state, ensuring consistent behavior and referential transparency.

### Higher-Order Functions

Higher-order functions are functions that can take other functions as arguments or return them as results. In this project, the use of higher-order functions is evident in the implementation of the game's mechanics. For instance, functions that handle the animation of the slot reels may accept other functions as parameters to customize the behavior of the animation, such as the speed or pattern of the spin. This approach enhances the modularity and reusability of the code.

By adhering to functional programming principles, the [`cli-slot-game`](https://github.com/ohalukkarakaya/cli-slot-game) achieves a clean and maintainable codebase, facilitating easier testing and debugging.
