---

## 1. `ls` 指令
列出当前目录下的文件列表。

```bash
ls                  # 默认列出当前目录下的文件名
ls -l               # 以列表形式显示文件详细信息
ls -a               # 显示所有文件（包括隐藏文件）
ls -d               # 查看目录本身属性
ls -n               # 显示UID和GID
```

### 其他选项（了解即可）：
+ `-i` 显示文件的 inode 编号
+ `-k` 以K字节显示文件大小
+ `-F` 标注文件类型（/ 目录，* 可执行，@ 符号链接）
+ `-r` 反向排序
+ `-t` 以时间排序
+ `-s` 显示文件大小
+ `-R` 递归列出所有子目录
+ `-1` 每行一个文件

```bash
which ls            # 查看ls命令的实际路径
```

## 2. `pwd` 指令
显示当前工作目录。

```bash
pwd
```

## 3. `cd` 指令
切换目录。

```bash
cd ..               # 返回上级目录
cd ~                # 返回用户家目录
cd -                # 返回上次所在目录
cd /path/to/dir     # 绝对路径切换
cd ../relative/dir  # 相对路径切换
```

## 4. 创建文件/目录
### 4.1 `touch` 指令
创建空文件或更改时间戳。

```bash
touch file.txt
```

常用选项：

+ `-a` 修改访问时间
+ `-m` 修改修改时间
+ `-r file` 使用参考文件的时间戳
+ `-d "YYYY-MM-DD"` 设置特定时间

### 4.2 `mkdir` 指令（重要）
创建目录。

```bash
mkdir mydir
mkdir -p p1/p2/p3   # 递归创建目录
```

## 5. 删除命令（重要）
### 5.1.1 `rmdir` 指令
删除空目录。

```bash
rmdir dirname
rmdir -p p1/p2/p3   # 递归删除空目录
```

### 5.1.2 `rm` 指令
删除文件或目录。

```bash
rm file.txt
rm -r dirname       # 递归删除目录
rm -rf dirname      # 强制删除，危险！
```

### 5.2 `mv` 指令（重要）
移动或重命名文件/目录。

```bash
mv old.txt new.txt             # 重命名
mv file.txt /path/to/dir/      # 移动
mv -f /src /dest               # 强制
mv -i /src /dest               # 提示覆盖
```

**安全删除脚本（不建议使用）**：

```bash
# ~/.bashrc 中添加
mkdir -p ~/.trash
alias rm=trash
alias ur=undelfile
undelfile() {
 mv -i ~/.trash/$@ ./
}
trash() {
 mv $@ ~/.trash/
}
```

## 6. `man` 指令（重要）
查看命令的手册页。

```bash
man man        # 查看man自身手册
```

## 7. `cp` 指令（重要）
复制文件或目录。

```bash
cp file1 file2
cp file /path/
cp -r dir1 dir2       # 递归复制目录
cp -rf dir1 dir2      # 强制递归
```

## 8. `cat` 指令
查看文件内容。

```bash
cat file.txt
cat -n file.txt       # 所有行编号
cat -b file.txt       # 非空行编号
cat -s file.txt       # 压缩空行
```

## 9. 文件查看
### 构造测试文件：
```bash
count=0; while [ $count -le 1000 ]; do echo "hello $count"; let count++; done > file.txt
```

### 9.1 分屏查看
#### 9.1.1 `more` 指令
分页查看（只能向下）。

```bash
more file.txt
more -n file.txt    # 显示n行
```

#### 9.1.2 `less` 指令（推荐）
分页浏览 + 搜索。

```bash
less file.txt
```

常用操作：

+ `/字符串` 向下搜索
+ `?字符串` 向上搜索
+ `n/N` 重复/反向搜索
+ `q` 退出
+ `-N` 显示行号

### 9.2 局部查看
#### 9.2.1 `head` 指令
默认显示前10行。

```bash
head file.txt
head -n 20 file.txt
```

#### 9.2.2 `tail` 指令
默认显示最后10行。

```bash
tail file.txt
tail -n 20 file.txt
```

### 9.3 查看中间区域内容
查看第100~120行：

```bash
head -120 file.txt | tail -20
```

## 10. 时间相关指令
```bash
date
date "+%Y-%m-%d %H:%M:%S"
```

格式：

+ `%Y` 年
+ `%m` 月
+ `%d` 日
+ `%H` 时
+ `%M` 分
+ `%S` 秒
+ `%F` 等价于 `%Y-%m-%d`

时间戳相关：

```bash
date +%s                  # 当前时间戳
date -d @1720345600      # 时间戳转时间
```

## 11. `cal` 指令
显示日历。

```bash
cal
```

## 12. `find` 指令（很重要）
查找文件：

```bash
find /path -name filename
```

## 13. `grep` 指令
行过滤工具。

```bash
grep "main" file.txt
grep -v "main" file.txt     # 反向匹配
grep -i "main" file.txt     # 忽略大小写
grep -n "main" file.txt     # 显示行号
```

## 14. 压缩/解压命令
### 14.1 `zip/unzip`
```bash
zip file.zip file.txt
zip -r dir.zip dir/
unzip file.zip
unzip file.zip -d /path/
```

### 14.2 `tar` 指令
```bash
tar czf file.tgz file/        # 打包压缩
tar xzf file.tgz              # 解压
tar xzf file.tgz -C /path/    # 解压到指定目录
```

参数说明：

+ `-c` 创建
+ `-x` 解压
+ `-z` 使用gzip压缩
+ `-f` 指定文件名
+ `-v` 显示详细过程

## 15. `bc` 指令
命令行计算器：

```bash
bc
```

配合管道：

```bash
echo "3.1 + 2.3" | bc
```

## 16. `uname` 指令
查看系统信息。

```bash
uname -a
```

## 17. 热键
| 热键 | 作用 |
| --- | --- |
| `Tab` | 自动补全 |
| `Ctrl + C` | 强制终止命令 |
| `Ctrl + D` | 退出shell |
| `Ctrl + R` | 搜索历史命令 |
| `history` | 显示命令历史 |


## 18. 关机/重启命令
```bash
shutdown -h now         # 立即关机
reboot                  # 重启
```

## 19. 扩展命令
连接远程服务器：

```bash
ssh user@ip_address
```

---

## 20. 参考链接
[【Linux】Linux基本操作指令_linux系统基本操作命令-CSDN博客](https://blog.csdn.net/qq_54851255/article/details/122697976?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522e200d13d2d5a990e134fa9ef9d67a9d2%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=e200d13d2d5a990e134fa9ef9d67a9d2&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-122697976-null-null.142^v102^pc_search_result_base2&utm_term=linux%E5%9F%BA%E6%9C%AC%E6%8C%87%E4%BB%A4&spm=1018.2226.3001.4187)

[【Linux】Linux权限管理 —— shell运行原理 | 权限 | 目录权限 | 粘滞位 | 权限掩码umask_sodu chmod-CSDN博客](https://blog.csdn.net/qq_54851255/article/details/122764048)

