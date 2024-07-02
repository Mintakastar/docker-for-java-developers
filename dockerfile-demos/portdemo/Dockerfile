#FROM openjdk:11.0-jre
FROM openjdk:17-jdk-slim-buster

RUN mkdir /app
ADD target/portdemo-0.0.1-SNAPSHOT.jar /app/portdemo.jar
CMD ["java", "-jar", "/app/portdemo.jar"]


