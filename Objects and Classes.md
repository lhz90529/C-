## [Objects and Classes](http://web.stanford.edu/class/cs106l/lectures/lecture09/09_Classes.pdf)
### Struct
```c++
struct Student{
    std::string name;
    std::string suid;
    int unitsTaken
}
```
- **Issues**
    1. **Public access** to all internal state data
    2. Users need to explicitly initialize each data member before using it

> A struct simply feels like an open pile of bits with very little
in the way of encapsulation or functionality. 
A class feels like a living and responsible member of society with
intelligent services, a strong encapsulation barrier, and a well defined interface
        - Bjarne Stroustrup

### Classes
```c++
class Student{
    std::string name;
    std::string suid;
    int unitsTaken    
}
```
- Members of `struct` by default **public**
- Members of `class` by default **private**

### Scope Resolution
- Using `namespace` to prevent name collisions especially when your code base includes multiple libraries

```c++
//bring nothing into scope, use fully qualified name 
ContosoData::ObjectManager mgr;  
mgr.DoSomething();  
ContosoData::Func(mgr);

//bring one identifier into scope:
using ContosoData::ObjectManager;  
ObjectManager mgr;  
mgr.DoSomething();

//bring everything into scope
using namespace ContosoData;
ObjectManager mgr;  
mgr.DoSomething();  
Func(mgr);  
```

- [Very good reference](https://docs.microsoft.com/en-us/cpp/cpp/namespaces-cpp)
