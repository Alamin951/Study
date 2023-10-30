# Java
	

the Java Language Specification(JLS) specifies nine distinct contexts in which an annotation may appear:

1. Module declarations
2. Package declarations
3. Type declarations: class, interface, enum, and annotation type declarations
4. Method declarations (including elements of annotation types)
5. Constructor declarations
6. Type parameter declarations of generic classes, interfaces, methods, and constructors
7. Field declarations (including enum constants)
8. Formal and exception parameter declarations
9. Local variable declarations (including loop variables of for statements and resource variables of try-with-resources statements)
	
### Some meta-annotation:
- @Target: Describes the targets to which an annotation can be applied; this directly corresponds to the nine contexts above. it's mainly used to refer or target another annotation.

- @Retention: Describes how long the annotation should be retained by the compiler

- @Inherited: Denotes that an annotation should be inherited by a subtype if applied to a supertype

- @Deprecated: Denotes that an annotation (or any other type) should no longer be used

- @Repeatable: Denotes that an annotation can be applied multiple times in the same context; i.e. a class can have the same annotation applied 
	to it two or more times
	
	
### Component:
The annotation serves the purpose of differentiating beans from other objects, such as domain objects.
Spring uses the @ComponentScan annotation to gather them into its ApplicationContext.

@Component is an annotation that allows Spring to detect our custom beans automatically.

In other words, without having to write any explicit code, Spring will:

1. Scan our application for classes annotated with @Component
2. Instantiate them and inject any specified dependencies into them
3. Inject them wherever needed but it's better to specialized stereotype annotation to serve the functionality of that method or class.
	
### @Component Limitations:

There are some scenarios where we want a specific object to become a Spring-managed bean when we can’t use @Component.
if the defined @Component is defined outside the project scope.
	 
	 
	
### Spring Stereotype Annotations
- @Controller, @Service, @Repository will act the same because all composed annotations with the @Component as a meta-annotation.
	
### @Component vs @Bean:
	
some important implications because of the differences between @Component and @Bean.
1. @Component is a class-level annotation, but @Bean is at the method level, so @Component is only an option when a class’s source code is editable. @Bean can always be used, but it’s more verbose.
2. @Component is compatible with Spring’s auto-detection, but @Bean requires manual class instantiation.
3. Using @Bean, decouples the instantiation of the bean from its class definition. This is why we can use it to make third-party classes into Spring beans. It also means we can introduce logic to decide which of several possible instance options for a bean to use.
	
	
	
	
### Return statement

- the return statement should be at the end of the code block or it will show an error or the compiler will flag a unreachable code as the rest of the lines will never be executed
	
- to prevent this we need to put the return statement under an if block.

	
	
	
### Type Casting
~~~
int a;
byte b;
// ...
b = (byte) a;
~~~	
- DownCasting object: In object downCasting we need to declare the object on () before the parent object
	~~~
	Dog dog = (Dog) animal; Down Casting / implicit casting
	~~~	
- UpCasting object:
	~~~
	Animal animal = new Animal("Casper", 3);
    animal = dog;
	~~~

### Collection 

- collections can store only references to, not values of primitive types.

- iterator: Another item closely associated with the Collections Framework is the Iterator interface. An iterator offers a general-purpose, standardized way of accessing the elements within a collection, one at a time.
	- Before you can access a collection through an iterator, you must obtain one. Each of the collection classes provides an iterator( ) method that returns an iterator to the start of the collection.
	- ListIterator extends Iterator to allow bidirectional traversal of a list.
	- For collections that implement List, you can also obtain an iterator by calling listIterator( ). As explained, a list iterator gives you the ability to access the collection in either the forward or backward direction and lets you modify an element. Otherwise, ListIterator is used just like Iterator.
	
### Collection Interface
- all collections stored Object references
- An IllegalArgumentException is thrown if an invalid argument is used.
- An IllegalStateException is thrown if an attempt is made to add an element to a fixed-length collection that is full
- s when an attempt is made to add an incompatible object to a collection. A NullPointerException is thrown if an attempt is made to store 
	a null object and null elements are not allowed in the collection
- Objects are added to a collection by calling add(). You can add the entire contents of one collection to another by calling addAll()
- remove an object by using remove(). To remove a group of objects, call removeAll().
- You can remove all elements except those of a specified group by calling retainAll(). To empty a collection, call clear().
- determine whether a collection contains a specific object by calling contains(). To determine whether one collection contains all the members
	of another, call containsAll().
- You can determine when a collection is empty by calling isEmpty().
- The toArray() methods return an array that contains the elements stored in the invoking collection.
- Two collections can be compared for equality by calling equals(). Alternatively, equals() can compare references to those elements.
	
### LIst Interface
- An IndexOutOfBoundsException if an invalid index is used.
- A NullPointerException is thrown if an attempt is made to store a null object and null elements are not allowed in the list
- To the versions of add( ) and addAll( ) defined by Collection, List adds the methods add(int, E) and addAll(int, Collection).

### The Set Interface
- The Set interface defines a set. It extends Collection and declares the behavior of a collection that does not allow duplicate elements.
	
### The SortedSet Interface
- The SortedSet interface extends Set and declares the behavior of a set sorted in ascending order.
- To obtain the first object in the set, call first( ). To get the last element, use last( ).

### Queue Interface
- poll( ) and remove( ). The difference between them is that poll( ) returns null if the queue is empty, but remove( ) throws an exception.
- there are two methods, element( ) and peek( ), that obtain but don’t remove the element at the head of the queue. They differ only in that element( ) throws an exception if the queue is empty, but peek( ) returns null.

### Deque Interface
- Deque includes the methods push( ) and pop( ). These methods enable a Deque to function as a stack. Also, notice the descendingIterator( ) method.
	It returns an iterator that returns elements in reverse order.

### The ArrayList Class
- The ArrayList class extends AbstractList and implements the List interface. ArrayList is a generic class that has this declaration:
	~~~
	class ArrayList<E>
	~~~
- Constructor of ArrayList
	~~~
	ArrayList has the constructors shown here:
	ArrayList( )
	ArrayList(Collection<? extends E> c)
	ArrayList(int capacity)
	~~~
- From arrayList to obtain actual array -> toArray();
	~~~
	Object[ ] toArray( )
	<T> T[ ] toArray(T array[ ])
	~~~

### The LinkedList Class
- The LinkedList class extends AbstractSequentialList and implements the List, Deque, and Queue interfaces It provides a linked-list data structure. 
LinkedList is a generic class that has this declaration:
	~~~
	class LinkedList<E>
	~~~
- Constructor:
	~~~
	LinkedList( );
	LinkedList(Collection<? extends E> c)
	~~~
		
### The HashSet Class
- a hash table stores information by using a mechanism called hashing.
- The advantage of hashing is that it allows the execution time of add( ), contains( ), remove( ), and size( ) to remain constant even for large sets.
- Constructor:
	~~~
	HashSet( )
	HashSet(Collection<? extends E> c)
	HashSet(int capacity)
	HashSet(int capacity, float fillRatio/ loadFactor)
	~~~
	
- The third form initializes the capacity of the hash set to capacity. (The default capacity is 16.)
- The fourth form initializes both the capacity and the fill ratio (also called load capacity) of the hash set from its arguments. The fill ratio must be between 0.0 and 1.0, and it determines how full the hash set can be before it is resized upward. Specifically, when the number of elements is greater than the capacity of the hash set multiplied by its fill ratio, the hash set is expanded. For constructors that do not take a fill ratio, 0.75 is used.
- It is important to note that HashSet does not guarantee the order of its elements, because the process of hashing doesn’t usually lend itself to the 
	creation of sorted sets. If you need sorted storage, then another collection, such as TreeSet, is a better choice.
- the elements are not stored in sorted order, and the precise output may vary.
	
### The LinkedHashSet Class
- LinkedHashSet maintains a linked list of the entries in the set, in the order in which they were inserted.

### The TreeSet Class
- Objects are stored in sorted, ascending order
- Access and retrieval times are quite fast, which makes TreeSet an excellent choice when storing large amounts of sorted information that must be found quickly.

### The PriorityQueue Class
- Heterogenous data is not allowed.
- PriorityQueue extends AbstractQueue and implements the Queue interface. It creates a queue that is prioritized based on the queue’s comparator.
- PriorityQueue defines the six constructors shown here:
	~~~
	PriorityQueue( )
	PriorityQueue(int capacity)
	PriorityQueue(int capacity, Comparator<? super E> comp)
	PriorityQueue(Collection<? extends E> c)
	PriorityQueue(PriorityQueue<? extends E> c)
	PriorityQueue(SortedSet<? extends E> c)
	~~~
- The first constructor builds an empty queue. Its starting capacity is 11.
- To properly use a PriorityQueue, you must call methods such as offer( ) and poll( ), which are defined by the Queue interface.
	
### The ArrayDeque Class
- ArrayDeque class, which extends AbstractCollection and implements the Deque interface
- Constructor:
	~~~
	ArrayDeque( )
	ArrayDeque(int size)
	ArrayDeque(Collection<? extends E> c)
	~~~	
- The first constructor builds an empty Deque. Its starting capacity is 16.
- In all cases, the capacity grows as needed to handle the elements added to the Deque
	
### The EnumSet Class
- EnumSet extends AbstractSet and implements Set
	~~~
	class EnumSet<E extends Enum<E>>
	~~~
- Here, E specifies the elements. Notice that E must extend Enum<E>, which enforces the requirement that the elements must be of the specified enum type. 
	
## Map
- A map is an object that stores associations between keys and values, or key/value pairs 
- There is one key point about maps that is important to mention at the outset: they don’t implement the Iterable
- This means that you cannot cycle through a map using a for-each style for loop. you can’t obtain an iterator to a map. However, as you will soon see, you can obtain a collection-view of a map, which does allow the use of either the for loop or an iterator
- null is not allowed in key of map.

- duplicate key is not allowed but duplicate value is allowed

- The API documentation explicitly states that Identity HashMap is not for general use.
	
##£ HashMap & HashTable 

**HashMap is preferred when we have more number of search operation.**

- underlying data structure is hashTable
- insertion order is not preserved.
- duplicate key are not allowed but duplicate values are allowed

This allows the execution time of get( ) and put( )
While both classes use keys to look up values, there are some important differences, including:

A HashTable doesn't allow null keys or values; a HashMap does.
A HashTable is synchronized to prevent multiple threads from accessing it at once; a HashMap isn't.
	
### Comparators
- Both TreeSet and TreeMap store elements in sorted order
- The Comparator interface defines two methods: compare( ) and equals( ).
	

### Collection Algorithms
Notice that several methods, such as synchronizedList( ) and synchronizedSet( ), are used to obtain synchronized (thread-safe) copies of the various collections.<br>
Collections defines three static variables: EMPTY_SET, EMPTY_LIST, and EMPTY_MAP. All are immutable.
	
### Arrays:
static <T> List asList(T ... array); here the array contains the data.
	
- The copyOfRange( ) method was also added by Java SE 6. It returns a copy of a range within an array and has the following forms:
	~~~.
	static boolean[ ] copyOfRange(boolean[ ] source, int start, int end)
	~~~
	
- The equals( ) method returns true if two arrays are equivalent. Otherwise, it returns false.
	
- The sort( ) method sorts an array so that it is arranged in ascending order. The sort( ) method has two versions. The first version, shown here, sorts the entire array:	
	~~~
	static void sort(byte array[ ])
	~~~	
	
	
	
## Thread-safety: 
- Stateless implementations are the simplest way to achieve thread-safety.
	
- If we need to share state between different threads, we can create thread-safe classes by making them immutable easiest way to make a class immutable is by declaring fields private and final and not providing any setters.
	
- by defining the fields private we can make their fields thread-local. Another way to make thread-local is assigning ThreadLocal instances to a field.
	~~~
	public class ThreadState {

		public static final ThreadLocal<StateHolder> statePerThread = new ThreadLocal<StateHolder>() {
			
			@Override
			protected StateHolder initialValue() {
				return new StateHolder("active");  
			}
		};

		public static StateHolder getState() {
			return statePerThread.get();
		}
	}
	~~~
- Synchronized Collection
	- we can create thread-safe collections by synchronized wrapper included 
		~~~
		Collection<Integer> syncCollection = Collections.synchronizedCollection(new ArrayList<>());
		Thread thread1 = new Thread(() -> syncCollection.addAll(Arrays.asList(1, 2, 3, 4, 5, 6)));
		Thread thread2 = new Thread(() -> syncCollection.addAll(Arrays.asList(7, 8, 9, 10, 11, 12)));
		thread1.start();
		thread2.start();
		~~~
		Synchronized means that the methods can be accessed by only one thread at a time, while other threads will be blocked until the method is unlocked by the first thread.
	
	- Concurrent Collections
		Alternatively to synchronized collections, we can use concurrent collections to create thread-safe collections. Java provides the java.util.concurrent package, which contains several
		concurrent collections, such as ConcurrentHashMap:
		
	### synchronized and concurrent collections only make the collection itself thread-safe and not the content
	
	- **Atomic objects:**
		Atomic classes allows us to perform atomic operations which are thread-safe without using synchronization. An atomic operation is executed in one single machine level operation.
	
	- **Synchronized Method:**
		Synchronized methods rely on the use of “intrinsic locks” or “monitor locks.” An intrinsic lock is an implicit internal entity associated with a particular class instance.
	
	- **Synchronized statement:**
		Sometimes, synchronizing an entire method might be overkill if we just need to make a segment of the method thread-safe. Synchronization is expensive, so with this we can only synchronize 
		only the relevant part of the method or class.
	
	- Other Objects as a Lock:
		
	
	-    Fields:	
	Synchronized methods and blocks are handy for addressing variable visibility problems among threads. Even so, the values of regular class fields might be cached by the CPU. 
	Hence, consequent updates to a particular field, even if they’re synchronized, might not be visible to other threads.
	To prevent this situation, we can use volatile class fields:
	~~~
	public class Counter {
		private volatile int counter;
		
		... ...
		}
	~~~
	
	### The volatile variable ensures that all the variable that are shared to a given thread will be read from main memory.
	
	- **Reentrant Locks:** Reentrant lock can improve the performance of waiting thread queue. It's a underlying mechanism that checks the queued thread and gives priority to the longest waiting thread.
	 ReentrantLock instances allow us to do exactly that, preventing queued threads from suffering some types of resource starvation:
	 	~~~
		private final ReentrantLock reLock = new ReentrantLock(true);
		~~~
		- class that implement the Lock interface. By default the value is false.
		 
	- Real / Write lock:
		it uses a pair of associated locks, one for real-only operations and other for write operation. the thread writing prevent other thread to read on same time.
	
		
#### The Dictionary class is obsolete. You should implement the Map interface to obtain key/value storage functionality.
 

	
### Java.net package
- provides the classes for implementing the networking related task or implementation on application.
Divided into two sections:
1. Low level API:
	- Addresses, which are networking identifiers -> IP addresses
	- Sockets, which are basically bidirectional data communication mechanisms.
	- Interfaces, which describe network interfaces.
2. High Level Api: 
	- URIs, Which represents Universal Resource Identifiers,
	- URLs, which represent Universal Resource Locators.
	- Connections, which represents connections to the resource pointed to by URLs.
	
### Sockets
Sockets are means to establish a communication link between machines over the network. The java.net package provides 4 kinds of Sockets:

**Socket** is a TCP client API, and will typically be used to connect to a remote host.<br>
**ServerSocket** is a TCP server API, and will typically accept connections from client sockets.<br>
**DatagramSocket** is a UDP endpoint API and is used to send and receive datagram packets.<br>
**MulticastSocket** is a subclass of DatagramSocket used when dealing with multicast groups.<br>
Sending and receiving with TCP sockets is done through InputStreams and OutputStreams which can be obtained via the Socket.getInputStream()
and Socket.getOutputStream() methods.
	
### Future object
 In java when we move to another thread  and the previous thread is executing some task now if we want to keep a track or track its progress then we can use future object to let us know when its done
 	
	