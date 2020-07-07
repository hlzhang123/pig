# 第一条指令必须为FROM指令, 并且如果在同一个Dockerfile中创建多个镜像时, 可以使用多个FROM指令 (每个镜像一次)

# https://hub.docker.com/r/anapsix/alpine-java/
FROM anapsix/alpine-java:8_server-jre_unlimited
# FROM anapsix/alpine-java:latest

# https://hub.docker.com/_/openjdk
# FROM openjdk:8u232-jdk

# 指定维护者的信息
MAINTAINER wangiegie@gmail.com

# 指定容器时间
ENV TZ=Asia/Shanghai

RUN ln -sf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# 创建文件夹
RUN mkdir -p /pig-sentinel

# 切换到该文件夹下
WORKDIR /pig-sentinel

# 告诉 Docker 服务端暴露端口, 在容器启动时需要通过 -p 做端口映射
EXPOSE 5003

# 将jar包复制到 Dockerfile 所在的相对目录下, 可以是URL, 也可以是tar.gz(自动解压) (当使用本地目录为源目录时, 推荐使用 COPY)
#  ADD 是复制指定路径到容器路径, COPY 是复制本地主机的路径到容器的路径
ADD ./target/pig-sentinel-dashboard.jar ./

# CMD 指定启动容器时执行的命令, 每个 Dockerfile 只能有一条 CMD 指令. 如果指定了多条指令, 则最后一条执行 (会被启动时指定的命令覆盖)
# 睡眠20ms在执行启动命令
# Djava.security.egd=file:/dev/./urandom 解决阿里云的tomcat启动慢的问题
CMD sleep 30;java -Djava.security.egd=file:/dev/./urandom -jar pig-sentinel-dashboard.jar
# ENTRYPOINT ["java","-jar","/register.jar"]  效果与CMD类似, 不可被 docker run 提供的参数覆盖. 如果指定了多条指令, 则最后一条执行
