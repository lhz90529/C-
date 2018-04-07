## [Templatised Classes](http://web.stanford.edu/class/cs106l/lectures/lecture12/12_Templatised_Classes.pdf)

### Reference
A reference, like a pointer, stores the address of an object that is located elsewhere in memory.

A reference holds the address of an object, but behaves syntactically like an object.
```c++
int x = 15;
int &refToX = x;// refToX is a synonym for x
refToX = 3;//modify refToX will result in modification of the actual value of x
cout << x << endl; // print x
```

#### Reference can be returned by function
```c++
//Good example of "function return reference
int global = 1;

int& getGlobal() {
    return global;
}

int main() {
    getGlobal() += 2;
    cout << global << endl; // prints 3
}
```
##### However, below is a really bad example
```c++
// REALLY BAD
int& getGlobal() {
    int x = 5;
    return x;
}

int main() {
    getGlobal() += 2; // undefined behavioud
    cout << global << endl;
}
//Why?
//The function getGlobal() return the reference of x. 
//However, x will be disappeared as long as getGlobal() return. 
//Thus the returned reference point to NO WHERE
```

### How does Reference work?
Usually implemented by the compilers _as pointer that get automatically dereference_
```c++
int x = 3;
int& refTox = x;
++refTox;

//is COMPLETELY equivalent to

int x = 3;
int* refTox = &x;
++(*refTox);
```

### Const Interface
Class can have **const** and **non-const** interfaces
- **const** instances of the class has to go through **const** interface
    > **const** function does not modify the object for which it is called
- **non-const** instance of the class can go through either

```c++
//const interface
size_t string::size() const {
    //implementation
}

//non-const interface
void string::clear() {
    //implementation
}
```

### Class Templates
```c++
//e.g. generic vector
template <typename ValueType>
class Vector {
public:
    void push_back(const ValueType& elem);//declaration
}

template <typename ValueType>//Every method need to be templated
void Vector<ValueType>::push_back(const ValueType& val) {
    //implementation
}
```
