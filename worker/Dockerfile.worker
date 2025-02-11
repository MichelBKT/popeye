# Étape 1 : Compilation
FROM maven:3.9.6-eclipse-temurin-21-alpine AS builder

# Définition du répertoire de travail
WORKDIR /app

# Copie des fichiers du projet
COPY pom.xml ./
RUN mvn dependency:resolve

COPY src ./src
RUN mvn package

# Étape 2 : Exécution
FROM eclipse-temurin:21-jre-alpine

WORKDIR /app

# Copie du fichier compilé depuis l'étape précédente
COPY --from=builder /app/target/worker-jar-with-dependencies.jar .

# Commande de démarrage
CMD ["java", "-jar", "worker-jar-with-dependencies.jar"]
