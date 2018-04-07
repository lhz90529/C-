## [Functions](http://web.stanford.edu/class/cs106l/lectures/lecture10/10_Functions.pdf)
### Operator Overloading
Allow you to **define functionality** for operators on any types

|  + |  -  |  *  |    /   |    %   |     ^     |
|:--:|:---:|:---:|:------:|:------:|:---------:|
|  & |  |  |  ~  |    !   |    ,   |     =     |
|  < |  >  |  <= |   >=   |   ++   |     --    |
| << |  >> |  == |   !=   |   &&   |     ||    |
| += |  -= |  *= |   /=   |   %=   |     ^=    |
| &= |  |= | <<= |   >>=  |   []   |     ()    |
| -> | ->* | new | new [] | delete | delete [] |

Use **ONLY** when overloading has an intuitive meaning
```c++
//e.g.
Set<int> mySet;
mySet += 3;
mySet += 2;
//now mySet = {2, 3}
```

#### Two ways to overload operators
##### Member functions
```c++
//Below is an example that define operator "=" for struct Point
struct Point {
    int x, y;
    bool operator==(const Point& rhs) {
        return x == rhs.x && y == rhs.y;
    }
};
```
In the example above, operator is defined **within the struct** such that the left-hand side of operator is defined **implicitly**

##### Non-member functions
```c++
struct Point {
    int x, y;
}

bool operator==(const Point& lfs, const Point& rhs) {
    return lfs.x == rhs.x && lhs.y == rhs.y;
}
```
However, if you define operator **outside of struct**, left-hand side of operator has to be defined **explicitly**

### Functors
Classes which defines the `()` operator
Functors let us make **customizable** functions

### Lambdas
A C++11 feature that lets you make functions on the fly
```c++
[capature-list](params) -> ReturnType {
    //code
}
//capture-list
[byValue, &byReference]
```
**For example**
```c++
auto print_int = [] (int x) {
                    cout << x << endl;
                }
print_int(5)//will print 5 to console
```

```c++
vector<int> v{3,1,4,1,5}
-----------------------------------------------------------------------
//Labmda
std::sort(v.begin(), v.end(), [](int i, int j) -> bool {return i > j;});
[](int i, int j) -> bool {
    return i > j;
}
-----------------------------------------------------------------------
//Normal function
bool myFunction(int i, int j) {
    return i > j;
}
std::sort(v.begin(), v.end(), myFunction);
-----------------------------------------------------------------------
//Functors
class myObject {
    bool operator() (int i, int j) {
        return i > j;
    }
}
std::sort(v.begin(), v.end(), myObject);
-----------------------------------------------------------------------
//The 3 way produce exatcly same result
//However, the first way "Labmda" will define the function when it is needed
//The rest requires the function is pre-defined
```
