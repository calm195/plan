# VMware 安装配置虚拟机

本例以`Ubuntu server 24.04.3 LTS`镜像为准，虚拟机软件为`VMware Workstation 17 Pro`

## 新建虚拟机

下载好镜像和虚拟机软件后，选择文件 - 新建虚拟机

1. 选择自定义

	![init](D:\plan\image\vmvare\new\init.png)

2. 默认选择兼容性即可，如果有需要可以修改

	![compatibility](D:\plan\image\vmvare\new\compatibility.png)

3. 选择稍后安装操作系统，因为配置完虚拟机后，如果有需要可以配置网络什么的

	![source](D:\plan\image\vmvare\new\source.png)

4. 根据实际镜像情况选择，我这里选Linux - Ubuntu 64位

	![system-type](D:\plan\image\vmvare\new\system-type.png)

5. 路径与命名随意，不要有中文字符和空格

	![name](D:\plan\image\vmvare\new\name.png)

6. 处理器数量根据物理机配置选，一般是物理机配置的50%或者以下。

  > 我物理机为一个处理器六个处理器内核，逻辑内核12。
  >
  > 我选 1 -  4/6

  ![cpu](D:\plan\image\vmvare\new\cpu.png)

6. 内存分配按照推荐即可，如果物理机性能较强选高一点，一般默认够用了

	![memory](D:\plan\image\vmvare\new\memory.png)

7. 网络类型选NAT类型，虚拟机隔离外网，相当于内建了一个子网

	![net-type](D:\plan\image\vmvare\new\net-type.png)

8. IO控制器默认推荐即可

	![io](D:\plan\image\vmvare\new\io.png)

9. 磁盘也是默认即可

	![disk](D:\plan\image\vmvare\new\disk.png)

11. 磁盘文件类型默认即可

    ![disk-type](D:\plan\image\vmvare\new\disk-type.png)

11. 磁盘大小默认够用了，有需要自己改

    ![disk-size](D:\plan\image\vmvare\new\disk-size.png)

12. 磁盘文件名一般默认是前面的虚拟机名，前面设好了这里不用管，直接下一步

    ![disk-name](D:\plan\image\vmvare\new\disk-name.png)

13. 完成

    ![completed](D:\plan\image\vmvare\new\completed.png)

## 配置网络 - 以NAT类型为例

选择 编辑 - 虚拟网络编辑器

1. 右下角更改配置

   ![change](D:\plan\image\vmvare\net\change.png)

2. 选择要更改的网卡，NAT类型一般是`VMnet8`

3. 然后本界面可以修改该网卡的子网，以及是否启用DHCP

   > 如果网卡启用了DHCP，那么虚拟机也需要启用DHCP
   >
   > 如果未启用DHCP，那么虚拟机需要设置IP信息

   ![select-nat](D:\plan\image\vmvare\net\select-nat.png)

4. NAT设置中可以设置网关、DNS、端口转发等

   ![nat](D:\plan\image\vmvare\net\nat.png)

5. 如果启用DHCP，DNCP设置中可以选择DHCP IP范围以及租用时间，IP超时后虚拟机将尝试自动续租。

   > 最长租用时间是63d 23h 59m

   ![dhcp](D:\plan\image\vmvare\net\dhcp.png)

## 启动虚拟机

配置完成后，即可启动虚拟机开始安装系统

