## [Const Correctness](http://web.stanford.edu/class/cs106l/lectures/lecture13/13_Const.pdf)

### Why const?
Instead of asking why you think const is important, I want to start with a different (related) question:
> Why don't we use global variables?

#### global vairables
- "Global variables can be read or modified by any part of the program, making it difficult to remember or reason about every possible use"
- "A global variable can be get or set by any part of the program, and any rules regarding its use can be easily broken or forgotten"

#### const variables
- "Non-const variables can be read or modified by any part of the function, making it difficult to remember or reason about every possible use"
- "A non-const variable can be get or set by any part of the function, and any rules regarding its use can be easily broken or forgotten"

```c++
//Find bug in this code
void f(int x, int y) {
 if ((x == 2 && y == 3)||(x == 1)) {
     cout << 'a' << endl;
 }

 if ((y == x-1)&&(x == -1||y = -1)) {//y = -1 is the bug
     cout << 'b' << endl;
 }

 if ((x == 3)&&(y == 2 * x)) {
     cout << 'c' << endl;
 }
}
```
```c++
//The compiler will find the bug for us if you define the function in the following way
void f(const int x, const int y) {//note the const here
 if ((x == 2 && y == 3)||(x == 1)) {
     cout << 'a' << endl;
 }

 if ((y == x-1)&&(x == -1||y = -1)) {//y = -1 is the bug
     cout << 'b' << endl;
 }

 if ((x == 3)&&(y == 2 * x)) {
     cout << 'c' << endl;
 }
}
//test.cpp: In function 'void f(int, int)':
//test.cpp:7:31: error: assignment of read-only parameter 'y'
```
#### The const Model
_const allows us to reason about whether a variable will be changed_
```c++
void f(int& x) {
    // The value of x here
    aConstMethod(x);
    anotherConstMethod(x);
    // Is the same value of x here
}
-----------------------------------
void f(const int& x) {
// Whatever you want
}
void g() {
 int x = 2;
 f(x);
 // x is still equal to two
}
```
##### Const Member Function
**const Object:** can call const member function **ONLY**
**non-const Object:** can call **everythig**

##### A Const Pointer
Using pointers with const is a little tricky 
- *When in doubt, read right to left*
```c++
//constant pointer to a non-constant int
int * const p;
//non-constant pointer to a constant int
const int* p;
int const* p;
//constant pointer to a constant int
const int* const p;
int const* const p;
```
##### A Const Iterator
```c++
//Here itr is a const pointer point to a non-const integer
const vector<int>::iterator itr = v.begin();
*itr = 5; //OK! changing what itr points to
++itr; //BAD! can’t modify itr
--------------------------------------------
//Here itr is a pointer point to a const int
vector<int>::const_iterator itr = v.begin();
*itr = 5; //BAD! can’t change value of itr
++itr; //OK! changing v
int value = *itr; //OK! reading from itr
```

### Conclusions
- For the most part, always anything that does not get modified should be marked    const
- Pass by const reference is better than pass by value
    - Not true for primitives (bool, int, etc)
- Member functions should have both const and non const iterators
- Read right to left to understand pointers

