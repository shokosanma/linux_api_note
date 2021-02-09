# Linux常用命令

## Bash快捷键

ctrl+a相当于home键，光标移至最前。

ctrl+e相当于end键，光标移至最后。

ctrl+u清除目前所有输入

## linux系统文件类型

普通文件(-)
目录文件(d)
字符设备文件(c)
块设备文件(b)
符号链接文件(l)
管道文件(p)
套接字(s)

## 软链接

创建时如使用相对路径，移动后依旧根据相对路径寻找原文件，导致无法使用。

```
ln -s ./file file.soft
```

## find

```
find /dir/path -type 'l'
find /dir/path -type '-'
find /dir/path -type 'c'
find /dir/path -name '*.cpp'
find /dir/path -maxdepth 1 -name 'l'
find /dir/path -size +20M -size -50M
-atime access	-mtime modify	-ctime change
```

