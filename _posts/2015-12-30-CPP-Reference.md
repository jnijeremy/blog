---
layout: post
title: CPP Reference

---

C, CPP programming language reference.

### compiler

gcc -o run_hello hello.c

./run_hello

* ( gcc -I [libdir] -o [output] [file] )
* `-I` flag indicates where to look for library files 
* `-Wall` Shows all warnings
* `-W` Show some warnings
* `-o [file]` Put the output binary in [file]
* `-pg` Compile with profiling information

### makefile
* way to manage compilation for large systems

```
target ... : prerequisites ...
    command
    ...
    ...
    
------------------------------    
CC=gcc
CFLAGS=-Wall
main: main.o hello_fn.o
clean:
    rm -f main main.o hello_fn.o
```

### preprocessor
// quotes indicate local header files
**\#include "filename"**

// angle brackets indicate library header files
**\#include \<filename>**

\#include <bits/stdc++.h>
// include all std headers

// If the filename is quoted, search for the file typically begins where the source program was found; if it is not found there, or if the name is enclosed in < and >, searching follows an implementation-defined rule to find the file.

***

### Namespace

an abstract space that contains a set of names, useful for resolving naming conflicts

```
namespace ford {
  class SUV {
    ...
  };
  class Compact {
   ...
  };
}
namespace dodge {
  class SUV {
    ...
  };
}

int main() {
  ford::SUV s1 = new ford::SUV();
  dodge::SUV s2 = new dodge::SUV();
  ...
  using namespace ford; // exposes SUV and Compact
  SUV s1 = new SUV();
  
  using ford::SUV // expose only the things that you need to use!
  SUV s2 = new SUV();
  
}
```
### Standard Template Library (STL)
a set of commonly used data structures & algorithms, parameterized with types, including: 

* vector
* map
* stack, queue, priority_queue
* sort

***

**external variable 外部变量**

**External variables are defined outside of any function and are thus potentially available to many functions.  External variables are permanent.**

**Functions themselves are always external.**

**External linkage**: external variables and functions have the property that all references to them by the same name, even from functions compiled separately , are references to the same thing. 

if an external variable is to be referred to before it is defined, or it is defined in a different source file from the one where it is being used, then an **extern** declaration is mandatory

variable defined outside of any function, need to be declared in each function that wants to access it.

// declaration of external variable for the rest of the source file 

`extern int sp;`

`extern double val[]`

***

**static variables 静态变量**

The **static** declaration, applied to an external variable or function, limits the scope of that object to the rest of the source file being compiled.

Normally, function names are global, visible to any part of the entire program.  If a function is declared **static**, however, its name is invisible outside of the file in which it is declared.

Internal **static** variables provides private, permanent storage within a single function.  They are not destroyed even after they go out of scope.

***
**automatic variable 自动变量**

**Automatic variables are internal to a function; they come into existence when the function is entered, and disappear when it left.**

An automatic variable declared and initialized in a block is initialized each time the block is entered.  And remain in existence until the matching right brace.

***

### initialization
**In the absence of explicit initialization, external and static variables are initialized to zero by default.**

For external and static variables, the initializer must be a constant expression;

**Automatic variables for which there is no explicit initializer have undefined values. (garbage)**

For automatic and register variables, the initializer is not restricted to being a constant: it may be any expression involving previously defined values, even function calls.
***

`x = f() + g();` // f may be evaluated before g or vice versa;

`a[i] = i++` // undetermined behaviour


**// conditional operator**

**// ternary**

`expr1 ? expr2 : expr3`

`7==5 ? 4 : 3` // evaluates to 3

`z = (a > b) ? a : b;` // z = max(a, b)


### memory

**stack**

* C functions (including function's local variables) get allocated on the **stack**.  
* Functions are pushed on to the stack when called.
* Functions are posed off the stack when they return.  
* Functions can access any memory below the current top of the stack.
* variables are allocated and freed automatically

**heap**

* The **heap** is a chunk of memory for the C program to use.  
* Access heap using `pointer`.  The whole program has access to the heap.  Heap variables are global.
* not automatically managed by the CPU

**read only segment**

* string literal is stored in OS defined read-only segment
* the storage for these objects shall last for the duration of the program

### dynamic memory
The size of a regular array needs to be a constant expression, and thus its size has to be determined at the moment of designing the program, before it is run.

The dynamic memory allocation performed by `new` allows to assign memory during runtime using any variable value as size.

**dynamic memory requested by the program is allocated by the system from the memory heap.** 

CPP

```
#include <new>
pointer1 = new type

pointer2 = new type [number_of_elements]

int * foo;
foo = new int [5]; // if allocation fails, an bad_alloc exception is thrown. efficient, preferred

int * foo;
foo = new (nothrow) int [5];
if (foo == nullptr) {
    // error handling
}

delete pointer1; // release the memory of a single element allocated using new

delete[] pointer2; // release the memory allocated for arrays of elements using new and a size in brackets
```
C

```
#include <stdlib.h> // C
#include <cstdlib> // C++

// returns a pointer to n bytes of uninitialized storage, or NULL is request cannot be satisfied.
void *malloc(size_t n);

calloc()
realloc()
free()

for (p=head; p != NULL; p=q) {
    q = p->next;
    free(p);
}

int* i = NULL;
free(i); // nothing bad happens, freeing NULL does nothing.

```

### constant
```
NULL
true
false

'A' // character constant
"12345" // string literal, stored in read-only-data and mapped to process space as read only

// symbolic constant ( no semicolon )
#define name replacement-text
#define forever for (;;)
#define max(A, B) ((A) > (B) ? (A) : (B))
// some functions are defined as macros to avoid the run-time overhead of a function call.

// enumeration constant:
enum boolean { NO, YES };
// No = 0, YES = 1

enum months { JAN = 1, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC };
// FEB is 2, MAR is 3, etc.

typedef enum BOOL { true = 0, false = 1 } bool_t;
bool_t b = true; 
```

### type
```
short // 2 bytes
int
long // 4 bytes 2^32, 10^9
long long

float
double >> float
long double

signed char // -127 - 127
unsigned chat // 0 - 255
// ASCII ( 0 - 127 )

int a = b = c = 1;
// a = 1,  b = 1,  c = 1

// explicit type conversions:
(type-name) expression

int a = 19/10 = 1;

```

### bitwise operators
```
&     bitwise AND
|     bitwise inclusive OR
^     bitwise exclusive OR
<<    left shift     x << 2 = x * 4
>>    right shift
~     one's complement

2^n - 1 = ( 1 << n )-1
1<<n-1 = 2^(n-1)

#include <bitset>
bitset<8> foo ("10110011");
foo.size() // # of bits
cout << foo.count() << endl; // # of 1s
// ! foo.count() returns size_t type, which is unsigned integral type returned by sizeof(), so can't be used to compare with negative integer. 
```

### IO
```
main(int argc, char *argv[]) {...}

// argc = argument count
// argv = argument vector
// By convention, argv[0] is the name by which the program was invoked, so argc is at least 1.
```

```
INPUT

int c = getchar();

int n;
scanf("%d", &n); // return # success reads

// 25 Dec 1988
int day, yeah;
char monthname[20];
scanf("%d %s %d", &day, monthname, &year);

// 12/25/1988
int day, month, year;
scanf("%d/%d/%d", &month, &day, &year);

// cpp
// read line including white space; 
string s;
getline(cin, s);

// test EOF using cin:
while(!cin.eof()) {
   cin >> l >> h;
   cout << l << " " << h << endl;
}
// or:
while (cin >> l >> h) {
  cout << l << " " << h << endl;
}

```
```
OUTPUT

#include <stdio.h> // c
#include <cstdio> // cpp
printf("You have %d item%s.\n", n, n==1 ? "" : "s");

printf(%3d %6.1f\n", fahr, cels);
//200    93.3
//220  104.4

printf((argc > 1) ? "%s " : "%s", *++argv);
// the format argument of printf can be an expression too.

// cpp
#include <iomanip>
cout << setiosflags(ios::fixed) << setprecision(2) << 1.123; // print out 1.12

// print ***
cout << string(3, ‘*’) << endl;

```

### file IO
// C++ #include \<fstream>

```
string line;
ifstream myfile ("path");
if (myfile.is_open()) {
    while (getline(myfile, line)) {
        cout << line << endl;
    }
    myfile.close();
} else {
    cout << "Unable to open file";

```


// C <stdio.h>

```
FILE *fp;
fp = fopen(name, mode)
// mode = "r", "w", "a" append
// opening an existing file for writing causes the old contents to be discarded.

int getc(FILE *fp) 
// returns the next char form a file
int putc(int c, FILE *fp)

int fscanf(FILE *fp, char *format, ...)
int fprintf(FILE *fp, char *format, ...)

// stdin, stdout are objects of type FILE *, they are constants.

int fclose(FILE *fp)
// fclose if called automatically for each open file when a program terminates normally.

// reads the next input line
char *fgets(char *line, int maxine, FILE *fp);

// out put one line to file, need not contain a newline
int fputs(char *line, FILE *fp);


```


### loop
```
for(expr1; expr2; expr3)
    statement
    
equals to    

expr1;
while(expr2) {
    statement;
    expr3;
}

for(;;){} // infinite loop
```

### array
```
// initialize array

int array[3] = {1,2,3};
int array[] = {1,2,3};
// When the size of the array is omitted, the compiler will compute the length by counting the initializers.

int array[10] = {1,2}; // 1,2,0,0,...
int array[10] = {0}; // 0,0,0,...
// If there are fewer initializers for an array than the number specified, the missing elements will be zero for external, static and automatic variables.

static int array[10]; 
// 0,0,0,... in C++ and C

int array[10];
// garbage value in C++ and C

// character arrays
char pattern[] = "ould";
// array size = 5, including '\0'
```
```
// two dimensional array
daytab[i][j] // [row][col]

int M[2][2] = { {1,1},{1,0} };
// each row is initialized by a corresponding sub-list

int dp[3][3] = {0};
/*
000
000
000
*/

// two dimensional array using vector
v = vector <string> (3, "aaa");
/*
aaa
aaa
aaa
*/

vector<int> row(3);
vector<vector<int>> dp(3, row);
/*
000
000
000
*/

// g++ -std=c++11
auto array = new int[10][10]();
delete[] array;

```

### \#include \<vector>
```
v1.front() // access first element
v1.back() // access last element
v1.at(index) // access element

v1.push_back(val); // add element to the end
v1.pop_back(void); // delete end element

v1.insert(position, val) // insert single element
v1.insert(position, repeat, val); // fill
v1.insert(v1.end(), vector2.begin(), vector2.end()); // insert range elements

v1.erase(v1.begin()+i) // reduce container size by 1, i = 0 ~ len-1
```
```
#initialization
vector<int> v1;
v[0] = 1 // segmentation fault

int a[] = {1,2,3,4,5};
vector<int> v(a, a+5);
// v == [1,2,3,4,5]

vector<int> v(5, -1);
// v = [-1, -1, -1, -1, -1]
vector<int> v(5);
// v = [0, 0, 0, 0, 0]

vector<int> v = {1};

// assign content
v1 = v2;
// compare two vectors
v1 == v2

// get vector length
v.size();

// remove all elements from the vector, leaving the container with a size of 0.
v.clear();

// c++11, vector<int> v
for (auto it:v) {
    cout << v << " ";
}
cout << endl;
```

### \#include \<deque>

```
//double ended queue

std::deque<int> first;
std::deque<int> second(4,100); // 4 ints with value 100

std::deque<int> third (second.begin(), second.end());

std::deque<int> fourth (third);

fourth = third;

int len = first.size();

first.push_back(1);
first.push_front(1);

// empty deque has undefined behaviour
int tmp = first.front();
tmp = first.back();

first.pop_back();
first.pop_front();

```


### \#include \<stack>
```
stack<int> first;

vector<int> myvecotr (2, 200);
stack<int, vector<int>> second (my vector);

bool .empty();
size_type .size();
value_type& .top();
void .push();
void .pop();


```

### \#include \<queue>
```
queue<int> q;

q.empty();
q.size();

// accessor
q.front();
q.back();

// modifier
void q.push();
void q.pop();


```

### \#include \<cmath>
```
sqrt(10) // 3.16...
pow(2,n) // 2^n
floor(1.1) = 1
ceil(1.1) = 2
sin(x);
cos(x);
exp(x); // exponential e^x
log(x); // natural logarithm of x
log10(x);
fabs(x); // absolute value of x
```

### \#include \<unordered_map>
// g++ -std=c++11

```
unordered_map<string, string> myMap = { {“key1”, “v1”}, {“key2”, “v2”} };

// insert new element
myMap["newKey"] = "newValue"; 
myMap.insert(make_pair(“s1”, “s2”));

myMap.count(“exit”) == 1
myMap.count(“no-exist”) == 0

myMap.size() == # of keys

myMap.clear()

mymap.erase ( mymap.begin() );      
// erasing by iterator

mymap.erase ("France");             
// erasing by key

mymap.erase ( mymap.find("China"), mymap.end() ); 
// erasing by range

for(auto x:myMap) {
    cout << x.first << x.second << endl;
}
```

### \#include \<unordered_set>
```
unordered_set<int> s;
s.insert(1);

s.count(1) = 1;

// empty set
s.clear();

// -std=c++11
for (auto x: s) {
    cout << x << " ";
}
```


### \#include \<set>
```
set<int> s;
s.insert();

for (set<int>::iterator it = s.begin(); it!= s.end(); it++) {
    cout << *it << endl;
}

// g++ -std=c++11
for (auto it = s.begin(); it != s.end(); it++) {
    cout << *it << endl;
}
```

### \#include \<algorithm>
```
max(a,b)
min(a,b)
// reverse string
s = "1234"
reverse(s.begin(), s.end())
s = “4321"

sort(vector.begin(), vector.end());
sort(v.begin(), v.end(), std::greater<int>());
  
int myints[] = {1,2,3}; 
while (next_permutation(myints, myints+3))
    // print myints
// 1 2 3
1 3 2
2 1 3
2 3 1
3 1 2
3 2 1

```

### \#include \<string>
```
string s  = to_string(1234) = “1234"
s.length() = 4
s.size() = 4

s2 = s.substr(index, length);

stol("some long number");
int bin = stoi("-10010110001", nullptr, 2);
// bin = -1201

// handle exception
try {
	x = stoi(line);
}
catch(...) {
// invalid input data
}

string constant / string literal:
"I am a string"

// sort string
sort(s.begin(), s.end());
```
C

```
#include <stirng.h>
strlen("123") = 3
char* s = "12345";
strlen(s) = 5
```

### \#include \<utility>
// g++ -std=c++11

```
pair <int, int> foo;
foo = make_pair(1,2);
```

### \#include \<cctype>
```
int isalpha( int c );
isupper()
islower()
isdigit()
isalnum() // check alphanumeric 

int tolower( int c );
int toupper( int c );
```


### \#include <stdlib.h>
```
// computes a sequence of pseudo-random integers in the range zero to RAND_MAX, which is defined in <stdlib.h>.
rand();

\#define frand() ((double) rand() / (RAND_MAX+1.0))

// sets the seed for rand.
srand(unsigned);
```

### pointer
the & operator only applies to objects in memory: variables and array elements.  It cannot be applied to expressions or constants.

the unary operator * is the ***indirection*** or ***dereferencing*** operator.

any pinter can be cast to void * and back again without loss of information.

```
int a[10];
int *pa;
pa = a;

a[i] = *(a+i)
&a[i] = &(*(a+i)) = a+i
pa[i] = *(pa+i)

char s[] = char *s (prefer)

f(int daytab[2][13]) {...}
== f(int faytab[][13]) {...}
== f(int (*daytab)[13]) {...}
// More generally, only the first dimension of an array if free; all others have to be specified when passed to a function.

char *name[] = {
    "Illegal month",
    "January", "February", "March",
    "April", "May", "June",
    "July", "August", "September",
    "October", "November", "December"
};


```

`char amessage[] = "now is the time"; // an array`

`char *pmessage = "now is the time"; // a pointer`

***amessage*** is an array, just big enough to hold the sequence of characters and '\0' that initializes it.  ***amessage*** will always refer to the same storage.

***pmessage*** is a pointer, initialized to point to a string constant.  The pointer may subsequently be modified to point elsewhere, but the result is undefined if you try to modify the string contents.

### cpp reference
pass-by-reference allows a function to modify the outside object, like passing a pointer.
calling a function that takes references is cleaner, syntactically, than than calling a function that takes pointer.

```
#include <iostream>
using namespace std;

void f(int& r) {
  cout << "r = " << r << endl;
  cout << "&r = " << &r << endl;
  r = 5;
  cout << "r = " << r << endl;
}

int main() {
  int x = 47;
  cout << "x = " << x << endl;
  cout << "&x = " << &x << endl;
  f(x); // Looks like pass by value, is actually pass by reference
  cout << "x = " << x << endl;
  return 0;
}
```

### structures
Structures may not be compared.

If a large structure is to be passed to a function, it is generally more efficient to pass a pointer than copy the whole structure.

The size of a structure may not be the sum of sizes of its members.  Because if alignment requirements for different objects, there may be unnamed "holes" in a struct.

C++ has added an extra rule that allows to omit the `struct` (and `class`) keyword if there is no ambiguity.

In C++, the only difference between `class` and `struct` is that members and base classes are  private by default in classes, whereas they are public by default in structs.

e.g.

```
struct a {
    char c;
    int i;
};
sizeof(a) = 8 bytes, not 5 bytes.
```


```
struct point {
    int x;
    int y;
    struct point(int a, int b) : x(a), y(b) {} 
};
// keyword struct
// structure tag = point
// variables named in a structures are called members

struct {...} x, y, z;
int x, y, z;
// allocate space for x, y, z 

struct point pt;
// defines a variable pt which is a structure of type struct point

struct point maxpt = { 320, 200 };

printf("%d, %d", pt.x, pt.y);

struct rect {
    struct point pt1;
    struct point pt2;
};
struct rect screen;
screen.pt1.x
// x coordinate of the pt1 member of screen.

```

### Typedef

```
typedef char *String;

typedef struct tnode *Treeptr;

typedef struct tnode {
    char *word;
    int count;
    Treeptr left;
    Treeptr right;
} Treenode;

Treeptr talloc(void)
{
    return (Treeptr) malloc(sizeof(Treenode));
}


typedef struct node {
    int val;
    struct node* next;
} node_t;

```

### Class
`class declaration` (.h file): list of functions & fields

`class definition` (.cc file): implementation of functions

`Object on heap`
To allocate an object on heap: use `new` keyword.  To deallocate: use `delete` keyword. 

A subtype `inherits` characteristics and behaviours of the base type

`Public`: accessible by anyone.

`Protected`: accessible inside the class and by all of its subclasses.

`Private`: accessible only inside the class, NOT including its subclasses.

`Polymorphism`: Ability of type A to appear as and be used like another type B, e.g. A Student object can be used in place of a MITPerson object.

`Leskov Substitution Principle`: If S is a subtype of T, then the behaviour of a program P must remain unchanged when objects of type T are replaced with objects of type S.

Every variable has a `declared type` at compile time, but turing runtime, the variable may refer to an object with an `actual type` (either the same or a subclass of the declared type)

`virtual table`

* stores pointers to all virtual functions
* created per each class
* lookup during the function call

`Virtual destructors`
We must always clean up the mess created in the subclass (otherwise, rises for memory leaks!)

**There is no** `Virtual constructor`, because to create an object, you must know its exact type.  The VPTR has not even been initialized at this point.

`Abstract methods`: a method without an implementation is called an abstract method.  Abstract methods are often used to create an interface.

`Abstract base class`: a class with one or more pure virtual functions, cannot be instantiated.  It's subclass must implement all the pure virtual functions (or itself become an abstract class)

`copy constructor` and  `copy assignment operator`: if you don't define one, the compiler will automatically generate one for each.

`Rule of three in C++`: define all or none:

* destructor
* copy constructor
* copy assignment operator

**Virus class declaration**

```
// Virus.h

class Virus {
    // private: can only be accessed inside the class
    float reproductionRate;
    float resistance;
    static const float;
    defaultReproductionRate = 0.1;
    
  public:
  
    // constructors: no return type
    Virus(float newResistance);
    Virus(float newReproductionRate, float newResistance);
    
    Virus* reproduce(float immunity);
    bool survive(float immunity);  
    
};


```

**Virus class definition**


```
// Virus.cpp
#include "Virus.h"

Virus::Virus(float newResistance) {
    reproductionRate = defaultReproductionRate;
    resistance = newResistance;
}

Virus::Virus(float newReproductionRate, float newResistance) {
    reproductionRate = newReproductionRate;
    resistance = newResistance;
}

/* constructor could also do:

Virus::Virus(float newReproductionRate, float newResistance) : reproductionRate(newReproductionRate), resistance(newResistance) {}

*/


// If this virus cell reproduces,
// returns a new offspring with identical genetic info.
// Otherwise, return NULL.
Virus* Virus::reproduce(float immunity) {

    float prob = (float) rand() / RAND_MAX;
    
    // If the patient's immunity is too string, it cannot reproduce
    if (immunity > prob)
        return NULL;
    
    // Does the virus reproduce this time?
    if (prob > reproductionRate)
        return NULL; // No
        
    return new Virus(reproductionRate, resistance);
}

// Return true if this virus cell survives, given the patient's immunity
bool Virus::survive(float immunity) {
    
    // If the patient's immunity is too strong, then this cell cannot survive
    if (immunity > resistance)
        return false;
        
    return true;
}

const float Virus::defaultReproductionRate;

```


**Patient class declaration**

```
// Patient.h
#include "Virus.h"

#define MAX_VIRUS_POP 1000

class Patient {

    Virus* virusPop[MAX_VIRUS_POP];
    int numVirusCells;
    float immunity; // in %
    bool checkRep();
  public:
  
    Patient(float initImmunity, int initNumVirus);
    ~Patient(); // Destructor
    void takeDrug():
    bool simulateStep();
};
```

**Patient class definition**

```
// Patient.cpp
#include "Patient.h"
#include <cassert>

Patient::Patient(float initImmunity, int initNumVirusCells) {

    float resistance;
    immunity = initImmunity;
    
    for(int i = 0; i < initNumVirusCells; i++) {
        resistance = (float) rand() / RAND_MAX;
        
        // Dynamic object creation
        virusPop[i] = new Virus(resistance);
    }
    
    numVirusCells = initNumVirusCells;
}

// The destructor is automatically called
Patient::~Patient() {
    for (int i = 0; i < numVirusCells; i++) {
        delete virusPop[i];
    }
}

bool Patient::simulateStep() {
    Virus* virus;
    bool survived = false;
    ...
    for (int i = 0; i < numVirusCells; i++) {
        virus = virusPop[i];
        
        survived = virus->survive(immunity);
        
        if(survived)
            ...
        else
            ...    
    }
    assert(checkRep());        
}

void Patient::takeDrugs() {
    assert(checkRep());
    ...
    assert(checkRep());
}

// returns true iff the representation invariants hold true
// call checkRep at the beginning and end of every public method
// call checkRep at the end of constructors
bool Patient::checkRep() {
    return (immunity >= 0.0) && (immunity < 1.0) && (numVirusCells >= 0) && (numVirusCells < MAX_VIRUS_POP);
}
```

**main function**

```
int main() {

    float initImmunity = 0.1;
    int initNumVirusCells = 5;
    
    Patient p1(0.1, 5); // Automatically destroy at the end of scope, on stack
    
    Patient* p2 = new Patient(0.1, 5); // Object allocated on heap, needs to be deleted
    delete p2;
    
    p1.takeDrug();
```


### Inheritance example

```
// MITPerson.h
#include <string>

class MITPerson {

  protected:
      int id;
      std::string name;
      std::string address;
        
  public:
      MITPerson(int id, std::string name, std::string address);
      // copy constructor
      MITPerson(const MITPerson& other);
      ~MITPerson():  
      
      MITPerson& operator=(const MITPerson& other);
      virtual void displayProfile();
      virtual void changeAddress(std::string newAddress);
};
```

```
// MITPerson.cc
MITPerson::MITPerson(int id, std::string name, std::string address) {
  this->id = id;
  this->name = name;
  this->address = address;
}
MITPerson::MITPerson(const MITPerson& other) {
  name = other.name;
  id = other.id;
  address = other.address;
}
MITPerson::~MITPerson() {}

MITPerson& MITPerson::operator=(const MITPerson& other) {
  name = other.name;
  id = other.id;
  address = other.id;
  
  return *this; // return a newly assigned MITPerson
}

void MITPerson::displayProfile() {
  std::cout << "--------\n";
  std::cout << "Name: " << name << " ID: " << id << " Address: " << address << "\n";
  std::cout << "--------\n";
```

```
// Student.h
#include <iostream>
#include <vector>
#include "MITPerson.h"
#include "Class.h"

class Student : public MITPerson {
    int course;
    int year; // 1 = freshman, 2 = sophomore, etc.
    std::vector<Class*> classesTaken;
  
  public:
    Student(int id, std::string name, std::string address, int course, int year);
    void displayProfile(); // override the method to display course & classes
    void addClassTaken(Class* newClass);
    void changeCourse(int newCourse);
```

```
// Student.cc
// Student constructor call the base constructor
Student::Student(int id, std::string name, std::string address, int course, int year) : MITPerson(id, name, address) {
  this->course = course;
  this->year = year;
  
void Student::displayProfile() {
  std::cout << "--------\n";
  std::cout << "Name: " << name << " ID: " << id << " Address: " << address << "\n";
  std::cout << "Course: " << course << "\n";
  std::vector<Class*>::iterator it;
  std::cout << "Classes taken:\n";
  for (it = classesTaken.begin(); it != classesTaken.end(); it++) {
    Class* c = *it;
    std::cout << c->getName() << "\n";
  }
  std::cout << "--------\n";
```

```
// main1

MITPerson* john = new MITPerson(901289, "John Doe", "500 Massachusetts Av.");
Student* james = new Student(971232, "James Lee", "32 Vassar St.", 6, 2);

Class* c1 = new Class("6.088");
james->addClassTaken(c1);
john->displayProfile();
james->displayProfile();

// output
-----------------------------
Name: John Doe ID: 901289 Address: 500 Massachusetts Ave.
-----------------------------
-----------------------------
Name: James Lee ID: 971232 Address: 32 Vassar St.
Course: 6
Classes taken:
6.088
-----------------------------
```



```
// main2

// Actual type vs. declared type
MITPerson* john = new MITPerson(901289, "John Doe", "500 Massachusetts Ave.");
MITPerson* steve = new Student(911923, "Steve", "99 Cambridge St.", 18, 3);

// Calling an overridden function

steve->displayProfile();
// It doesn't display the course number and classes taken
// In order to override an function, we need to declare overridden method as virtual in the base.

// Type casting
Class* c1 = new Class("6.088");
steve->addClassTaken(c1); // error
// Can only invoke methods of the declared type!

Student* steve2 = dynamic_cast<Student>*(steve);
steve2->addClassTaken(c1);
// Use dynamic_cast<...> to downcast the pointer


// Static vs. dynamic casting
// Only use static_cast<...> when sure.

Student* steve3 = static_cast<Student>*(steve);
// cheaper but dangerous! No runtime check!

// e.g.
MITPerson* p = new MITPerson(...);
Student* s1 = static_cast<Student>*(p);
// s1 is not checked! BAD!
Student* s2 = dynamic_cast<Student>*(p);
// s2 is set to NULL


// output
-----------------------------
Name: Steve ID: 911923 Address: 99 Cambridge St.
-----------------------------

// after adding the virtual keyword
-----------------------------
Name: Steve ID: 911923 Address: 99 Cambridge St.
Course: 18
Classes taken:
-----------------------------
```

**Virtual destructor example**

```
class Base1 {
public:
  ~Base1() { std::cout << "~Base1()\n"; }
};
class Derived1 : public Base1 {
public:
  ~Derived1() { std::cout << "~Derived1()\n"; }
};
class Base2 {
public:
  virtual ~Base2() { std::cout << "~Base2()\n"; }
};
class Derived2 : public Base2 {
public:
  ~Derived2() { std::cout << "~Derived2()\n"; }
};

int main() {
  Base1* bp = new Derived1; // Upcast
  delete bp;
  Base2* b2p = new Derived2; // Upcast
  delete b2p;
}
```

**abstract methods using pure virtual functions**

```
class BST {
  public:
    // You should still create a constructor to initialize its members, since they will be inherited by its subclass.
    BST();
    // Always define a virtual destructor in the base class, to make sure that the destructor of its subclass is called.
    virtual ~BST() = 0;
    
    virtual void insert(int val) = 0;
    virtual bool find(int val) = 0;
    virtual void print_inorder() = 0;
    
    // = 0 says that the function is pure (no implementation)

```

**inherentance example**

```
class A 
{
public:
    int x;
protected:
    int y;
private:
    int z;
};

class B : public A
{
    // x is public
    // y is protected
    // z is not accessible from B
};

class C : protected A
{
    // x is protected
    // y is protected
    // z is not accessible from C
};

class D : private A    // 'private' is default for classes
{
    // x is private
    // y is private
    // z is not accessible from D
};

//IMPORTANT NOTE: Classes B, C and D all contain the variables x, y and z. It is just question of access.
```

**copying objects example**

```
void print(MITPerson p){
  // pass by value, so make a copy
  p.displayProfile();
  
int main() {
  MITPerson p1(921172, “James Lee”, “32 Vassar St.”);
  
  // Creating an object from another
  // copy constructor are called.
  MITPerson p2 = p1;  // initialization by value, so make a copy
  print(p2);
  
  // Assigning an object to another
  // Copy assignment operator is called
  MITPerson p1(921172, “James Lee”, “32 Vassar St.”);
  MITPerson p2(978123, “Alice Smith”, “121 Ames St.”);
  p2 = p1;  // assigns p2 to p1, does NOT create a new object
}

```