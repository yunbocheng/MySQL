## DOS 命令(不用加分号，不区分大小写，按上下键可以使用历史命令)
1. 创建一个文件夹
> mkdir abc (相当于创建一个名字为abc的目录)

> md abc;
2. 删除文件夹
> rd abc; (删除名字为 abc 的文件夹)
3. 默认情况下DOS命令窗口打开之后，定位在
> C:\Users\YunboCheng
4. 切换盘符
> c: 回车 d: 回车 (直接盘符+:)
5. 切换目录
> cd 路径 (change directory)改变目录
> cd 1/2 和 cd 1\2 效果是一样的
> cd C:\Users\YunboCheng
- 路径在盘符上分为两种:绝对路径和相对路径。
- 相对路径一定是相对于当前所在位置而言的，从当前所在的位置作为起点。
- 在windows操作系统中凡是路径起点为盘符的都是绝对路径，例如:
  > C:\Users\YunboCheng
6. 返回上级路径
> cd .. (其中 .. 代表的是一个文件夹)
> cd \ 或者 cd /(空格可加可不加)
> cd . (一个点代表当前路径)
7. 清屏
> cls
8. 查看当前目录下有的什么东西
> dir
9. 退出 DOS命令窗口
> exit
10. 删除一个或多个文件
> E:\JavaProject>del 1.txt (删除名字为 1.txt 的文件)
11. 查看本机的 IP 地址
> ipconfig (ip地址的配置信息)
12. 查看更加详细的网路信息
> ipconfig /all (/与all中间不要加空格)
- 这个详细信息中包括 网卡 的物理地址，例如： D0-94-66-EE-49-0D
- 这个物理地址具有全球唯一性。物理地址通常叫做MAC地址。
13. 查看两台计算机正常通信
> ping IP地址 (ping 180.101.49.12)(百度的 IP 地址)
> ping 域名 (ping www.baidu.com)
14. 查看网路稳不稳定,看数据中的时间毫秒数值
> ping 域名(IP地址) -t (ping 180.101.49.12 -t)
15. 想强行终止掉 一个一直在执行的命令
> Ctrl + C 键即可
16. 域名底层最终还是会被解析成IP地址的形式。

17. 文本编辑快捷键

![](https://gitee.com/YunboCheng/imageBad/raw/master/image/20210507165634.png)

18. 查看应用的版本号
> 名称 -version (java -version)

19. 查看编译器的版本
> javac -version

20. 查看Java虚拟机的版本
> java -version

19. 环境变量
- 系统变量：范围比较大，系统变量会让计算机所有用户都起作用
- 用户变量：范围比较小，这个变量只是作用于当前用户

注意：path 属于系统环境变量，path环境变量隶属于windows操作系统，Java只不过是用了一下path环境变量。
 