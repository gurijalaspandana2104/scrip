# scrip

pipeline {
    agent any
    tools {
        maven 'MAVEN HOME' // Replace with your configured Maven version in Jenkins
    }
    stages {
        stage('Git Repo & Clean') {
            steps {
                bat '''
                    if exist sample (
                        rmdir /s /q sample
                    )
                    git clone https://github.com/gurijalaspandana2104/sample.git
                    mvn clean -f sample/pom.xml
                '''
            }
        }
        stage('Install') {
            steps {
                bat "mvn install -f sample/pom.xml"
            }
        }
        stage('Test') {
            steps {
                bat "mvn test -f sample/pom.xml"
            }
        }
        stage('Package') {
            steps {
                bat "mvn package -f sample/pom.xml"
            }
        }
    }
    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed. Check the logs for details.'
        }
    }
}



	install docker ---apt-get update
-	                            		     apt-get install docker.io
                            apt-get install nano


step 2:-  git clone <paste the github link of maven-web-java project>
step 3:- Navigate to the path where your index.jsp is there….

VI.	 Create the image

Step 4:-  nano Dockerfile 
 

V.  Run the image and access it with public ip of virtual machine

Step 1:- build your image 
	docker build –t <imagename> .(dot)
Step 2:- check for images
Step 3:- run image
	docker  run –d  --name app-demo –p 6060:8080 <image name>
Step:-4 Accessing the app by public ip of virtual machine
Note:-if your are not able to connect change the inbound rules..








# Use the official NGINX Alpine image
FROM nginx:alpine

# Set the working directory inside the container (optional)
WORKDIR /usr/share/nginx/html

# Copy the content from your local directory to the NGINX container
COPY . /usr/share/nginx/html

# Expose port 80 to access the application
EXPOSE 80

# NGINX by default runs as a daemon, no need for an ENTRYPOINT since it's already configured in NGINX's base image

