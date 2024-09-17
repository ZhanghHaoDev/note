采样点的个数问题

采样点的个数，计算的点包括：文件时长，声道数，采样频率，都会影响采样点的个数。

gtest的使用

我们在运行ctest的时候，如果全部测试都通过会显示下面的信息：
```shell
100% tests passed, 0 tests failed out of 1
```
如果有测试失败，会显示：
```shell
50% tests passed, 1 tests failed out of 2
```
如果有测试没有通过，我们可以使用下面的命令来查看具体的测试结果：
```shell
ctest --rerun-failed --output-on-failure
```
这个命令会重新运行失败的测试，并且在失败的时候输出失败的信息。
测试的输出会显示具体是哪个测试失败了，以及失败的原因。
显示FAILED的就是失败的测试，PASSED的就是通过的测试。