###
###
###
chapter 1 
clean code 

Total cost of owning a mess. Unclean code leads to decrease of productivity.
The management recruits more people. The new employees dont understand the 
system which leads less productivity and to a faster growing of the mess.

When it comes to the project the manager is defending the schedule and the 
programmer is definding the (clean) code.
It is unprofessional to bend to the will of managers who dont understand the 
risks of making a mess.

The only way to go fast is to keep the code as clean as possible at all time .
Not write a mess to fulfill the deadline. 

What is clean code?

Clean code is focused. (Single Responsibility Principle)
It should contain only what is necessary.
Is easy to read and for others to enhance.
Smaller is better.
Readable by humans.
Is Tested.
Looks like it was written by someone who cares about the code.
Reduced duplication, high expressivness, and early building of simple 
abstractions is clean code.
The code may look like the language was made to solve the problem.
In fact the programmer can use the laanguage so it looks like this is the case.


Simple code...
Runs all the tests.
Contains no duplication.
Expresses all the design ideas that are in the system.
Minimizes the number of entities such as classes, methods, 
functions, and the like.

Read to write Ratio 10:1. Reading 10 times more code than writing it.
So readability and clean coed matters.
The Boy scout rule. Leave the campground cleaner than u found it.


###
###
###
Chapter 2
Meaningful names

Use intention-revealing names.
Not "t" but "timeSpent".

Avoid Disinformation
Dont use Collection types like list or collection in a name.
Not "accountList" but "accounts".
Dont use "l" and "O" since can visually interpreted as 1  and 0.

Make meaningfull distinctions.
Dont use "klass" because "class" is reserved by the compiler.
Dont use meaningless noise words like "Info", "Data", "Object", "Variable", 
"(all kind of datatype names)".
Use names so the reader can immediatly understand the difference between 2 
names.

Use pronounceable names 

Use Searchable names
Not "n" but "userCount". Since "n" can be found thousends of times.
The length of a name should correspond to the size of its scope.

Avoid encodings
No Hungarian notation. $varaibleName the $ signs the variable as a string.
Dont use member prefixes like "m_".
Dont name an interface "IMyInterfaceName". The leading "I" tells all that 
is they are using an interface. Better name the concrete implementation 
different.

Avoid mental mapping
Clarity is king. Professionals use their abilities to write code that other can 
read by using meaningful names.

Class names
Use nouns or noun phrase names.


Method names
Use verbs or verb phrase names.
When constructors are overloaded use static factory methods that describe
the arguments instead of the simply overloaded constructor.
bad: 
    new Complex(23.0) 
good:
    new Complex.FromRealNumber(23.0)

Dont be cute
No humor in names. Be concrete and factual.

Pick one word per concept
Pick one word for an abstract concept and stick with it.
E.g. use "get" in all accessing function names and not one time 
"get" and in another class "fetch".
Or "Controller", "Manager", "Handler". Decide one and stick with it.

Dont pun (word games)
E.g. using "add" means in all classe creates a new value.
Then dont use "add" but "insert" when adding values to an array.

Use solution domain names
Use computer science terms like patterns, algorithems and math terms in your 
names.

Use problem domain names 
If the name can not be given by the solution domain use a name from the 
problem domain instead.

Add meaningful context 
Instead of make variables holding firstname, lastname, street, state use 
a class  Address that has these fields.

Dont add gratuitios context 
E.g. Application BreakdownPlanGuide. Dont prefix every class with bpg.
Shorter is better. Only add words that add information to the name.

###
###
###
Chapter 3 
functions

Should be small.
Should be smaller than that(the function u are currently writing).

Blocks and indenting
Between if, else, while statemnets should only be one line.
Usually calling another function. This is also documentary since the function 
can show intent by a well chosen name.

Does one thing and does it well.
Difficulty is the defintion of what is one thing.
Generally speaking "one thing" means all the steps that are needed to fulfill
the job of the function as described in its name BUT only one step below.

Sections within functions 
A function may not have sections but calling other fuctions instead.
Sections in a function are an obvious symptom of doing more than one thing.

One Level of abstraction per function
There should be no mix of low, middle or high level of abstractions like 
calling File.getHTML() and File.append("\n") in the same function.

Stepdown rule: Reading code from top to bottom
Function calls may be read like TO-paragraphs and therefore build a letter 
of abstractions.

    To copy text from a file, we open a file if the file exists, then we buffer 
    the file content from an opened file, then we close the file and then we 
    return the buffer.

    To open a file we check for the file to open, then we create a file object, 
    then we return the file object.

Switch statements 
Each switch statement should do only one thing. 
Do this by using polymorphism.
Switch statemnets can be tolerated if 
they appear only once in the code
are used to create polymorphic objects 
are hidden behind an inheritance relationship so the rest of the system can not 
see them.
See the example in the book. 
abstract class Employee 
interface EmployeeFactory 
class EmployeeFactoryImplementation implements EmployeeFactory
(contains the switch statement) 

Use descriptive names 
Short names are easier to chose if a function does only one thing.
But long descriptive names are better than short enigmatic names.
Use the same phrases, nouns, verbs for function names.
E.g. findSetupPage, deleteSetupPage for SetupPage then in case of a 
TeardownPage use the same names for the same logic e.g. 
findTeardownPage, deleteTeardownPage

Function Arguments 
As less as possible.
Preferably no more than 3.
Preferably is 0, 1, 2, 3.
One Reason is the abstraction the reador of the code need to interpret 
the argument when he is reading.
Second testing more than 2 arguments is hard. Since all the combinations need 
to be tested.

Common monadic forms (1 argument)
3 common forms are testing the argument for a bool. FileExists(File) 
or modify the argument then return the modified argument. WriteNextLine(File)
Events like passwordFailedNTimes(int attempts) does not return a value 
but changes state of the system.

Any other forms do not use single argument (monadic forms)
Avoid functions that transform the input and instead of return it as a value
using an output argument.

Important there are only these 3 monadic forms 
1. test the argument for a bool.
2. transoform the argument and return the modified value 
3. Events

Flag Arguments 
DO NOT PASS BOOL VALUES INTO FUNCTIONS. This because it harms the rule that 
a function does only one thing since it does one thing if bool is true else
it does another thing.

Dyadic Functions (2 arguments)
Are more difficult to read than monadic. Since the 2 arguments have no natural 
ordering and neither natural cohesion.
E.g. AssertEquals(expected, actual) needs to be learned that the first argument 
is the expected value and actual value is second.
Prefer make Dyadic to Monadic if possible.
E.g. where it should be dyadic new Point(x, y)

Tryads (3 arguments)
Are harder to understand since the amount of arguements to ignore are more than 
the double.
Try to reduce arguments if possible.
A good way is to use argument objects.

Argument objects 
If a function takes 2 or more arguments try to wrap the arguments into a class 
E.g. makeCircle(double x, double y, double radius) 
better use makeCircle(Point center, double radius) 

Argument Lists 
If the arguments that are passed are treated the same in the function, then they
are equivalent to a single argument of type list.

Verbs and Keywords
keyword form
This form encodes the argument into the function name.
E.g. instead of assertEquals() use assertExcpectedEqualsActual(expected, actual)
The name of the function gives clue to the ordering of the arguments.

Have no side effects
A function promises to do one thing but does hidden other things. This harms
the "does one thing" principle.
E.g. a function called checkPassword() also initialises the session.
The initializing of the session should be placed in another function or at least
the function renamed to checkPasswordAndInitializeSession().

Output Arguments 
Using appendFooter(s) is confusing since the reader can not know if "s" gets 
appended to a footer or a footer is appended to "s".
Dont use output arguments in OO. Looking up the function signature means a 
double-take in time and should be avoided.
Use report.appendFooter() instead and use the "this" keyword as the output 
argument. If the function needs to change the state of something, have it change
the state of its iwning object.

Command Query Separation
Functions may either do something or answer something but not both.
Separate the command from the query. 
Means e.g. 
if(set("username", "bob"))
should be 
if(attributeExists("username")){
    setAttribute("username", "bob")
}

Prefer exceptions over returning error codes
Long story short dont use error codes but exceptions.

Extract Try/Catch Blocks 
Instead of directly write into Try/Catch blocks write their own functions 
to call in the block. For the try logic as well as for the error handling logic
even if it is only a error.log().

Error handling is one thing 
Means in a function with a try and catch block the try should be the 
first word and after catch or finally there should be no more code in the block.

The Error.java dependency magnet
Exceptions might be inherited from the Exception Base Class so when more errors
are added not all the code needs to be changed. No recompilation and 
redeployment needed.

Dont repeat yourself DRY 
Remove code duplication in all its occureneces.

Structured Programming 
Only relevant rule is to never use goto statements.
Other rules are obsolete since make no sense for small functions.

Write functions as desribed inthis chapter is an iterative process.
Every function starts ugly and gets redefined over iterations of clean up.


###
###
###
chapter 4 

Avoid comments whereever possible.
Instead of write a comment rewrite the code so it is self explaining.

There are the following cases where a comment is valid:

1. Informative Comment 
E.g. Describing the format of a regular expression.

2. Explanation of Intent.
Decribing why the implementation detail was chosen.

3. Warning of consequences  
E.g. A unit test that is ignored because of it's high execution duration.

4. TODO
TODO comment may describe issues that the programmer recognized but for some
reason thinks, could be solved better in the future.

5. Amplification 
Comments can be used to amplify the importance of a code snippet.

6. (Java) Docs for public APIs. 
Good for public APIs.
Unnecessary for non public system components.
Java Docs that don't add additional information are noise as well.


### 5. Code formatting

1. Vertical Formatting
A typical file size of 200 with an upper limit of 500 lines can be considered 
desirable.

2. Vertical Openness 
Do separate functions by line breaks.
Keep together what belongs together.
Declare variables as close to their ussage as possible.
Declare instance variables at the top of the class.
Order the calling functions above callee functions.
Group conceptual equal functions togehter.  

3. Horizontal Formatting 
The maximum amount of characters by line is 120.
Try to stay at 80 characters per line.
Use indentation. After the opening braces and before the clsing braces use a
line break.

4. Team Rules
When create a software the team should unite for code formatting rules 
and every one has to follow the rules elected.


### 6. Objects and Data Structures 

1. Hide implementation details by abstraction
Don't make your private variables public.
Don't generate getters and setter for all variables.

2. Data/Object Anti-Symmetry
Objects hide internal data and expose functions to operate on their data (Object Oriented Programming).
Object Oriented code makes it easy to add new classes without changing existing functions.

Data structures (DTO) have no functions but expose their data (Proceedural Programming).
Procedural code makes it easy to add new functions without changing data structures (DTO).

Dont' mix data structures and objects (hybrid). 
It's hard to add functions and new classes to hybrids. 

3. Law of Demeter
An object should not know about the innards of an object it manipulates.
A method *f* of a class *C* should only call methods of ...
* *C*
* An object created by *f*
* An object passed as an argument to *f*
* An object held in an instance variable of *C* 
Don't invoke methods of objects that are returned by any of the allowed functions.
E.g. final String outputDir = ctxt.getOptions().getScratchDir().getAbsoluePath(); (Train wreck).
Train wrecks can be avoided by using a single method abstracting the steps to create the e.g. outputDir.

4. Data Transfer Object (DTO)
A class with public variables and no functions.
They are used to translate raw data into objects of application code.
Beans can be DTOs, the getters and setters make variables public.


### 7. Error Handling 

1. Use exceptions rather than return codes.

2. When writing a function with a potetional exception beeing thrown.
Write the try-catch-finally block first. 
Due to the fact that exceptions have their own scope.
The catch block is exectuted whenever the try block fails.

The catch block is meant to lead to a fail-safe-state so the program can continue running.
3. Use unchecked exceptions.
Checked exceptions violate the Open Closed Principle (OCP).
Top level functions call lower level functions which can throw checked exceptions.
If the top level function needs to handle the checked exception it has a dependency to the low level function.
If the checked exception changes in the low level function the exception handling in the top level function needs to be changed as well.
This is a violation of the OCP.
Checked exceptions can be useful when writing a critical library.

4. What belongs to a good exception
* A timestamp
* The operation that failed
* A reason describing why the operation failed
* The stack trace
Log exceptions.

5. Error classification 
Use wrapper classes around 3rd party API and add a general Exception to handle mutltiple exceptions of the API.
E.g. The class of the 3rd party API throws 3 different exceptions.
Wrap the class with your own class and call the method that throws 3 different exceptions.
Catch all of the 3 Exceptions by a more commen exception and the one exception.

6. Special Case Pattern 
When handling special cases with if or try and catch.
Use the special case pattern instead and keep the logic without special case.
This means create a new class or configure an object so it handles the special case instead of the logic.
E.g. Sum values of DTOs. Instead of try and catch if a DTO has no value to sum. Create a class
that always returns a value, e.g. a default value.

7. Don't return Null
Use the Special Case Pattern instead.

8. Don't pass Null
There is no good way to handle a null in the arguments. So just don't.


### 8. Boundaries

1. Using third-party code
Dont pass interfaces at a boundry around your system.
Keep the interface inside a class where it is used and pass the class.
Avoid returning it from, or accepting it asa an argument to, public APIs.

2. Learning tests 
Write tests using the 3rd party API parts we want to use.
They document and test the way we want to use the third party API.
Another benefit is, that when 3rd party API code changes, the test will fail
if the changes don't match the intent we planed to use the 3rd party API code.

3. Adapter Pattern
Build Code on top of code that does not yet exist.
The Adapter encapsulates the interaction with the API and provides a single place to change when the API changes.
Using a FakeAdapterImplementation helps to test the code written before the Adapter implementation is written.

4. Clean Boundaries
Keep 3rd party code at the edge of the system.
There should be only a few places in the code where we refer to it.
Use **Wrapper**s and **Adapter**s to keep control. 

### 9. Unit Tests

1. Readability
Tests must be readable.
DRY (no code duplication).
Use the triple A arrangement inside any test.
* Arrange
* Act
* Assert

2. Domain specific language
Write an API for Tests only.
Create functions and utilities for writing tests.
E.g. reading and pasing fixtures form files.
It is ok to use different techniques in the test API but only as long as they don't 
harm the cleanliness / readability (Dual Stnadard).

3. Assert count per test
Try to have one assert per test.
It is ok to have more than one assert per test.
The number of asserts per test ought be minimized.

4. Single Concept per test 
Test one case per test. 
Use the formulation template 
* *TestMethodName*
* *Does*
* *When*
E.g. divideNumbers_throwDivisionByZeroException_WhenNumbersContainsZero

5. FIRST
Clean tests are...
* Fast, so they can be run frequently.
* Independent, tests should have no dependency to other test.
* Repeatable, tests have to run on any environment and configuration (including no network connection).
* Self-Validating, tests have a boolean state. They either pass or fail.
* Timely, tests should be written before production code. 


### 10. Classes

1. Class Organization
* public static vars
* private static vars
* private instance vars 
* public functions
* private fucntions (directly under the public function that uses it)

2. Single Responsibility Principle
A class should be small.
A class should have one responsibility and therefore have exactly one reason to change.
A good indicator if a class has too many responsibilities when they can't be named precisely.
Another indicator can be if one can not describe in a few words what a class is responsible of without using the words *if* *and* *or* *but*.

3. Cohesion
Classes should have a small number of instance variables.
A class in which every instance variable is used by each method is maximally cohesive. 
Try to make as cohesiv classes as possible.
It is an indicator that the class has one responsibility. 

4. Open Closed Principle (OCP)
Use an abstract class to represent concepts. 
Use separated small classes instead of functions and inherit from the abstract class to implement behaviour (Strategy Pattern).
This makes the parent abstract class unsing the behaviour classes "open for extension but closed for modification".

5. Dependency Inversion Principle
Classes should depend on abstractions (abstract classes or interfaces) not on concrete details (other classes).

### 11. Systems