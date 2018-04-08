## [RAII and Smart Pointers](http://web.stanford.edu/class/cs106l/lectures/lecture15/15_RAII.pdf)

#### Conversion Operators
- Let you define how a class can be converted to other types
> For example, we could define a conversion of the MyVector to a bool to be false if the vector is empty and true otherwise.
```c++
//template
class MyClass {
public:
    operator Type() {
        // return something of type Type
    }
}
-----------------------------------------
//e.g.
class MyVector {
public:
    operator bool() {
        return empty();
    }
};
-----------------------------------------
//When you do the following, 
//the object Myvector will be converted to bool variable
Myvector v;
if (v) {
    cout << "vector is not empty";
}
```

### RAII 
**I**nitialisation
#### What is a resources?
- Anything that exists in limited supply
- Something you have to **acquire** and **release**
> Examples: memory, open files, sockets etc.
```c
//Example of C file I/O
//To read a file in C, you need to:
1. Open the file with fopen()   // acquire resource
2. Read data using fgets()    
3. Close the file with fclose() // release resource
//If a programmer forget to close an open file, bad things happen(memory leaks, crashes, etc)
```
|             |     Acquire    |      Release      |
|:-----------:|:--------------:|:-----------------:|
|  **Files**  |      fopen     |       fclose      |
|  **Memory** |   new, new[]   | delete, delete [] |
|  **Locks**  | lock, try_lock |       unlock      |
| **Sockets** |     socket     |       close       |

#### Back to RAII
> **R**esource **A**cquisition **I**s 
- A modern C++ idiom
- When you **initialize** an object, it should already have **acquired** any resources it needs (in the constructor)
- When an object goes **out of scope**, it should **release** every resource it is using (using the destructor).
##### Key points
- There should **never** be a half-ready or half-dead object
- When an object is created, it should be in a **ready** state
- When an object goes out of scope, it should **release** its resources.

##### How does C File I/O violate RAII?
```c
void printFile(const char* name) {
    // acquire file resource
    FILE* f = fopen(name, "r");
    
    // print contents of f
    
    // If the programmer forget to close the file
    // Even "f" goes out of scope, but "f" doesn't release its resource
}
------------------------------------
//an RAII friendly solution for C file I/O
class FileObj {
public:
    FILE* ptr;
    FileObj(char* name)//acquire resource in constructor
        : ptr(fopen(name, "r") {}

    ~FileObj() {//release resource in deconstructor
        fclose(ptr);
    }
};

void printFile(const char* name) {
// initialization(constructor) will acquire resources
FileObj fobj(name);
// print contents of f
// FileObj destructor will be called to release resources
}
```
##### RAII is actually a bad name
Better alternative names will be:
- Constructor Acquires, Destructor Releases
- Scope Based Resource Management  

### Smart Pointer
**Raw pointer** and **heap allocation** is actually an violation of RAII
- Calls to `new` aquire resource(memory)
- Calls to `delete` release resource
- But this is not automatically done when the pointers go out of scope.
```c++ 
void rawPtrFn() {
    // acquire memory resource
    Node* n = new Node;
    // manually release memory
    delete n; <--- if we forget this, we leak memory
}
//Definition of leak: memory which is no longer needed is not released
```
##### What would be an RAII solution to this?
Have a class that
- Allocates the memory when initialized
- Frees the memory when destructor is called
- Allows access to underlying pointer

##### C++ built-in smart pointers
- `std::unique_ptr`
- `std::shared_ptr`
- `std::weak_ptr`

###### unique_ptr
- Uniquely own its resource and deletes it when the object is destroyed
- **Cannot be copied!**
```c++
{
std::unique_ptr<int> p(new int);
// Use p
}
// Freed!
```
###### shared_ptr
- Resource can be stored by any number of shared_ptrs
- Deleted when none of them point to it
```c++
{
    std::shared_ptr<int> p1(new int);
    // Use p1
    {
        std::shared_ptr<int> p2 = p1;
        // Use p1 and p2
    }
    // Use p1
}
// Freed!
```

###### weak_ptr
Todo
