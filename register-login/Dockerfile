# Build stage
FROM eclipse-temurin:21-jdk AS build

# Set the working directory
WORKDIR /app

# Copy Maven wrapper and POM files
COPY .mvn/ .mvn
COPY mvnw pom.xml ./

# Verify Java version
RUN java -version

# Download Maven dependencies
RUN ./mvnw dependency:go-offline -B

# Copy the source code
COPY src ./src

# Build the application
RUN ./mvnw package -DskipTests

# Runtime stage
FROM eclipse-temurin:21-jre

# Set the working directory
WORKDIR /app

# Copy the built JAR file from the build stage
COPY --from=build /app/target/*.jar app.jar

# Expose the application port
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
