## [StreamsI](http://web.stanford.edu/class/cs106l/lectures/lecture01/01_Streams.pdf)

$\text{C++'s stream library is the means by which a C++ program can \textbf{interact} with its environment,}$
-  $\textbf{the user and}$ 
-  $\textbf{the file system}$


```c++ 
#include <iostream>

int main() {
    std::cout << "Hellow World!" << std::endl;
    return 0;
}
```
$\text{The program above can \textbf{get annoying} to write for common names like}$
- $\text{\color{Crimson}{cout}}$
- $\text{\color{Crimson}{endl}}$

```c++
#include <iostream>

using std::cout;
using std::endl;
int main() {
    cout << "Hellow World!" << endl;
    return 0;
}
```
- $\text{Whenever you use \color{Crimson}{cout}}$ $,\text{the compiler will assume you mean \color{Crimson}{std::cout}}$

### $\textbf{Stream}$
$\texttt{An abstraction for I/O}$

```
Illustration:
                        std cout
            -----------------------------
screen      |                           |  << "Hello world!"
            -----------------------------

                        std cout
            -----------------------------
screen      |       "Hello world!"      |
            -----------------------------

                                std cout
                    -----------------------------
"Hello world!"      |                           |  
                    -----------------------------
```
$\text{You can write data of multiple types to stream objects}$
```c++
cout << "Strings work!" << endl;//you can push data of string type into stream
cout << 1729 << endl;//integer type
cout << 3.14 << endl;//double type
cout << "Mixed types - " << 1123 << endl;//mix
```
$\textbf{In particular, any primitive type can be inserted into a stream!}$
$\text{For other types, you need to \textbf{explicitly} tell C++ how to do this.}$

#### $\textbf{Output Stream}$
- $\text{Can only receive data}$
- $\text{Operator Insertion:}$ $\texttt{\color{Crimson}{<<}}$
- $\text{Insertion converts data to string and sends to stream}$
- $\text{You can send the data to a file using a \color{Crimson}std::ofstream}$ $\text{, which is a special type of \color{Crimson}std::ostream}$

```c++
#include <iostream>
#include <fstream>

using std::cout;
using std::endl;
using std::string;
using std::ofstream;//Output file stream
int main() {
    //Output to console
    string s = "Why is 1 + 1 equal to ";
    cout << s <<  2 << endl;//insert different primitive types of data into output stream "cout"
    //Output to file
    ofstream file("output.txt");
    file << s << 2 << endl;
}
```

### $\textbf{Input Stream}$
- $\text{Can only give you data}$
- $\text{The \color{Crimson}{std::cin}}$ $\text{is an example of an input stream}$
- $\text{Operator Extraction:}$ $\texttt{\color{Crimson}{>>}}$
- $\text{Extraction gets data from stream as a string and converts it into the appropriate type}$

```c++
#include <iostream>
#include <fstream>

using std::cout;    using std::endl;
using std::string;

void readNumbers() {
    // Create our ifstream and make it open the file
    std::ifstream input("numbers.txt");

    // This will store the values as we get them form the stream
    int value;
    while(input >> value) {// Extract next number from input
        cout << "Value read: " << value << endl;
    }
}

void readHaikuWord() {
    // Create our ifstream and make it open the file
    std::ifstream input("haiku.txt");

    // This will store the values as we get them form the stream
    string word;
    while(input >> word) {//Extract next string from input
        cout << "Word read: " << word << endl;
    }
}

void readHaikuLine() {
    // Create our ifstream and make it open the file
    std::ifstream input("haiku.txt");

    // This will store the lines as we get them from the stream
    string line;
    while(std::getline(input, line)) {
        cout << line << endl;
    }
}

int main() {
    readNumbers();
    cout << "==========================" << endl;
    readHaikuWord();
    cout << "==========================" << endl;
    readHaikuLine();
    return 0;
}
```
- $\texttt{When \color{Crimson}<<}$ $\texttt{, \color{Crimson}>>}$  $\texttt{or \color{Crimson}getline()}$ $\texttt{cannot read any data from stream,}$
$\texttt{they will set fall bit as \color{Crimson}true}$ $\texttt{and return \color{Crimson}true}$


