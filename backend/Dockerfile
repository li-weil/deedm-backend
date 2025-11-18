# 第一阶段：使用 Maven 构建 Spring Boot 项目
FROM maven:3.9-eclipse-temurin-17 AS builder

WORKDIR /app

# 拷贝依赖文件并构建（建议保留测试）
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests=false

# 第二阶段：使用轻量 JRE 镜像运行 jar 包
FROM eclipse-temurin:17-jre-alpine

WORKDIR /app

# 拷贝构建产物（建议明确 jar 名）
COPY --from=builder /app/target/*.jar app.jar

# 暴露端口
EXPOSE 8080

# 启动 Spring Boot 应用，并设置 JVM 参数
ENTRYPOINT ["java", "-Xms256m", "-Xmx512m", "-jar", "app.jar"]
