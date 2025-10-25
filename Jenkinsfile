pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Yash151005/Jenkins.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                // Copy WAR into Docker container
                sh 'docker cp target/myapp.war myapp:/usr/local/tomcat/webapps/'
                sh 'docker restart myapp'
            }
        }
    }

    post {
        success {
            echo '✅ Deployment Successful!'
        }
        failure {
            echo '❌ Build or Deployment Failed.'
        }
    }
}
