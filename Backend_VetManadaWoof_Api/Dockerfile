# -------------------------------------------------------------------
# ETAPA 1: CONSTRUCCIÓN (Build)
# Usamos una imagen con Maven para compilar el proyecto
# -------------------------------------------------------------------
FROM maven:3.9.6-eclipse-temurin-17 AS build

# Copiamos todo el código fuente al contenedor
COPY . .

# Compilamos y empaquetamos el .jar (saltando los tests para ir rápido)
RUN mvn clean package -DskipTests

# -------------------------------------------------------------------
# ETAPA 2: EJECUCIÓN (Run)
# Usamos una imagen ligera de Java solo para correr la app
# -------------------------------------------------------------------
FROM eclipse-temurin:17-jdk-alpine

# Copiamos el .jar generado en la etapa anterior
# IMPORTANTE: El asterisco *.jar busca cualquier nombre generado
COPY --from=build /target/*.jar app.jar

# Exponemos el puerto (Render usará su propia variable PORT, pero esto es buena práctica)
EXPOSE 8080

# Comando para iniciar la aplicación
ENTRYPOINT ["java","-jar","/app.jar"]