# Let's do this:

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
