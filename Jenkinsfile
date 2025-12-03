pipeline
{
    agent any
    stages
    {
        stage('Build')
        {
            steps
            {
                echo 'Build Docker Image'
                bat 'docker build -t kubedemoapp:v1 .'
            }
        }
        stage('Docker Login')
        {
            steps
            {
                echo 'Login to Docker'
                    bat 'docker login -u srithu -p Docker@123'
            }
        }
        stage('Push Docker image')
        {
            steps
            {
                echo 'Push Docker Image'
                bat 'docker tag kubedemoapp:v1 srithu/sample:kubeimage1'
                bat 'docker push srithu/sample:kubeimage1'
            }
        }
        stage('Run in Kubernetes')
        {
            steps
            {
                echo 'Run application in Kubernetes'
                bat 'kubectl apply -f deployment.yaml --validate=false --insecure-skip-tls-verify'
                bat 'kubectl apply -f service.yaml --insecure-skip-tls-verify'
            }
        }
    }

    post
    {
        success
        {
            echo 'Pipeline Succeeded'
        }
        failure
        {
            echo 'Pipeline Failed'
        }
        always
        {
            echo 'Pipeline Completed'
        }
    }
}
