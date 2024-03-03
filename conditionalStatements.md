# Conditional Statements


## if Statement
```
string input;
int number;

Console.Write("Enter a number: ");
input Console.ReadLine();

number = int.Parse(input);

if (number % 2 == 0)
{
    Console.WriteLine($"The number {number} is even.");
}
```
## else Clause
```
if (number % 2 == 0)
{
    Console.WriteLine($"The number {number} is even.");
}
else
{
    Console.WriteLine($"The number {number} is odd.");
}
```

## else if Clause
```
Console.Write("Enter a package weight: ");
input Console.ReadLine();

decimal weight = decimal.Parse(input);

if(weight > 100)
{
    Console.WriteLine("This is a very heavy package!");
}
else if (weight > 50)
{
    Console.WriteLine("This is a moderately heavy package.");
}
else if (weight > 10)
{
    Console.WriteLine("This is a fairly heavy package.");
}
else
{
    Console.WriteLine("This is a light package");
}
```
## switch Statement
```
int place = 2;
string medal;

switch(place)
{
    case 1:
        medal = "Gold";
        Console.WriteLine("First place!");
        break;
    case 2:
        medal = "Silver";
        Console.WriteLine("Second Place!");
        break;
    case 3
        medal = "Bronze";
        Console.WriteLine("Third Place!");
        break;
    default:
    medal = "None";
    Console.WriteLine("no medal");
    break;
}
```


### When to use switch vs if blocks
- for statements that cover a range (less than/ greater than type situations) use if Blocks
- for statements that are specefic (all are == statements) use switch block
- case statements can only match primitive values

### fall-through switch statements
```
string color = "orange";

switch (color){
    case "red":
    case "yellow":
    case "blue" :
        Console.WriteLine("primary color");
        break;
    case "green":
    case "purple":
    case "orange":
        Console.WriteLine("secondary color");
    default:
        Console.WriteLine("other color");
        break;
}
```
This allows you to have multiple conditions result in the same output. Essentially if ("red" || "blue" || "yellow") {do stuff here}

### Selection Statements
Versions 9.0 or higher in C#!! <br>
older versions will not support the code below!!
```
switch(temp)
{
    case < 32:
    {
        Console.WriteLine("It's below freezing!");
        break;
    }
    case > 50:
    {
        Console.WriteLine("It's pleasant outside");
        break;
    }
    default:
    {
        Console.WriteLine("Getting cold outside");
    }
}
```
### Case Guard
This is a way of using when statements to make a more specific case (used the same way as SQL uses when statements)
```
ValidateAge(30,40);
ValidateAge(50,50);

void ValidateAge(int a, int b)
{
    switch ((a, b))
    {
        case(> 0, > 0) when a == b:
            Console.WriteLine($"Both ages are valid and equal to {a}.");
            break;

        case(> 0, > 0):
            Console.WriteLine($"First age is {a}, second age is {b}.");
            break;
        default:
            Console.WriteLine($"One or both ages are not valid.");
            break;
    }
}
```
