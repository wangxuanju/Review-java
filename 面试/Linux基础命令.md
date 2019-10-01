# pwd当前所在文件夹
# clear清屏
# 查看命令位置：which
# ls 显示当前目录
ls -a 显示目录下所有子目录与文件，包括隐藏文件

ls -l 以列表方式显示文件的详细信息

ls –lah 

（ls -h 配合 -l 以人性化的方式显示文件大小）




# 创建文件
touch创建文件

例如touch 1.txt

# 删除文件

rm删除文件

rm –r 1.txt强制删除

rm wenjian/2.txt 删除文件wenjian下的2.txt

rm –i 1.txt

-i 以进行交互式方式执行

rm –f 1.txt

-f 强制删除，忽略不存在的文件，无需提示



# 创建文件夹
mkdir wodewenjian 创建文件夹

mkdir wodewenjian/a在wodewenjian下建a文件夹（只能建一层，即在文件里面建一个文件夹）

# 删除文件夹
rmdir wodewenjian 删除文件夹

rmdir wode/wode2删除wode下的wode2文件夹

cd wodewenjian 切换目录到wodewenjian

cd 切换到当前用户主目录

cd ~ 切换到当前用户的主目录(/home/用户目录)（和上一个命令作用一样）

cd .当前目录

cd .. 切换到上级目录

cd –进入上次所在目录

# 复制
cp

cp 1.txt 2.txt复制1.txt生成2.txt

cp 1.txt wode/3.txt将1.txt拷贝到wode文件夹下命名为3.txt

cp –a 1.txt 2.txt

-a 该选项通常在复制目录时使用，它保留链接、文件属性，并递归地复制目录，简单而言，保持文件原有属性

cp –f 1.txt 2.txt

-f 覆盖已经存在的目标文件而不提示

cp –i 1.txt 2.txt

-i 交互式复制，在覆盖目标文件之前将给出提示要求用户确认

cp –r wodewenjian wodewenjain2

-r若给出的源文件是目录文件，则cp将递归复制该目录下的所有子目录和文件，目标文件必须为一个目录名。

cp 1.txt 2.txt

-v 显示拷贝进度


# 移动重命名
mv 1.txt 3.txt重命名1.txt为3.txt

mv 1.txt wodewenjian2将1.txt移动到wodewenjian2中

# 压缩解压
gzip 2.txt 压缩2.txt文件

gzip –d 2.txt解压缩刚才生成的压缩文件



# cat 查看或者合并文件内容
cat 1.txt显示内容

cat 1.txt 2.txt则1.txt和2.txt的内容均显示到面板


# grep文本搜索
选项 含义

grep –v a 1.txt将1.txt中不是a的字符全部返回

grep –v m 1.txt将1.txt中字符全部返回，因为里面没有字符m

-v 显示不包含匹配文本的所有行（相当于求反）

grep –i A 1.txt 在1.txt文件中查A字符，其实A字符不存在只有a字符，返回a字符

-i 忽略大小写

grep –n a 1.txt在1.txt文件中找 a字符，返回行数（找不到则没反应）

-n 显示匹配行及行号

grep –n 我是 1.txt将1.txt中中文输出

grep -n '^a' 1.txt

^a 行首,搜寻以 m 开头的行；

grep -n 'ke$' 1.txt

 ke$ 行尾,搜寻以 ke 结束的行；

# 查找文件 find
find –name 1.txt找出当前目录下所有1.txt文件

find –name ‘*.txt’找出当前目录下所有带.txt后缀的文件

