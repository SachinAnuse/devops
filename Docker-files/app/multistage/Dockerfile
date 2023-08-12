# Stage 1: Build the application
FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install -y git maven
RUN git clone https://github.com/SachinAnuse/devops.git
RUN cd vprofile-project && git checkout docker && mvn install

# Stage 2: Create the final image
FROM tomcat:9-jre11

# Remove existing webapps
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy the WAR file from the build stage to the Tomcat webapps directory
COPY --from=BUILD_IMAGE /vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

# Expose the Tomcat port
EXPOSE 8080

# Start Tomcat
CMD ["catalina.sh", "run"]
