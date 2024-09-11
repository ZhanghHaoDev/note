# 文件I/O函数

#### 头文件
- `#include <fcntl.h>`：包含`open`和`openat`函数的声明。
- `#include <unistd.h>`：包含`read`、`write`、`close`和`lseek`函数的声明。
- `#include <sys/types.h>`：包含一些数据类型的定义，如`mode_t`。
- `#include <sys/stat.h>`：包含文件状态的定义。

#### 文件描述符
- 内核使用文件描述符来引用所有打开的文件，是一个非负整数。

#### 函数`open`和`openat`
- `open`：打开或创建文件，返回文件描述符。
- `openat`：相对于目录文件描述符打开文件，提供更大的灵活性。

#### 打开文件的选项
- `O_RDONLY`：只读打开。
- `O_WRONLY`：只写打开。
- `O_RDWR`：读写打开。
- `O_CREAT`：创建文件。
- `O_TRUNC`：截断文件，用于写操作。

#### 函数`creat`
- 创建新文件，只能创建只写文件。

#### 函数`close`
- 关闭打开的文件。

#### 函数`lseek`
- 移动文件指针到指定位置。

#### 函数`read`
- 从文件描述符读取数据。

#### 函数`write`
- 向文件写入数据。

### 示例代码

#### 使用`openat`打开文件
```c
#include <stdio.h>
#include <errno.h>
#include <fcntl.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
    int dirfd = open("/example", O_RDONLY);
    if (dirfd == -1) {
        perror("open directory");
        return 1;
    }

    int fd = openat(dirfd, "test.txt", O_RDONLY);
    if (fd == -1) {
        perror("openat");
        close(dirfd);
        return 1;
    }

    close(fd);
    close(dirfd);

    return 0;
}
```

#### 创建文件
```c
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>

int main() {
    const char *filename = "example.txt";
    mode_t mode = 0644; // rw-r--r--

    int fd = creat(filename, mode);
    if (fd == -1) {
        perror("creat");
        return 1;
    }

    // 文件创建成功，进行其他操作
    close(fd);
    return 0;
}
```

#### 读取文件
```c
#include <unistd.h>
#include <fcntl.h>
#include <stdio.h>

int main() {
    int fd = open("example.txt", O_RDONLY);
    if (fd == -1) {
        perror("open");
        return 1;
    }

    char buffer[128];
    ssize_t bytesRead = read(fd, buffer, sizeof(buffer) - 1);
    if (bytesRead == -1) {
        perror("read");
        close(fd);
        return 1;
    }

    // 确保缓冲区以空字符结尾
    buffer[bytesRead] = '\0';
    printf("Read %zd bytes: %s\n", bytesRead, buffer);

    close(fd);
    return 0;
}
```

#### 写入文件
```c
#include <unistd.h>
#include <fcntl.h>
#include <stdio.h>

int main() {
    int fd = open("example.txt", O_WRONLY | O_CREAT, 0644);
    if (fd == -1) {
        perror("open");
        return 1;
    }

    const char *message = "Hello, World!";
    ssize_t bytesWritten = write(fd, message, strlen(message));
    if (bytesWritten == -1) {
        perror("write");
        close(fd);
        return 1;
    }

    printf("Wrote %zd bytes\n", bytesWritten);

    close(fd);
    return 0;
}
```

### 补充知识

- **文件描述符**：在Linux中，文件描述符是一个整数，用于标识打开的文件。
- **文件权限**：在创建文件时，可以通过`mode`参数设置文件权限。
- **错误处理**：使用`errno`和`perror`来处理和报告错误。
- **文件偏移量**：`lseek`函数用于改变文件的当前偏移量。

了解这些文件I/O函数和它们的使用方法对于进行系统编程和处理文件操作非常重要。
