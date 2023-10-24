FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven -y
RUN git clone https://github.com/ruffwise/main-vprofile-project.git
RUN cd main-vprofile-project && git checkout docker && mvn install -y

FROM tomcat:9-jre11
LABEL "Project"="Vprofile"
LABEL "Author"="Ruffwise"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE main-vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD [ "catalina.sh","run" ]