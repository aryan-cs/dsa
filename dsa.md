```c++
#include <iostream>
using namespace std;
```


```c++
cout << "Hello, World! \n";
```

    Hello, World! 



```c++
// PRIMITIVE DATA TYPES //

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



```c++
#include <string>

// STATIC ARRAYS //

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
```

    0x7f059e0e58e0
    abcd
    0x7f059e0e58f8
    0x7f059e0e5910



```c++
// POINTERS //
// Used to point to data in memory for direct access

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



```c++
// RESIZEABLE ARRAYS (aka VECTORS) //

cout << "As of 04/12/2025, these cannot be implemented in a C++ Notebook." << endl;
```

    As of 04/12/2025, these cannot be implemented in a C++ Notebook.


```c++
// REFERENCING //
// To get the address of any data, use the & operator

int some_integer = 5;
cout << &some_integer << endl;

cout << "Notice that the address of the data on the heap is not the same as the address of the pointer." << endl;
double* heap_double = new double(5.0);
cout << heap_double << endl;
cout << &heap_double << endl;
// The pointer is some data that resides in the stack, which 
// points to an address on the heap (where our allocated data is stored)

delete heap_double;
heap_double = nullptr;
```

    0x7f66f97ad058
    Notice that the address of the data on the heap is not the same as the address of the pointer.
    0x56162fd6b710
    0x7f66f97ad050



```c++
// HASH MAPS //
```


```c++
// [SINGLY] LINKED LIST //
```


```c++
// DOUBLY LINKED LIST //
```


```c++
// STACK //
```


```c++
// QUEUE //
```


```c++
// LRU CACHE //
```


```c++
// BINARY SEARCH TREE //
```
