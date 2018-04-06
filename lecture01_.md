## [StreamsI](http://web.stanford.edu/class/cs106l/lectures/lecture01/01_Streams.pdf )
  
  
<img src="https://latex.codecogs.com/gif.latex?&#x5C;text{C++&#x27;s%20stream%20library%20is%20the%20means%20by%20which%20a%20C++%20program%20can%20&#x5C;textbf{interact}%20with%20its%20environment,}"/>
-  <img src="https://latex.codecogs.com/gif.latex?&#x5C;textbf{the%20user%20and}"/> 
-  <img src="https://latex.codecogs.com/gif.latex?&#x5C;textbf{the%20file%20system}"/>
  
  
```c++
#include <iostream>
  
int main() {
    std::cout << "Hellow World!" << std::endl;
    return 0;
}
```
<img src="https://latex.codecogs.com/gif.latex?&#x5C;text{The%20program%20above%20can%20&#x5C;textbf{get%20annoying}%20to%20write%20for%20common%20names%20like}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{&#x5C;color{Crimson}{cout}}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{&#x5C;color{Crimson}{endl}}"/>
  
```c++
#include <iostream>
  
using std::cout;
using std::endl;
int main() {
    cout << "Hellow World!" << endl;
    return 0;
}
```
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{Whenever%20you%20use%20&#x5C;color{Crimson}{cout}}"/> <img src="https://latex.codecogs.com/gif.latex?,&#x5C;text{the%20compiler%20will%20assume%20you%20mean%20&#x5C;color{Crimson}{std::cout}}"/>
  
### <img src="https://latex.codecogs.com/gif.latex?&#x5C;textbf{Stream}"/>
  
<img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{An%20abstraction%20for%20I&#x2F;O}"/>
  
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
<img src="https://latex.codecogs.com/gif.latex?&#x5C;text{You%20can%20write%20data%20of%20multiple%20types%20to%20stream%20objects}"/>
```c++
cout << "Strings work!" << endl;//you can push data of string type into stream
cout << 1729 << endl;//integer type
cout << 3.14 << endl;//double type
cout << "Mixed types - " << 1123 << endl;//mix
```
<img src="https://latex.codecogs.com/gif.latex?&#x5C;textbf{In%20particular,%20any%20primitive%20type%20can%20be%20inserted%20into%20a%20stream!}"/>
<img src="https://latex.codecogs.com/gif.latex?&#x5C;text{For%20other%20types,%20you%20need%20to%20&#x5C;textbf{explicitly}%20tell%20C++%20how%20to%20do%20this.}"/>
  
#### <img src="https://latex.codecogs.com/gif.latex?&#x5C;textbf{Output%20Stream}"/>
  
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{Can%20only%20receive%20data}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{Operator%20Insertion:}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{&#x5C;color{Crimson}{&lt;&lt;}}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{Insertion%20converts%20data%20to%20string%20and%20sends%20to%20stream}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{You%20can%20send%20the%20data%20to%20a%20file%20using%20a%20&#x5C;color{Crimson}std::ofstream}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{,%20which%20is%20a%20special%20type%20of%20&#x5C;color{Crimson}std::ostream}"/>
  
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
  
### <img src="https://latex.codecogs.com/gif.latex?&#x5C;textbf{Input%20Stream}"/>
  
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{Can%20only%20give%20you%20data}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{The%20&#x5C;color{Crimson}{std::cin}}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{is%20an%20example%20of%20an%20input%20stream}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{Operator%20Extraction:}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{&#x5C;color{Crimson}{&gt;&gt;}}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{Extraction%20gets%20data%20from%20stream%20as%20a%20string%20and%20converts%20it%20into%20the%20appropriate%20type}"/>
  
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
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{When%20&#x5C;color{Crimson}&lt;&lt;}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{,%20&#x5C;color{Crimson}&gt;&gt;}"/>  <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{or%20&#x5C;color{Crimson}getline()}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{cannot%20read%20any%20data%20from%20stream,}"/>
<img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{they%20will%20set%20fall%20bit%20as%20&#x5C;color{Crimson}true}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{and%20return%20&#x5C;color{Crimson}true}"/>
  
  
  