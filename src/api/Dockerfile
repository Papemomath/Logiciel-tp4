# ---- STAGE 1 : Build ----
FROM maven:3.9.6-eclipse-temurin-21 AS build

WORKDIR /app

COPY pom.xml .
RUN mvn -q dependency:resolve

COPY src ./src

RUN mvn -q clean package -DskipTests

# ---- STAGE 2 : Run ----
FROM eclipse-temurin:21-jdk-alpine

WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080

# Environment variables
ENV DB_USERNAME="root" \
    DB_PASSWORD="1234" \
    DB_NAME="tododb" \
    DB_HOST="mariadb-service"

ENTRYPOINT ["java", "-jar", "app.jar"]