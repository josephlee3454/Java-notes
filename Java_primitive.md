# Java Primitive

## Java Type System 
* Java has a two fold system consisting of primitives such as int, and reference types such as integer and boolean.
* objects contains a single value of the corresponding primitive type. wrapper classes are immutable(so the state dosnt change if obj constructed)

### Example:
#### Integer j = i;// autoboxing 
#### int i = new Integer(1);/// unboxng 

## Memory Foot print of single item
* Boolean - 1 bit.
* byte - 8 bits.
* short, char - 16 bits.
* int , float - 32  bits.
* long, double - 64 bits.


## Performance 
* Java's performance code is a subtle issue it all depends on the the hardware on which the code runs. the compiler that migth perform certain operations while your compiling, the state of the vm , and other activity performed by the the operating sytem 

## default values
* the default value fot the primitive types are 0 for numerical types, fales for boolean type , \u0000 char type , wrtapper class is null.
* this means that primitive types only may accurie values from their domain. while ref type might get a null value that really dosnt belong in their domain

## Usage 
* primitive types are much faster and require less memory which is why it might be perferred by the developer.

