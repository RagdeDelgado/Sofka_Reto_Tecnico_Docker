# Etapa de build (Maven + JDK 17)
FROM maven:3.9.9-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn -B -DskipTests=true dependency:go-offline
COPY src ./src
RUN mvn -B -DskipTests=true clean package

# Etapa de runtime (JRE 17)
FROM eclipse-temurin:17-jre
WORKDIR /app
ENV JAVA_OPTS=""
COPY --from=build /app/target/*.jar app.jar
EXPOSE 4000
ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS -jar app.jar"]
