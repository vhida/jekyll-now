Java IO is designed te work with stream. Each time one or more bytes are read from stream until the end. They are not buffered. The reader can’t move forward or backward in the stream as well. If that is needed, data from stream has to be stored somewhere first.   
Java NIO, instead, works with buffer. Data are read to a buffer which user can manipulate later. More flexibility.   
For instance, with InputStream or Reader, data from a row based txt file, is read consecutively, in this case, line by line.    

```
InputStream input = … ; // get the InputStream from the client socket
BufferedReader reader = new BufferedReader(new InputStreamReader(input));
String nameLine   = reader.readLine();  
String ageLine    = reader.readLine();  
String emailLine  = reader.readLine();  
String phoneLine  = reader.readLine();  
```  
The processing status is decided by the progress of the execution. If reader.readLine() returns, reading one particular line is finished. The method itself is blocked until one whole line is read in. The reader only keeps the line it is reading. After it finishes, it has no hook on the previous data.      
    
The principle is, Java IO is blocked. That means, whenever a thread calls read() or write(), it is blocked, until the IO operation finishes. Java NIO works differently though. A thread opens a channel(a key class in Java NIO library) and use it to send request to read data. If where’s no readable data available, the thread can proceed to do other work, instead of waiting, usually executing IO operations in other channels because one single thread can handle multiple channels. The same applies for write operation.      
Java NIO ibrary contains 3 main classes.  
# Channel  and Buffer   
Almost all IOs in Java NIO starts with a channel. Data can be read from channel to butter and written to channel from butter.    
Channel implementations in JAVA NIO includes, which covers udp, tcp network IO and file IO.  
```
FileChannel  
DatagramChannel  
SocketChannel  
ServerSocketChannel   
``` 
And the implementations of some key buffer covers all basic java data types that transfer using IOs.       
```
ByteBuffer  
CharBuffer  
DoubleBuffer  
FloatBuffer  
IntBuffer  
LongBuffer  
ShortBuffer  
```
# Selectors   
    
Selectors enables one thread to monitor multiple channels. It becomes handy when multiple channels have to be kept and each has low and non-consecutive traffic, for example, a chatting service. User can register multiple channels to one selector and then use select() to “select” working channel with a single thread.     

