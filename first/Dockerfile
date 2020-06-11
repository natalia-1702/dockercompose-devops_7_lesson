FROM ubuntu:18.04 AS build
RUN apt-get update
RUN apt-get install -y git
RUN apt-get install -y maven
WORKDIR /home/
RUN git clone https://github.com/boxfuse/boxfuse-sample-java-war-hello.git
WORKDIR /home/boxfuse-sample-java-war-hello/
RUN mvn package
#CMD ["mvn", "package"]


FROM ubuntu:18.04
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y default-jdk
WORKDIR /opt/tomcat
RUN curl -O https://apache-mirror.rbc.ru/pub/apache/tomcat/tomcat-8/v8.5.56/bin/apache-tomcat-8.5.56.tar.gz
RUN tar xvfz apache-tomcat-8.5.56.tar.gz
#RUN file apache-tomcat-8.5.55.tar.gz
RUN mv apache-tomcat-8.5.56/* /opt/tomcat/.
#COPY --from=build /home/ /home/
#RUN ls /home/
COPY --from=build /home/boxfuse-sample-java-war-hello/target/hello-1.0.war /opt/tomcat/webapps/

#RUN ls -la /home/boxfuse-sample-java-war-hello/
#RUN cp /home/boxfuse-sample-java-war-hello/target/hello-1.0.war /opt/tomcat/webapps/
#RUN cp /home/boxfuse-sample-java-war-hello/target/*.war /opt/tomcat/webapps/
EXPOSE 8080
CMD ["/opt/tomcat/bin/catalina.sh", "run"]
