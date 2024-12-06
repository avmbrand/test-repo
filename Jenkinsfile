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

        stage('Deploy Version 1') {
            steps {
                script {
                    sh """
                        kubectl apply -f deployment-v1.yaml
                        kubectl apply -f hpa-v1.yaml
                    """
                }
            }
        }

        stage('wait till the rollout succed') {
            steps {
                script {
                    sh """
                        kubectl rollout status deployment/deployment-v1
                    """
                }
            }
        }
        stage('switch to version to v1') {
            steps {
                script {
                    sh """
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
}
