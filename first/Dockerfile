FROM ubuntu:18.04 AS build
WORKDIR /home/
RUN apt-get update; \
    apt-get install -y git; \
    apt-get install -y maven; \
    git clone https://github.com/boxfuse/boxfuse-sample-java-war-hello.git;
WORKDIR /home/boxfuse-sample-java-war-hello/
RUN mvn package

FROM ubuntu:18.04
RUN apt-get update; \
    apt-get install -y curl; \
    apt-get install -y default-jdk;
WORKDIR /opt/tomcat
RUN curl -O https://apache-mirror.rbc.ru/pub/apache/tomcat/tomcat-8/v8.5.56/bin/apache-tomcat-8.5.56.tar.gz; \
    tar xvfz apache-tomcat-8.5.56.tar.gz; \
    mv apache-tomcat-8.5.56/* /opt/tomcat/ 
COPY --from=build /home/boxfuse-sample-java-war-hello/target/hello-1.0.war /opt/tomcat/webapps/
EXPOSE 8080
CMD ["/opt/tomcat/bin/catalina.sh", "run"]
