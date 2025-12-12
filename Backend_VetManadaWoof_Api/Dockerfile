# -------------------------------------------------------------------
# ETAPA 1: CONSTRUCCIÓN (Build)
# Usamos Maven con Java 21 (La versión que tu proyecto necesita)
# -------------------------------------------------------------------
FROM maven:3.9.6-eclipse-temurin-21 AS build

# Copiamos todo el código fuente al contenedor
COPY . .

# Compilamos y empaquetamos el .jar
RUN mvn clean package -DskipTests

# -------------------------------------------------------------------
# ETAPA 2: EJECUCIÓN (Run)
# Usamos Java 21 ligero para correr la app
# -------------------------------------------------------------------
FROM eclipse-temurin:21-jdk-alpine

# Copiamos el .jar generado
COPY --from=build /target/*.jar app.jar

# Exponemos el puerto
EXPOSE 8080

# Comando de inicio
ENTRYPOINT ["java","-jar","/app.jar"]