# C++

## C++ vs java Compiling?

To run a C++ code it will **be first compiled to machine code for that specific target platform (X86 = 32 bit platform)** and then you run it on that platform but **java runs on a virtual machine** , it means that the **code is getting compiled into an intermediate language first** , then when you run your application on that platform the **virtual machine will convert it to machine code at run time**

Compiler will compile source files into binary files (executable programs or libraries) or object files

## Build a c++ project

	cd projectDir
	mkdir build & cd build
	cmake ..
	make
	cd projectDir
	g++ test.cpp

##### Build Types : 

`-DCMAKE_BUILD_TYPE=RelWithDebInfo       # Release With Debug Info`
This option is a configuration flag passed to CMake during the build process. It specifies the **build type** for your project. It produces a **highly optimized binary with debugging information**.

This will **compile the package exporting the symbols** (allow the breakpoints where you want to stop the code)

### Preprocess stataments :

Anything that starts with # in a source file is a preprocess statement and it is the first statement that compiler preprocess when getting a source file

**Preprocessing statements are** : #include , #define , #if , #ifdef

When you include a header file #include \<bonxai.h\> it will just copz the hear file content and add to the current file

- **#Include:**

  It will find the file and paste all the contents in that file in your current file, this files that you include are called header files

- **#Define :**

  It just replaces a variable with another , define it as another

        it will search for word INTEGER and replaces it with int
        #define INTEGER int  

- **#If :**

  It lets us to include or exclude a part of code based on a condition

        #if condition

        Void multiply(a,b)

        {

        }

        #endif

- **#ifdef** :

  Using **#ifdef** allows developers to conditionally compile certain parts of the code based on the presence or absence of specific macros, which can be useful for enabling or disabling certain features or configurations during compilation.

        #ifdef COLOR\_OCTOMAP\_SERVER

        #endif

    If **COLOR\_OCTOMAP\_SERVER** is defined, the code within the **#ifdef** block will be compiled. If it's not defined, the code within the block will be ignored by the preprocessor.



### Main function :

Main is the entry point for c++ program

### Decleartion vs definition :

Definition --\> it has also a body {}

Declare --\> void log(int a); ---\> it just says this function exists

When we want to use a function or so in a source file we have to declare this function with a declartion that tell this file that this function exists in another file

### Linker :

After compiling the source file , it will go through linking that will link multiple cpp files you have to each other

Pay attention that compiling the file will only do compiling so it just checks if a declaration for that function that you used in your source file exists inside your file but it does not checks if a function really exists in another file because this is the job of linking but if you do build the project then it will compiling and linking

### Header files :

As I said earlier when you want to use a function that is defined originally in another file, in your current file then you need to add a declaration (without abody) of this function in this current file to just tells it that this function exists in another file elswhere

But imagine in this way you have to add this declaration in any files that want to use this function and that is not efficicent

So at this point header files come handy

- Header files are files that get included in cpp files
- Is used to declare certain functions or so that you want to use in another files , so in header files we only add the decalartions without any body and definition

## C++ Syntax

### Struct vs class :

- **Struct is** used to create a data type. It declares the all the variables in one group be following the struct keyword. After that, creating an object of the struct, all the variables are retrieved.
- Struct members are public in default but a class members are private in default, A class contains the data and the function and these are the only differences
- When you want all your members to be public than use struct
- Use it when you just want to represent a bunch of variables

        struct student

        { string first\_name, last\_name;int roll\_no;

        };

        int main()

        {structstudent stu;

        stu.first\_name ="EDU";}

### Nemespace :

- Namespace provide the space where we can define or declare identifier i.e. variable, method, classes.
- Using namespace, you can define the space or context in which identifiers are defined i.e. variable, method, classes. In essence, a namespace defines a scope.

#### Advantage of Namespace to avoid name collision.

- Example, you might be writing some code that has a function called xyz() and there is another library available which is also having same function xyz(). Now the compiler has no way of knowing which version of xyz() function you are referring to within your code.
- A namespace is designed to overcome this difficulty and is used as additional information to differentiate similar functions, classes, variables etc. with the same name available in different libraries.
- The best example of namespace scope is the C++ standard library (std) where all the classes, methods and templates are declared . Hence while writing a C++ program we usually include the directive** using namespace std;

To call the namespace-enabled version of either function or variable :

        Namespace\_name :: variable\_name

### Using :

- **Using for namespaces** : You can also avoid prepending of namespaces with the **using** namespace directive. This directive tells the compiler that the subsequent code is making use of names in the specified namespace then **you can use cout\<\< insted of std::cout\<\<**
- **Using for aliasing:** allows you to specify an alternate name for a type.

        using ll = long long; // Here we alias "ll" to stand for long long

- **Using for directives** : Using can be used as a directive to the compiler to tell it to include a particular header file. This is useful if you want to make sure that a particular header file is always included when you compile your codes

        using std::cout;

Bonxai **::** ProbabilisticMap : ProbabilisticMap is a class or type within namespace Bonxai


### Inheritance :

        class Derived : public Base {

        public :

        int y;

        };


## Refrence vs Pointer :

PointOut ConvertPoint(const PointIn & v) : here v is the function parameter that is a refrence to object of type PointIn

- **pointer** in C++ is a integer (number) that holds the memory address of another variable.

  Memory is just a linear one dimentional line and we have every bites of data in this line, (a street of many houses) and we want to have the address of each byte

  It does not matter which type of pointer you define , the pointer for all type of pointers is just an inetger


- **reference** is an **alias for an already existing variable**. Once a reference is initialized to a variable, it cannot be changed to refer to another    

  variable. Hence, a reference is similar to a const pointer (not to be confused with a pointer to a constant value!). Refrences do not occupy memory.

### Key differences :

### Pointer

- A **pointer** can be initialized to any value anytime after it is declared.

        int a = 5;
        // some code
        int\* p = &a;

- A **pointer** can be assigned to point to a NULL value.
- **Pointers** need to be dereferenced with a \*.
- A **pointer** can be changed to point to any variable of the same type.


        int a = 5;
        int \*p;
        p = &a;
        int b = 6;
        p = &b;

### Reference

- A **reference** must be initialized when it is declared.

        int a = 5;
        int& ref = a;

- **References** cannot be NULL.
- **References** can be used ,simply, by name.
- Once a **reference** is initialized to a variable, it cannot be changed to refer to a variable object.


### Other Differences :

A **pointer** has its own memory address and size on the stack whereas a **reference** shares the same memory address (with the original variable) but also takes up some space on the stack

### Pass by reference / pointer :

If you write a function and pass the parameter as a normal value, then what is happening is that it will create a brand new variable in the function and use that new variblle for the purpose in the function and modifying the variable in local scope.

But when you pass the parameter with a refrence or a pointer then it just modifying the same variable that you send the adddress or reference of it so you are modifying the variable in the global scope.

the variable inside the function is an alias for the passed variable. Therefore, any operations performed on the variable inside the function will also be reflected in the calling function.

### Templates :

Templates in C++ are a way to create generic functions and classes that can work with any data type. They allow the programmer to write a single function or class that can be used with multiple data types without the need to write separate function for each data type, and you specify the exact type when you call the function.

- **Class templates**

  A class template in C++ is similar to a function template, but it is used to create generic classes.

  template class:
```c++
template \<typename T\>
class MyClass {
// Class definition here
};

//OR

template \<typename T, int N\>
class MyClass {
// Body
};
```

- **Function templates**

  C++ template functions are a type of feature that allows the creation of generic functions. These functions can operate on multiple data types rather than being limited to a specific type.

  template function:

```
template <typename T>
T ConvertPoint(int size) {}
// Function definition here
```

  Then when you make an instance of the class or call the fucntion you can specify the type for that template argument as below :

```
ConvertPoint <Point3D>(v); 
it is calling the function ConvertPoint and specify the template parameter 
to be as type Point3D
```

```
# function implemnetaion
template <typename PointT>
std::tuple<bool, double> checkMap(const std::shared_ptr<Bonxai::ProbabilisticMap>& map) {
thread_local std::vector<PointT> occupied;
}


# function calling
auto res = checkMap<ColorPoint>(bonxai_);

```
### **Types**

int8_t , int32_t, int64_t
signed integer type with width of exactly 8, 16, 32 and 64 bits respectively 
- `int32_t`     signed 32-bit integer
- `int32_t a : 4`    signed 32-bit integer, since it uses 4 bits then it stores valus from -8 to 7
	- The `: 4` after the variable name is a **bit field** specification, which limits this variable to **4 bits**, it is not a value assignment but bit filed assigment

uint8_t, uint32_t, uint64_t
unsigned integer type with width of exactly 8, 16, 32 and 64 bits respectively 
- `unit32_t`   unsigned 32-bit integer , It can store values from `0` to `4,294,967,295` , Occupies **4 bytes** of memory

Plain int is quite a bit different from the others. Where int8_t and int32_t each have a specified size, int can be any size \>= 16 bits.

Always remember that 'size' is variable unless explicitly stated

        int i = 10;

On some systems, the compiler can result in a 16-bit integer, and on others, a 32-bit integer (on newer systems, a 64-bit integer).

In embedded environments, this can lead to strange results (especially when dealing with memory-mapped I/O or as a simple array situation). It is therefore highly recommended to specify variables with a fixed size.** In legacy systems, you may come across something



### Cmakelists.txt  

This below command links the octomap\_server library with the libraries specified in **${OCTOMAP\_LIBRARIES}** and **${PCL\_LIBRARIES}**
These variables likely contain paths to the libraries required by the **octomap\_server** library, such as OCTOMAP and PCL (Point Cloud Library)

        target\_link\_libraries(octomap\_server ${OCTOMAP\_LIBRARIES} ${PCL\_LIBRARIES})


This command registers the **octomap\_server** library as a node with the ROS 2 system.
It specifies that the node plugin is named **"octomap\_server::OctomapServer"** and the executable is named **octomap\_server\_node**.
When ROS 2 starts up, it will be able to locate and run the **octomap\_server\_node** executable, which is implemented using the functionality provided by the **octomap\_server** library.
Registering the node with ROS 2 allows it to be discovered and used within a ROS 2 ecosystem, enabling communication with other nodes, topics, services, and parameters.

        rclcpp\_components\_register\_node(octomap\_server PLUGIN "octomap\_server::OctomapServer" EXECUTABLE octomap\_server\_node)


#### Read and Store a File :
```c++
using json = nlohmann::json;

 // Create an ifstream to read the file :
std::ifstream input_file(filename);
  
 // Parse the JSON file

json j; input_file >> j;

// Close the file
input_file.close();

//Create a std::map to store the JSON data
std::map<std::string, std::string> data_map;

//Populate the map with JSON
data for (auto& el : j.items()) { 
// Convert JSON value to string for 
simplicity data_map[el.key()] = el.value().dump(); }
```

---

### `# pragma once`

A preprocessor directive that ensures a header file is included only once per compilation unit. It prevents multiple inclusion errors in a simpler way than traditional include guards. Widely supported by modern compilers but not part of the official C++ standard.

```
// A.h
struct A {};

// B.h
#include "A.h"
struct B {};

// C.h
#include "A.h"
#include "B.h"

// main.cpp
#include "C.h"

```

If `A.h` doesn't protect itself, `struct A` might get included twice.

---

## Templating
### `template <typename B>`

This before a function, declares it as a function template with a type parameter `B`. It lets you write generic code that works with any type `B`.

```
template <typename B>
void printTwice(const B& value) {
    std::cout << value << " " << value << std::endl;
}
```
You can then call `printTwice` with **any** type

***Key Idea*** : Enables type flexibility and code reuse.




```
VoxelGrid<typename B::Voxel> grid;
```

is **declaring a variable** named `grid` whose type is `VoxelGrid<typename B::Voxel>` in simpler words declare a variable called `grid` of type `VoxelGrid`, parameterized with the type `B::Voxel`.

`VoxelGrid` is a **template class**.
You give it a _type parameter_ in `<...>`.

---

#### Why use `const B&`?

`const B& value` in C++ is a _parameter type_ meaning:

> “a **reference** to a value of type B, which I **promise not to modify**.”


##### 1.  Efficiency : pass by value

If you pass by **value**:

```
void f(B value);
```

C++ makes a **copy** of `value`.
Fine for small types (like `int`, `double`).
Expensive for big types (like `std::string`, custom classes).

##### 2. References avoid copies : pass by reference

If you pass by **reference**:

```
void f(B& value);
```

No copy!
But the function **can modify** the original value you passed.

##### 3.`const B&` = safe, efficient

```
void f(const B& value);
```

No copy (efficient).
`const` says “I _won’t_ change it.”

---

#### Member function/variable

```
PointCloud2 MapImpl<B>::chunk(const ChunkConfig& chunk_config) {}
```

defines the `chunk` member function of the template class `MapImpl<B>`, which takes a `ChunkConfig` parameter and returns a `PointCloud2`.

---

### Virtual

n C++, **polymorphism** lets us work with objects through **base-class pointers or references**, while still using behavior defined in **derived classes**. To achieve this, we declare methods as `virtual` in the **base class**, telling the compiler that _derived classes can override them_, and at runtime, the correct derived implementation will be called even if we only know the base type. For example, in a mapping system, we might define a base class `Map` with abstract (pure virtual) methods that describe a common interface for all maps:

```c++
class Map {
 public:
   virtual ~Map() = default;
   virtual PointCloud2 publishAll() = 0;
   virtual void applyRules(const RulesConfig& rules_config) = 0;
};
```

The `= 0` syntax makes `applyRules` **pure virtual**—this means _all derived classes must implement it_. Then, in our concrete implementation `MapImpl`, we provide the actual behavior:

```c++
template <typename B>
class MapImpl : public Map {
 public:
   PointCloud2 publishAll() override { ... }
   void applyRules(const RulesConfig& rules_config) override { ... }
};

```

Because of `virtual`, even if we only have `std::shared_ptr<Map> map`, when we do:

```c++
map->applyRules(rules_config);
```

the program will _automatically call_ `MapImpl<B>::applyRules()` at runtime. This design allows flexible code that can use different map types interchangeably without knowing their exact implementation—only their shared interface defined by the base class.

---
### inline

When a function is fully defined (implemented) inside a header file (`.hpp`) and that header is included in multiple source files (`.cpp`), each source file ends up with its own copy of that function’s code. During linking, the linker finds multiple definitions of the same function, causing a “multiple definition” error. To fix this, either move the function implementation to a single source file (.cpp file) or mark the function `inline` in the header. Declaring a function as `inline` allows multiple identical definitions across translation units because the linker merges them, preventing multiple definition errors. This is useful for small functions meant to be defined in headers. Without `inline`, functions should only be declared (not defined) in headers and defined in one source file.

---
### Circular dependency

A circular dependency is when two or more header files include each other. `#pragma once` helps prevent infinite loops from this, but it doesn't solve the underlying problem of compilation order.

A **circular dependency** happens when two files need each other's definitions.

- `queue.hpp` needs functions from `serialize.hpp`. So, `queue.hpp` has `#include "serialize.hpp"`.
- `serialize.hpp` needs to know what a `Queue` is. So, `serialize.hpp` has `#include "queue.hpp"`.

When the compiler tries to build this, it enters an infinite loop:

1. It starts compiling a `.cpp` file that includes `queue.hpp`.
2. It opens `queue.hpp` and sees `#include "serialize.hpp"`.
3. It pauses `queue.hpp` and opens `serialize.hpp`.
4. It sees `#include "queue.hpp"`.
5. It pauses `serialize.hpp` and opens `queue.hpp`... and the loop continues forever.

---
#### pragma once

**`#pragma once`** is a simple instruction to the compiler: "Only include this file one time for any single `.cpp` file you are compiling."

It breaks the infinite loop. Here’s how the compiler works with `#pragma once`:

1. It starts compiling a `.cpp` file that includes `queue.hpp`.
2. It opens `queue.hpp` and sees `#pragma once`. It makes a note: "`queue.hpp` has been seen."
3. It then sees `#include "serialize.hpp"`. It pauses `queue.hpp` and opens `serialize.hpp`.
4. It sees `#pragma once` in `serialize.hpp` and notes: "`serialize.hpp` has been seen."
5. It then sees `#include "queue.hpp"`. The compiler checks its notes and says, "I've already included `queue.hpp` in this chain," so it **skips** this include.
6. It finishes processing `serialize.hpp` and returns to `queue.hpp` to finish processing it.

#### The Real Problem: Compilation Order

Your issue is exactly what you described: `#pragma once` fixes the infinite include, but **not the compilation order issue.**

The compiler reads a file from top to bottom. Even with `#pragma once`, the order of events causes a failure.
depending on how the headers are nested and which file is included first, it's very easy for the compiler to try and compile the `read()` method **before** it has properly processed the declaration of `read()` from `serialize.hpp`.

---
### Visitor

In C++, a **visitor** is just a _function object_ or _lambda function_ that you pass to another function so that it can "visit" elements in a data structure and apply some operation on each one.

In your code, `visitor` is a **lambda function** like this:

```c++
auto visitor = [&](typename B::Voxel& cell, const CoordT& coord) {     // logic on each cell here };


grid.forEachCell(visitor);
```

It captures variables (like `zlimit`, `label_to_check`, `grid`, etc.) by reference (`&`) and is designed to be called on **each voxel cell** in your map, and it receives:

- The `cell` (voxel object)
- The `coord` (its 3D coordinate)


`forEachCell(visitor)` is a loop that **goes over every cell in the map/grid** and calls the `visitor` function for each.

---
###  The if Statement with Initializer

```c++
if (typename B::Voxel* cell = accessor.value(coord, false); cell && cell->probability_log > logods(occupancy_threshold)) { // ... }
```

**Part A**: typename B::Voxel* cell = accessor.value(coord, false)
- This is an **initializer**. It declares a new variable cell and assigns a value to it.

**Part B**: cell && cell->probability_log > ...
- This is the actual **condition** that is checked.


---

### The Lambda Function: auto fun = [&...]

This is a **lambda function**, which is essentially a shorthand way to define a function right where you need it, without giving it a formal name.

```c++
auto fun = /* This part declares a variable named 'fun' and lets the compiler figure out its type. The type will be 'a function that takes a CoordT and returns a bool'. */ 
           [&accessor, &occupancy_threshold, &pixel_value, &level] // This is the CAPTURE CLAUSE. 
           (const Bonxai::CoordT& coord) // This is the PARAMETER LIST, like a normal function. 
           { /* ... function body ... */ }; // This is the FUNCTION BODY.
```

##### The Capture Clause: [&...]

- The [] brackets are what signal the start of a lambda.
- The content inside tells the lambda what variables from the outer scope, it needs to "see" or "capture."
- The & symbol means **"capture by reference."**

**In simple terms:** The capture clause is like giving the temporary fun function a "pass" to see and **modify** specific variables from its parent function.

This Lambada function will be implemented inline inside another function like this:

```c++
template <typename B>

RayHit MapImpl<B>::checkRayHit(const RayConfig& ray_config){

    CoordT start = grid.posToCoord(ray_config.x_start, ray_config.y_end, ray_config.z_start);

    CoordT end = grid.posToCoord(ray_config.x_end, ray_config.y_end, ray_config.z_end);

    float occupancy_threshold = ray_config.occupancy_threshold;

    Bonxai::CoordT hit_coord;

    RayHit ray_hit;

    auto accessor = grid.createAccessor();

    float res_half = grid.getResolution() / 2.0;

    // find the first hit
    auto fun = [&accessor, &occupancy_threshold, &hit_coord, &ray_hit](const Bonxai::CoordT& coord){

        if(typename B::Voxel* cell = accessor.value(coord, false);

        cell && cell->probability_log > logods(occupancy_threshold)){

            ray_hit.hit = true;

            hit_coord = coord;

            return false;   // stop ray traversal

        }

        return true;   // keep going

    };

    RayIterator(start, end, fun);
   }
```

and we call this lambada function like this 

```
RayIterator(start, end, fun);
```

---

### C++ Template Linker Error Due to Missing Definition

In C++, **template functions and classes must have their full implementation visible to the compiler at the point of instantiation**. If you define a template method like `checkRayHit()` (which is a class method of map.hpp) in a separate file (e.g., `ray_hit.hpp`) and only include its **declaration** in the main header (`map.hpp`), the compiler won’t be able to generate the necessary code for specific template instantiations like `MapImpl<BehaviorDefault>`. This leads to a **linker error: undefined reference to the template method**. 

The fix is to **include the implementation file** (e.g., `#include "ray_hit.hpp"`) at the **bottom of the class header file** (after the class definition in `map.hpp`), ensuring the compiler sees both the declaration and the implementation when needed. This approach avoids needing a `.cpp` file and satisfies the "templates must be fully visible at point of use" rule.

---
### Copy Constructor

A constructor is a special member function in a class that is automatically called when a new object of that class is created. Its primary job is to initialize the object's member variables.

A **copy constructor** is a specific type of constructor that creates a new object as a copy of an existing object. The default copy constructor performs a "shallow copy," meaning it copies the values of the member variables directly. If a member variable is a pointer, only the pointer's address is copied, not the data it points to. This can lead to issues where two objects incorrectly share the same block of memory.

To fix this, you can define a custom copy constructor to perform a "deep copy." In a deep copy, you manually allocate new memory for the copied object and then copy the contents of the original object's memory into this new space. This ensures that the original and the copy are completely independent.

---
### Smart pointers

In older C++ (and in C), when you wanted to create an object that lives beyond the current scope (e.g., outside of a single function), you had to allocate memory for it on the **heap**. You did this with the new keyword.

```c++
// Manually allocate a new MyObject on the heap
MyObject* ptr = new MyObject();

// ... use the object via the pointer ...
ptr->doSomething();

// CRUCIAL: You must remember to free the memory when you're done
delete ptr; // If you forget this line, you have a MEMORY LEAK!
```


This manual management is a massive source of bugs:

1. **Memory Leaks:** Forgetting delete.
2. **Dangling Pointers:** Calling delete too early while another pointer still tries to use the memory.
3. **Double Free:** Calling delete on the same pointer twice.
4. **Exception Safety:** If an error occurs between new and delete, the delete might never be called, causing a leak.
    
### The Solution: Smart Pointers (std::shared_ptr)

To solve this, C++11 introduced **smart pointers**. `std::shared_ptr` is one of the most common. It's an object that acts like a pointer but automatically manages the memory for you.

- It keeps track of how many shared_ptrs are pointing to the same object. This is called **reference counting**.
- When the very last shared_ptr pointing to an object is destroyed (e.g., goes out of scope), it automatically calls delete on the managed object.

```c++
// This is safer, faster, and cleaner
auto ptr = std::make_shared<MyObject>("some argument");
```



---

### pointer or reference access

In C++, **how you access a member of a variable depends on whether the variable is an object/reference or a pointer**. If you have a regular object or a reference, like `Voxel voxel` or `const Voxel& voxel`, the object itself contains the members, so you use the **dot operator (`.`)**:

```c++
voxel.label_probs  // Access the label_probs vector

```

If you have a pointer to an object, like `Voxel* voxel` or `const Voxel* voxel`, the pointer stores the memory address of the object. To access members through a pointer, you must use the **arrow operator (`->`)**, which dereferences the pointer and accesses the member:

```c++
voxel->label_probs  // Access the label_probs vector through a pointer

```

Using `.` on a pointer or `->` on an object will cause a compiler error. This distinction is important whenever you unpack tuples from functions, index member vectors, or pass objects around in your code. Always check the variable type: **object/reference → dot, pointer → arrow**.



---

### static vs constexpr

In C++, a **`static`** member belongs to the class rather than any instance, so it is shared across all objects and must usually be defined in a `.cpp` file; it can be modified at runtime. A **`constexpr` static** member is a compile-time constant that must be initialized in-class and cannot change at runtime, allowing the compiler to optimize its usage. An **`inline static`** member (C++17+) combines both features: it belongs to the class like `static`, can be initialized directly in the header without a separate definition, and can be modified at runtime, making it convenient for shared configuration values that don’t need to be per-instance.

Essentially, `static` = shared runtime value, `constexpr static` = shared immutable compile-time constant, and `inline static` = shared runtime value defined inline in the header.


---
