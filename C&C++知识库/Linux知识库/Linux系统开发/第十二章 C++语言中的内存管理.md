# 分配内存

- **malloc函数**：用于动态分配内存。
  ```c
  #include <stdlib.h>
  void *malloc(size_t size);
  ```
- **示例**：分配1MB内存并存储字符串。
  ```c
  #include <stdio.h>
  #include <stdlib.h>
  #include <unistd.h>

  #define A_MEGABYTE (1024 * 1024)

  int main() {
      char *some_memory;
      int megabyte = A_MEGABYTE;
      int exit_code = EXIT_FAILURE;

      some_memory = (char *)malloc(megabyte);
      if (some_memory != NULL) {
          sprintf(some_memory, "Hello World\n");
          printf("%s", some_memory);
          free(some_memory); // 释放内存
          exit_code = EXIT_SUCCESS;
      }
      exit(exit_code);
  }
  ```

# 释放内存

- **free函数**：用于释放先前分配的内存。
  ```c
  #include <stdlib.h>
  void free(void *ptr_to_memory);
  ```

# C语言中的内存知识

- **内存区域**：
  1. **栈（Stack）**：存储局部变量、函数参数，由系统自动管理。
  2. **堆（Heap）**：通过`malloc`和`free`手动管理的内存区域。
  3. **全局/静态存储区**：存放全局变量和静态变量。
  4. **常量存储区**：存放`const`常量。

# 内存分配方式

- **静态内存分配**：编译时分配，如局部变量。
- **动态内存分配**：运行时分配，如`malloc`和`free`。

# 栈的作用

- **临时变量存储**：存储函数参数和局部变量。
- **多线程编程**：每个线程拥有自己的栈，用于存储临时变量和维护函数调用关系。

# 补充知识

- **内存泄漏**：未释放已分配的内存，可能导致程序运行时占用过多内存。
- **野指针**：指向已释放内存的指针，可能导致未定义行为。
- **内存对齐**：为了提高内存访问效率，分配的内存通常需要对齐到特定的边界。
- **`calloc`函数**：分配初始化为零的内存。
  ```c
  void *calloc(size_t num, size_t size);
  ```
- **`realloc`函数**：重新分配已分配的内存块的大小。
  ```c
  void *realloc(void *ptr, size_t new_size);
  ```
- **`alloca`函数**：在栈上分配内存，通常用于函数内部。
  ```c
  void *alloca(size_t size);
  ```