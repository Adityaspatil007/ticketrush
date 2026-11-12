# Stage 1: Build the application
FROM eclipse-temurin:21-jdk-jammy AS builder
WORKDIR /app

COPY .mvn .mvn
COPY mvnw pom.xml ./
RUN chmod +x mvnw && ./mvnw -B dependency:go-offline

# Copy source code and build the fat JAR
COPY src src
RUN ./mvnw -B -DskipTests package

# Stage 2: Runtime image with a secure non-root user
FROM eclipse-temurin:21-jre-jammy AS runtime
WORKDIR /app

# Create a non-privileged system user and group (UID 10001)
RUN groupadd --gid 10001 ticketrush && \
    useradd --uid 10001 --gid ticketrush --no-create-home --shell /usr/sbin/nologin ticketrush

# Copy the built JAR from the builder stage
COPY --from=builder /app/target/*.jar app.jar

# Switch to the non-root user for security
USER 10001:10001

# Expose the application port
EXPOSE 8080

# Run the Spring Boot application
ENTRYPOINT ["java", "-XX:MaxRAMPercentage=70", "-jar", "app.jar"]