# Arrays

## Unique Characteristics to C#
- An array must be given a size at creation and the size cannot change after the fact, however it can have empty slots
- arrays are declared with the data type keyword and []
- when delcaring the values go into {} instead of []
- the [] suffix is what tells the computer that its a collection of items instead of a single instance of one


## Creating an Array
```
// declare an array of strings with 7 elements that are null
string[] names = new string[7];

//declare an array of ints with 3 elements, all 0
int[] ints = new int[3];

// declare an array of strings with 3 elements
string[] primary = {"red", "blue", "yellow" };

//declare an array with 4 integers
int[] nums = {5, 10, 15, 20}

// get a number from a method to initialize an array
int[] nums = new int[getSizeFromUser()]
```
- String array default value is null
- int array default value is 0

## Storing and Retrieving Elements
```
string[] planets = new string[9];

planets[0] = "Mercury";
planets[2] = "Earth";

Console.WriteLine($"The element at index 2 is {planets[2]}"); // Earth

string val = planets[5] // null (the default value for unassigned strings)

planets[8] = "Pluto"
planets[8] = null // overright this value since Pluto "isnt a planet anymore" - Mainstream Science

string val = planets[50] // this is outside the bounds of our array so we will get an error
```

## Array Navigation

### Getting length

Length is the size that the array was created to be. This will include all null or 0 valuese. It will never change unless a new array is created and the elements are copied over
```
string[] planets = new string[9];
Console.WriteLine($"There are {planets.Length} planets in the solar system")

int[] oddNumbers = {1, 3, 5, 7};
int oddCount = oddNumbers.Length; // 4
```
### Hat Operator ^
iterate from the end elements.
- ^1 = last element
- ^2 = second to last element
- ^3 = third to the last element
```
int[] array = {1, 2, 3, 4, 5, 6, 7}
int lastElement = array[^1] // 7
int secondToLastElement = array[^2] // 6
```

### Range Operator ..
- putting .. between two indexes will retrieve all elements inbetween
- x .. y starting from x get all elements up until y. Includes x, excludes y
- x .. gets the end of the array starting from x. Includes x
- ..y gets the first bit of the array before y. Excludes y

```
int[] array = {1, 2, 3, 4, 5};

int[] middleElements = array[1..4]; // 2, 3, 4
int[] allButFirst = array[1..]; // 2, 3, 4, 5
int[] allButLast = array[..^1]; // 1, 2, 3, 4
int[] lastThreeElements = array[^3..]; // 3, 4, 5
int[] slice = array[2..^3]; // 3
```

## Loops

### While Loop
```
string[] elements = {"Hydrogen", "Helium", "Lithium", "Beryllium"};

int index = 0;
while(index < elements.Length)
{
    Console.WriteLine($"The element at index {index} is {elements[index]}");
    index++;
}

index = elements.Length -1;
while(index >= 0)
{
    Console.WriteLine($"the elements at index {index} is {elements[index]}")
    index--;
}
```

### For Loop
```
string[] elements = {"Hydrogen", "Helium", "Lithium", "Beryllium"};

for(int i=0; i<elements.Length; i++)
{
    Console.WriteLine($"the element at index {index} is {elements[index]}")
}

for(int i=elements.Length-1; i>=0; i++)
{
    Console.WriteLine($"The element at index {index} is {elements[index]}")
}
```
# Multi-dimensional Array/ Matrix

## Creation
```
string[,] twoDimensional Array

int[,] values = new int[10,12];

string[,] threeOfAKind = {
    {"Strawberry", "Blueberry", "Blackberry"},
    {"Red", "Yellow", "Blue"},
    {"Atlantic", "Pacific", "Indian"},
};

int[,,] valueCube = {
    {
        { 1, 2, 3 },
        { 4, 5, 6 },
        { 7, 8, 9 }
    },
    {
        { 11, 12, 13 },
        { 14, 15, 16 },
        { 17, 18, 19 }
    },
    {
        { 21, 22, 23 },
        { 24, 25, 26 },
        { 27, 28, 29 }
    }
}
```
## Reading and Writing
```
string[,] threeOfAKind = new string[3,3]{
    { "Strawberry", "Blueberry", "Blackberry" },
    { "Red", "Yellow", "Blue" },
    { "Atlantic", "Pacific", "Indian" }
};

string element = threeOfAKind[1,2]; //Blue
string ocean = threeOfAKind[2,0]; // Atlantic

threeOfAKind[2,0] = "Artic"
```

## Looping
```
string[,] grid =
{
    { "(0,0)", "(0,1)", "(0,2)" },
    { "(1,0)", "(1,1)", "(1,2)" },
    { "(2,0)", "(2,1)", "(2,2)" }
}

int rows = grid.GetLength(0);
int cols = grid.GetLength(1);

for (int i = 0; i < rows; i++)
{
    for (int j = 0; j < cols; j++)
    {
        Console.WriteLine(grid[i, j]);
    }
}
```

# Jagged Arrays

## initialize
```
int[][] familyAges = new int[3][];

familyAges[0] = new int[] {44, 44, 13, 16, 20};
familyAges[1] = new int[] {32, 23, 3, 5};
familyAges[2] = new int[] {55, 53};

int val = familyAges[1][2];  // 3
```
## Loop
```
for(int 1 = 0; i < familyAges.Length; i++)
{
    Console.WriteLine($"Family {i}");
    for (int j = 0; j < familyAges[i].Length; j++)
    {
        ConsoleWriteLine($"Member {j} is {familyAges[i][j]} years old");
    }
}
```
