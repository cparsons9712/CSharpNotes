# Console in C#
## General Info

console = terminal <br>

Benefits over GUI:
-	fast and resource efficient
-	user experience is the same on all operating systems
-	scriptable and easy to automate

Popular CLI’s
-	NPM
-	Maven
-	EMACs
-	VIM
-	Nano
-	Powershell
-	.NET

## Console Methods to receive data from user:
- ReadLine()
  - recieve input from client until Enter is pushed
    ```
    static void Main(string[] args)
    {
        string name;
        Console.Write("Enter your name: ");
        name = Console.ReadLine();
        Console.WriteLine($"Hello {name}!");
    }
    ```
- ReadKey()
    - Single keypress input from client
    - Returns ConsoleKeyInfo
        - that means it also keeps track when the keystroke used Shift, ALT or Ctrl
    - Usually used with Press any key to continue
        ```
        Console.Write("press any key to continue ...");
        Console.ReadKey();
        ```
    - Can also make a specific key press a quit option
        ```
        Console.Write("Press the enter key to quit...");
        ConsoleKeyInfo keypress;

        do
        {
            keypress = Console.ReadKey();
        } while (keypress.Key != ConsoleKey.Enter);
        ```

- Write() vs WriteLine():
    - WriteLine -> puts a new line after string output
    - Write -> cursor stays on the same line as prompt

## Using Parse to Change String Input to Numbers
- .Parse() = string to number
    - Might throw an exception (error)
    - If theres no error handling the program will crash and close
    - Parse should be used only with trusted inputs (not directly from users)
- .ToString() = number to string
```
int a, b;
string input;

Console.Write("Enter a number: ");
input = Console.ReadLine();

a = int.Parse(input);

Console.Write("Enter another number: ");
input = Console.ReadLine();

b = int.Parse(input);

int sum = a + b;
Console.WriteLine("the sum is " + sum.ToString());

```
