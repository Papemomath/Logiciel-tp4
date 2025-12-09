# Étape 1 : Build avec Java 21
FROM maven:3.9.9-eclipse-temurin-21 AS build
WORKDIR /app

COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests -Dmaven.test.skip=true

# Étape 2 : Image finale pour exécution avec Java 21
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app

# Copier le JAR compilé
COPY --from=build /app/target/*.jar app.jar

# Créer le répertoire pour la base de données persistante
RUN mkdir -p /data

# Exposer le port
EXPOSE 8080

# Lancer l'application
ENTRYPOINT ["java", "-jar", "app.jar"]