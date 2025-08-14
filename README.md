
# java-maven-app-multipipe

Set up Maven Project: Create a Maven-based Java project with pom.xml and necessary Java files.

Build Project Locally: Run mvn clean package to generate the .war file inside the target/ folder.

Create Dockerfile: Write a Dockerfile to copy the .war file into a Tomcat container.

Build Docker Image: Use docker build -t java-maven-app . to create the Docker image.

Run Docker Container: Run the container with docker run -d -p 8080:8080 java-maven-app.

Access the App: Open http://localhost:8080/myproject to view the deployed app.

