#FROM eclipse-temurin:21-jre-alpine

#WORKDIR /usr/src

#COPY Main.class .

#CMD ["java", "Main"]
# FROM eclipse-temurin:21-jdk-alpine AS build

# WORKDIR /usr/src

# COPY Main.java .
# RUN javac Main.java

# FROM eclipse-temurin:21-jre-alpine

# WORKDIR /usr/src

# COPY --from=build /usr/src/Main.class .

# CMD ["java", "Main"] ctrl K C 

# Build stage
FROM eclipse-temurin:21-jdk-alpine AS myapp-build
ENV MYAPP_HOME=/opt/myapp
WORKDIR $MYAPP_HOME

RUN apk add --no-cache maven

COPY pom.xml .
COPY src ./src
RUN mvn package -DskipTests

# Run stage
FROM eclipse-temurin:21-jre-alpine
ENV MYAPP_HOME=/opt/myapp
WORKDIR $MYAPP_HOME
COPY --from=myapp-build $MYAPP_HOME/target/*.jar $MYAPP_HOME/myapp.jar

ENTRYPOINT ["java", "-jar", "myapp.jar"]
