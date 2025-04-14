# Preface

This manual was made by Aryan Gupta. If you see anything wrong, feel free to open a pull request & commit the fixed changes.

**GitHub Repository**: https://github.com/aryan-cs/dsa

## Hello, World!


```c++
#include <iostream>
using namespace std;

cout << "Hello, World! \n";
```

    Hello, World! 


# Programming Foundations

## Primitive Data Types

The building blocks that make up programs.


```c++
#include <iostream>
using namespace std;

// Variable Declaration | 32-bit Architecture | 64-bit Architecture

short s = -1;          // 2 bytes             | 2 bytes
int i = -1;            // 4 bytes             | 4 bytes 
long l = -1;           // 4 bytes             | 8 bytes
long long ll = -1;     // 8 bytes             | 8 bytes

// Same number of bytes, but only works for natural numbers
unsigned short us = -1;          // 2 bytes             | 2 bytes
unsigned int ui = -1;            // 4 bytes             | 4 bytes 
unsigned long ul = -1;           // 4 bytes             | 8 bytes
unsigned long long ull = -1;     // 8 bytes             | 8 bytes

// Note: unsigned int has a range of [0, (2^32) - 1], 
// whereas the signed int has a range of [-(2^31), (2^31) - 1]
// Takeaway: unsigned means only positive values

// More bytes, more precision, reduces floating-point errors
float f = -1.0;          // 4 bytes             | 4 bytes
double d = -1.0;         // 8 bytes             | 8 bytes
long double ld = -1.0;   // 16 bytes            | 16 bytes

// Use sizeof() to check how many 
// bytes a datatype uses at COMPILE time
cout << "An integer takes up " << to_string(sizeof(i))  << " bytes."<< endl;
```

    An integer takes up 4 bytes.


## Pointers & The Heap

Used to point to a location in memory. 


```c++
#include <iostream>
using namespace std;

// Allocates data on the heap (aka freestore) and 
// creates a pointer in the stack pointing to that data
int* integer_pointer = new int(5); // Allocates 4 bytes
cout << *integer_pointer << endl;

// Data on the heap can be edited using the pointer
*integer_pointer = 3;
cout << *integer_pointer << endl;

// ALWAYS MAKE SURE YOU DELETE POINTERS AND FREE THEM
delete integer_pointer;
integer_pointer = nullptr;
```

    5
    3


## Referencing

To get the address of any data, use the & operator.


```c++
#include <iostream>
using namespace std;

int some_integer = 5;
cout << &some_integer << endl;

cout << "Notice that the address of the data on the heap is not the same as the address of the pointer." << endl;
// The pointer is some data that resides in the stack, which 
// points to an address on the heap (where our allocated data is stored)
double* heap_double = new double(5.0);
cout << heap_double << endl;
cout << &heap_double << endl;

delete heap_double;
heap_double = nullptr;
```

    0x7f6336043148
    Notice that the address of the data on the heap is not the same as the address of the pointer.
    0x558254e1b660
    0x7f6336043140


## Structs

Used to group a set of context-dependent data types.   


```c++
#include <iostream>
#include <string>
using namespace std;

struct Grouping_Structure_1 {

    int member_A;
    double member_B;
    string member_C;
    float member_D;

    Grouping_Structure_1(int a, double b, string c, float d) : member_A{a},member_B{b}, member_C{c}, member_D{d} {}

};

Grouping_Structure_1 group_1(1, 100, "Hello, World!", -1.0);
cout << group_1.member_A << endl;
cout << group_1.member_B << endl;
cout << group_1.member_C << endl;
cout << group_1.member_D << endl;

struct Grouping_Structure_2 {

    int member_A;
    double member_B;
    string member_C;
    float member_D;

    // These can also be made without a constructor

};

Grouping_Structure_2 group_2;

cout << "Without any default value, they parameters on the default value of their datatype." << endl;
cout << group_2.member_A << endl;
cout << group_2.member_B << endl;
cout << group_2.member_C << endl;
cout << group_2.member_D << endl;

cout << "These values can be edited, however." << endl;
group_2.member_A = 1;
cout << group_2.member_A << endl;
```

    1
    100
    Hello, World!
    -1
    Without any default value, they parameters on the default value of their datatype.
    0
    0
    
    0
    These values can be edited, however.
    1


## Classes

The key to object-oriented programming, builds upon the idea of a struct.


```c++
#include <iostream>
#include <string>
using namespace std;

class MyClass {

    public: // access specifier, details the scope of the following
        int public_int; // attribute
        void public_func() { // method
            cout << "You can declare methods alongside attributes in the class." << endl;
            private_func();
        }
        void outside_method();

    private:
        int private_int;
        void private_func() {
            cout << "However, private methods can only be called in the scope of the class." << endl;
        }
};

// This is not supported in the C++ notebook, 
// but is also a valid method for declaring methods.
// void MyClass::outside_method() {
//   cout << "You can also declare a method outside the class." << endl;
// }

MyClass example;
cout << example.public_int << endl;
example.public_int = 1;
cout << example.public_int << endl;
example.public_func();
```

    0
    1
    You can declare methods alongside attributes in the class.
    However, private methods can only be called in the scope of the class.



```c++
// However, notice what happens when we try to access a private attribute.
cout << example.private_int << endl;
```

    [1minput_line_21:3:17: [0m[0;1;31merror: [0m[1m'private_int' is a private member of 'MyClass'[0m
    cout << example.private_int << endl;
    [0;1;32m                ^
    [0m[1minput_line_20:12:13: [0m[0;1;30mnote: [0mdeclared private here[0m
            int private_int;
    [0;1;32m            ^
    [0m


    Interpreter Error: 


## Type Definitions & Function Templates

Useful for writing cleaner code & fixing compiler warnings.


```c++
#include <iostream>
using namespace std;

// We can redefine data types to abstract commonly used patterns
// This doesn't change the behavior of the data type, only how much we need to type
// This is useful when the compiler throws warnings on 
// things such as commonly switched parameters
typedef int triple[3];
typedef double super_double;

triple custom_triple = {0, 1, 2};
super_double nothing_special = 1.0;

cout << custom_triple[0] << custom_triple[1] << custom_triple[2] << endl;
cout << nothing_special << endl;
```

    012
    1



```c++
// We can also define functions without specific data types,
// which reduces how much repetitive code we need to write
template <typename T>
T find_max(T a, T b) {
    return (a > b) ? a : b;
}
```


```c++
cout << find_max(1, 2) << endl;
cout << find_max(3.0, 4.0) << endl;
cout << find_max('a', 'A') << endl;
```

    2
    4
    a



```c++
// But T is not flexible--every parameter of type T must be of the same type
// If it isn't, we can define multiple T's

template <typename T1, typename T2>
T1 find_max(T1 x, T2 y) {
    return (x > y) ? x : y;
}
```


```c++
cout << find_max('a', 300) << endl;
// Notice what happens here: 
// 1. 'a' is converted into its ASCII value, 97 
// 2. 97 is then compared to 300
// 3. 300 is greater than 97, so it is converted into the return type of find_max(), which is the type of variable x (char)
// 3.5. BUT, 300 is greater than the range of ASCII, so we return 300 % 128 = 44 (there are 128 items in the ASCII table)
// 4. 44 in ASCII is ',', so that is what we return
```

    ,





    @0x7f6e7e76fd20



# Data Structures

## Static Arrays

Used to store a fixed amount of data contiguously in memory.  
**Time complexity**: O(1) read, O(1) write, O(n) search  
**Space complexity**: O(n) 


```c++
#include <iostream>
#include <string>
using namespace std;

int integer_array[5] = { 0, 1, 2, 3, 4 };
char character_array[4] = { 'a', 'b', 'c', 'd' };
float float_array[3] = { -1.0, 0.0, 1.0 };
string string_array[2] = { "Hello,", " World!" };

// Notice how printing an array returns the pointer (stay tuned) to 
// the first element of the array, rather than the array itself
// However, it does work for char[], as
// that is essentially what a string is
cout << integer_array << std::endl;
cout << character_array << std::endl;
cout << float_array << std::endl;
cout << string_array << std::endl;
cout << string_array[0] << string_array[1] << std::endl;
```

    0x7f111970c110
    abcd
    0x7f111970c128
    0x7f111970c140
    Hello, World!


## Resizable Arrays

Arrays of non-fixed size.  
**Time complexity**: O(1) read, O(1) write*, O(n) search  
**Space complexity**: O(n) 

*\* O(n) if attempting to write while at maximum capacity, as we will need to resize.*


```c++
#include <iostream>
using namespace std;

// RESIZEABLE ARRAYS (aka VECTORS) //

cout << "As of 04/12/2025, these cannot be implemented in a C++ Notebook." << endl;
```

    As of 04/12/2025, these cannot be implemented in a C++ Notebook.


## Hash Maps

Used for quick lookups, mapping one value to another.  
**Time complexity**: O(1) read*, O(1) write*  
**Space complexity**: O(n)  

*\* O(n) if hash collisions occur, where each bucket degrades into a list.*


```c++
#include <iostream>
#include <unordered_map>
#include <string>
using namespace std;

std::unordered_map<std::string, int> hash_map;

hash_map["Archibald"] = 30;
hash_map["Bartholomew"] = 25;
hash_map["Charleston"] = 35;

cout << "Archibald's age: " << hash_map["Archibald"] << endl;
cout << "Bartholomew's age: " << hash_map["Bartholomew"] << endl;

if (hash_map.find("Dawood") == hash_map.end()) {
    std::cout << "Key 'Dawood' not found." << endl;
}

for (const auto& pair : hash_map) {
    cout << pair.first << "'s age: " << pair.second << endl;
}

hash_map.erase("Bartholomew"); // Only Archibald and Charleston remain

cout << "There are " << hash_map.size() << " elements in the hash map." << std::endl;
```

    Archibald's age: 30
    Bartholomew's age: 25
    Key 'Dawood' not found.
    Charleston's age: 35
    Bartholomew's age: 25
    Archibald's age: 30
    There are 2 elements in the hash map.


## [Singly] Linked List

*Coming soon...*

## Doubly Linked List

*Coming soon...*

## Stack

*Coming soon...*

## Queue

*Coming soon...*

## LRU Cache

*Coming soon...*

## Binary Tree

*Coming soon...*

# Algorithms

## Depth-first Search (DFS)

*Coming soon...*

## Breadth-first Search (BFS)

*Coming soon...*

## Iterative Deepening

*Coming soon...*

## Pre-order Traversal

*Coming soon...*

## In-order Traversal

*Coming soon...*

## Post-order Traversal

*Coming soon...*

## Level-order Traversal

*Coming soon...*

## Binary Search Algorithm

*Coming soon...*

## Merge Sort Algorithm

*Coming soon...*

## Bubble Sort Algorithm

*Coming soon...*

## Djikstra's Algorithm

*Coming soon...*

## A* Algorithm

*Coming soon...*
