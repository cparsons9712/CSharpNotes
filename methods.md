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

#### Questions to figure out structure
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
