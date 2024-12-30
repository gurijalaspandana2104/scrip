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
