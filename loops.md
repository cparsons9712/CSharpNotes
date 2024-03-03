# Loops

## while
Continues to run for as long as test condition is true

```
string s = "Hello";

int index = 0;
while (index < s.Length)
{
    Console.WriteLine($"{s[index]}")
    index++;
}
```

Most often used when the amount of iterations it takes to get the code block to register false is unknown
<br>
Can be used to check for valid input and force reruns until a valid input is given.
```
string input;
int number = 0;
bool isValid = false;

while(!isValid)
{
    Console.Write("Enter a number: ");
    input = Console.ReadLine();

    // out = variable to send out; number = name of varaible
    if (int.TryParse(input, out number))
    {
        isValid = true;
    }
    else
    {
        Console.WriteLine("That is not a valid number, try again!");
    }
}
Console.WriteLine($"You entered the number {number}.");
```

## do-while
is like a while loop but the test is after the code block
<br>
The code block will always run at least once
```
do
{
    Console.Write("Enter a number: ");
    input = Console.ReadLine();

    if (int.TryParse(input, out number))
    {
        isValid = true;
    }
    else
    {
        Console.WriteLine("That is not a valid number, try again!");
    }
}while (!isValid)
```

## for
```
for (int i = 0; i < s.Length; i +=2)
{
    if (i+1 == s.Length)
    {
        Console.WriteLine(s[i])
    }
    else
    {
        Console.WriteLine($"{s[i]}, {s[i+1]}");
    }
}
```

## foreach
When you need to do something to everything in a bunch and the order it is done in doesnt matter

```
string s = "Hello";

foreach(char c in s)
{
    Console.WriteLine(c)
}
```

## Break and Continue

### break
Break = immediately exit the loop
```
string s = "Problem";
bool vowelFound = false;

foreach(char c in s.ToLower())
{
    if (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c== 'u')
    {
        vowelFound = true;
        break
    }
}
if (vowelFound == true)
{
    Console.WriteLine($"We found a vowel in the string \"{s}\"");
}
else
{
    Console.WriteLine($"We did not find a cowel in the string \"{s}\"");
}
```
```
string input;
int value;

while(true)
{
    Console.Write("Enter a number between 1 and 10: ");
    input = Console.ReadLine();

    if(int.TryParse(input, out value))
    {
        if (value >= 1 && value <= 10)
        {
            break;
        }
        else
        {
            Console.WriteLine("Value out of range. Try again.");
        }
    }
    else
    {
        Console.WriteLine("That was not a numeric value")
    }
}
```

### continue
continue = ends current block but continues processing the loop
```
for(int i=10; i<=20; i++)
{
    if (1 % 3 == 0 && i % 5 == 0)
    {
        continue;
    }

    Console.WriteLine(i)
}
```
