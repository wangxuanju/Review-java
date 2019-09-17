# Linux
Linux是一个长时间运行比较稳定的操作系统，一般会拿它作为服务器（web/db/nginx）

Linux具有C的编译环境，一些软件没有软件包（redis等）需要在Linux的C编译环境上运行得到软件包。
## 常用命令
pwd:获取当前路径

clear:清屏

Command --help：显示Command命令的帮助信息

### man command:查阅Command命令的使用手册
空格  显示手册页下一屏

Enter 一次滚动手册页的一行

b     回滚一屏

f     前滚一屏

q     退出

/word 搜索word字符串
### ls:查看文件
ls -lah

-a 指定所有子目录与文件，包括隐藏文件

-l 文件的详细信息

-h 文件大小
# cd：切换工作目录
cd ~ 切换到当前用户文件主目录

cd . 切换到当前工作目标

cd ..切换到上级目录

cd - 进入上次所在的目录
# mkdir:创建目录
mkdir a/b/c -p

mkdir app 当前目录下创建app目录
# rmdir:删除目录
rmdir app 删除app目录
# rm 删除文件
rm -r abc

-i 交互式方式执行

-f 强制删除

rm a.txt删除a.tet文件

rm -f a.tet不询问直接删除
# cp:拷贝
cp 1.txt 2.txt 1.txt复制到2.txt

cp 1.txt ../   将1.txt文件复制到上一层目录
# mv:移动、重命名
mv 1.txt ../将a.txt移动到上一层目录

mv a.txt b.txt  a.txt文件命名为b.txt
# touch：创建文件
touch a.txt创建一个空文件
# 关机重启
reboot 重启操作系统

shutdown -r now 重启

shutdown -h now 关机

shutdown -h 20:25 20:25关机

shutdown -h +10 10分钟后关机
# useradd 用户管理
useradd test 添加test目录

useradd test -d /home/t/指定用户home目录

passwd test 为test用户设置密码

userdel test 删除test用户（不删home目录）

userdel -r test 删除用户及home目录
# 组管理
groupadd public 创建名为public的值

useradd u1 -g public 创建目录指定组

groupdel public 删除组（如果该组有成员，先删除成员，才能删除组）

