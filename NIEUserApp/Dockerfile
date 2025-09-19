

# build stage
FROM maven:3.9.9-eclipse-temurin-17 AS build
WORKDIR /src
COPY NIEUserApp/pom.xml .
RUN mvn -q -DskipTests dependency:go-offline
COPY NIEUserApp/src ./src
RUN mvn -q -DskipTests package

# run stage
FROM eclipse-temurin:17-jre
WORKDIR /app
COPY --from=build /src/target/*.war app.war
EXPOSE 9900
ENTRYPOINT ["sh","-c","java -Dserver.port=${PORT:-9900} -jar app.war"]