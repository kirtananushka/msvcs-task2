FROM maven:3.8.4-openjdk-17-slim AS build
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src/ ./src/
RUN mvn clean package -DskipTests

FROM mcr.microsoft.com/openjdk/jdk:17-ubuntu AS package
WORKDIR /app
COPY --from=build /app/target/song-svc-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8072
CMD ["java", "-jar", "app.jar"]
