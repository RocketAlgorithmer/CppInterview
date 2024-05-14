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
