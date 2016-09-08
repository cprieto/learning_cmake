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

