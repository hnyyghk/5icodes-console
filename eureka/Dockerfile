# 基础镜像
FROM openjdk:8-jre-alpine

# 作者
MAINTAINER hnyyghk

# 系统编码
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

# 声明一个挂载点，容器内此路径会对应宿主机的某个文件夹
VOLUME /tmp

# 设置环境变量
ENV eureka.client.service-url.cn-qingdao http://192.168.31.131:8761/eureka/
ENV eureka.client.service-url.cn-beijing http://192.168.31.131:8762/eureka/
# Necessary for Docker otherwise you will get 172.0.0.x IP
ENV eureka.instance.ip-address 192.168.31.131

# 将应用构建成功后的jar文件复制到镜像根目录下，并重命名为app.jar
ADD target/eureka-0.0.1.jar app.jar

# 暴露端口，如果需要使用端口，在执行run命令时使用-p命令映射
EXPOSE 8761-8762

# 启动容器时的进程
# 为了解决tomcat可能启动慢的问题，添加java.security.egd的系统属性指向/dev/urandom，具体可查看：https://www.cnblogs.com/mightyvincent/p/7685310.html
ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "-jar", "/app.jar", "--eureka.environment=stg"]