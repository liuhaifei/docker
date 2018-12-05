

1.docker commit

 	使用centos镜像启动Docker容器 

 		docker run -ti centos bash

	安装wget

 		wget

		yum install -y wget
	
		exit 退出容器
	
		docker ps -a
	
	通过docker commit创建镜像
	
		docker commit dockerID Tag
	
		docker images
	
	docker run --rm -ti wget:0.1 bash
	
	exit

2.Dockerfile

	FROM centos
	
	LABEL maintainer "Clare Yang(xxx@example.com)"
	
	RUN yum install -y wget


​	

	mkdir demo
	
	vim Dockerfile 
	
	wq



	docker bulid --help
	
	创建docker镜像
	
	docker build .
	
	docker images
	
	docker run --rm -ti dockerId bash
	
	exit
	
	命名tag docker tag dockerId wget:0.2
	
		docker build -t wget:0.3 .



    深入DOCKERFILE
    
    Dockerfile 必须以FROM 打头
    
    WORKDIR指令：WORKDIR 路径
    
    COPY和ADD指令：实现从主机到容器的文件传输功能
    
    			 ADD <source> <destination>
    
    		 如果destination不存在 则自动创建
    
    RUN指令
    
     查看层数
    
    docker history centos



	减少镜像层数
	
		多个Run 命令通过&&合并		
	
	CMD/ENTRYPOINT指令
	
		语法
	
		--exec形式
	
		CMD ["executable","param1","param2"]  
	
		--默认参数
	
		CMD ["param1","param2"]  
	
		--shell形式
	
		CMD command param1 param2



		--exec形式
	
		ENTRYPOINT["executable","param1","param2"] 
	
		--shell形式
	
		ENTRYPOINT command param1  param2
	
		1.如果在Dockerfile中不指定CMD/ENTRYPOINT指令，Docker将使用基础镜像提供的默认指
	
		令
	
		2.CMD/ENTRYPOINT在docker镜像创建是不执行 在容器启动时才执行		
	
		3.既可以已exec形式也可以以shell形式执行



		eg :CMD curl	 
	
			ENTRYPOINT["curl","-s"] 
	
			CMD ["https://http"


​	



 上传DOCKER 镜像到DOCKER HUB

  1.注册账号

	登陆  docker login

2.Repository格式：ID/镜像名字

​	

3.docker tag给镜像打标签

docker tag cmd:0.2 dockerHubId/cmd:0.2

docker push dockerHubId/cmd:0.2









### 应用使用

docker run -d centos sleep 3000

查看容器

docker ps 

查看所有容器

docker ps -a

查看镜像

docker images

--rm 退出后自动删除容器

docker run --rm centos ls /

进入容器

docker run -ti centos bash

删除容器

docker rm dockerId





nginx

-d 容器运行在后台

docker run -d -p 8080:80 nginx:alpain

查看某个容器的运行信息

docker inspect DockerId

进入某个容器

docker exec -ti dockerId sh

停止某个容器

docker stop dockerId

docker start dockerId





卸载

yum list installed | grep docker 

yum -y remove *

rm -rf /var/lib/docker 