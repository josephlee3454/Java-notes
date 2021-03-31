# Solid

## S single responsibility principal
* uncle bob says a class should have only one reason to change
* this means class should have only one job 

## O open closes principle
* uncle bob says that Objects should only be open for extension but closed for modification 
* what this means is that the extendable class sshould only do that extend its self to another class you should never have to modify the class itself 

## L Liskov substion 
* uncle bob says Let q(x) be a property provable about objects of x of type T. Then q(y) should be provable for objects y of type S where S is a subtype of T.
* in english this means that every subclass should be subsitable form their parent

## I Interface Segregation Principle
* uncle bob says A client should never be forced to implement an interface that it doesn’t use, or clients shouldn’t be forced to depend on methods they do not use
* just dont include shit that is uncessary like just becuase you you have a get method in another class dosnt mean you need one in the class and interface it is not being used 


## D Dependency Inversion Principle
* uncle bob says Entities must depend on abstractions, not on concretions. It states that the high-level module must not depend on the low-level module, but they should depend on abstractions.
* this means that we are allowed to decouple. 