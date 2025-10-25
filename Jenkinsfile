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
                script {
                    // Copy WAR to VM2 (Docker host)
                    sh 'scp target/myapp.war azureuser@57.159.29.82:/home/azureuser/'

                    // Deploy WAR into Docker Tomcat
                    sh """
                        ssh azureuser@<VM2-IP> '
                        docker cp /home/azureuser/myapp.war myapp:/usr/local/tomcat/webapps/ &&
                        docker restart myapp
                        '
                    """
                }
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
