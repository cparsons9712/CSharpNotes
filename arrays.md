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

## Iterating Over Arrays

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

