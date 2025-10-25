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
            steps {pipeline {
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
                dir('.') {  // ensures Maven runs in repo root
                    sh 'mvn clean package'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'WAR will be deployed manually or via docker cp later'
            }
        }
    }

    post {
        success {
            echo '✅ Build Successful!'
        }
        failure {
            echo '❌ Build Failed.'
        }
    }
}

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
