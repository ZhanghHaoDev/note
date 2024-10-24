
# 文件存储

## 1. inode
- **定义**：inode是文件系统中存储文件属性的数据结构，如权限、类型、大小、时间、用户、磁盘块位置等。
- **存储**：大多数inode存储在磁盘上，但近期使用的inode会缓存到内存中。

## 2. dentry（目录项）
- **定义**：dentry是文件系统中用于快速查找文件的目录项。
- **组成**：包含文件名和指向inode的指针。
- **好处**：允许多个目录项（不同文件名）指向同一个inode，实现文件共享。

# 文件操作

## 1. `stat()` 函数
- **功能**：获取文件属性。
- **原型**：
  ```c
  int stat(const char *restrict pathname, struct stat *restrict statbuf);
  ```
- **参数**：
  - `pathname`：文件路径。
  - `statbuf`：存放文件属性的传出参数。
- **返回值**：
  - 成功：0
  - 失败：-1

## 2. `link()` 函数
- **功能**：为已存在的文件创建目录项（硬链接）。

## 3. `unlink()` 函数
- **功能**：删除文件的目录项。
- **注意**：删除文件后，文件内容不会立即释放，直到所有打开该文件的进程关闭文件。

# 目录操作

## 1. `chmod()` 系统调用
- **功能**：改变文件或目录的访问权限。
- **原型**：
  ```c
  int chmod(const char *pathname, mode_t mode);
  ```

## 2. `chown()` 系统调用
- **功能**：改变文件的所有者和组。
- **原型**：
  ```c
  int chown(const char *pathname, uid_t owner, gid_t group);
  ```

## 3. `mkdir()` 函数
- **功能**：创建目录。
- **原型**：
  ```c
  int mkdir(const char *pathname, mode_t mode);
  ```

## 4. `rmdir()` 函数
- **功能**：删除目录。
- **原型**：
  ```c
  int rmdir(const char *pathname);
  ```

## 5. `chdir()` 函数
- **功能**：改变当前工作目录。
- **原型**：
  ```c
  int chdir(const char *path);
  ```

## 6. `getcwd()` 函数
- **功能**：获取当前工作目录。
- **原型**：
  ```c
  char *getcwd(char *buf, size_t size);
  ```

# 扫描目录

## 1. `opendir()` 和 `closedir()` 函数
- **功能**：打开和关闭目录。
- **原型**：
  ```c
  DIR *opendir(const char *name);
  int closedir(DIR *dirp);
  ```

## 2. `readdir()` 函数
- **功能**：读取目录的下一个目录项。
- **原型**：
  ```c
  struct dirent *readdir(DIR *dirp);
  ```

## 3. `telldir()` 和 `seekdir()` 函数
- **功能**：获取和设置目录的当前位置。
- **原型**：
  ```c
  off_t telldir(DIR *dirp);
  void seekdir(DIR *dirp, off_t offset);
  ```

# 错误处理

## 1. `strerror()` 函数
- **功能**：返回错误码的描述字符串。
- **原型**：
  ```c
  char *strerror(int errnum);
  ```

## 2. `perror()` 函数
- **功能**：打印错误信息。
- **原型**：
  ```c
  void perror(const char *s);
  ```

# 格式化输入输出

## 1. `printf()` 函数
- **功能**：格式化输出到标准输出。
- **原型**：
  ```c
  int printf(const char *format, ...);
  ```

## 2. `sprintf()` 函数
- **功能**：格式化输出到字符串。
- **原型**：
  ```c
  int sprintf(char *str, const char *format, ...);
  ```

## 3. `scanf()` 函数
- **功能**：格式化输入从标准输入。
- **原型**：
  ```c
  int scanf(const char *format, ...);
  ```

## 4. `fscanf()` 函数
- **功能**：格式化输入从文件流。
- **原型**：
  ```c
  int fscanf(FILE *stream, const char *format, ...);
  ```

## 5. `sscanf()` 函数
- **功能**：格式化输入从字符串。
- **原型**：
  ```c
  int sscanf(const char *str, const char *format, ...);
  ```
