# ---- Base Node ----
FROM maven:alpine AS base
# Create app directory
WORKDIR /app

# ---- Dependencies ----
FROM base AS build  
# A wildcard is used to copy all project files
COPY . ./
# install app dependencies and compile using maven
RUN mvn clean compile && mvn package

# --- Release with Alpine ----
FROM openjdk:8-jre-alpine AS release  
# Create app directory
WORKDIR /app
# Copy build jar file from target to app for release
COPY --from=build /app/target/*.jar ./
# Run application and pass jar file name in docker run command
ENTRYPOINT ["java", "-jar"]
