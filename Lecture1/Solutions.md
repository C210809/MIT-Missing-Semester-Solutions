1. To make sure you’re running an appropriate shell, you can try the command `echo $SHELL`. If it says something like `/bin/bash` or `/usr/bin/zsh`, that means you’re running the right program.

```shell
echo $SHELL
```

2. Create a new directory called `missing` under `/tmp`.

```shell
mkdir /tmp/missing
```

3. Look up the `touch` program. The `man` program is your friend.

```shell
man touch
```

4. Use `touch` to create a new file called `semester` in `missing`.

```shell
cd /tmp/missing
touch semester
```

5. Write the following into that file, one line at a time:

```
#!/bin/sh
curl --head --silent https://missing.csail.mit.edu
```

```shell
alt+tab  # 切换到浏览器
ctrl+a  # 全选
ctrl+c  # 复制
vim semester
i  # 进入insert模式
shift+insert  # 粘贴
```

6. Try to execute the file, i.e. type the path to the script (`./semester`) into your shell and press enter. Understand why it doesn’t work by consulting the output of `ls` (hint: look at the permission bits of the file).

```shell
./semester
```

显示：`-bash: ./semester: Permission denied`

原因是没有执行权限：`-rw-rw-r-- 1 ubuntu ubuntu 61 Aug 21 15:58 semester`。

7. Run the command by explicitly starting the `sh` interpreter, and giving it the file `semester` as the first argument, i.e. `sh semester`. Why does this work, while `./semester` didn’t?

```shell
./semester
```

8. Look up the `chmod` program (e.g. use `man chmod`).

```shell
man chmod
```

9. Use `chmod` to make it possible to run the command `./semester` rather than having to type `sh semester`. How does your shell know that the file is supposed to be interpreted using `sh`? See this page on the [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)) line for more information.

```shell
chmod +x semester
```

10. Use `|` and `>` to write the “last modified” date output by `semester` into a file called `last-modified.txt` in your home directory.

修改 `semester` 文件如下：

```shell
#!/bin/sh
read name
echo $name
exit 0
```

执行命令：

```shell
echo "last modified" | ./semester > ~/modified.txt
```

