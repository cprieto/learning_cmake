# Let's do this:

## The simplest example

Simplest executable `hello.c`:

```c
#include <stdio.h>

int main() {
    printf("hello world\n");
}
```

And the equivalent simplest `CMakeLists.txt`:

```cmake
add_executable (hello hello.c)
```

Let's generate the `Makefiles` with CMake:
    
    cmake .

And you can compile the solution in two different ways, when you know a Makefile is created:

    make

Or when you want an unique command without caring what build scripts were generated:

    cmake --build . --clean-first

Notice the `--clean-first` parameter, it cleans the build first, of course.

## Extending the example

Sometimes CMake tells you a nasty warning about required version, let's get rid of it:

```cmake
cmake_minimum_required (VERSION 3.5)
add_executable (hello hello.c)
```

And while we are there, let's assign a name for our cmake project:

```cmake
cmake_minimum_required (VERSION 3.5)
project (HelloCMake)
add_executable (hello hello.c)
```

Now, if you generate a XCode project or Visual Studio solution, they will have the name of the project, not something generic like `Project.sln`.

## Libraries

Let's create a simple library with its header file `greeter.h`:

```c
void sayHello();
```

And, well, its body `greeter.c`:

```c
#include <stdio.h>

void sayHello() {
    printf("hello world\n");
}
```

It is time to modify our `CMakeLists.txt` file

```cmake
cmake_minimum_required (VERSION 3.5)
project (HelloCMake)
add_executable (hello hello.c)
add_library (greeter greeter.c)
```

Now if we regenerate the script and build it again, we will see a _static library_, that is because it is the default for CMake, let's change it to a dynamic library:

```cmake
cmake_minimum_required (VERSION 3.5)
project (HelloCMake)
add_executable (hello hello.c)
add_library (greeter SHARED greeter.c)
```

## Linking libraries

We have a library but we are not using it, let's change that and modify `hello.c`:

```c
#include "greeter.h"

int main() {
    sayHello();
}
```

If we try to run this with the `CMakeLists.txt` file as is, it will fail. Let's explicitly say we want to link our library to our executable:

```cmake
cmake_minimum_required (VERSION 3.5)
project (HelloCMake)
add_executable (hello hello.c)
add_library (greeter SHARED greeter.c)
target_link_libraries (hello greeter)
```

Now our executable will be build and have a dependency on our greeter shared library.

## Moving out-of-source

Let's start moving the headers, let's move `greeter.h` to the directory `includes`

```cmake
cmake_minimum_required (VERSION 3.5)
project (HelloCMake)
add_executable (hello hello.c)
include_directories (includes)
add_library (greeter SHARED greeter.c)
target_link_libraries (hello greeter)
`
