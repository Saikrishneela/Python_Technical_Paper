SOLID Principles in Python: A Technical Perspective
Abstract

The SOLID principles are a set of five design guidelines that help developers build maintainable, extensible, and testable software. Originally introduced by Robert C. Martin (Uncle Bob), they are widely applied in object-oriented programming. This paper discusses each principle in detail, contextualized within Python, and provides practical code examples.

1. Introduction

Software design often suffers from issues like tight coupling, rigidity, and poor readability. The SOLID principles provide a framework to avoid these pitfalls:

S – Single Responsibility Principle (SRP)

O – Open/Closed Principle (OCP)

L – Liskov Substitution Principle (LSP)

I – Interface Segregation Principle (ISP)

D – Dependency Inversion Principle (DIP)

Although Python is a dynamically typed language and more flexible than strictly object-oriented languages like Java or C#, SOLID principles still apply and greatly improve software quality.


2. Single Responsibility Principle (SRP)

Definition:
A class should have only one reason to change. In other words, it should do one thing only.
A class only one job to do Respectively Each class have only one change or one operation to do

EXAMPLE CODE:
--------------------

# SOLIDS


class baker:
    def bakemaker(self):
        print("I bake cake")


class manage:
    def manager(self):
        print("i manage the staff")


class delivery:
    def deliveryPerson(self):
        print("I deliver the cake")


def main():
    b = baker()
    m = manage()
    d = delivery()
    b.bakemaker()
    m.manager()
    d.deliveryPerson()


if __name__ == "__main__":
    main()


3. Open/Closed Principle (OCP)

Definition:
Software entities should be open for extension but closed for modification.

class AreaCalculator:
    def area(self, shape):

        if isinstance(shape, Circle):
            return 3.14 * shape.radius ** 2

        elif isinstance(shape, Rectangle):
            return shape.width * shape.height

4. Liskov Substitution Principle (LSP)

Payment System--

class Payment:
    def pay(self, amount: float):
        print(f"Paid {amount} using default payment method")
        

class CreditCardPayment(Payment):
    def pay(self, amount: float):
        print(f"Paid {amount} using Credit Card")
        

class CashPayment(Payment):
    def pay(self, amount: float):
        print(f"Paid {amount} in cash")
        

class CouponPayment(Payment):
    def pay(self, amount: float):
        raise Exception("Coupons cannot be used for direct payments")


Refactored --

from abc import ABC, abstractmethod

class PaymentMethod(ABC):
    @abstractmethod
    def pay(self, amount: float):
        pass


class Redeemable(ABC):
    @abstractmethod
    def redeem(self, amount: float):
        pass


class CreditCardPayment(PaymentMethod):
    def pay(self, amount: float):
        print(f"Paid {amount} using Credit Card")
        

class CashPayment(PaymentMethod):
    def pay(self, amount: float):
        print(f"Paid {amount} in cash")
        

class Coupon(Redeemable):
    def redeem(self, amount: float):
        print(f"Redeemed coupon worth {amount}")

5. Interface Segregation Principle (ISP)

📖 Definition of ISP

Formal definition (by Robert C. Martin, Uncle Bob):
"Clients should not be forced to depend upon interfaces that they do not use."

Simplified definition:
Instead of creating one big interface (or abstract class) with lots of methods, we should split it into smaller, role-specific interfaces.
This ensures that classes only implement what they actually need.

✅ Key Points

Avoid “fat” interfaces

Large interfaces force classes to implement irrelevant methods.

This creates unnecessary coupling and often leads to dummy implementations (like raise Exception("Not supported")).

Favor smaller, specific interfaces

Break down big interfaces into multiple smaller ones.

A class should only implement the interfaces relevant to its behavior.

Improves maintainability

Changes to one part of the interface don’t ripple into unrelated classes.

Easier to extend and test.

⚡ Example (Violation of ISP)

from abc import ABC, abstractmethod

class Worker(ABC):
    @abstractmethod
    def work(self):
        pass

    @abstractmethod
    def eat(self):
        pass


class HumanWorker(Worker):
    def work(self):
        print("Human working")

    def eat(self):
        print("Human eating lunch")


class RobotWorker(Worker):
    def work(self):
        print("Robot working")

    def eat(self):
        raise Exception("Robots do not eat!")  # ❌ Irrelevant
    

✅ Refactored (ISP Applied)

from abc import ABC, abstractmethod

class Workable(ABC):
    @abstractmethod
    def work(self):
        pass


class Eatable(ABC):
    @abstractmethod
    def eat(self):
        pass


class HumanWorker(Workable, Eatable):
    def work(self):
        print("Human working")

    def eat(self):
        print("Human eating lunch")


class RobotWorker(Workable):
    def work(self):
        print("Robot working")

6. Dependency Inversion Principle (DIP)

📖 Definition --

The Dependency Inversion Principle is the last principle in SOLID.

Formal definition (Robert C. Martin):
"High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions."

Simplified definition:

Don’t make your core (high-level) logic depend directly on concrete implementations (low-level details).

Instead, make both depend on abstractions (interfaces or abstract base classes).

This decouples your system and makes it easier to swap implementations.

✅ Key Ideas
-----------------
High-level modules → contain business rules (e.g., OrderProcessor).

Low-level modules → deal with details (e.g., MySQLDatabase, FileLogger).

Instead of high-level modules directly calling low-level modules, both should communicate through abstract contracts.

Makes it easy to change implementations without touching core business logic.

Violation of DIP---

class MySQLDatabase:
    def connect(self):
        print("Connecting to MySQL Database")


class DataProcessor:
    def __init__(self):
        self.db = MySQLDatabase()  #  Direct dependency

    def process(self):
        self.db.connect()
        print("Processing data")

DIP Applied ---

from abc import ABC, abstractmethod

class Database(ABC):
    @abstractmethod
    def connect(self):
        pass


class MySQLDatabase(Database):
    def connect(self):
        print("Connecting to MySQL Database")


class PostgreSQLDatabase(Database):
    def connect(self):
        print("Connecting to PostgreSQL Database")
        

class DataProcessor:
    def __init__(self, db: Database):  # depends on abstraction
        self.db = db

    def process(self):
        self.db.connect()
        print("Processing data")

------------------------------------------------------------------------------------------

Conclusion on SOLID Principles in Python

The SOLID principles serve as a foundation for writing clean, maintainable, and extensible object-oriented code. While Python is a dynamically typed language and allows great flexibility, applying these principles leads to more robust and testable designs.

🔹 1. Single Responsibility Principle (SRP)

A class should have only one reason to change.

Keeps classes small, focused, and easier to understand.

Example: Separate a Report generator from a ReportSaver.

🔹 2. Open/Closed Principle (OCP)

Open for extension, closed for modification.

Add new behavior without altering existing code.

Example: Adding new Shape classes instead of modifying an AreaCalculator.

🔹 3. Liskov Substitution Principle (LSP)

Subtypes must be substitutable for their base types without breaking correctness.

Prevents unexpected exceptions and broken behavior.

Example: An Ostrich should not inherit from a FlyingBird.

🔹 4. Interface Segregation Principle (ISP)

No client should be forced to implement methods it doesn’t use.

Break down large interfaces into smaller, role-specific ones.

Example: Split Worker into Workable, Eatable, and Sleepable.

🔹 5. Dependency Inversion Principle (DIP)

High-level modules should not depend on low-level modules; both should depend on abstractions.

Makes systems flexible, testable, and easy to extend.

Example: DataProcessor depending on an abstract Database instead of MySQLDatabase.

