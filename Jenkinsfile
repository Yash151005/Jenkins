pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/<username>/<repo>.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Stop old container if exists
                    sh 'docker rm -f myapp || true'

                    // Run new container with WAR
                    sh '''
                    docker run -d --name myapp \
                        -p 8080:8080 \
                        -v $WORKSPACE/target:/usr/local/tomcat/webapps \
                        tomcat:9.0.78-jdk17
                    '''
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
