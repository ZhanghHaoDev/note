# nvim

## 1. nvim 简介

### 安装与卸载

1. 安装 

brew install nvim

2. 卸载

删除配置：rm -rf ~/.config/nvim
删除可执行文件：brew uninstall nvim

### 需求

1. 右侧文件树，文件图标
2. 左侧迷你地图，自动启动，显示上下进度，选中的行高亮
3. 终端 ctrl + t
4. 保存：w全部保存
5. 标签页，标签页显示图标,标签页切换tab
6. q 键退出，退出编辑页面，退出文件树
7. F1 F2 切换标签页
8. LSP（C/C++）clang cmake 代码补全，代码跳转 gd 跳转到声明，ctrl + t跳转到实现
10. git 显示 新增，删除，修改等操作
11. 目前我把插件的目录 packer.nvim 安装到 ~/.config/nvim 目录下
12. 下面的状态栏，颜色为橘黄色
13. 命令模式输入w 保存全部文件
14. 分屏,鼠标支持拖动分屏

## 2. 配置

1. 创建配置目录(nvim 所有的配置)：mkdir ~/.config/nvim
2. 迷你地图需要安装 code-minimap 工具 ：brew install code-minimap
3. 显示图标的字体，需要专门下载


## 3. 插件管理

1. 更新插件：:PackerUpdate
