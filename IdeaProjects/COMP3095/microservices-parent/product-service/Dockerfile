# --------------------------------
# Dockerfile for product-service
# --------------------------------

# -----------
# BUILD stage
# -----------
# Base Image
FROM gradle:8-jdk17-alpine AS builder

# Copy the application files from the host machine to the image filesystems
COPY --chown=gradle:gradle . /home/gradle/src

# set the directory within the image, for executing future commands
WORKDIR /home/gradle/src

# run gradle build within the container - NOT the host machine
RUN gradle build -x test

#--------
# Package Stage
#--------
# Base Image
FROM openjdk:17-alpine

RUN mkdir /app

COPY --from=builder /home/gradle/src/build/libs/*.jar /app/product-service.jar

ENV MONGO_DB_USERNAME=rootadmin \
    MONGO_DB_PASSWORD=password

EXPOSE 8084

ENTRYPOINT ["java","-jar","/app/product-service.jar"]