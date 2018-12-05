### 容器启动方式

> docker 容器启动方式有这两种 1.`docker commit `2.`Dockerfile `下面就使用这两种方式启动。

#### `一、Docker commit`

1. 使用`centos`镜像启动`Docker`容器 

   ```properties
   #命令 docker run -ti centos bash
   [root@iZbp1aivbpv57lpujwza5tZ /]# docker run -ti centos bash
   .....
   latest: Pulling from docker.io/library/centos
   aeb7866da422: Pull complete 
   Digest: sha256:67dad89757a55bfdfabec8abd0e22f8c7c12a1856514726470228063ed86593b
   Status: Downloaded newer image for docker.io/centos:latest
   ```

2. 安装`wget`

   ``` properties
   #命令 yum install -y wget
   [root@2030a1d19ca8 /]# yum install -y wget                                       
   ......
   Complete!
   ```

3. 退出容器

   ```properties
   #命令 exit
   [root@2030a1d19ca8 /]# exit
   exit
   [root@iZbp1aivbpv57lpujwza5tZ /]# 
   ```

4. 查看所有`Docker`容器

   ```properties
   #命令
   [root@iZbp1aivbpv57lpujwza5tZ /]# docker ps -a
   CONTAINER ID IMAGE  COMMAND CREATED   STATUS      			PORTS      NAMES
   2030a1d19ca8 centos "bash"  5 ...     Exited (0)...                      hopeful..
   ```

5. 通过`docker commit`创建镜像

   ```properties
   #命令 docker commit dockerID Tag
   [root@iZbp1aivbpv57lpujwza5tZ /]# docker commit 2030a1d19ca8 wget:0.1
   sha256:e3fecb1359564eace9535bdf9ac6e4dc7d085397d0420256c998afcf906f7655
   ```

6. 查看镜像(可以看到刚刚我们创建的镜像已经存在 `e3fecb135956`)

   ```properties
   #命令 docker images
   [root@iZbp1aivbpv57lpujwza5tZ ~]# docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   wget                0.1                e3fecb135956         7 seconds ago       270 MB
   docker.io/centos    latest             75835a67d134        8 weeks ago         200 MB
   ```

7. 运行镜像创建容器

   ``` properties
   #命令 docker run --rm -ti wget:0.1 bash
   [root@iZbp1aivbpv57lpujwza5tZ /]# docker run --rm -ti wget:0.1 bash
   #输出hell world
   [root@23186db78fc6 /]# echo hell world
   hell world
   #退出
   [root@23186db78fc6 /]# exit
   exit
   ```

8. Ok docker commit创建镜像方式已经完成

   

#### `二、Dockerfile`

1. 新建一个文件夹

   ```properties
   [root@iZbp1aivbpv57lpujwza5tZ local]# mkdir docker
   ```

2. 创建`Dockerfile`文件

   ```properties
   [root@iZbp1aivbpv57lpujwza5tZ docker]# vim Dockerfile
   FROM centos
   LABEL maintainer "docker_user docker_user@email.com"
   RUN yum install -y wget
   ```

3. 创建镜像

   ```properties
   [root@iZbp1aivbpv57lpujwza5tZ docker]# docker build -t wget:0.2 .
   ....                                                 
   Complete!
   Successfully built 4e47ce31fe00
   ```

4. 查看镜像

   ``` properties
   [root@iZbp1aivbpv57lpujwza5tZ ~]# docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   wget                0.2                 4e47ce31fe00        47 seconds ago      270 MB
   wget                0.1                 e3fecb135956        2 hours ago         270 MB
   docker.io/centos    latest              75835a67d134        8 weeks ago         200 MB
   ```

5. 使用镜像创建容器

   ```properties
   [root@iZbp1aivbpv57lpujwza5tZ docker]# docker run --rm -ti 4e47ce31fe00 bash
   [root@4dd95ae71e28 /]# exit
   exit
   ```

6. 上传docker镜像到`dockerhub`,[dockerHub注册地址](https://hub.docker.com/)

   ```properties
   #登陆docker
   [root@iZbp1aivbpv57lpujwza5tZ ~]# docker login
   #输入dockerId
   Username: 
   #输入密码
   Password: 
   Login Succeeded
   
   #docker tag给镜像打标签 格式：docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
   #注意 目标target斜杠前面的必须要是自己的dockerId 不然不能上传成功
   [root@iZbp1aivbpv57lpujwza5tZ ~]# docker tag wget:0.2 fei1992/wget:0.2
   [root@iZbp1aivbpv57lpujwza5tZ ~]# docker images
   REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
   wget                0.2                 4e47ce31fe00        24 minutes ago      270 MB
   fei1992/wget        0.2                 4e47ce31fe00        24 minutes ago      270 MB
   ....
   #上传到dockerhub
   [root@iZbp1aivbpv57lpujwza5tZ ~]# docker push fei1992/wget:0.2
   14b259a8b308: Pushed 
   f972d139738d: Pushed 
   0.2: digest: sha256:01e07b1ddc3ff53c5caa72fcd9ee60d20d0134ed8e8171900ce7ee0716f2c952 size: 741
   ```

7. 登陆到dockehub可以查看已上传的镜像

   ![我的镜像图片](C:\Users\18040111\Desktop\dockeimage.jpg)

8. 容器启动就到此结束啦