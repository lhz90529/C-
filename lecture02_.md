## [StreamII](http://web.stanford.edu/class/cs106l/lectures/lecture02/02_Streams_II.pdf )
  
  
### <img src="https://latex.codecogs.com/gif.latex?&#x5C;textbf{Buffering}"/>
  
<img src="https://latex.codecogs.com/gif.latex?&#x5C;text{Writing%20to%20console&#x2F;file%20is%20a%20slow%20operation}"/>
> <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{If%20the%20program%20had%20to%20write%20each%20character%20&#x5C;textbf{immediately},}"/>
<img src="https://latex.codecogs.com/gif.latex?&#x5C;text{the%20runtime%20would%20&#x5C;textbf{significantly%20slow%20down},%20What%20can%20we%20do?}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{Accumulate%20characters%20into%20a%20buffer}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{When%20buffer%20is%20&#x5C;textbf{full},%20write%20out%20all%20contents%20of%20the%20buffer%20to%20the%20output%20device%20&#x5C;textbf{at%20once}}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{This%20process%20is%20known%20as%20&#x5C;textbf{flushing}%20the%20stream}"/>
  
### <img src="https://latex.codecogs.com/gif.latex?&#x5C;textbf{Flushing%20the%20Buffer}"/>
  
<img src="https://latex.codecogs.com/gif.latex?&#x5C;text{If%20you%20want%20to%20force%20the%20content%20of%20the%20buffer%20to%20their%20destination,%20we%20can%20flush%20the%20stream}"/>
```c++
stream.flush();
stream<<std::flush;
```
  
<img src="https://latex.codecogs.com/gif.latex?&#x5C;textbf{Not%20all%20streams%20are%20buffered}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{&#x5C;color{Crimson}{std::cerr}}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{is%20not%20buffered}"/>
    - <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{Each%20time%20you%20insert%20something%20into%20it,%20it%20flush%20immediately}"/>
-  <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{&#x5C;color{Crimson}{std::cout}}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{is%20buffered}"/>
    - <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{&#x5C;color{Crimson}{std::cout}}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{will%20only%20flush%20if}"/>
        - <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{it%20reaches%20maximum%20capacity}"/>
        - <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{you%20explicitly%20ask%20it%20to%20do%20so}"/>
### <img src="https://latex.codecogs.com/gif.latex?&#x5C;textbf{Stream%20bits}"/>
  
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{&#x5C;color{DarkGreen}{Good%20bits}}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{No%20errors,%20the%20stream%20is%20good%20to%20go}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{&#x5C;color{Black}{EOF%20bits}}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{End-of-file%20was%20reached%20during%20a%20previous%20operation}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{&#x5C;color{DarkRed}{Fail%20bits}}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{Logical%20error%20on%20a%20previous%20operation}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{&#x5C;color{DarkRed}{Bad%20bit}}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{Likely%20unrecoverable%20error%20on%20previous%20operation}"/>
  
### <img src="https://latex.codecogs.com/gif.latex?&#x5C;textbf{Chaining}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{&#x5C;color{Crimson}{&gt;&gt;}}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{or%20&#x5C;color{Crimson}{&lt;&lt;}}"/>
  
<img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{&#x5C;color{Crimson}{&gt;&gt;}}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{and%20&#x5C;color{Crimson}{&lt;&lt;}}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{are%20not%20magic,%20they%20are%20actually}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;textbf{functions}"/>
  
<p align="center"><img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{std::cout&lt;&lt;&quot;hello&quot;;}	%20	&#x5C;xleftrightarrow{&#x5C;texttt{is%20equivalent%20to}}%20&#x5C;texttt{operator&lt;&lt;(std::cout,%20&quot;hello&quot;)}"/></p>  
  
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{&#x5C;color{Crimson}{&gt;&gt;}}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{is%20&#x5C;textbf{function}}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{std::cout%20and%20hello%20are%20function&#x27;s%20&#x5C;textbf{arguments}}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{&#x5C;color{Crimson}{&gt;&gt;}}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{&#x5C;textbf{return%20the%20stream}%20%20passed%20as%20its%20left%20argument}"/>
- <img src="https://latex.codecogs.com/gif.latex?&#x5C;text{That&#x27;s%20why%20we%20can%20chain%20a%20lot%20of%20}"/> <img src="https://latex.codecogs.com/gif.latex?&#x5C;texttt{&#x5C;color{Crimson}{&gt;&gt;}}"/>
  
### <img src="https://latex.codecogs.com/gif.latex?&#x5C;textbf{Stream%20Manipulator}"/>
  
<img src="https://latex.codecogs.com/gif.latex?&#x5C;text{Useful%20when%20you%20need%20to%20format%20your%20data}"/>
[Check this link](http://www.cplusplus.com/reference/library/manipulators/ )
  