FROM maven:3.6.3-adoptopenjdk-11 as stage1
ENV MAVEN_OPTS="-XX:+TieredCompilation -XX:TieredStopAtLevel=1"
WORKDIR /opt/service
COPY ./pom.xml .
RUN mvn dependency:go-offline
COPY ./src ./src
RUN mvn clean install -Dmaven.test.skip=true

FROM adoptopenjdk/openjdk11:jre-11.0.9_11-alpine
WORKDIR /opt/service
COPY --from=stage1 /opt/service/target/servicio1-0.0.1-SNAPSHOT.jar /opt/service