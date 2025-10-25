pipeline {
    agent any

    tools {
        maven 'Maven' // Make sure this matches Jenkins global tool name
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Yash151005/jenkins.git'
            }
        }

        stage('Build') {
            steps {
                dir('.') {  // ensure Maven runs in repo root
                    sh 'mvn clean package'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Copy WAR into Docker Tomcat container on VM2
                sh 'scp target/myapp.war azureuser@52.225.85.234:/home/azureuser/'
            }
        }
    }

    post {
        success {
            echo '✅ Build and Deployment Successful!'
        }
        failure {
            echo '❌ Build or Deployment Failed.'
        }
    }
}
