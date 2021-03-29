# whats a exception 
* short hand "exceptional event"
* is a event that occors during the execution of a program that disrupts a normal flow.
* so when a error occurs within a method the method crfeates aan object and hands it off to the runtime system the object called an execption object contains info about the error and its type and tyhe state of the preogram when error occured. The action of creating an exception object and handing it to the runtime system this is called throwing an exception.
* so after the method throws ythe execption the runtime system trys to find something to handle it. the set of possible "somthings" to handle exception is the ordered list of methods tha had beeen called to get to the method where the error ocurred. AKA "call-stack".

# Exception handler
* the runtime system searches the call stack for a method that contains a block of code to handle the exception. AKA "this is a exception handler". 


# Exception Handler Actions 
* The search begins with the method in which the error occurred and proceeds through the call stack in the reverse order in which the methods were called. When an appropriate handler is found, the runtime system passes the exception to the handler. An exception handler is considered appropriate if the type of the exception object thrown matches the type that can be handled by the handler.

# the catch 
* must honor catch or specify 
* a try statement that catches the exception , a try must provide a handler for the exception 
* a method that specifes that it can throw the exception the method must provide a throws clause the lists out the exception 

# 3 Kinds of exceptionds 

* Checked eception - conditions that a well written application should anticipate and recover form it.

* Error - exceptional conditions that are external to the application, and that the application usually cannot anticipate or recover from. For example, suppose that an application successfully opens a file for input, but is unable to read the file because of a hardware or system malfunction. The unsuccessful read will throw java.io.IOError. 

* The third kind of exception is the runtime exception. These are exceptional conditions that are internal to the application, and that the application usually cannot anticipate or recover from. These usually indicate programming bugs, such as logic errors or improper use of an API. For example, consider the application described previously that passes a file name to the constructor for FileReader.


# Example - 
### public Object pop() {
###    Object obj;

###    if (size == 0) {
###        throw new EmptyStackException();
###    }

###    obj = objectAt(size - 1);
###    setObjectAt(size - 1, null);
###    size--;
###    return obj;
### }