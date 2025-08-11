# 整体流程

从零开始部署各组件 - 以本地虚拟机为例

## 虚拟机准备

1. 下载`VMvare Workstation`

   > 进入[官网](https://support.broadcom.com/)`https://support.broadcom.com/`后，注册登录即可免费下载，这里用的是**17 pro**

2. 下载Ubuntu镜像

   > 进入[Ubuntu 官网](https://ubuntu.com/download/)`https://ubuntu.com/download/`后，可以直接下载，这里用的是**Ubuntu server 24.04.3 LTS**
   >
   > or
   >
   > 进入[itellyou官网](https://next.itellyou.cn/)`https://next.itellyou.cn/`也可下载，相当于Ubuntu官网的镜像

3. [创建虚拟机](./steps/vmware.md) - 使用**Ubuntu server 24.04.3 LTS**镜像

4. [Ubuntu Sever安装](./steps/ubuntu-install.md) - 最小安装，并且容量全设为系统盘容量

5. bash 美化 - [Bash-it](https://bash-it.readthedocs.io/en/latest/)

   1. 安装git：`sudo apt install git`

   2. 克隆Bash-it仓库：`git clone --depth=1 https://github.com/Bash-it/bash-it.git ~/.bash_it`

      > 如果connection refused，那么设置一下代理
      >
      > - `git config --global http.proxy "http://proxy:port"`：配置全局HTTP代理
      > - `git config --global https.proxy "https://proxy:port"`：配置全局HTTPS代理

   3. 运行安装脚本：`~/.bash_it/install.sh`

   4. 重启或者`source ~/.bashrc`使Bash-it生效

   5. 修改主题`vim ~/.bashrc` 修改 `BASH_IT_THEME`为`axin`

   6. 启用插件：`bash-it enable plugins sudo history history-search history-eternal history-substring-search`

   7. 重新加载配置：`bash-it reload`

6. 安装`net-tools`：`sudo apt install net-tools`

## mysql

1. 运行命令 `sudo apt-get install mysql-server`

2. 检查运行状态 `systemctl status mysql`

3. 修改配置文件，开放外部IP访问以及设置端口

   1. 寻找mysqld.cnf文件：`sudo find / -name mysqld.cnf`

   2. 修改mysql服务对应的mysqld.cnf文件

      ```ini
      [mysqld]  
      user=mysql
      bind-address=0.0.0.0 # 允许所有IP访问
      port=3306 # MySQL默认端口
      ```

4. 重启mysql服务：`sudo systemctl restart mysql`

5. 登录mysql：`sudo mysql`

   > 首次登录mysql，root用户无密码

6. 修改root密码：`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'new_password';`

   > mysql8.0版本以上修改root密码命令与之前版本不同
7. 创建用于远程访问的用户：`create user 'user'@'%' identified by 'password';`

8. 创建应用数据库：`create database myblog`

9. 授权用户访问数据库：`grant all privileges on database_name.* to 'user'@'localhost';`

10. 刷新：`flush privileges;`

## postgresql

1. 安装：`sudo apt install postgresql`

2. 切换到 `postgres`用户：`sudo -i -u postgres`

3. 进入Postgresql命令行：`psql`

4. 修改postgres用户密码：`\password postgres`

5. 创建远程访问用户：`create user user-name with password 'password';`

6. 创建数据库：`create database db owner user;`

7. 监听外部IP以及设置端口：`sudo vim /etc/postgresql/<version>/main/postgresql.conf`

   ```ini
   listen_addresses = '*'
   posrt = 5432
   ```

8. 允许外部IP访问数据库：`sudo vim /etc/postgresql/<version>/main/pg_hba.conf`

   ```ini
   # Type  Database        User            Address                 Method
   host    db              user            0.0.0.0/0               scram-sha-256
   ```

9. 重启postgresql服务：`sudo systemctl restart postgresql`

# redis

1. 安装：`sudo apt install redis-server`

2. 修改配置文件：`sudo vim /etc/redis/redis.conf`

   ```ini
   bind 0.0.0.0 # 允许所有IP访问
   protected-mode no # 关闭保护模式
   port 6379 # Redis默认端口
   daemonize no # 前台运行，方便调试
   requirepass your_password # 设置密码，开启后需要使用密码登录
   ```

3. 重启服务：`systemctl restart redis`

## nginx

1. 安装gpg相关包：`sudo apt install curl gnupg2 ca-certificates lsb-release ubuntu-keyring`

2. 导入nginx离线key

   ```bash
   curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor \
       | sudo tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null
   ```

3. 验证key：`gpg --dry-run --quiet --no-keyring --import --import-options import-show /usr/share/keyrings/nginx-archive-keyring.gpg`

4. 设置apt stable仓库

   ```bash
   echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] \
   http://nginx.org/packages/ubuntu `lsb_release -cs` nginx" \
       | sudo tee /etc/apt/sources.list.d/nginx.list
   ```

5. 设置仓库优先级

   ```bash
   echo -e "Package: *\nPin: origin nginx.org\nPin: release o=nginx\nPin-Priority: 900\n" \
       | sudo tee /etc/apt/preferences.d/99nginx
   ```

6. 安装`sudo apt install nginx`

7. 修改配置文件`nginx.conf`

   > 可能需要修改`vim /etc/nginx/conf.d/default.conf`

   ```nginx
   server {
   	listen                80;
   	server_name    localhost;
   }
   ```

8. 重启服务：`systemctl restart nginx`