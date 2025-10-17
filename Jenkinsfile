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
                sshPublisher(publishers: [
                    sshPublisherDesc(configName: 'deploy-server',
                    transfers: [
                        sshTransfer(
                            sourceFiles: 'target/*.war',
                            remoteDirectory: '/var/lib/tomcat9/webapps',
                            removePrefix: 'target'
                        )
                    ],
                    usePromotionTimestamp: false,
                    verbose: true)
                ])
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
