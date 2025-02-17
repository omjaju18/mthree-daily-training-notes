# SOLID Principles - Simple Explanation with Amazon Website Example

## What is SOLID?
SOLID is an acronym for five object-oriented design principles that help software be **more maintainable**, **flexible**, and **easier to understand**. The principles are:

1. **S**ingle Responsibility Principle (SRP)
2. **O**pen/Closed Principle (OCP)
3. **L**iskov Substitution Principle (LSP)
4. **I**nterface Segregation Principle (ISP)
5. **D**ependency Inversion Principle (DIP)

![image](https://github.com/user-attachments/assets/2c285c26-d0ac-4d44-a2fe-8e8f7f98a4aa)


## Principles with Simple Explanation and Amazon Example

### 1. **Single Responsibility Principle (SRP)**
- **Meaning:** A class should do only **one thing**.
- **Amazon Example:**  
  - The `Order` class only handles the tasks related to orders (e.g., processing orders, adding items to cart).  
  - It should **not** handle unrelated tasks like sending emails or displaying order details. These tasks should be in separate classes.

### 2. **Open/Closed Principle (OCP)**
- **Meaning:** You should be able to **add new features** without changing the existing code.
- **Amazon Example:**  
  - Imagine adding a new payment option, like **Google Pay**. Instead of changing the whole payment processing system, we can simply extend it by adding a new class for **Google Pay** that fits into the existing system.

### 3. **Liskov Substitution Principle (LSP)**
- **Meaning:** You should be able to replace an object with its subclass, and it should still work correctly.
- **Amazon Example:**  
  - If you replace the `CreditCardPayment` class with the `PayPalPayment` class, everything should still work as expected.  
  - If replacing a class causes issues, that would violate this principle.

### 4. **Interface Segregation Principle (ISP)**
- **Meaning:** Don’t force a class to implement things it **doesn’t need**.
- **Amazon Example:**  
  - If a shipping method only needs to **track orders**, it should only implement the `TrackableShipping` interface.
  - There’s no need to force it to implement other methods (like changing addresses) that are irrelevant to it.

### 5. **Dependency Inversion Principle (DIP)**
- **Meaning:** High-level classes should depend on **abstractions**, not low-level classes.
- **Amazon Example:**  
  - The `Cart` class should depend on an abstraction like the `IPayment` interface, not on specific classes like `CreditCardPayment` or `PayPalPayment`.  
  - This makes it easy to add new payment methods without modifying the `Cart` class.

---

## Summary of SOLID with Amazon Example

| **SOLID Principle**  | **What it Means** | **Amazon Example** |
|----------------------|-------------------|--------------------|
| **SRP**              | A class should do one job. | The `Order` class only handles order tasks, not email or display tasks. |
| **OCP**              | Add new features without changing old code. | Add a new payment method (e.g., Google Pay) without changing the entire payment system. |
| **LSP**              | Subclasses should work like the parent class. | You can replace `CreditCard` with `PayPal` without breaking payment processing. |
| **ISP**              | Don’t force classes to do things they don’t need. | A shipping method should only implement the methods that are relevant to it. |
| **DIP**              | High-level classes depend on abstractions. | The `Cart` class should depend on the `IPayment` interface, not specific payment methods. |

---
