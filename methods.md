# Methods

## Benefits of Methods
### Code Reuse
- If theres a bug in the function you only have to fix it in one place
- You only have to write the section of code once
- Fixing/ Changing things is easy

### Organization
- Makes understanding code easier
- moving/ reordering code is much easier


### Abstraction
- Allows other users to use your code without understanding how to impliment it
- The code is easier to read and understand

## Single Responsibility Principle
- Every class or method shoulg have responsibility over a single part of the programs functionality
- Code breaking or changing in one area should not break code in other areas

### BEFORE:
```
string firstname, lastname;
int age;
bool valid;

do
{
    Console.Write("Enter your first name: ");
    firstname = Console.ReadLine();
}while (string.IsNullOrEmpty(firstname));

do
{
    Console.Write("Enter your last name: ");
    lastname = Console.ReadLine();
}while(string.IsNullOrEmpty(lastname));

valid = false;
do
{
    Console.Write("Enter your age: ");
    if(!int.TryParse(Console.ReadLine(), out age))
    {
        Console.WriteLine("That wasn't a number!");
    }
    else
    {
        if (age > 0)
        {
            valid = true;
        }
        else
        {
            Console.WriteLine("Age must be positive. ");
        }
    }
}while(!valid);

Console.WriteLine($"First name: {firstname}");
Console.WriteLine($"Last name: {lastname}");
Console.WriteLine($"Age: {age}");
```
- IsNullOrEmpty() --> boolean that checks for value

### Refactored with Methods and SRP
```
class Program
{
    public static string GetRequiredString(string prompt)
    {
        string input;

        do
        {
            Console.Write(prompt);
            input = Console.ReadLine();
        } while(string.IsNullOrEmpty(input));

        return input;
    }

    public static int GetPositiveInteger(string prompt)
    {
        bool valid = false;
        int value;

        do
        {
            Console.Write(prompt);
            if(!int.TryParse(Console.ReadLine(), out value))
            {
                Console.WriteLine("That wasn't a number!");
            }
            else
            {
                if (value > 0)
                {
                    valid = true
                }
                else
                {
                    Console.WriteLine("Value must be positive.")
                }
            }
        }while(!valid);
        return value;
    }

    static void Main(string[] args)
    {
        string firstname = GetRequiredString("Enter your first name: ");
        string lastname = GetRequiredString("Enter your last name: ")
        int age = GetPositiveInteger("Enter your age: ");

        Console.WriteLine($"First name: {firstname}");
        Console.WriteLine($"Last name: {lastname}");
        Console.WriteLine($Age: {age});
    }
}
```
#### Breakdown of the above:
- public = acces modifier = ruleset for what other types can access this method.
    - public = Any other type can invoke this
    - private = Only other Program types would be able to invoke this.
- static =
    - Use when there is common behavior across all instances and it does not depend on object-specific data.
    - Used for utility or helper methods.
    - Use to make only one instance instead of many simular instances.
- String =
    - what type to expect the method to return if it returns a value
    - creates a promise that must be fulfilled
    - if a method won't return a value we use void in this spot
- GetRequiredString =
    - method name
    - should be proper cased
- (string prompt) =
    - arguments/ the data that the method will recieve

#### Important Tips
- methods = function members
    - function members must exist in a type definition AKA class
- Invoking =
    - in the same type = just use name
        ```
        string firstname = GetRequiredString("...")
        ```
    - static && in a different type= use dot notation to specify the type
        ```
        Program.GetRequiredString("...")
        ```
    - !static && another type = instantiate an object

        ```
        Program p = new Program();
        p.GetRequiredString("...")
        ```

## Structure

### Questions to figure out structure
- Where should this method be accessible from?
    - It should be accessible from any part of the code base and from any external assemblies
        - Public
    - It will only be used inside of the class its instantiated in, its going to be a helper method specific to the internal workings of THIS class
        - Private
    - It should be accessible by subclasses of this class. It will allow overridden methods or specific modifiable functionality
        - Protected
    - It should be accessible to other code in this assembly (program) but not to outside assemblies (orograms). For example it should not be exposed externally as part of the API
        - Internal

- Does this method need access to the instance fields (state) or instance methods of the class to perform its task?
    - No, the functionality is independent of any particular object and it can be invoked directly on the class itself
        - static
    - Yes, the method needs to access or modify instance-specific data or will need to call on other instance methods. It is tied in some way to an instance of the class
        - instance
- Are we going to return a value? and if so what are we returning?
    - No return
        - void
    - yes, primitive type
        - int, bool, or char
    - yes, an object or complex type
        - name of that class or structure
        - EX: Customer
    - yes, a collection or multiple things
        - int[]
        - List<Customer>
        - Dictionary<int, string>
    - yes, a promise
        - return with data Task<T>
        - return no data Task
- What is this method going to do?
    - Something short, descriptive, and CorrectCased for name
    - GetPositiveInteger
- Does this method need any data passed in to perform its actions?
    - Yes, specify the type and name
    - No, empty parenthesis

### Anatomy of the method declaration

> [access modifier][static][return type]\[Name]([parameters]){}

#### Access Modifiers
- determines what can access the method
- optional
    - if omitted defaults to the most restrictice option
- types:
    - Public
        - accessed by any other code in this assembly or others
    - Private
        - Only accessed by other code within the same type
    - Protected
        - only within the same type or types that inherit from it
    - Internal
        - only accessed within this assembly
    - Protected Internal
        - combines protected's same type/ children of type rule with Internal's only in this assembly rule

#### Static
- optional
- makes the member accessible without a new object instance
- Useful in these cases:
    - When theres only ever one instance of the type, like Console
    - The method is general purpose and does not save data between calls

#### Return Type
- If a method returns a value, it has to be declared and the method is required to ALWAYS return that value type
    - if it isnt returned you'll see a not all code paths return a value compiler error

```
public void SayHello()
{
    Console.WriteLine("Hello, world!");
}
```
- when theres no return value use void
    - there will be no return statement generally
    - empty return statements can be used to leave a method early
```
public void Divide(Book book, Borrower person)
{
    if (book.IsReserved() || person.HasOutstandingFees())
    {
        return;
    }
    book.Checkout()
}
```
- When a method does return a value
    - it must be specified in the signature
    - something of a compatible type HAS to be returned
    - null is compatible with all types
    - Exceptions are also allowable for all types
```
public Employee Get EmployeeInformation(int employeeID)
{
    if(!Employee.has(employeeId)) return null
}
```

#### Method Names and Overloading
- Names
    - Proper cased
    - Cannot start with a number
    - Cannot contain symbols
    - Do not have to be unique with a type
    - combination of name and parameters must be unique
- Overloading
    - Same name, different parameters
    ```
    public class Calculator
    {
        public int Add(int x, int y)
        {
            return x + y
        }

        public int Add(int x, int y, int z)
        {
            return x + y + z
        }

        public decimal Add(decimal x, decimal y)
        {
            return x + y
        }
    }
    ```
####  Parameters
- must be declared with a type that will be strictly enforced
- we make parameters optional with the following strategies:
    - Overloading
    ```
    public class Calculator
    {
        public int Add(int x, int y)
        {
            return x + y
        }
        public int Add(int x, int y, int z)
        {
            return x + y + z
        }
    }
    ```
    - Default Value
        - allow the invoker to skip providing a value
        - comes at the end of the parameter list
        ```
        public class Calculator
        {
            public int Add(int x, int y, int z = 0)
            {
                return x + y + z
            }
        }
        ```
    - out keyword
        - allows us to send out a value in a parameter in addition to the return value

        ```
        public bool SafeDivide(int x, int y, out int result)
        {
            if (y != 0)
            {
                result = x / y;
                return true
            }
            else
            {
                result = 0;
                return false;
            }
        }
        ```
        - the output variable is usable by the invoker
        ```
        int quotient;

        if(SafeDivide(5, 0, out quotient))
        {
            Console.WriteLine($"The result is {quotient}")
        }
        else
        {
            Console.WriteLine("Could not divide those two numbers")
        }
        ```
- params
    - populates an array of values
    - allows a method to take an indeterminate number of parameters
    ```
    public static int Add(params int[] values)
    {
        int sum = 0;

        foreach(int val in values)
        {
            sum += val;
        }
        return sum;
    }
    ```
### Method Chaining
```
string s = "   hello   ";
s = s.Trim().ToUpper();
```

### Methods as Parameters
```
int result = Add(GetPositiveInteger(), GetPositiveInteger())
```
