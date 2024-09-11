### Make 命令的参数选项

| 序号 | 参数选项 | 解释 | 示例 |
|------|----------|------|------|
| 1    | `-f file` 或 `--file=file` | 指定要使用的 Makefile 文件。 | `make -f MyMakefile` |
| 2    | `-C dir` 或 `--directory=dir` | 切换到指定目录后再执行 make。 | `make -C src` |
| 3    | `-j [jobs]` 或 `--jobs[=jobs]` | 指定同时运行的任务数。 | `make -j4` |
| 4    | `-k` 或 `--keep-going` | 即使某个目标失败，也继续执行其他目标。 | `make -k` |
| 5    | `-n` 或 `--just-print` 或 `--dry-run` 或 `--recon` | 只打印将要执行的命令，但不实际执行。 | `make -n` |
| 6    | `-s` 或 `--silent` 或 `--quiet` | 执行命令时不打印命令本身。 | `make -s` |
| 7    | `-r` 或 `--no-builtin-rules` | 禁用内置规则。 | `make -r` |
| 8    | `-R` 或 `--no-builtin-variables` | 禁用内置变量。 | `make -R` |
| 9    | `-t` 或 `--touch` | 通过更新目标文件的时间戳来使目标文件看起来是最新的，但不实际执行命令。 | `make -t` |
| 10   | `-q` 或 `--question` | 检查目标是否需要更新，但不实际执行命令。如果目标需要更新，则返回非零状态。 | `make -q` |
| 11   | `-B` 或 `--always-make` | 无条件地重新构建所有目标。 | `make -B` |
| 13   | `-W file` 或 `--what-if=file` 或 `--new-file=file` 或 `--assume-new=file` | 假设指定的文件已被更新。 | `make -W main.c` |
| 14   | `-p` 或 `--print-data-base` | 打印 Makefile 数据库，包括所有变量、规则等。 | `make -p` |
| 15   | `-v` 或 `--version` | 打印 make 的版本信息。 | `make -v` |
| 16   | `-d` 或 `--debug` | 打印调试信息。 | `make -d` |

### 隐含规则使用的变量

| 序号 | 变量 | 解释 |
|------|------|------|
| 1    | `CC` | C 编译器（默认值为 `cc`） |
| 2    | `CXX` | C++ 编译器（默认值为 `g++`） |
| 3    | `FC` | Fortran 编译器（默认值为 `gfortran`） |
| 4    | `LD` | 链接器（默认值为 `ld`） |
| 5    | `CFLAGS` | C 编译器选项 |
| 6    | `CXXFLAGS` | C++ 编译器选项 |
| 7    | `FFLAGS` | Fortran 编译器选项 |
| 8    | `CPPFLAGS` | C/C++ 预处理器选项 |
| 9    | `LDFLAGS` | 链接器选项 |
| 10   | `LDLIBS` | 链接库选项 |
| 11   | `$@` | 目标文件名 |
| 12   | `$<` | 第一个依赖文件名 |
| 13   | `$^` | 所有依赖文件名 |
| 14   | `$?` | 所有比目标文件新的依赖文件名 |
| 15   | `$*` | 不包括扩展名的目标文件名 |

### 补充说明
- 使用 `make -B` 可以强制重新构建所有目标，这在某些情况下非常有用，比如当你需要从头开始清理并重建项目时。
- `make -W file` 选项可以用来测试更新某个文件后，哪些目标会被重新构建。
- `make -p` 选项非常有用于调试 Makefile，因为它会显示所有的规则和变量，帮助你理解 make 如何解析和执行 Makefile。

这些参数选项和变量提供了对 `make` 构建过程的精细控制，使得 `make` 成为一个非常强大的工具，适用于各种复杂的构建场景。
