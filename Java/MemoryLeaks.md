# Memory Leaks in Java
One of the core benefits of Java is the automated memory management with the help of the built-in **Garbage Collector( GC )**. The GC implicitly takes care of allocating and freeing up memory, and this handles the majority of memory leak issues. **But it doesn't guarantee thee foolproof solution of memory leakage.** <br>
There might still be situations where the application generates a substantial number of **Unnecessary objects**, thus depleting crucial memory resources, and sometimes resulting in the whole application’s failure.

### Memory Leak
Memory leak is a situation where the objects are present but there is no use of that object and  the garbage collector is unable to remove them from the memory. <br>
If we don't deal with it there is a possibility that this will cause performance issues over time. The GC removes unreferenced objects periodically but never collects the objects that is still referenced. 

![Memory Leaks](../images/Memory-_Leak-_In-_Java.webp)

### Symptoms of a Memory Leak
- Severe performance degradation when the application is continuously running for a long time
- OutOfMemoryError heap error in the application
- Spontaneous and strange application crashes
- The application is occasionally running out of connection objects.

## Types od Memory Leaks
### Memory Leak through *static* Fields
- heavy use of static variables in code. static fields have a entire lifetime of the running application unless the class becomes GC.
    ~~~
    public class StaticFieldsMemoryLeakUnitTest {
        public static List<Double> list = new ArrayList<>();

        public void populateList() {
            for (int i = 0; i < 10000000; i++) {
                list.add(Math.random());
            }
            Log.info("Debug Point 2");
        }

        public static void main(String[] args) {
            Log.info("Debug Point 1");
            new StaticFieldsDemo().populateList();
            Log.info("Debug Point 3");
        }
    }
    ~~~
    on this code block when we leave the populateList() method at the debug point 3 but the heap memory is not the garbage collected yet. but if we drop the static keyword then will we be collected by GC as there is no reference on it.
- by declaring a large object or list will hold the memory space of application lifetime.

#### Prevent
- maximize the use of *static* variable
- when use singletons< rely on the implementation that lazily loads the object instead eagerly loading.

### Through Unclosed Resource
Whenever we use new connection or open stream the JVM will allocates corresponding memory for this resource.
- like: *Database connections*, *input Stream*, *session Objects*.

if we don't close this connection then these open connections reach out of GC's range. sometimes this occurs for throwing exception before closing the connections.

- This may result the *OutOfMemoryError*

#### Prevent
- Always use Finally block when we need to close resources
- The codes inside the Finally should not contain any exception
- On Java 7+ we can use try-with-resources block
    ~~~
    try (FileReader fr = new FileReader(path);
	         BufferedReader br = new BufferedReader(fr)) {
	        return br.readLine();
	    }
    ~~~

### Improper *equals()* and *hashCode()* Implementations
While declaring a new class we shouldn't oversight *equals()* and *hashCode()* method. if they are not properly declared they can become the source for memory leak. 

For this small ignorance equals object can pile up and can lead to performance issues for heap memory in VirtualVM.

#### Prevent
- As a rule of thumb, when defining new entities, always override the equals() and hashCode() methods.
- It’s not enough to just override, these methods must be overridden in an optimal way as well.