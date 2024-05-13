1. **Differences Between C and C++**
   1. C is a procedural language, structured around how to process inputs to produce outputs through procedures. C++ is an object-oriented language characterized primarily by "encapsulation, inheritance, and polymorphism". Encapsulation hides implementation details, enabling modularized code; derived classes can inherit data and methods from parent classes, extending existing modules for code reuse; polymorphism refers to "one interface, multiple implementations", achieved by overriding virtual functions in derived classes, enabling interface reuse.

   2. C and C++ have different methods for dynamic memory management. C uses malloc/free, while C++ additionally provides new/delete keywords.

   3. C++ introduces references, a concept absent in C.

2. **Differences Between Pointers and References in C++**
   1. **Pointers**:
      - A pointer is a variable that stores the address of another variable.
      - It can be reassigned to point to different objects.
      - It can be null, indicating it doesn't point to any valid object.
      - Requires dereferencing using the * operator to access the pointed-to object.

      Example:
      ```cpp
      int x = 10;
      int* ptr = &x; // ptr points to variable x
      *ptr = 20;     // Modify the value of x to 20
      ```

   2. **References**:
      - A reference is an alias, occupying no memory space itself, merely another name for an existing variable.
      - Once initialized, it cannot be made to refer to another object.
      - There's no concept of null reference; references must be initialized upon declaration.

      Example:
      ```cpp
      int x = 10;
      int& ref = x;  // ref is a reference to x
      ref = 20;      // Modify the value of x to 20
      ```

      In the above example, `ptr` is a pointer to `x`, while `ref` is a reference to `x`. Both can modify the value of `x`, but pointers can be made to point to different objects, whereas references cannot be changed after initialization. 

      Do references occupy memory? Taking the address of a reference actually yields the address of the memory corresponding to the referred variable. This phenomenon makes it seem like references aren't entities. However, references do occupy memory, and the amount of memory they occupy is the same as pointers, as references are internally implemented using pointers.

   Both pointers and references in C++ can be used to indirectly access objects, but they have some important differences.

3. **Differences Between Struct and Union in C++**
   - **Struct**:
     - Combines different types of data into a single entity, defining a custom type.
   - **Union**:
     - Multiple variables of different types share the same memory.
   1. Each member of a struct has its own independent address and exists simultaneously; all members of a union share the same memory and cannot coexist.
   2. `sizeof(struct)` is the sum of the lengths of all members after memory alignment, while `sizeof(union)` is the length of the longest data member after memory alignment.

   Why does struct need memory alignment?
   1. Platform reasons (portability): Not all hardware platforms can access any data at any address. Some hardware platforms can only access specific types of data at specific addresses, otherwise throwing hardware exceptions.
   2. Hardware reasons: After memory alignment, CPU memory access speed is greatly improved.

4. **Differences Between struct and class?**
   1. Let's first talk about the similarities and differences between structs in C and structs in C++:
   2. In C++, both `struct` and `class` can be used to define classes, differing primarily in default access control (i.e., default member access level) and default inheritance. Specifically, members of `struct` are public by default, while members of `class` are private by default.

   Here's a comparison of `struct` and `class`:
   | Feature | struct | class |
   |---------|--------|-------|
   | Default access control | Members are public | Members are private |
   | Default inheritance | Default public inheritance | Default private inheritance |
   | Member functions | Can include constructors, destructors | Can include constructors, destructors |
   | Usage | Lightweight objects, data transfer | Data encapsulation, object behavior implementation |

   In practice, the choice between `struct` and `class` depends on specific needs and habits. If only used to store data without requiring strict encapsulation and access control, `struct` can be used; if stricter encapsulation and access control are needed, `class` can be used.
