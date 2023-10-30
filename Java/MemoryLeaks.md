# Memory Leaks in Java
One of the core benefits of Java is the automated memory management with the help of the built-in **Garbage Collector( GC )**. The GC implicitly takes care of allocating and freeing up memory, and this handles the majority of memory leak issues. **But it doesn't guarantee thee foolproof solution of memory leakage.** <br>
There might still be situations where the application generates a substantial number of **Unnecessary objects**, thus depleting crucial memory resources, and sometimes resulting in the whole application’s failure.

### Memory Leak
Memory leak is a situation where the objects are present but there is no use of that object and  the garbage collector is unable to remove them from the memory. <br>
If we don't deal with it there is a possibility that this will cause performance issues over time.
![Memory Leaks](images\Memory-_Leak-_In-_Java.webp)