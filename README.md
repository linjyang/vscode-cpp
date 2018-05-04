# VSCode 搭建C++开发环境

## 安装gcc/g++
MacOS默认已安装

Ubuntu下：
```bash
sudo apt install gcc
sudo apt install g++
```
## macos安装gdb
调试用，如果不需要可以跳过这步。
MacOS下比较麻烦，用`brew install gdb`之后还要创建证书并给gdb签名。可以参考[教程](https://blog.csdn.net/cairo123/article/details/52054280)

坑：
- 教程中创建证书类型为“系统”，若是创建失败，可以创建为登陆，然后把生成的证书拖到“系统”那一栏
- 完成后要重启系统，否则签名可能不会生效。

## vscode安装插件
![](https://github.com/linjyang/vscode-cpp/blob/master/pic/vscode_plugin.jpg)

## 生成launch.json
![](https://github.com/linjyang/vscode-cpp/blob/master/pic/launch_json.jpg)

修改launch.json如下：
```
{
    "version": "0.2.0",
    "configurations": [

        {
            "name": "C++ Launch",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceRoot}/main.out", 
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceRoot}",  
            "environment": [],                 
            "externalConsole": true,        
            "linux": {
                "MIMode": "gdb",
                "setupCommands": [
                    {
                        "description": "Enable pretty-printing for gdb",
                        "text": "-enable-pretty-printing",
                        "ignoreFailures": true
                    }
                ]
            },
            "osx": {
                "MIMode": "lldb"
            }
        }
    ]
}
```
## 生产tasks.json
菜单栏选则task -> configure task -> 出现的输入框中输入task -> create task json from template -> Others

生成后修改tasks.json如下：
```
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "hello",
            "type": "shell",
            "command": "g++",
            "args": [
                "-g", "main.cpp",
                "-o", "main.out"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```
注意：g++编译要加参数“-g”，否则gdb无法调试

## 编译运行
MacOS 编译快捷键 cmd + shift + b

Ubuntu 编译快捷键 ctrl + shift + b

运行调试如图：
![](https://github.com/linjyang/vscode-cpp/blob/master/pic/compile.png)
