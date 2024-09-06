# vs开发cmake项目

# 1. 遇到的问题

1. 在window上使用IDEvs，cmake，来构建qt项目的时候现在找不到ui.exe

问题描述：在cmake构建的时候没有错误，但是在make这个阶段出现错误，显示找不到ui.exe，仔细观察发现vs在查找ui.exe的时候会在bin目录的debug目录下面查找ui.exe，但是这个根本没有这个目录，所以报错

解决办法：不要使用debug模式，使用release模式会自动修正这个错误