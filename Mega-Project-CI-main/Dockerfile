# Stage 1: Build the Java application
FROM maven:3.9.6-eclipse-temurin-17-alpine AS build

# Set working directory
WORKDIR /usr/src/app

# Copy Maven project files
COPY pom.xml .
COPY src ./src

# Build the application and skip tests (optional)
RUN mvn clean package -DskipTests

# Stage 2: Create a lightweight runtime image
FROM eclipse-temurin:17-jdk-alpine

# Set application directory
ENV APP_HOME /usr/src/app
WORKDIR $APP_HOME

# Copy the JAR file from the build stage
COPY --from=build /usr/src/app/target/*.jar app.jar

# Expose port
EXPOSE 8080

# Run the application
CMD ["java", "-jar", "app.jar"]
