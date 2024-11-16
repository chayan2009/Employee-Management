# Use OpenJDK as the base image for Java applications
FROM openjdk:17-jdk-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the Maven build artifact (the .jar file) into the container
COPY target/EmployeeService.jar /app/EmployeeService.jar

# Expose the port the application will run on
EXPOSE 8081

# Set the entrypoint for the container to run the Java application
ENTRYPOINT ["java", "-jar", "/app/EmployeeService.jar"]
