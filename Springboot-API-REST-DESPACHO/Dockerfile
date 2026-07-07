# ==========================================
# Etapa 1: Construcción (Build Stage)
# ==========================================
FROM maven:3.9.6-eclipse-temurin-17 AS builder
WORKDIR /app

# Descargar dependencias
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Compilar el proyecto de Despachos
COPY src ./src
RUN mvn clean package -DskipTests

# ==========================================
# Etapa 2: Ejecución (Run Stage)
# ==========================================
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

# Copiamos el .jar con el nombre exacto que genera tu pom.xml
COPY --from=builder /app/target/Springboot-API-REST-DESPACHO-0.0.1-SNAPSHOT.jar app.jar

# Exponemos el puerto 8081 (según tu application.properties)
EXPOSE 8081

# Iniciar la aplicación
ENTRYPOINT ["java", "-jar", "app.jar"]