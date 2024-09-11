# 标准输入输出

在C语言中，标准输入输出通常使用`stdio.h`头文件中的函数来实现。这些函数包括：

- `printf`：将格式化的字符串输出到标准输出（通常是屏幕）。
- `fprintf`：将格式化的字符串输出到指定的文件流，可以是标准输出、标准错误或任何打开的文件流。
- `perror`：输出当前错误信息到标准错误流，错误信息由全局变量`errno`提供。

#### 程序示例

```c
#include <stdio.h>

int main() {
    char input[100];

    // 从标准输入读取
    printf("Enter some text: ");
    fgets(input, sizeof(input), stdin);

    // 输出到标准输出
    printf("You entered: %s", input);

    // 输出到标准错误
    fprintf(stderr, "This is an error message\n");

    return 0;
}
```

### 错误处理

在Linux中，系统函数出错时会设置全局变量`errno`。`errno`是一个宏，它对应于一个线程局部存储的变量，因此在使用多线程程序中也是安全的。

- `errno`：全局宏，用于获取最近一次系统调用错误的错误码。
- `perror`：打印错误信息到标准错误流。
- `strerror`：将错误码转换为可读的错误消息字符串。

#### 程序示例

```c
#include <stdio.h>
#include <errno.h>
#include <string.h>

void handle_error(const char *msg) {
    fprintf(stderr, "%s: %s\n", msg, strerror(errno));
}

int main(int argc, char *argv[]) {
    if (argc < 2) {
        fprintf(stderr, "Usage: %s <filename>\n", argv[0]);
        return 1;
    }

    // 模拟一个错误
    fprintf(stderr, "EACCES: %s\n", strerror(EACCES));
    errno = ENOENT;
    handle_error(argv[1]);

    return 0;
}
```

在这个示例中，`handle_error`函数用于打印错误信息。在主函数中，我们模拟了一个`EACCES`错误，并设置`errno`为`ENOENT`，然后调用`handle_error`来处理错误。

