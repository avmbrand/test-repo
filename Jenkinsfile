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
        stage('Auth to Kubernetes Cluster') {
            steps {
                script {
                    sh """
                        gcloud container clusters get-credentials cluster-1 --zone=us-central1-c
                    """
                }
            }
        }

        stage('Deploy Version 2') {
            steps {
                script {
                    sh """
                        kubectl apply -f deployment-v2.yaml
                        kubectl apply -f service-v2.yaml
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
}
