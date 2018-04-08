## [Constructors and Assignment](http://web.stanford.edu/class/cs106l/lectures/lecture14/14_Constructors_and_Assignment.pdf)

#### Why Constructors?
Set up **initial** state of obejct
- Make sure everything has a **sensible** starting value
- Take information from `user` to set up object appropriately

#### Initialisation vs Assignment
##### Initialization
- Transform an object initial **junk** data into **valid** data
- Defined by the **constructor** of a type
##### Assignment
- Replace **existing valid** data with **other valid** data
- Defined by the **assignment operator** for a type

#### Constructors
##### Normal Constructor
- What we are used to
##### Copy Constructor
- Initialise an instance of a type to be a **copy** of another instance
##### Copy Assignment
- Not a constructor
- Assign an instance of a type to be a **copy** of another instance

```c++
Vector<string> defV; // normal constructor
// initialisation
Vector<string> fillV(10, "hello"); // normal constructor
// initialisation
Vector<string> copyV(defC); // copy constructor
// initialisation
Vector<string> v = defV; // copy constructor
// initialisation
v = fillV; // copy assingment 
// assignment

//Note, constructor always create an NEW instance of object
//However, assignment is always performed on exsiting object
```
> If you don't define some of these constructors, the compiler will create default version for you
_However, this may not always do what you want_


##### Default Constructor
- Takes **no** arguments
- Used to initialise members to sensible starting value
```c++
class MyClass {
public:
    MyClass() { // default constructor
        privInt = 3;
    }
private:
    int privInt;
};

//Usage
MyClass temp; // calls defautl constructor
MyClass buggy(); // Doesn't work
```

##### Copy Constructor
- Used to **initialise** an instance of a class from _another exsiting instance_
- Two ways it can be called
```c++
    // vector<string> v created earlier
    // copy constructor called
    vector<string> copyV(v);//initialise an new instance of vector called "copyV" from another exsiting instance called "v"
    vector<string> copyV2 = v;
``` 
- Syntax is that of a constructor that takes a class object as its argument
```c++
MyClass::MyClass (const MyClass& rhs) {
// implementation
}
```
- If you have pointer variables, you should always define a copy constructor

##### Copy Assignment
- Takes already initialised object and gives it new values
```c++
// vector<string> v, v2 created earlier
// copy assignment
v = v2;//take already initialised object "v" and give it new values
```
- Works by overloading the `=` operator
```c++
class MyClass {

public:
    MyClass& operator=(const MyClass& rhs) {
    }

private:
    int privInt;
};
```