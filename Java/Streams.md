# Streams

By using Filter and Map we can process the data from Collection. we use lambda expression for this.

### Filter:
Filter the data from stream of collection.

***Stream<T> filter(Predicate<? super T> predicate)***

Returns a stream consisting of the elements of this stream that match the given predicate.
This is an intermediate operation.

*Parameters:*
predicate - a non-interfering, stateless predicate to apply to each element to determine if it should be included

Returns:
the new stream

### Map:
Map the data to a stream. It returns a stream.

***<R> Stream<R> map(Function<? super T,? extends R> mapper)***

Returns a stream consisting of the results of applying the given function to the elements of this stream.
This is an intermediate operation.

*Type Parameters:*
*R* - The element type of the new stream

*Parameters:*
mapper - a non-interfering, stateless function to apply to each element

*Returns:*
the new stream

### Sorted: 
Sort the data.

### Count() 
Count the data or value.

### Collect(): 
After filter the data we can collect the data and store it to somewhere.

### distinct(): 
To select unique value.

### foreach()
Iterate each value of the stream.

**void forEach(Consumer<? super T> action)**
Performs an action for each element of this stream.
This is a terminal operation.

The behavior of this operation is explicitly nondeterministic. For parallel stream pipelines, this operation does not guarantee to respect the encounter order of the stream, as doing so would sacrifice the benefit of parallelism. For any given element, the action may be performed at whatever time and in whatever thread the library chooses. If the action accesses shared state, it is responsible for providing the required synchronization.

Parameters:
action - a non-interfering action to perform on the elements

### min(): 
Find minimum value.

### max(): 
Find maximum value.

### FlatMap: 
**<R> Stream<R> flatMap(Function<? super T,? extends Stream<? extends R>> mapper)**

Returns a stream consisting of the results of replacing each element of this stream with the contents of a mapped stream produced by applying the provided mapping function to each element. Each mapped stream is closed after its contents have been placed into this stream. (If a mapped stream is null an empty stream is used, instead.)

This is an intermediate operation.

**API Note:**
The flatMap() operation has the effect of applying a one-to-many transformation to the elements of the stream, and then flattening the resulting elements into a new stream.

**Examples:**

If orders is a stream of purchase orders, and each purchase order contains a collection of line items, then the following produces a stream containing all the line items in all the orders:


     orders.flatMap(order -> order.getLineItems().stream())...
 
If path is the path to a file, then the following produces a stream of the words contained in that file:


     Stream<String> lines = Files.lines(path, StandardCharsets.UTF_8);
     Stream<String> words = lines.flatMap(line -> Stream.of(line.split(" +")));
 
The mapper function passed to flatMap splits a line, using a simple regular expression, into an array of words, and then creates a stream of words from that array.
Type Parameters:
R - The element type of the new stream
Parameters:
mapper - a non-interfering, stateless function to apply to each element which produces a stream of new values

Returns:
the new stream

Also:
***mapMulti(java.util.function.BiConsumer<? super T, ? super java.util.function.Consumer<R>>)***

We don't process the data directly from collection, make a stream of it and process it or map to another collection.


### Ref Link:
[Official Documentation](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/stream/Stream.html)