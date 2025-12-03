pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                echo "Building Docker Image"
                bat "docker build -t kubedemoapp:v1 ."
            }
        }

        stage('Docker Login') {
            steps {
                bat 'docker login -u srithu -p Docker@123'
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                echo "Pushing Docker Image to Docker Hub"
                bat "docker tag kubedemoapp:v1 srithu/sample:kubeimage1"
                bat "docker push srithu/sample:kubeimage1"
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                echo "Deploying to Kubernetes cluster"
                bat 'kubectl apply -f deployment.yaml --validate=false --insecure-skip-tls-verify'
                bat 'kubectl apply -f service.yaml --insecure-skip-tls-verify'
            }
        }
    }

    post
    {
        success {
            echo 'Build Successful'
        }
        failure {
            echo 'Build Failed'
        }
        always 
        {
            echo 'Pipeline completed'
        }
    }
    
}
