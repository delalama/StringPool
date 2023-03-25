## WHAT IS THIS ABOUT ?

### Understand String immutability

#### Is pretty known that in JAVA, String class is immutable.....yes?

So................

```java
String string1 = "a";
string1 = "b";
```

Have we change an immutable object?
No, we have only changed the reference of a variable.

Why is this possible ? 
It's possible because the JVM has created 2 immutable strings instances and 1 variable
and 1 String object

1 - "a" // instances

2 - "b" // instances

3 - string1 // variable

Variable "string1" has changed its reference from "a" to "b".

So don't confuse String variables with String instances.

```java

// given
String string1 = "a";
// "a" String is stored in the String pool
// string1 receives the reference of "a"
System.identityHashCode("a");
System.identityHashCode(string1);
Assertions.assertEquals("a", string1);
```


In this example we see that creating a String object
(not good practice) assigns different memory location
```java

// given
String a = new String("a");
String b = new String("a");

// then
int idA = System.identityHashCode(a);
int idB = System.identityHashCode(b);
Assertions.assertNotEquals(idA, idB);
```

but.........
```java
// given
String a = new String("a");
String b = new String("a");
String c = "a";
String d = "a";


int idA = System.identityHashCode(a);
int idB = System.identityHashCode(b);
Assertions.assertNotEquals(idA, idB);

int idC = System.identityHashCode(c);
int idD = System.identityHashCode(d);
Assertions.assertEquals(idC, idD);

LinkedHashSet map = new LinkedHashSet();
map.add(a);
map.add(b);
map.add(c);
map.add(d);  // size = 1 !!!  WTF!!!

```

LinkedHashSet class has a HashMap object to store elements, across this method:
  
map.put 
And inside the implementatino we can find:

```java
key.equals(k)
  ```
This method is used to find repeated String values.

So it does not mind how many different variables we declare, all variables that has
the same value will share their reference, end of story.

