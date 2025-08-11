# Ubuntu server 安装

Ubuntu server 24.04.3 LTS 最小安装

配置好虚拟机后，启动虚拟机，等待安装程序加载

1. 选择Install

   ![init](D:\plan\image\ubuntu\init.png)

2. 语言选英语 ~~语言大佬请随意~~

   ![language](D:\plan\image\ubuntu\lang.png)

3. 如果联网了，应该会有更新提示，直接继续

   ![no update](D:\plan\image\ubuntu\update.png)

4. 键盘配置默认英文键盘就好

   ![keyboard](D:\plan\image\ubuntu\keyboard.png)

5. 安装类型选最小安装 

   > 全量安装也可以，他会安装一些常用的包，还不错

   ![mini-install](D:\plan\image\ubuntu\mini-install.png)

6. 如果开启了DHCP，网络信息会自动获取

   ![net-dhcp](D:\plan\image\ubuntu\net-dhcp.png)

7. 如果是手动配置，那么选择Edit IPv4

   ![net-edit](D:\plan\image\ubuntu\net-edit.png)

8. 选择Manual - 手动配置

   ![net-manual](D:\plan\image\ubuntu\net-manual.png)
   
   大致配置如下：
   
   ![example](D:\plan\image\ubuntu\net-manual-example.png)

9. 代理服务器视情况配置

   > 虚拟机中，代理服务器一般是主机的代理软件
   >
   > IP一般为相关子网中主机IP
   >
   > 端口为代理软件的端口
   >
   > **注：代理软件需要开启局域网访问**

   ![png](D:\plan\image\ubuntu\proxy.png)

10. 网络检测

    > 如果检测失败，回去检查网络设置

    ![check](D:\plan\image\ubuntu\net-check.png)

11. 磁盘使用默认即可

    ![conf](D:\plan\image\ubuntu\disk-conf.png)

12. 进入分区挂载，默认分配了一半的容量给系统分区

    > 即，如果就这样进入系统，那么有一半容量没有利用到
    >
    > 当然也可以后期进行分区

    ![disk-default](D:\plan\image\ubuntu\disk-default.png)

13. 如果不想要其他分区，那么可以先删除默认系统分区

    ![disk-delete](D:\plan\image\ubuntu\disk-delete.png)

14. 将空闲空间分区 - 有需要的话

    > 如果上一步删除了默认系统分区，这一步必须执行

    ![disk-create](D:\plan\image\ubuntu\disk-create.png)

    分配可用空间与路径

    ![disk-alloc](D:\plan\image\ubuntu\disk-alloc.png)

    完成后直接下一步

15. 配置用户名，主机名和密码

    ![user-name](D:\plan\image\ubuntu\user-name.png)

16. Ubuntu Pro 跳过 - 高级货咱要不起

    ![skip-pro](D:\plan\image\ubuntu\skip-pro.png)

17. 安装OpenSSH用于ssh连接 - 后面自己装也行

    ![ssh](D:\plan\image\ubuntu\ssh.png)

18. 组件选择 - 自己选吧 - 空格是选择

    ![module](D:\plan\image\ubuntu\module.png)

19. 确认后，Ubuntu会自己开始安装内核和选择的组件

20. 重启

    ![reboot](D:\plan\image\ubuntu\reboot.png)

    这里直接回车就好

    ![reboot-mount](D:\plan\image\ubuntu\reboot-mount.png)

21. 输入用户名密码登录就好

    ![login](D:\plan\image\ubuntu\login.png)

22. 设置root密码 - `sudo passwd root`
23. 更新apt - `sudo apt update`
24. 更新软件 - `sudo apt upgrade`