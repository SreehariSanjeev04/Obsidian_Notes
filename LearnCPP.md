
## Data Structures

- Double
- String
- Char
- Float 
## Type Conversion

Using implicit and explicit type conversions, we change the data type

## User Input

getline(cin, input) -> to accept strings with spaces 

```
cin >> age;
getline(cin, input)
```
This can cause newline character to be accepted by the getline command

```
cin >> age;
getline(cin >> ws, input) 
```
ws -> whitespaces

## String Methods

```
string.length()
string.erase(0,3)
string.insert()
string.append()
string.clear()
```


### this-> is used because this is a pointer to current instance of the class

Static keyword is used to specify that the variable is shared among all the instances of the class. Any changes will reflect in all. :: -> scope resolution operator

```cpp
class Car {
	public:
		static int model;
}
Car::model = 2015; // must be initialized outside the class
```

```cpp
class Car {
	public:
		static int model;
	public:
		static void printModel() {
			cout << model << endl;
		}
}
Car::model = 2015;
Car::printModel(); 
```

### : operator in CPP

Member initialization

```cpp

class Randomclass{
	 int x;
	 const int y;
	 MyClass(int val1, int val2) : x(val1), y(val2) {
	 } // initializes x and y with val1 and val2
}
```

### Member variables are instance specific (not shared unless static)

[285_OOPS lecture notes Complete.pdf](https://www.cet.edu.in/noticefiles/285_OOPS%20lecture%20notes%20Complete.pdf) Learn this
