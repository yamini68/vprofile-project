FROM eclipse-temurin:11 AS BUILD_IMAGE
LABEL Project="vprofile"
LABEL Author="Yamini"
RUN apt update && apt install -y maven git

RUN git clone https://github.com/devopshydclub/vprofile-project.git
RUN cd vprofile-project && git checkout docker && mvn install

FROM tomcat:9.0.48-jdk11-openjdk-slim
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war  /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]