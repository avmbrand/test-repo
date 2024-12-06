pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                script {                  
                    sh """
                       echo image already available
                    """
                }
            }
        }

        stage('Deploy Green Version') {
            steps {
                script {
                    sh """
                        kubectl apply -f hpa-v1.yaml
                        kubectl apply -f deployment-v1.yaml
                        kubectl apply -f service-v1.yaml
                    """
                }
            }
        }

    post {
        always {
            sh 'kubectl get all'
        }
    }
}
