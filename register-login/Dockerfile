# Build stage
FROM eclipse-temurin:21-jdk AS build
WORKDIR /app

# Copy Maven files
COPY .mvn/ .mvn
COPY mvnw pom.xml ./

# Pre-download dependencies
RUN ./mvnw dependency:go-offline -B

# Copy source code and build the application
COPY src ./src
RUN ./mvnw package -DskipTests

# Runtime stage
FROM eclipse-temurin:21-jre
WORKDIR /app

# Copy the built JAR file
COPY --from=build /app/target/*.jar app.jar

# Expose the application port
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
