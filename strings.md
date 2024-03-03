# Strings

## Escape Characters
\\\\" --> insert double quote <br>
\\\\n --> Insert new line <br>
\\\\t --> Insert a tab <br>
\\\\\\\\ --> Inserts a literal backslash

```
string s1 = "the cow says, \"Moo\"";
string s2 = "This is the first line, \nThis is the second line";
string s3 = "c:\\myfiles\\";
```
## Immutable
Strings cannot be changed, they are always overwritten or saved to a new var

```
string s1 = "OPTION 1";

***DONT DO ****
s1.ToLower()

**** DO ****
string s2 = s1.ToLower();
s1 = s1.ToLower();
Console.WriteLine($"whisper please {s1.ToLower()}");
```
## format shortcuts
### Numeric
- :c -> currency
- :d -> decimal; use a trailing number to specify how many total digits (1234("D6") -> 001234)
- :e -> exponential notation
- :f2 -> Fixed point num wuth specific num of decimal places (1234("f2")-> 1234.00)
- :n2 -> thousand seperators and specified decimal places (1234.56("n3") -> 1,234.560)
- :p Percentage/ Multiples by 100 and adds % (1("P1") -> 100%)
- :x hexadecimal

### Date and Time
- :D -> long date
- :d -> short date
- :F -> long date and long time
- :f -> long date short time
- :G -> short date long time
- :g -> short date short time
- :T ->long Time
- :t -> short time
- :O -> round trip
- :R -> RFC1123 pattern
- :U universal sortable DateTime pattern

<br>
Can calso be used like this:

```
double number = 123.456
string formattedNumber = number.ToString("F2");
```

### String Interpolation
Allows you to insert strings into literal text <br>

```
string item = "Ice Cream Cone";
decimal price = 3.99M;

Console.WriteLine($"The price of the {item} is {price:c}.");
```

### Composite Formatting
Older method that might be seen in legacy applications

```
string item = "Ice Cream Cone";
decimal price = 3.99M;

string message = string.Format("The price of the {0} is {1:c}", item, price);
Console.WriteLine(message);

Console.WriteLine("the price of the {0} is {1:c}, item, price);
```
You can also use the indexes multiple times in the string
```
string aussie = "Aussie!";
string oy = "Oy!";
string message = string.Format("{0} {0} {0}\n{1} {1} {1}", aussie, oy);
```

## String Methods

### Concat()
```
string s1 = "Hello";
string s2 = " world!";

string s3 = string.Concat(s1, s2);

string s4 = s1 + s2;

// s3 & s4 = "Hello world!"
```

### ToLower and ToUpper()

```
string s1 = "Anders Hamm";
string s2 = s1.ToLower(); // anders hamm
string s3 = s1.ToUpper(); // ANDERS HAMM
```

### Substring()
- with one arguement, it takes the end of the string starting from the specified index
- with two arguements it takes a string starting on first arg index ending at second arg index

```
string s = "Hello, world!";

string s2 = s.Substring(7); // "world!"
string s3 = s.Substring(1,4); // "ello"
```
### Replace()
```
string horse = "I love horses. Horses are my favorite animal."

string goat = horse.Replace("horses", "goats") //"I love goats. Horses are my favorite animal"
```
In the above example Replace() didnt replace the second Horses because Replace is case-sensitive.

```
using System.Text.RegularExpressions;

string horses = "I like horses. Horses are my favorite animal."
string goats = horses.Replace("horses", "goats",RegexOptions.IgnoreCase ); // "I like goats. goats are my favorite animal."
```
here we use IgnoreCase to make Replace work across cases.

### IndexOf()

```
string s = "Hello, world!";

int index;

index = s.IndexOf("z"); // -1
index = s.IndexOf("o"); // 4 -> the first instance of o in the string
index = s.IndexOf("o", 5) // 8 -> searches the string starting from index 5 to the end
index = s.IndexOf("o", 9) // -1 -> there are no o's from index 9 to the end of the string
```

### StartsWith()
```
string s = "Hello, world!";

bool startsWith = s.StartsWith("Hello"); //true

bool startsWith = s.StartsWith("Zebra"); //false
```

## StringBuilder Type
- When you need to concat hundreds or more times
- Faster method of concatting when dealing with large volumes of data
- Append() or AppendLine() adds into it
- ToString() to output the data

```
using System;
using System.Text; // where StringBuilder comes from

namespace StringBuilderExample
{
    class Program
    {
        static void Main(string[] args)
        {
            StringBuilder sb = new StringBuilder();

            sb.AppendLine("Banana");
            sb.AppendLine("Grape");
            sb.AppendLine("Apple");
            sb.AppendLine("Orange");
            sb.AppendLine("Mango");

            Console.WriteLine(sb.ToString());
        }
    }
}
```
terminal:
> Banana
 <br>Grape
<br> Apple
<br> Orange
<br> Mango

- AppendLine() adds a line break after the text.
- Append() would not add in the line break


