### 安装步骤 （`centos7`）

1. 使用`yum install -y docker`命令安装

   ```properties
   [root@iZbp1aivbpv57lpujwza5tZ docker]# yum install -y docker
   Loaded plugins: fastestmirror
   ...                   
   Complete!
   ```

2. 使用 `systemctl start/stop/restart docker ` 启动/停止/重启 `docker`

   ```properties
   [root@iZbp1aivbpv57lpujwza5tZ docker]# systemctl start docker
   #关闭docker
   [root@iZbp1aivbpv57lpujwza5tZ docker]# systemctl stop docker
   #c重启docker
   [root@iZbp1aivbpv57lpujwza5tZ docker]# systemctl restart docker
   ```

3. 使用`docker version `查看`docker`版本

   ```properties
   [root@iZbp1aivbpv57lpujwza5tZ docker]# docker version
   shell-init: error retrieving current directory: getcwd: cannot access parent directories: No such file or directory
   #客户端版本信息
   Client:
    Version:         1.13.1
    API version:     1.26
    Package version: docker-1.13.1-84.git07f3374.el7.centos.x86_64
    Go version:      go1.10.2
    Git commit:      07f3374/1.13.1
    Built:           Fri Nov 30 02:48:45 2018
    OS/Arch:         linux/amd64
   #服务端版本信息
   Server:
    Version:         1.13.1
    API version:     1.26 (minimum version 1.12)
    Package version: docker-1.13.1-84.git07f3374.el7.centos.x86_64
    Go version:      go1.10.2
    Git commit:      07f3374/1.13.1
    Built:           Fri Nov 30 02:48:45 2018
    OS/Arch:         linux/amd64
    Experimental:    false
   
   ```

4. 使用`docker info`查看`docker`安装信息

   ``` properties
   [root@iZbp1aivbpv57lpujwza5tZ docker]# docker info
   .....
   Server Version: 1.13.1
   Storage Driver: overlay2
    Backing Filesystem: extfs
    Supports d_type: true
   ....
   #docker 根目录
   Docker Root Dir: /var/lib/docker
   Debug Mode (client): false
   Debug Mode (server): false
   Registry: https://index.docker.io/v1/
   WARNING: bridge-nf-call-iptables is disabled
   WARNING: bridge-nf-call-ip6tables is disabled
   Experimental: false
   Insecure Registries:
    127.0.0.0/8
   Live Restore Enabled: false
   #registries地址
   Registries: docker.io (secure)
   ```

5. 好了 `docker`安装很简单 就到这里结束了 下一篇介绍`docker`镜像的使用