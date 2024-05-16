# Part 1: C++ Basics

## 1. Differences Between C and C++

1. **Language Paradigm:**
   - **C:** Procedural language focused on structured programming, processing input through a sequence of steps to produce output.
   - **C++:** Object-oriented language characterized by encapsulation, inheritance, and polymorphism. Encapsulation hides implementation details, making code modular. Derived classes inherit data and methods from base classes, enabling code reuse. Polymorphism allows one interface to have multiple implementations, achieved by overriding virtual functions in derived classes.

2. **Memory Management:**
   - **C:** Uses `malloc` and `free` for dynamic memory management.
   - **C++:** Uses `malloc` and `free`, and also introduces `new` and `delete` keywords.

3. **References:**
   - **C:** Does not have the concept of references.
   - **C++:** Introduces references.

## 2. Differences Between Pointers and References in C++

1. **Pointers:**
   - A pointer is a variable that stores the address of another variable.
   - Pointers can be reassigned to point to different objects.
   - Pointers can be null, indicating they do not point to any valid object.
   - Use the dereference operator `*` to access the object pointed to.
   
   Example:
   ```cpp
   int x = 10;
   int* ptr = &x; // ptr points to variable x
   *ptr = 20;     // modifies the value of x to 20
   ```

2. **References:**
   - A reference is an alias for an existing variable and does not occupy separate memory space.
   - Once initialized, a reference cannot be reassigned to refer to another object.
   - References cannot be null; they must be initialized when declared.
   
   Example:
   ```cpp
   int x = 10;
   int& ref = x;  // ref is a reference to x
   ref = 20;      // modifies the value of x to 20
   ```

   In the examples above, `ptr` is a pointer to `x`, while `ref` is a reference to `x`. Both can be used to modify `x`'s value, but a pointer can be reassigned to point to different objects, whereas a reference cannot be changed once initialized. Although references do not appear to occupy memory, they do, similar to pointers, as their implementation is based on pointers.

## 3. Differences Between `struct` and `union`

1. **Memory Allocation:**
   - **struct:** Combines different types of data into a single entity, each member having its own memory address and existing simultaneously.
   - **union:** Different types of data share the same memory space, with members occupying the same memory location and cannot exist simultaneously.

2. **Size Calculation:**
   - **struct:** `sizeof(struct)` is the sum of the sizes of all members, considering memory alignment.
   - **union:** `sizeof(union)` is the size of its largest member, considering memory alignment.

### Why Memory Alignment in Structures?

1. **Platform Reasons:** Not all hardware platforms can access arbitrary addresses for any data type, and some may only retrieve specific data types from certain addresses, or else throw hardware exceptions.
2. **Hardware Efficiency:** Aligned memory access significantly improves CPU memory access speed.

## 4. Differences Between `struct` and `class`

1. **C vs. C++ Structs:**
   - In C, `struct` is used only for grouping variables. In C++, both `struct` and `class` can define classes.

2. **Default Access Control:**
   - **struct:** Members are public by default.
   - **class:** Members are private by default.

3. **Default Inheritance:**
   - **struct:** Inherits publicly by default.
   - **class:** Inherits privately by default.

4. **Member Functions:**
   - Both can include constructors and destructors.

5. **Use Cases:**
   - **struct:** Suitable for lightweight objects and data transfer.
   - **class:** Used for encapsulating data and implementing object behavior.

   Choosing between `struct` and `class` depends on the need for encapsulation and access control. Use `struct` for simple data storage without strict encapsulation, and `class` for more controlled access and behavior encapsulation.

## 5. Differences Between `#define` and `const`

1. **Type Association:**
   - `#define` defines constants without types; they are immediate values.
   - `const` defines constants with type names and stores them in the static area.

2. **Processing Stage:**
   - `#define` constants are replaced during preprocessing, potentially having multiple copies.
   - `const` variables are determined at compile time with a single copy.

3. **Pointer Association:**
   - `#define` constants cannot be pointed to by a pointer.
   - `const` constants can be pointed to by a pointer.

4. **Function Definition:**
   - `#define` can define simple functions.
   - `const` cannot define functions.
## 6. Differences Between Overload, Override, and Hide in C++

1. **Overload:**
   - Allows multiple functions with the same name to exist in the same scope, differing by their parameter lists (number, types, or order of parameters).
   - Overloaded functions can have different return types.
   - The compiler determines which overloaded function to call based on the provided argument types and numbers.

   Example:
   ```cpp
   void print(int x) {
       std::cout << "Printing integer: " << x << std::endl;
   }

   void print(double x) {
       std::cout << "Printing double: " << x << std::endl;
   }
   ```

2. **Override:**
   - Redefines a virtual function in a derived class. The function signature (name, parameter list, and return type) must exactly match the virtual function in the base class.
   - Used to achieve polymorphism. When a virtual function is called through a base class pointer or reference, the function of the actual object type is invoked.

   Example:
   ```cpp
   class Base {
   public:
       virtual void func() {
           std::cout << "Base::func()" << std::endl;
       }
   };

   class Derived : public Base {
   public:
       void func() override {
           std::cout << "Derived::func()" << std::endl;
       }
   };
   ```

3. **Hide:**
   - Defines a non-virtual function in the derived class with the same name as a function in the base class. This hides the base class function, even if the parameter lists are different.
   - Hiding does not affect the base class function; it only hides it in the derived class.

   Example:
   ```cpp
   class Base {
   public:
       void func() {
           std::cout << "Base::func()" << std::endl;
       }
   };

   class Derived : public Base {
   public:
       void func(int x) {
           std::cout << "Derived::func(int)" << std::endl;
       }
   };
   ```

Summary:
- **Overload:** Multiple functions with the same name in the same scope, differentiated by parameter lists.
- **Override:** Redefines a base class's virtual function in a derived class to implement polymorphism.
- **Hide:** A derived class defines a non-virtual function with the same name as a base class function, hiding the base class function in the derived class.

## 7. Differences Between `new`/`delete` and `malloc`/`free`

1. **new Operation Handling:**
   - **Simple Data Types:** Calls `operator new` to allocate memory; handles `new` failure with `new_handler`. If `new` fails, it throws a `bad_alloc` exception instead of returning NULL like `malloc`. Use exception handling to check for allocation success.
   - **Complex Data Types:** Calls `operator new` to allocate memory, then calls the constructor to initialize the object.

2. **delete Operation Handling:**
   - **Simple Data Types:** `delete` simply calls the `free` function.
   - **Complex Data Types:** `delete` calls the destructor and then `operator delete`.

Differences Between `new`/`delete` and `malloc`/`free`:

1. **Nature:**
   - `new`/`delete` are C++ keywords requiring compiler support.
   - `malloc`/`free` are library functions needing C headers.

2. **Parameters:**
   - `new` automatically calculates memory size based on type information.
   - `malloc` requires explicit size specification.

3. **Return Type:**
   - `new` returns a pointer of the specified type, ensuring type safety.
   - `malloc` returns a `void*`, needing type casting.

4. **Failure Handling:**
   - `new` throws `bad_alloc` on failure.
   - `malloc` returns NULL on failure.

5. **Custom Types:**
   - `new` calls `operator new` to allocate memory (often using `malloc`), then calls the constructor. `delete` calls the destructor, then `operator delete` (often using `free`).
   - `malloc`/`free` allocate and free memory without handling object construction/destruction.

6. **Overloading:**
   - C++ allows overloading `new`/`delete`.
   - `malloc`/`free` cannot be overloaded.

7. **Memory Region:**
   - `new` allocates memory from the free store, while `malloc` allocates from the heap. The free store is an abstract concept based on `new`, while the heap is a specific memory area managed by the OS.

Comparison Table:

| Feature | new/delete | malloc/free |
| --- | --- | --- |
| Syntax | `new Type;` `delete ptr;` | `malloc(size);` `free(ptr);` |
| Return Type | Type pointer | `void*` pointer |
| Header File | `<new>` | `<cstdlib>` |
| Constructors/Destructors | Calls constructors and destructors | Does not call constructors and destructors |
| Size | Automatically calculates size | Requires manual size calculation |
| Object Arrays | Supported | Not supported |
| Memory Bounds Checking | Supported | Not supported |
| Exception Handling | Supported | Not supported |
| Type Safety | Better | Poorer |

**Why use `new`/`delete` if `malloc`/`free` exist?**
- Operators like `new`/`delete` are intrinsic to the language, interpreted by the compiler to generate appropriate code, ensuring constructor/destructor calls for non-primitive types. Library functions like `malloc`/`free` depend on libraries and do not inherently handle object construction/destruction.

## 8. Difference Between `delete` and `delete[]`

- `delete` calls the destructor once, while `delete[]` calls the destructor for each element in an array.
- Use `delete` for memory allocated with `new`, and `delete[]` for memory allocated with `new[]`.

## 9. The `const` Keyword

- **Declaring Constants:** Declares constants that cannot be modified after initialization.
  
  Example:
  ```cpp
  const int MAX_SIZE = 100;
  ```

- **Function Parameters:** Specifies constant function parameters, disallowing modification within the function.
  
  Example:
  ```cpp
  void print(const std::string& str) {
      std::cout << str << std::endl;
  }
  ```

- **Member Functions:** Declares constant member functions that do not modify the object’s state.
  
  Example:
  ```cpp
  class MyClass {
  public:
      void func() const {
          // Cannot modify member variables
      }
  };
  ```

- **Pointer to Const:** Points to a constant value, disallowing modification through the pointer but allowing pointer reassignment.
  
  Example:
  ```cpp
  int value = 10;
  const int* ptr = &value;  // Pointer to const
  // *ptr = 20;  // Error
  ptr = nullptr;  // Allowed
  ```

- **Const Pointer:** Declares a constant pointer that cannot be reassigned, but allows modifying the value it points to.
  
  Example:
  ```cpp
  int value = 10;
  int* const ptr = &value;  // Const pointer
  *ptr = 20;  // Allowed
  // ptr = nullptr;  // Error
  ```

The `const` keyword improves readability, maintainability, and helps prevent unintended modifications.

## 10. The `static` Keyword

1. **Static Variables:** Within a function, a static variable retains its value across function calls.
   
   Example:
   ```cpp
   void func() {
       static int count = 0;
       count++;
       std::cout << "Function has been called " << count << " times." << std::endl;
   }

   int main() {
       func();
       func();
       func();
       return 0;
   }
   // Output:
   // Function has been called 1 times.
   // Function has been called 2 times.
   // Function has been called 3 times.
   ```

2. **Static Global Variables:** Limits the variable's scope to the current file.
   
   Example:
   ```cpp
   static int globalVar = 10;  // Only accessible within the current file
   ```

3. **Static Functions:** Limits the function's scope to the current file.
   
   Example:
   ```cpp
   static void helperFunc() {
       // Only callable within the current file
   }
   ```

4. **Static Class Members:** Declares static member variables and functions shared among all class instances. Static functions belong to the class and can be accessed directly by the class name.
   
   Example:
   ```cpp
   class MyClass {
   public:
       static int staticVar;
       static void staticFunc() {
           // Implementation of static member function
       }
   };

   int MyClass::staticVar = 0;  // Definition of static member variable
   ```

The `static` keyword helps control the scope and lifetime of variables and functions, enhancing code structure, security, and maintainability.

## 11. Differences between Heap and Stack

1. **Space Allocation Differences:**
   - **Stack (Operating System):** Automatically allocated and released by the operating system. It stores function parameter values, local variables, etc. Its operation is similar to the stack data structure.
   - **Heap (Operating System):** Generally allocated and released by the programmer. If not released by the programmer, it may be reclaimed by the OS when the program ends. Its allocation is similar to a linked list.

2. **Caching Differences:**
   - **Stack:** Stores value types in memory, with a size limit of 2M on Windows (8M by default on Linux, configurable). Exceeding this limit causes errors or memory overflow.
   - **Heap:** Stores reference data types in memory. The size of reference data types is indeterminate. The heap is a linked list structure using scattered memory space, with its size directly determined by the size of reference types, which changes dynamically.

3. **Data Structure Differences:**
   - **Heap (Data Structure):** Can be viewed as a tree, e.g., heap sort.
   - **Stack (Data Structure):** A LIFO (Last In, First Out) data structure.

**Differences in Heap and Stack in C++ Memory Regions:**

- **Management:** The stack is automatically managed by the compiler, requiring no manual control. Heap management is done by the programmer, potentially leading to memory leaks.
- **Space Size:** In a 32-bit system, heap memory can reach up to 4G, making it nearly unlimited. Stack memory has a fixed size, e.g., 1M by default in VC6, modifiable via project settings.
- **Fragmentation:** Frequent new/delete operations on the heap can cause memory fragmentation, reducing program efficiency. The stack does not have this issue.
- **Growth Direction:** The heap grows upwards (towards increasing memory addresses), while the stack grows downwards (towards decreasing memory addresses).
- **Allocation Method:** The heap is dynamically allocated, whereas the stack is statically allocated by the compiler for local variables.
- **Allocation Efficiency:** The stack, supported by the machine system with specialized instructions and registers, is more efficient. The heap, managed by C/C++ library functions, has a more complex mechanism, resulting in lower efficiency.

**Heap vs. Free Store:**
- **Heap:** A term used in C and operating systems, referring to a dynamically allocated memory area maintained by the OS.
- **Free Store:** A C++ concept for dynamic allocation and deallocation of objects using new and delete. It's an abstract concept, not entirely the same as the heap. Most C++ compilers implement the free store using the heap, making them functionally similar.

## 12. Difference between #include <file.h> and #include "file.h"
- The former searches in the standard library path.
- The latter searches in the current working directory.

## 13. What is Memory Leak? How to Handle Memory Leak and Pointer Out-of-Bounds?
- **Memory Leak:** Occurs when dynamically allocated memory is not freed, leading to wasted memory resources.
- **Methods:**
  - Ensure malloc/free are paired.
  - Check if the pointer being assigned needs to be freed.
  - Track pointer lengths to prevent out-of-bounds access.

## 14. Difference between Definition and Declaration:
- **Definition:** Allocates memory and storage space for a variable.
- **Declaration:** Does not allocate memory; a variable can be declared multiple times but defined only once.
- **extern Modifier:** Indicates a variable is declared but will be defined elsewhere or later in the file.

## 15. Four Stages of C++ File Compilation and Execution:
1. **Preprocessing:** Modifies source file content based on preprocessing directives.
2. **Compilation:** Converts source code to assembly code.
3. **Assembly:** Translates assembly code to machine code instructions.
4. **Linking:** Links object code to create an executable program.

## 16. C++ Memory Management
Memory allocation in C/C++ programs involves several areas:

● **Stack Area**
When a function executes, the storage units for local variables within the function can be created on the stack. These storage units are automatically released when the function execution ends. Stack memory allocation operations are built into the processor's instruction set, making it highly efficient, but the allocated memory capacity is limited. The stack area primarily stores local variables, function parameters, return data, return addresses, etc., allocated during function execution.

● **Heap Area**
Generally allocated and released by the programmer. If not released by the programmer, it may be reclaimed by the OS when the program ends. The allocation method is similar to a linked list.

● **Data Segment (Static Area)**
Stores global variables and static data. The system releases this area after the program ends.

● **Code Segment**
Stores the binary code of function bodies (class member functions and global functions).

You can use the `size` command and `objdump` to view the structure and content of the target file:

## 17. Four Types of Casting in C++
Type conversion mechanisms can be divided into implicit type conversion and explicit type conversion (type casting).

- `(new-type) expression` or `new-type(expression)`
  
Implicit type conversion is common, often occurring in mixed-type expressions. The four type-casting operators are `static_cast`, `dynamic_cast`, `const_cast`, and `reinterpret_cast`.

1. **static_cast:** 
   Performs compile-time type checking. It's similar to C-style casting but cannot perform arbitrary pointer data casts (except for null pointers). It is generally used for conversions between pointers and references in parent-child relationships. There is no runtime type check to ensure the safety of the cast.
   - Used for conversions between base class (parent class) and derived class (child class) pointers or references within class hierarchies. The compiler won't report errors regardless of whether polymorphism occurs.
     ● Upcasting (converting a derived class pointer or reference to a base class representation) is safe.
     ● Downcasting (converting a base class pointer or reference to a derived class representation) is unsafe without dynamic type checks, but the compiler won't report errors.
   - Used for conversions between basic data types, such as converting `int` to `char` or `int` to `enum`. The developer must ensure the safety of such conversions.
   - Converts null pointers to target type null pointers.
   - Converts any pointer type to a null pointer type.
   - Can convert `const` and `non-const` on ordinary data but cannot add or remove `const` on pointers to ordinary data.
   - Cannot convert unrelated custom types and does not support cross-class conversions.
   - Cannot convert away `const`, `volatile`, or `__unaligned` attributes. (Use `const_cast` for the first two.)

2. **dynamic_cast:**
   Performs runtime checks. The dynamic type and operands must be complete class types or null pointers/references. It is mainly used for conversions between pointers or references within class hierarchies.
   - Upcasting is safe and allowed.
   - Downcasting without dynamic type checks is unsafe and disallowed; the compiler will report errors.
   - Allows mutual conversion in the presence of polymorphism.
   - Allows cross-class conversions between unrelated classes.
   - If a `dynamic_cast` statement's target is a pointer type and the conversion fails, the result is `0`. If the target is a reference type and the conversion fails, the `dynamic_cast` operator throws a `std::bad_cast` exception.

3. **const_cast:**
   Used to remove the `const` attribute from objects, typically pointers or references.

4. **reinterpret_cast:**
   In C++, `reinterpret_cast` is mainly used for:
   - Converting a pointer or reference to an integer type of sufficient length.
   - Converting an integer type to a pointer or reference type.

**Why not use C-style casting?**
C-style casting appears powerful and can convert anything but lacks clarity, cannot perform error checks, and is prone to errors.

## 18. Purpose of extern "C"
The primary purpose of `extern "C"` is to enable C++ code to correctly call other C language code. Adding `extern "C"` directs the compiler to compile the specified code as C language rather than C++.

## 19. Difference Between typedef and #define
Both `typedef` and `#define` can create type aliases, but there are important differences:

1. **typedef:**
   - A C++ keyword used to create aliases for existing types.
   - The alias created by `typedef` is a new type name that can be used anywhere.
   - `typedef` does not create macros, avoiding potential macro-related issues.
   - Example:
     ```cpp
     typedef int Integer;  // Creates an alias Integer for int
     Integer num = 10;
     ```

2. **#define:**
   - A preprocessor directive in C/C++ used to define macros.
   - `#define` creates simple text replacements, not new types.
   - `#define` can define constants, functions, expressions, etc., not limited to type aliases.
   - Example:
     ```cpp
     #define INTEGER int  // Creates a macro alias INTEGER for int
     INTEGER num = 10;
     ```

**Summary of Differences:**
- `typedef` is a C++ keyword used to create type aliases, resulting in a new type name.
- `#define` is a preprocessor directive for creating macros that can define constants, functions, expressions, etc., not limited to type aliases.

## 20. Benefits of Using References as Function Parameters and Return Values
Compared to value passing, reference passing offers several advantages:
1. Parameters can be modified within the function.
2. Improves function call and execution efficiency (eliminates the time and space overhead of copying values).

**Value Passing:**
- The formal parameter is a copy of the actual parameter, and modifying the formal parameter does not affect the external actual parameter. From the called function's perspective, value passing is unidirectional (actual parameter -> formal parameter), allowing the parameter's value to be passed in but not out. When the function needs to modify a parameter without affecting the caller, value passing is used.

**Pointer Passing:**
- The formal parameter is a pointer to the actual parameter's address. Operations on the formal parameter affect the actual parameter directly.

**Reference Passing:**
- The formal parameter is an alias for the actual parameter. Operations on the formal parameter are actually operations on the actual parameter. During reference passing, the formal parameter is stored in the stack as a local variable but holds the address of the actual parameter. Thus, any operation on the formal parameter affects the actual parameter.

**Benefits of Using References as Return Values:**
- No copies of the returned value are created in memory.

**Restrictions:**
1. Cannot return references to local variables because local variables are destroyed after the function returns.
2. Cannot return references to memory allocated by `new` within the function. Although local variables are not destroyed in this case, the referenced memory may cause a memory leak if not assigned to an actual variable.
3. Can return references to class members, but it is best to return `const` references to prevent external modification of internal attributes, which can maintain the integrity of business rules.

## 21. What is a Dangling Pointer and How to Avoid It
A dangling pointer is not a NULL pointer; it is an uninitialized or unset pointer that points to a memory address not intended by the programmer and may point to restricted memory. Causes:
1. The pointer variable is not initialized.
2. The memory pointed to by the pointer is freed, but the pointer is not set to NULL.
3. The pointer exceeds the scope of the variable, such as `b[10]` and the pointer `b+11`.

How to avoid:
1. **Initialize pointers**: When defining a pointer, immediately initialize it to `nullptr` to avoid uninitialized pointers.
    ```cpp
    int* ptr = nullptr;
    ```
2. **Nullify pointers promptly**: After freeing memory, immediately set the pointer to `nullptr`.
    ```cpp
    delete ptr;
    ptr = nullptr;
    ```
3. **Avoid dangling pointers**: Ensure that the pointer is not used after its lifecycle ends or set it to `nullptr`.
    ```cpp
    void foo() {
        int* ptr = new int;
        // Use ptr
        delete ptr;
        // Nullify the pointer
        ptr = nullptr;
    }
    ```
4. **Use smart pointers**: Smart pointers help manage memory more conveniently and avoid manual memory deallocation and dangling pointers.
    ```cpp
    std::unique_ptr<int> ptr(new int);
    // No need to manually free memory
    ```
    
Example:
```cpp
int* ptr = new int;  // Allocate dynamic memory
delete ptr;          // Free memory
ptr = nullptr;       // Nullify the pointer to avoid it becoming a dangling pointer
```
In this example, `delete` frees the memory pointed to by `ptr`, and then `ptr` is set to `nullptr` to prevent it from becoming a dangling pointer.

## 22. Memory Leak Situations in C++
A memory leak occurs when dynamically allocated heap memory is not released or cannot be released, wasting system memory, slowing down the program, or even causing system crashes.

1. `new` and `delete` are not matched in the constructor and destructor of a class.
2. `delete` is used instead of `delete[]` when freeing an array of objects.
3. The destructor of the base class is not defined as a virtual function. When a base class pointer points to a derived class object, if the base class destructor is not virtual, the derived class destructor will not be called, leading to a memory leak.
4. Nested object pointers are not correctly cleared.

## 23. Causes and Solutions of Stack Overflow
Stack overflow occurs when local variables in a function cause an overflow (note: function parameters and local variables are stored on the stack). The stack size is usually 1M-2M, so stack overflow can happen in two cases: either the allocated size exceeds the maximum stack size, or the allocated size does not exceed the maximum but the received buffer is smaller than the original buffer.

1. Function call depth is too deep. Each call pushes function parameters, local variables, etc., onto the stack.
2. Local variables are too large.

Solutions:
1. **Increase stack memory size**: If the allocated size does not exceed the maximum stack size, increase the allocated size.
2. **Use heap memory**: There are many ways to implement this, such as directly defining arrays as pointers and dynamically allocating memory. Alternatively, convert local variables to global variables. A lazy approach is to add `static` before the definition, making them static variables (essentially global variables).

## 24. Lvalue and Rvalue
In general terms, an lvalue is a variable (or expression) that can appear on both the left and right side of an assignment operator, while an rvalue can only appear on the right side. For example, a defined variable `a` is an lvalue, and the return value of `malloc` is an rvalue. Lvalues can be addressed, have names, and are non-temporary. Rvalues, on the other hand, cannot be addressed, do not have names, are temporary, and usually exist within an expression's lifespan. However, with C++11, the concept has become slightly more complex, introducing lvalue, glvalue, rvalue, xvalue, and prvalue.

## 25. Lvalue References and Rvalue References
Lvalue references are what we typically refer to as references. They can usually be considered as aliases for variables.
```cpp
type-id & cast-expression

// Demo
int a = 10;
int &b = a;

int &c = 10;  // Error, cannot reference an immediate value

const int &d = 10;  // Correct, constant reference can refer to constants
```
Rvalue references are a new feature introduced in C++11. Rvalue references are used to bind to rvalues, and the lifespan of the rvalue is extended to the lifespan of the rvalue reference it is bound to.
- Rvalue references support the implementation of move semantics, reducing copies and improving program efficiency.
- Rvalue references can make overloaded functions more concise. They can be used in both `const T&` and `T&` parameter forms.
```cpp
type-id && cast-expression

// Demo
int &&var = 10;  // OK

int a = 10;
int &&b = a;  // Error, a is an lvalue

int &&c = var;  // Error, var is an lvalue

int &&d = std::move(a);  // OK, rvalue reference to a using std::move
```
At the assembly level, rvalue references and constant references do the same thing, generating temporaries to store constants. However, the key difference is that rvalue references allow read and write operations, while constant references only allow read operations.

## 26. What are `#ifndef/define/endif` in Header Files Used For? What is the Difference from `#pragma once`?
Similarities: Their purpose is to prevent a header file from being included multiple times.
Differences:
1. `#ifndef` is supported by the language itself, whereas `#pragma once` is generally supported by the compiler, meaning it might not be supported by some older compilers.
2. In terms of runtime performance, `#ifndef` is generally slower than `#pragma once`, especially in large projects, so more compilers are starting to support `#pragma once`.
3. `#ifndef` applies to a block of code between `define` and `endif`, while `#pragma once` applies to the entire file containing the statement, which is why `#pragma once` is faster.
4. If `#ifndef` is used to wrap a macro definition, a name collision might occur, leading to a macro undefined error in the program (especially in large programs with many developers writing code simultaneously). In contrast, `#pragma once` applies to the entire file, avoiding name collision issues. However, if a header file is copied multiple times, `#pragma once` cannot ensure the file is not included multiple times, as `#pragma once` determines the same header file physically, not by its content.

## 27. Differences Between Pointer Arrays and Array Pointers
An array pointer is a pointer to an array, while a pointer array is an array whose elements are pointers.

1. An array pointer is a pointer to an array. Essentially, it is a pointer. The syntax is as follows: `int (*p)[n]`, where `p` is a pointer to an array of integers of length `n`. The parentheses indicate that `p` is a pointer, and it points to a one-dimensional array of integers of length `n`. This means that when `p+1` is executed, `p` skips over `n` integers. An array pointer is a pointer to the address of the first element of the array and can be considered a double pointer.
    ```cpp
    type-id (*array-identifier)[array-length]
    ```

2. A pointer array is an array in which all elements are pointers. In C and C++, an array whose elements are all pointers is called a pointer array. The syntax for defining a one-dimensional pointer array is as follows: `int* p[n]`. The square brackets have higher precedence, so `p` is first recognized as an array, and then `int*` indicates that it is an array of integer pointers with `n` elements. When `p+1` is executed, `p` points to the next array element. The assignment `p = a` is incorrect because `p` is an array identifier and exists only as `p[0], p[1], p[2], ..., p[n-1]`, each being a pointer variable that can store addresses of variables. However, the assignment `p[0] = a` is correct, as `p[0]` is a pointer element of the array.
    ```cpp
    type-id* array-identifier[array-length]
    ```

## 28. Is C++ Type-Safe?
No. Pointers of different types can be forcibly cast.

## 29. What Executes Before the `main` Function?
Before a C++ program executes, several initialization steps occur, including the following:

1. **Runtime environment initialization**: The runtime environment initializes global variables and static variables.
2. **Global object constructors**: If global objects (including global and static variables) exist, their constructors are called before the `main` function executes.
3. **Setting `argc` and `argv`**: The number and content of command-line arguments are set.
4. **Static variable constructors**: Constructors of static variables are called before the `main` function executes.
5. **Global object constructors**: For global objects, their constructors are called before the `main` function executes.

Example:
```cpp
#include <iostream>

class GlobalObject {
public:
    GlobalObject() {
        std::cout << "GlobalObject constructed" << std::endl;
    }

    ~GlobalObject() {
        std::cout << "GlobalObject destroyed" << std::endl;
    }
};

GlobalObject globalObject;  // Global object

int main() {
    std::cout << "Main function" << std::endl;
    return 0;
}
```
In this example, the global object `globalObject` is constructed before the `main` function executes, outputting "GlobalObject constructed". After the `main` function completes, the global object is destroyed, outputting "GlobalObject destroyed".

## 30. Differences Between Global Variables and Local Variables? How are They Implemented? How do the Operating System and Compiler Recognize Them?
1. **Different lifetimes**: Global variables are created with the main program and destroyed with the main program. Local variables exist within local functions or local loops and cease to exist after exiting them. Global variables are allocated in the global data area.
2. **Different usage**: After declaration, global variables can be used throughout the program, while local variables can only be used locally and are allocated on the stack.

The operating system and compiler distinguish them by their memory allocation locations. Global variables are allocated in the global data segment and are loaded when the program starts running. Local variables are allocated on the stack.
