# SOLID Principles in Laravel

## **S - Single Responsibility Principle (SRP)**
> **Separate your application into small, focused classes**

Each class should have a single, well-defined responsibility. This makes the code easier to read, maintain, and modify without affecting other parts of the application.

### **Examples:**
1. **Form Request Classes:** Instead of validating data in controllers, use Laravel's `FormRequest` classes.
2. **Service Layer:** Move business logic from controllers to service classes. 
   - The service class should not directly interact with the request, only with the necessary data passed to it.
3. **Using Model Boot Method:**
   - Define model-related methods and attributes inside the model's `boot()` method.

### **Best Structure:**
- Use **DTOs (Data Transfer Objects)** to structure incoming data.
- In controllers, create DTOs from requests and pass them to services.
- Services interact with **repositories** (using the Repository Pattern) for CRUD operations.
- Always use **try-catch** in services to ensure a robust service-based architecture.

---

## **O - Open/Closed Principle (OCP)**
> **Your code should be open for extension but closed for modification.**

### **What violates OCP?**
- **Excessive `if-else` or `switch-case` statements**, especially when they control behavior that might change in the future.

### **Better Approach:**
- Use **interfaces** and **subclasses** to encapsulate different behaviors.
- Instead of modifying core code, define a **new class** that implements the necessary interface and configure Laravel to use it.
- For example, instead of modifying a package inside `vendor/`, extend the class or define a new implementation and configure it via `config/service provider`.

### **Example:**
#### **Salary Calculation for Different Roles**
Instead of handling different salary calculations inside a single `Employee` model:
1. Create a `Calculators` folder inside `app/`.
2. Define classes like `DeveloperSalaryCalculator` and `DesignerSalaryCalculator`.
3. Each class implements a `SalaryCalculatorInterface` with a `calculate()` method.
4. Use an **associative array** in the model to map personnel types to their respective calculators.

---

## **L - Liskov Substitution Principle (LSP)**
> **A subclass should be able to replace its parent class without breaking functionality.**

To follow LSP:
- Use **type hints** in method parameters and return types.
- If a new parameter is needed in one subclass:
  1. **Provide a default value** in that specific class.
  2. **Add the parameter to all related classes and interfaces**.
- If a method is required only in a specific subclass, either:
  - **Make it private** (if it’s not needed elsewhere), or
  - **Implement it in all subclasses and the interface**.

> **Key SOLID question:** _What if someone changes this in the past or future?_

---

## **I - Interface Segregation Principle (ISP)**
> **A class should not be forced to implement methods it does not need.**

### **Example in Laravel:**
- Laravel's `User` model implements `Authenticatable`, which provides authentication methods.
- If a class implements an interface but does not use all its methods, **split the interface into smaller, more specific interfaces**.

### **Common Violation:**
- If you implement an interface but some methods are not applicable (e.g., returning an error or throwing an exception for an unused method), **this violates ISP**.
- Instead, create **separate interfaces** for different responsibilities.

---

## **D - Dependency Inversion Principle (DIP)**
> **High-level modules should not depend on low-level modules. Both should depend on abstractions.**

- **Abstractions should not depend on details; details should depend on abstractions.**

### **Example in Laravel:**
- Instead of injecting concrete child classes into controllers, inject an **interface**.
- Use **Dependency Injection (DI)** by type-hinting the interface in the controller's constructor.
- Register the interface binding in a **service provider**, ensuring that every time the interface is requested, the appropriate child class is instantiated.

### **Conditional Dependency Injection:**
- In the service provider, instantiate different implementations based on the environment:
  - **Local environment:** Use a `Test` implementation.
  - **Production environment:** Use the real implementation.

This ensures flexibility and scalability while maintaining clean and maintainable code.
