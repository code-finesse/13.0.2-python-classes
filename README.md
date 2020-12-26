# 13.0.2-python-classes

## OOP in Python

- objects are intuitive and modeling things in programming is easy for both developers and computers to understand
- with object oriented programming we can group relevant data and functions into objects, grouping together related data (encapsulation)
- objects manage complexity by hiding all but the most relevant/high level data about an object, whose internal details are hidden because they aren't necessary for users (abstraction)
- objects can be in control of their own data and can stay consistent
- objects are modular and can interact with each other in well-defined ways
    - this allows us to refactor objects without causing bugs in other areas or our programs
- classes can inherit data from other classes and extend attributes while maintaining flexibility by still being able to be refactored

## How to Make a Class

- basic javascript class

```jsx
class User {
    constructor(name){
        this.name = name
    }
    # functions inside of a class is a method
    greet(){
        console.log("Hi my name is ${this.name}.")
        # do a dope handshake
        # our pet is goin HAM
        # some other stuff is also poppin off

        # abstraction is the ability to use an element to accomplish a task but not necessarily understanding how the element accomplishes the task
    }
}
# encapulation is hiding some parts of code from other parts of code so classes can't interfere with each other (like scope)

const Finesse = {
    name: "Finesse"
}

# will not work because greet is a method of the User class
Finesse.greet()
# Finesse is not an instance of the User class

const me = new User('Ya Boi')
me.greet()
```

- basic python class

```python
class User:
    # dunder is two underscores
    # this is a constructor
    def __init__(self, name):
    # python needs to be explicitly told "self" so it knows to refer to itself (like this but in javasript this is implicit and it already knows)
        self.name = name

    def greet(self):
        # self needs to be passed into class functions everytime when refering to itself
        print(f"Hi my name is {self.name}")

me = User("Finesse")

me.greet()
```

- extra example

### dictionaries vs objects

### .__dict__

## Inheritance in Python

- inheritance allows us to build new classes out of old classes
- we can extend functionality defined by a parent class and create children classes that extend and compartmentalized different pieces of functionality
- we can define one general class to model something and then inherit the methods and properties of the class to make new classes out of the first

## Inheritance Syntax

```python
# create a class
class Phone:
    def __init__(self, phone_number):
        self.phone_number = phone_number
        self.hello = 'wassup'

    def call(self, other_number):
        print(f"{self.phone_number} is calling {other_number}")
    def text(self, other_number, message):
        print(f"{self.phone_number} is sending a message to {other_number}. Incoming message is \n{message}.")

boring_phone = Phone(18005558888)

# "extension"
class iPhone(Phone):
    def __init__(self, phone_number):
        super().__init__(phone_number)
        self.finger_print = None
    
    def set_fingerprint(self, finger_print):
        self.finger_print = finger_print
    def unlock(self, finger_print):
        if self.finger_print == finger_print:
            print(f"iPhone Unlocked")
        else:
            print(f"Fingerprint does not match")

iphone = iPhone(8883001000)

class Android(Phone):
    def __init__(self, phone_number):
        super().__init__(phone_number)
        self.keyboard = "Default"

    def set_keyboard(self, keyboard):
        self.keyboard = keyboard
        print(f"Your keyboard is now set to {self.keyboard}")
    
    def update_helo(self, new_hello):
        self.hello = new_hello
        print(f"Your hello message is now set to {self.hello}")

    def call(self, other_number):
        print(f"Android phone is calling {other_number}")

android = Android(1234567890)
```

There are two new pieces of syntax used in the code above:

1. Class definitions can accept a parameter specifying what class they inherit from.
2. Child classes can invoke a method called `super()` to gain access to methods defined in the parent class and execute them.

Take another look at the Phone classes to see how these pieces of syntax are used to define how the classes define their inheritance and how the `super()` method is used.

Notice how the Android class doesn't repeat the code that attaches the phone_number passed to the `__init__` method to the `self` reference. The Android class calls the parent constructor through the `super()` method and allows the parent class to execute that default behavior.

- extra example

## Dunder Methods

- TLDR

There is a special (or a "magic") method for every operator sign. The magic method for the "+" sign is the `__add__` method. For "-" it is `__sub__` and so on. We have a complete listing of all the magic methods a little further down.

The mechanism works like this: If we have an expression "x + y" and x is an instance of class K, then Python will check the class definition of K. If K has a method `__add__` it will be called with `x.__add__(y)`, otherwise we will get an error message:

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/44bfc56d-83b9-4cac-8280-c7f7a8ec36da/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/44bfc56d-83b9-4cac-8280-c7f7a8ec36da/Untitled.png)

```
Traceback (most recent call last):
  File "", line 1, in 
TypeError: unsupported operand type(s) for +: 'K' and 'K'
```

A special attribute of every module is __dict__. This is the dictionary containing the module’s symbol table.

```
object.__dict__
```

A dictionary or other mapping object used to store an object’s (writable) attributes.

```python
class BankAccount:
    def __init__(self, name, type):
        self.name = name
        self.type = type
        self.balance = 0
        self.overdraft_fees = 0

    def withdraw(self, amount):
        if self.balance - amount >= 0:
            self.balance -= amount
            print(f"${self.balance} left in {self.type}")
            return self.balance
        else:
            if self.overdraft_fees >= 100:
                print(f"Your current overdraft fee is ${self.overdraft_fees} and you have reached your limit")
                return self.overdraft_fees
            else:
                self.overdraft_fees += 20
                print(f"Your current balance is ${self.balance} and too low to withdraw.")
                return self.overdraft_fees
    def deposit(self, amount):
        self.balance += amount
        print(f"${self.balance} left in {self.type}")
        return self.balance

    # dunder methods are used to allow different classes to "work together"

    # to be able to print it out as a string
    def __str__(self):
        return self.balance

    # for debugging?????
    def __repr__(self):
        return f"BankAccount('{self.type}')"
    
    # to be able to add
    def __add__(self, other):
        return self.balance + other.balance
    
    # to be able to subtract
    def __sub__(self, other):
        return self.balance - other.balance
    
    # to be able to multiply
    def __mul__(self, other):
        return self.balance * other.balance
    
    # to be able to divide
    def __truediv__(self, other):
        return self.balance / other.balance

    # to check if one account balance is greater than the other
    def __gt__(self, other):
        return self.balance > other.balance

    # to check if one account balance is greater than the other
    def __lt__(self, other):
        return self.balance < other.balance

    # to check if one account balance is greater than the other
    def __eq__(self, other):
        return self.balance == other.balance

savings = BankAccount("Mattress", "savings")
checking = BankAccount("Shoe Box", "checking")
```
