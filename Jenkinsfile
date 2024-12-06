pipeline {
    agent any

    environment {
        // GOOGLE_PROJECT = 'your-gcp-project'
        // GKE_CLUSTER = 'your-gke-cluster'
        // GKE_ZONE = 'your-gke-zone'
        // IMAGE_NAME = 'my-app'
        // BLUE_VERSION = 'blue'
        // GREEN_VERSION = 'green'
        // IMAGE_TAG = "${env.BUILD_ID}"  // Using Jenkins build ID as the image tag
        // GCR_REGISTRY = 'gcr.io/your-gcp-project'
    }

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
                        kubectl apply -f deployment-v2.yaml
                        kubectl apply -f service-v2.yaml
                    """
                }
            }
        }

        stage('Switch Traffic to Green') {
            steps {
                script {
                    sh """
                        kubectl apply -f switch.yaml
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
