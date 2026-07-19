# syntax=docker/dockerfile:1

# Build stage: compile the jar with Maven
FROM maven:3.8.6-jdk-17 AS builder
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn -B package -DskipTests

# Runtime stage: run the jar on a lightweight JRE
FROM eclipse-temurin:17-jre-alpine
EXPOSE 8080

ARG JAR_FILE=target/*.jar
COPY --from=builder /app/${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
