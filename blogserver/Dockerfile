# 使用官方的 OpenJDK 作为基础镜像
FROM openjdk:11-jre-slim

# 设置工作目录
WORKDIR /app

# 复制构建好的 Spring Boot JAR 文件到容器中
COPY target/blogserver-0.0.1-SNAPSHOT.jar vblog.jar

# 暴露服务端口
EXPOSE 8083

# 启动 Spring Boot 应用
CMD ["java", "-jar", "vblog.jar"]
